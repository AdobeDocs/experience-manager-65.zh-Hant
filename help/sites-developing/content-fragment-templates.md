---
title: 內容片段範本
seo-title: Content Fragment Templates
description: 建立內容片段時會選取範本，並提供具有基本結構、元素和變異的新片段
seo-description: Templates are selected when creating a content fragmen and provide the new fragment with the basic structure, element, and variation
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
source-git-commit: 2ec9625d480eb8cae23f44aa247fce2a519dec31
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 4%

---

# 內容片段範本{#content-fragment-templates}

>[!CAUTION]
>
>[建議您建](/help/assets/content-fragments/content-fragments-models.md) 立所有片段時，使用內容片段模型。
>
>內容片段模型用於We.Retail中的所有範例。

>[!NOTE]
>
>在AEM 6.3之前，是使用範本（而非模型）建立內容片段。 不再提供範本以建立新片段，但使用此範本建立的任何片段仍受支援。

建立內容片段時會選取範本。 它們為新片段提供了基本結構、元素和變異。 用於內容片段的範本需受Granite Configuration Manager的規範。

現成可用的範本位於：

* `/libs/settings/dam/cfm/templates`

您可以在下方為內容片段建立網站特定範本：

* `/apps/settings/dam/cfm/templates`
用於覆蓋現成可用的模板或提供客戶特定、應用程式範圍的模板的位置，這些模板不打算在運行時擴展/更改。

* `/conf/global/settings/dam/cfm/templates`
需要在執行階段變更之執行個體範圍客戶專屬範本的位置。

優先順序為（降序）`/conf`、`/apps`、`/libs`。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何項目。
>
>這是因為下次升級執行個體時會覆寫`/libs`的內容（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 在`/apps`下重新建立所需項（即`/libs`中存在的項）
>
>1. 在`/apps`內進行任何更改

>


範本的基本結構如下：

```xml
conf
  global
    settings
      dam
        cfm
          templates
            <template-name>
              ...
```

具體結構為：

```xml
+ <template-name>
    - jcr:primaryType
    - jcr:title
    - jcr:description
    - initialAssociatedContent
    - precreateElements
    - version
    + elements
        - jcr:primaryType
        + <element-name>
            - jcr:primaryType
            - jcr:title
            - defaultContent
            - initialContentType
            - name
        ... + other element definitions
    + variations
        - jcr:primaryType
        + <variation-name>
            - jcr:primaryType
            - jcr:title
            - jcr:description
            - name
        ... + other variation definitions
```

有關節點及其屬性的詳細資訊包括：

* **範本**

   <table>
   <tbody>
    <tr>
     <th>名稱</th>
     <th>類型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<em>template-name</em>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此節點是每個模板的根節點。 此為必要項目，且名稱應是唯一的。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必要<br /> </p> </td>
     <td>範本的標題（顯示在<strong>建立片段</strong>精靈中）。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可選</p> </td>
     <td>說明範本用途的文字（顯示在<strong>建立片段</strong>精靈中）。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可選</p> </td>
     <td>依預設，具有系列路徑的陣列應與新建立的內容片段相關聯。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必填</p> </td>
     <td><p><code>true</code>，如果在建立內容片段時，應建立代表內容片段元素（主版元素除外）的子資產；<em>false</em>如果應「即時」建立它們。</p> <p><strong>注意</strong>:目前此參數必須設為 <code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必填</p> </td>
     <td><p>內容結構的版本；目前支援：</p> <p><strong>注意</strong>:目前此參數必須設為 <code>2</code>。<br /> </p> </td>
    </tr>
   </tbody>
  </table>

* **元素**

   <table>
   <tbody>
    <tr>
     <th>名稱</th>
     <th>類型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>elements</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>必填</p> </td>
     <td><p>包含內容片段元素定義的節點。 它是強制項，並且需要為<strong>Main</strong>元素包含至少一個子節點，但可以包含[1.n]子節點。</p> <p>使用模板時，元素子分支將被複製到片段的模型子分支。</p> <p>第一個元素(如CRXDE Lite中所檢視)會自動被視為<i>main</i>元素；節點名稱無關，節點本身除以主要資產表示外，沒有特殊意義；其他元素會以子資產的形式處理。</p> </td>
    </tr>
   </tbody>
  </table>

* **元素名稱**

   <table>
   <tbody>
    <tr>
     <th>名稱</th>
     <th>類型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>element-name</i>&gt;</code></td>
     <td><code>nt:unstructured</code></td>
     <td>此節點定義元素。 此為必要項目，且名稱應是唯一的。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>元素的標題（顯示在片段編輯器的元素選取器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>元素的初始內容；僅在<code>precreateElements</code><i> = </i><code>true</code>時使用</td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: <code>text/html</code></p> </td>
     <td><p>元素的初始內容類型；僅在<code>precreateElements</code><i> = </i><code>true</code>時使用；目前支援：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>元素的內部名稱；片段類型必須是唯一的。</td>
    </tr>
   </tbody>
  </table>

* **變數**

   <table>
   <tbody>
    <tr>
     <th>名稱</th>
     <th>類型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>variations</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>可選</p> </td>
     <td>此選用節點包含內容片段初始變異的定義。</td>
    </tr>
   </tbody>
  </table>

* **變數名稱**

   <table>
   <tbody>
    <tr>
     <th>名稱</th>
     <th>類型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>若變異節點存在，則此為必要項目</p> </td>
     <td><p>定義初始變數。<br /> 依預設，變異會新增至內容片段的所有元素。</p> <p>變異的初始內容將與個別元素相同（請參閱<code class="code">defaultContent/
       initialContentType</code>）</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>變異的標題(顯示在片段編輯器的<strong> Variation</strong>標籤中（左側欄）)。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>提供變異<span>說明的文字(顯示在片段編輯器的<strong>Variation</strong>標籤中（左側邊欄）。</code></td>
    </tr>
   </tbody>
  </table>
