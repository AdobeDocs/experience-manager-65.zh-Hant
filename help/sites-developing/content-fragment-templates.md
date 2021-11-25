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
source-git-commit: a2b1bd5462ae1837470e31cfeb87a95af1c69be5
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 4%

---

# 內容片段範本{#content-fragment-templates}

>[!CAUTION]
>
>[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建議您建立所有新內容片段。
>
>內容片段模型用於WKND中的所有範例。

>[!NOTE]
>
>在AEM 6.3之前，內容片段是根據範本而非模型建立。
>
>內容片段範本現已過時。 它們仍可用於建立片段，但建議改用內容片段模型。 片段範本不會新增任何功能，且這些功能將在未來版本中移除。

建立內容片段時會選取範本。 它們為新片段提供了基本結構、元素和變異。 用於內容片段的範本需受Granite Configuration Manager的規範。

現成可用的範本位於：

* `/libs/settings/dam/cfm/templates`

您可以在下方為內容片段建立網站特定範本：

* `/apps/settings/dam/cfm/templates`
用於覆蓋現成可用的模板或提供客戶特定、應用程式範圍的模板的位置，這些模板不打算在運行時擴展/更改。

* `/conf/global/settings/dam/cfm/templates`
需要在執行階段變更之執行個體範圍客戶專屬範本的位置。

優先順序順序為（降序） `/conf`, `/apps`, `/libs`.

>[!CAUTION]
>
>您 ***必須*** 不會變更 `/libs` 路徑。
>
>這是因為 `/libs` 下次升級執行個體時即會覆寫（而當您套用Hotfix或Feature Pack時，很可能會覆寫）。
>
>設定和其他變更的建議方法為：
>
>1. 重新建立所需項目(亦即， `/libs`)底下 `/apps`
>
>1. 在內進行任何變更 `/apps`

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
     <td><p><code>String</code></p> <p>必填<br /> </p> </td>
     <td>範本的標題(顯示於 <strong>建立片段</strong> 精靈)。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可選</p> </td>
     <td>說明範本用途的文字(顯示於 <strong>建立片段</strong> 精靈)。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可選</p> </td>
     <td>依預設，具有系列路徑的陣列應與新建立的內容片段相關聯。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必填</p> </td>
     <td><p><code>true</code>，如果在建立內容片段時，應建立代表內容片段元素（主版元素除外）的子資產； <em>false</em> 如果應該「即時」建立它們。</p> <p><strong>附註</strong>:目前此參數必須設為 <code>true</code>.</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必填</p> </td>
     <td><p>內容結構的版本；目前支援：</p> <p><strong>附註</strong>:目前此參數必須設為 <code>2</code>.<br /> </p> </td>
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
     <td><p>包含內容片段元素定義的節點。 此為必要項目，需要包含 <strong>主要</strong> 元素，但可以包含[1..n]子節點。</p> <p>使用模板時，元素子分支將被複製到片段的模型子分支。</p> <p>第一個元素(如CRXDE Lite中所檢視)會自動被視為 <i>main</i> 元素；節點名稱無關，節點本身除以主要資產表示外，沒有特殊意義；其他元素會以子資產的形式處理。</p> </td>
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
     <td>元素的初始內容；僅使用 <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: <code>text/html</code></p> </td>
     <td><p>元素的初始內容類型；僅使用 <code>precreateElements</code><i> = </i><code>true</code>;目前支援：</p>
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
     <td><p>定義初始變數。<br /> 依預設，變異會新增至內容片段的所有元素。</p> <p>變異的初始內容將與個別元素相同(請參閱 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必填</p> </td>
     <td>變異的標題(顯示在片段編輯器的 <strong>變異</strong> 標籤（左側欄）。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>提供變異說明的文字 <span>(顯示在片段編輯器的 <strong>變異</strong> 標籤（左側欄）。</code></td>
    </tr>
   </tbody>
  </table>
