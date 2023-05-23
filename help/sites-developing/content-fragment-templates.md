---
title: 內容片段模板
seo-title: Content Fragment Templates
description: 在建立內容片段時選擇模板，並為新片段提供基本結構、元素和變體
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

# 內容片段模板{#content-fragment-templates}

>[!CAUTION]
>
>[內容片段模型](/help/assets/content-fragments/content-fragments-models.md) 建議建立所有新內容片段。
>
>WKND中的所有示例都使用內容片段模型。

>[!NOTE]
>
>6.AEM3之前的內容片段是基於模板而不是模型建立的。
>
>內容片段模板現在已棄用。 它們仍可用於建立片段，但建議改用「內容片段模型」。 將不向碎片模板添加任何新功能，並將在將來的版本中刪除這些功能。

建立內容片段時將選擇模板。 為新碎片提供了基本結構、元素和變異。 用於內容片段的模板受Granite Configuration Manager的約束。

現成模板保存在以下位置：

* `/libs/settings/dam/cfm/templates`

您可以在以下位置為內容片段建立特定於站點的模板：

* `/apps/settings/dam/cfm/templates`
用於覆蓋現成模板或提供客戶特定的應用程式範圍模板的位置，這些模板在運行時不打算擴展/更改。

* `/conf/global/settings/dam/cfm/templates`
運行時需要更改的實例範圍客戶特定模板的位置。

優先順序為（按降序） `/conf`。 `/apps`。 `/libs`。

>[!CAUTION]
>
>你 ***必須*** 沒有改變 `/libs` 路徑。
>
>這是因為 `/libs` 在下次升級實例時被覆蓋（在應用修補程式或功能包時很可能被覆蓋）。
>
>建議的配置和其他更改方法是：
>
>1. 重新建立所需項(如 `/libs`) `/apps`
>
>1. 在 `/apps`

>


模板的基本結構如下：

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
     <td>此節點是每個模板的根節點。 它是必需的，應具有唯一的名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>要求<br /> </p> </td>
     <td>模板的標題(顯示在 <strong>建立片段</strong> )的正平方根。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可選</p> </td>
     <td>描述模板用途的文本(顯示在 <strong>建立片段</strong> )的正平方根。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可選</p> </td>
     <td>預設情況下，具有到集合的路徑的陣列應與新建立的內容片段相關聯。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>要求</p> </td>
     <td><p><code>true</code>，如果在建立內容片段時應建立表示內容片段的元素（主元素除外）的子集； <em>假</em> 是否應「即時」建立。</p> <p><strong>注釋</strong>:當前此參數必須設定為 <code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>要求</p> </td>
     <td><p>內容結構的版本；當前支援：</p> <p><strong>注釋</strong>:當前此參數必須設定為 <code>2</code>。<br /> </p> </td>
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
     <td><p><code>nt:unstructured</code></p> <p>要求</p> </td>
     <td><p>包含內容片段元素定義的節點。 它是必需的，並且需要包含至少一個子節點 <strong>主</strong> 元素，但可以包含[1..n]子節點。</p> <p>使用模板時，元素子分支會複製到片段的模型子分支。</p> <p>第一個元素(如CRXDE Lite中所述)自動被視為 <i>主</i> 元素；節點名稱無關，節點本身除以主資產表示外，沒有特殊意義；其他要素作為子資產處理。</p> </td>
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
     <td>此節點定義元素。 它是必需的，應具有唯一的名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>要求</p> </td>
     <td>元素的標題（顯示在片段編輯器的元素選擇器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>元素的初始內容；僅用於 <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: <code>text/html</code></p> </td>
     <td><p>元素的初始內容類型；僅用於 <code>precreateElements</code><i> = </i><code>true</code>;當前支援：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>要求</p> </td>
     <td>元素的內部名稱；對於片段類型必須唯一。</td>
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
     <td>此可選節點包含內容片段的初始變體的定義。</td>
    </tr>
   </tbody>
  </table>

* **變體名稱**

   <table>
   <tbody>
    <tr>
     <th>名稱</th>
     <th>類型</th>
     <th>值</th>
    </tr>
    <tr>
     <td><code>&lt;<i>variation-name</i>&gt;</code> </td>
     <td><p><code>nt:unstructured</code></p> <p>變體節點存在時所需</p> </td>
     <td><p>定義初始變體。<br /> 預設情況下，變體會添加到內容片段的所有元素中。</p> <p>變體的初始內容與相應元素相同(請參見 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>要求</p> </td>
     <td>變體的標題（顯示在片段編輯器中） <strong>變異</strong> )。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>提供變體描述的文本 <span>(顯示在片段編輯器中 <strong>變異</strong> )。</code></td>
    </tr>
   </tbody>
  </table>
