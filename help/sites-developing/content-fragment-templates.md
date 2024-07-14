---
title: 內容片段範本
description: 建立內容片段時會選取範本，並為新片段提供基本結構、元素和變數
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 1b75721c-b223-41f0-88d9-bd855b529f31
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 3%

---

# 內容片段範本{#content-fragment-templates}

>[!CAUTION]
>
>建議使用[內容片段模型](/help/assets/content-fragments/content-fragments-models.md)來建立所有新的內容片段。
>
>內容片段模型用於WKND中的所有範例。

>[!NOTE]
>
>AEM 6.3之前，內容片段是根據範本而非模型建立的。
>
>內容片段範本現已棄用。 仍可用於建立片段，但建議改用內容片段模型。 片段範本不會新增任何新功能，未來版本中將移除這些功能。

建立內容片段時會選取範本。 它們為新片段提供基本結構、元素和變數。 用於內容片段的範本須受限於Granite Configuration Manager。

現成可用的範本位於下：

* `/libs/settings/dam/cfm/templates`

您可以在下列位置建立內容片段的網站專屬範本：

* `/apps/settings/dam/cfm/templates`
用於覆蓋現成範本或提供客戶特定、應用程式範圍範本（不打算在執行階段擴充/變更）的位置。

* `/conf/global/settings/dam/cfm/templates`
必須在執行階段變更的執行個體範圍客戶特定範本的位置。

優先順序為（以遞減順序） `/conf`、`/apps`、`/libs`。

>[!CAUTION]
>
>您&#x200B;***必須***&#x200B;不要變更`/libs`路徑中的任何專案。
>
>這是因為下次升級執行個體時，`/libs`的內容會被覆寫（當您套用Hotfix或Feature Pack時，這些內容很可能會被覆寫）。
>
>設定和其他變更的建議方法是：
>
>1. 在`/apps`下重新建立必要專案（亦即，它存在於`/libs`中）
>
>1. 在`/apps`中進行任何變更
>

範本的基本結構儲存在下方：

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

特定結構為：

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

有關節點及其屬性的更多詳細資訊如下：

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
     <td>此節點是每個範本的根。 此為必填欄位，且應具有唯一名稱。</td>
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
     <td>一個陣列，內含的集合路徑依預設應關聯至新建立的內容片段。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必要</p> </td>
     <td><p><code>true</code>，表示內容片段之元素（主要元素除外）的子資產是否應在內容片段建立時建立；<em>false</em>表示這些子資產是否應「即時」建立。</p> <p><strong>附註</strong>：此引數目前必須設定為<code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必要</p> </td>
     <td><p>內容結構的版本；目前支援：</p> <p><strong>附註</strong>：此引數目前必須設定為<code>2</code>。<br /> </p> </td>
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
     <td><code>elements</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>必要</p> </td>
     <td><p>包含內容片段元素定義的節點。 它是強制性的，而且至少必須包含<strong>Main</strong>專案的子節點，但可以包含[1.n]個子節點。</p> <p>使用範本時，元素子分支會複製到片段的模型子分支。</p> <p>系統會自動將第一個元素(在CRXDE Lite中檢視)視為<i>主要</i>元素；節點名稱不相關，且節點本身除了由主要資產表示外，並無特殊意義；其他元素則會處理為子資產。</p> </td>
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
     <td>此節點會定義元素。 此為必填欄位，且應具有唯一名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必要</p> </td>
     <td>元素的標題（顯示在片段編輯器的元素選取器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設值：「」</p> </td>
     <td>元素的初始內容；僅在<code>precreateElements</code><i> = </i><code>true</code>時使用</td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設： <code>text/html</code></p> </td>
     <td><p>專案的初始內容型別；僅在<code>precreateElements</code><i> = </i><code>true</code>時使用；目前支援：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必要</p> </td>
     <td>元素的內部名稱；對片段型別而言必須是唯一的。</td>
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
     <td><code>variations</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>可選</p> </td>
     <td>此選用節點包含內容片段初始變數的定義。</td>
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
     <td><code>&lt;<i>variation-name</i>&gt;</code><br /> </td>
     <td><p><code>nt:unstructured</code></p> <p>如果有變數節點，則必須填寫此項</p> </td>
     <td><p>定義初始變數。<br />依預設，此變數會新增至內容片段的所有元素。</p> <p>變數將與個別元素有相同的初始內容（請參閱<code class="code">defaultContent/
       initialContentType</code>）</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必要</p> </td>
     <td>變數的標題(顯示在片段編輯器的<strong>變數</strong>索引標籤（左側邊欄）中)。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設值：「」</p> </td>
     <td>提供變數<span>說明的文字(顯示在片段編輯器的<strong>變數</strong>索引標籤（左側欄）中)。</code></td>
    </tr>
   </tbody>
  </table>
