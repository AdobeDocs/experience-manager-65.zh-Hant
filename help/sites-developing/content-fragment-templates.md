---
title: 內容片段範本
seo-title: 內容片段範本
description: 建立內容片段時會選取範本，並提供具有基本結構、元素和變數的新片段
seo-description: 建立內容片段時會選取範本，並提供具有基本結構、元素和變數的新片段
uuid: d147bac8-b710-40ed-9664-decb5ffcf8e7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: a975ea2e-5e24-4a96-bd62-63bb98836ff2
docset: aem65
translation-type: tm+mt
source-git-commit: 0dc96f07e45ccbfea4edc87431677ada5b1bfa8c

---


# 內容片段範本{#content-fragment-templates}

>[!CAUTION]
>
>[現在建議使用內容片段模型](/help/assets/content-fragments-models.md) ，以建立您的所有片段。
>
>We.Retail中的所有範例都使用內容片段模型。

建立內容片段時會選取範本。 它們為新碎片提供了基本結構、元素和變異。 用於內容片段的範本受Granite Configuration Manager的規範。

現成可用的範本位於：

* `/libs/settings/dam/cfm/templates`

您可以在下列網址建立內容片段的網站特定範本：

* `/apps/settings/dam/cfm/templates`
覆蓋現成可用範本或提供客戶特定、應用程式範圍範本的位置，這些範本在執行時期不會延伸／變更。

* `/conf/global/settings/dam/cfm/templates`
需要在執行時期變更的整個客戶特定範本位置。

優先順序是（降序） `/conf`, `/apps`、 `/libs`。

>[!CAUTION]
>
>您 ***不得*** 更改路徑中的任 `/libs` 何內容。
>
>這是因為下次升級 `/libs` 實例時會覆寫的內容（套用修補程式或功能套件時可能會覆寫）。
>
>配置和其他更改的建議方法為：
>
>1. 重新建立下列項目的必要項目(如中所 `/libs`示): `/apps`
   >
   >
1. 在 `/apps`
>



範本之基本架構如下：

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
     <td>此節點是每個模板的根節點。 它是強制的，應具有唯一的名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>required<br /> </p> </td>
     <td>範本的標題(顯示在「建立片段 <strong>」精靈中</strong> )。</td>
    </tr>
    <tr>
     <td><code>jcr:description</code></td>
     <td><p><code>String</code></p> <p>可選</p> </td>
     <td>說明範本用途的文字(顯示在「建立片段 <strong>」精靈中</strong> )。</td>
    </tr>
    <tr>
     <td><code>initialAssociatedContent</code></td>
     <td><p><code>String[]</code></p> <p>可選</p> </td>
     <td>預設情況下，具有系列路徑的陣列，應與新建立的內容片段相關聯。</td>
    </tr>
    <tr>
     <td><code>precreateElements</code></td>
     <td><p><code>Boolean</code></p> <p>必要</p> </td>
     <td><p><code>true</code>,if the subsasets resporting the elements（master element除外）of the content fragment is created; <em>false</em> （如果應「即時」建立）。</p> <p><strong>注意</strong>:目前，此參數必須設為 <code>true</code>。</p> </td>
    </tr>
    <tr>
     <td><code>version</code></td>
     <td><p><code>Long</code></p> <p>必要</p> </td>
     <td><p>內容結構版本；目前支援：</p> <p><strong>注意</strong>:目前，此參數必須設為 <code>2</code>。<br /> </p> </td>
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
     <td><p><code>nt:unstructured</code></p> <p>必要</p> </td>
     <td><p>包含內容片段元素定義的節點。 它是強制性的，並且需要為 <strong>Main元素至少包含一個子節點</strong> ，但可以包含[1...n]子節點。</p> <p>使用模板時，元素子分支將被複製到片段的模型子分支。</p> <p>第一個元素（如CRXDE Lite中所述）會自動被視為主 <i>要元</i> 素；節點名稱無關，節點本身除了以主資產表示外，沒有特殊意義；其他元素則視為子資產處理。</p> </td>
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
     <td>此節點定義元素。 它是強制的，應具有唯一的名稱。</td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必要</p> </td>
     <td>元素的標題（顯示在片段編輯器的元素選擇器中）。</td>
    </tr>
    <tr>
     <td><code>defaultContent</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>元素的初始內容；只有在 <code>precreateElements</code><i> = </i><code>true</code></td>
    </tr>
    <tr>
     <td><code>initialContentType</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: <code>text/html</code></p> </td>
     <td><p>元素的初始內容類型；僅用於 <code>precreateElements</code><i> = </i><code>true</code>;目前支援：</p>
      <ul>
       <li><code>text/html</code></li>
       <li><code>text/plain</code></li>
       <li><code>text/x-markdown</code></li>
      </ul> </td>
    </tr>
    <tr>
     <td><code>name</code></td>
     <td><p><code>String</code></p> <p>必要</p> </td>
     <td>元素的內部名稱；必須為片段類型的唯一。</td>
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
     <td>此可選節點包含內容片段的初始變化的定義。</td>
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
     <td><p><code>nt:unstructured</code></p> <p>變異節點存在時所需</p> </td>
     <td><p>定義初始變化。<br /> 依預設，變數會新增至內容片段的所有元素。</p> <p>變數的初始內容會與個別元素相同(請參閱 <code class="code">defaultContent/
       initialContentType</code>)</p> </td>
    </tr>
    <tr>
     <td><code>jcr:title</code></td>
     <td><p><code>String</code></p> <p>必要</p> </td>
     <td>變數的標題(顯示在片段編輯器的「變數」( <strong>Variation</strong> )頁籤中（左側邊欄）)。</td>
    </tr>
    <tr>
     <td><code>jcr:desciption</code></td>
     <td><p><code>String</code></p> <p>可選</p> <p>預設: ""</p> </td>
     <td>提供變化說明的文字(顯 <span>示在片段編輯器的「變 <strong>化</strong> 」標籤（左側欄）中)。</code></td>
    </tr>
   </tbody>
  </table>
