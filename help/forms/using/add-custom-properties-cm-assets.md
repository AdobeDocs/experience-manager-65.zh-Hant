---
title: 將自定義屬性添加到Tergement Management資產
seo-title: Add custom properties to Correspondence Management assets
description: 瞭解如何將自定義屬性添加到Tergement Management資產。
seo-description: Learn how to add custom properties to Correspondence Management assets.
uuid: 4716e181-d3ea-424b-9544-376cc649bce7
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79437b96-7b57-4581-b7e7-fcaedc3d05de
docset: aem65
feature: Correspondence Management
exl-id: ba2e145d-51ee-4844-a9e1-9927971d25a1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4443'
ht-degree: 4%

---

# 將自定義屬性添加到Tergement Management資產{#add-custom-properties-to-correspondence-management-assets}

## 概觀 {#overview}

您可以自定義Tergement Management用戶介面，並向用戶顯示一組定製的屬性和頁籤。 此自定義包括向特定資產類型/字母或所有資產類型和字母添加自定義欄位/屬性和標籤。

## 將自定義屬性添加到Tergement Management資產 {#adding-custom-properties-to-correspondence-management-assets}

以下方案顯示如何將屬性/標籤添加到Oracle Tergement資產和信函中：

* 向所有資產類型添加公用屬性
* 向所有資產類型添加公用標籤
* 向特定資產類型添加自定義屬性

通過調整這些方案中的屬性、路徑和值，您可以根據您的要求將自定義屬性和標籤添加到不同的資產集中。

### 方案：向所有資產類型添加公用欄位（屬性） {#scenario-adding-a-common-field-property-to-all-the-asset-types}

此方案顯示如何將自定義屬性添加到所有資產類型（文本、清單、條件和佈局片段）和字母。 使用此方案，您可以將一個屬性「收件人的位置」添加到所有資產和信函中。 「收件人的地點」屬性有助於確定資產或信件的交貨地理區域。

>[!NOTE]
>
>如果已添加自定義屬性，則該屬性將開始出現在資產建立頁面中。 要隱藏此類屬性，請參閱「在資產建立和屬性上顯示/隱藏自定義屬性」頁。

![自定義屬性已添加到所有資產類型](assets/lcoationofrecipientsui.png)

完成以下步驟，將自定義屬性添加到所有資產類型和字母中：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在apps資料夾中，使用以下步驟建立名為css的資料夾，其路徑/結構與css資料夾（位於ccrui資料夾中）類似：

   1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![覆蓋節點](assets/itemsoverlaynode.png)

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **位置：** /apps/

      **匹配節點類型：** 已選擇

      ![覆蓋節點](assets/cmmetapropertiesoverlaynode.png)

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

   1. 按一下 **全部保存**。

1. 在新建立的項資料夾下，為所有資產中的custom屬性添加一個節點(示例：GeoLocation)，執行以下步驟：

   1. 按一下右鍵項目資料夾並選擇 **建立** > **建立節點**。

      ![在CRX中建立節點](assets/itemscreatenode.png)

   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** GeoLocation（或要為此屬性指定的名稱）

      **類型：** nt：非結構化

      ![建立節點：地理位置](assets/geographicallocationcreatenode.png)

   1. 按一下您建立的新節點（此處為GeoLocation）。 CRX顯示節點的屬性。
   1. 將以下屬性添加到節點（此處為GeoLocation）:

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 欄位標籤 | 字串 | 要指定欄位/屬性的名稱。 (此處：收件人的位置) |
      | 名稱 | 字串 | `./extendedproperties/GeoLocation` （保持值與在「項」節點下建立的欄位名稱相同） |
      | renderReadOnly | 布林值 | true |
      | sling:resourceType | 字串 | `granite/ui/components/coral/foundation/form/textfield` |

   1. 按一下 **全部保存**。

1. 要查看自定義，請將滑鼠懸停在資產（文本、清單、條件或佈局片段）或字母上，按一下 **查看屬性**，然後按一下 **編輯**。 新欄位（收件人的位置）顯示在資產/信件屬性的「基本」頁籤中。

   >[!NOTE]
   >
   >在UI中顯示自定義項之前，可能需要清除瀏覽器快取。

   ![自定義屬性已添加到所有資產](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >添加的所有資產的公用屬性將顯示在資產屬性的基本頁籤中。 預設情況下，為所有資產添加的公用屬性將出現在屬性頁面和資產建立頁面上。 要隱藏公用屬性，您需要 <!--link to show / hide properties]-->。

### 方案：將自定義下拉清單和值添加到自定義屬性/欄位 {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

此方案顯示如何將自定義屬性添加到所有資產類型並向其添加下拉清單值。

1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 在新建立的覆蓋節點(/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items)下，為需要為其建立下拉清單的每個屬性（欄位）建立一個節點（此處） `geographicallocation`)類型。
1. 將以下屬性添加到節點（此處為地理位置分配），然後按一下 **全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>欄位標籤</td>
      <td>字串</td>
      <td>要指定欄位/屬性的名稱。 (此處：地理分配)</td>
   </tr>
   <tr>
      <td>名稱</td>
      <td>字串</td>
      <td>./extendedproperties/geographicallocation（與在「項」節點下建立的欄位名保持相同值）</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>布林值</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>字串</td>
      <td>花崗岩/ui/元件/珊瑚/地基/形式/選擇<br /> </td>
   </tr>
   </tbody>
   </table>

1. 在屬性節點（此處為地理位置分配）下，添加一個名稱為 `items`。 在「項」節點下，為下拉清單中的值分別添加一個節點。 作為一種好的做法，將第一個節點添加為空，作為下拉框的預設值，並為用戶指定欄位不值的選項。 要添加多個選項/下拉值，請重複以下步驟：

   1. 按一下右鍵屬性節點（此處為地理位置分配），然後選擇 **建立** > **建立節點**。
   1. 輸入欄位名稱為 `item1,` 將類型保留為nt：非結構化，然後按一下 **確定**。
   1. 將以下屬性添加到新建立的節點（此處為item1），然後按一下 **全部保存**:

      <table>
         <tbody>
         <tr>
          <td><strong>名稱</strong></td>
          <td><strong>類型</strong></td>
          <td><strong>值</strong></td>
         </tr>
         <tr>
          <td>text</td>
          <td>字串</td>
          <td>這是用戶可見的下拉選項的值。 為空值（預設值）保留空值或輸入值，如 <strong>國際</strong> 或 <strong>美國境內</strong>。<br /> </td>
         </tr>
         <tr>
          <td>值</td>
          <td>字串</td>
          <td>儲存在CRXDE中的文本值。 輸入任何唯一關鍵字。 <br /> </td>
         </tr>
         </tbody>
   </table>

   ![自定義下拉清單](assets/customizationdropdownvaluescrxde.png)

自定義下拉清單在資產屬性中顯示如下：

![下拉清單自定義](assets/drop-down_customization.png)

### 方案：所有資產類型的公用頁籤 {#scenario-common-tab-for-all-asset-types}

此方案顯示如何將自定義頁籤「收件人」添加到所有資產類型（文本、清單、條件和佈局片段）和字母。 「收件人」頁籤是您計畫將所有與收件人相關的自定義屬性放在其中。

![為所有資產類型添加的自定義頁籤](assets/recipientstab.png)

使用以下過程，您可以將帶有欄位的頁籤添加到所有資產中：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在apps資料夾中，使用以下步驟建立名為cmmetadataproperties的資料夾，其路徑/結構類似於cmmetadataproperties資料夾（位於內容資料夾中）:

   1. 按一下右鍵以下路徑中的cmmetadataproperties資料夾，然後選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![覆蓋節點](assets/cmmetadatapropertiesoverlaynode.png)

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

      ![在CRX中建立的覆蓋資料夾結構](assets/cmmetadatapropertiesappsfolder.png)

      按一下 **全部保存**。

1. 在cmmetadataproperties資料夾下，添加一個節點，用於為所有資產建立自定義頁籤(示例：（公用頁籤），使用以下步驟：

   1. 按一下右鍵cmmetadataproperties資料夾並選擇 **建立** > **建立節點**。

      ![建立節點](assets/cmmetadatapropertiescreatenode.png)

   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** commontab（或要指定給此屬性的名稱）

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處為公用頁籤）。 CRX顯示節點的屬性。
   1. 將以下屬性添加到節點（此處為公用頁籤）:

      <table>
         <tbody>
         <tr>
          <td><strong>名稱</strong></td>
          <td><strong>類型</strong></td>
          <td><strong>值</strong></td>
         </tr>
         <tr>
          <td>jcr:title</td>
          <td>字串</td>
          <td>要指定列的名稱。 (此處：收件人)</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>字串</td>
          <td>花崗岩/ui/元件/珊瑚/地基/集裝箱<br /> </td>
   </tr>
         </tbody>
       </table>

   1. 按一下 **全部保存**。

1. 對於在上一步（此處為公用頁籤）中建立的頁籤節點，使用以下步驟建立一個名為item的節點：

   1. 按一下右鍵相關節點（此處為公用頁籤）並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 項目

      **類型：** nt：非結構化

   1. 按一下 **全部保存：**

1. 在上一步中建立的項節點（在公用頁籤下）中，使用以下步驟（要添加更多列，請重複此步驟），在自定義頁籤（公用頁籤）中添加一個用於建立列的節點（此處為「列1」）:

   1. 按一下右鍵項目節點並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** Column1（或您要給節點的名稱 — 此名稱不顯示在用戶介面中。）

      **類型：** nt：非結構化

   1. 將以下屬性添加到節點（此處為列1），然後按一下 **全部保存**:

      <table>
         <tbody>
         <tr>
           <td><strong>名稱</strong></td>
           <td><strong>類型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字串</td>
           <td>花崗岩/ui/元件/珊瑚/地基/集裝箱<br /> </td>
         </tr>
         </tbody>
       </table>

1. 在上一步（此處為Column1）中建立的節點中，使用以下步驟添加名為items的節點：

   1. 按一下右鍵節點（此處為Column1），然後選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 項目

      **類型：** nt：非結構化

   1. 按一下 **全部保存**。

1. 要在自定義頁籤（此處為收件人）中建立欄位，請添加節點（此處為GerolaticLocation）。 此屬性與您建立的列相對應。 使用以下步驟建立欄位（要建立更多欄位/節點，請重複這些步驟）。:

   1. 按一下右鍵項目節點並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** GerolaticLocation（或欄位屬性的其他名稱）

      **類型：** nt：非結構化

   1. 將以下屬性添加到欄位節點（此處為GerolaticLocation），然後按一下 **全部保存**。

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 欄位標籤 | 字串 | 收件人的位置（或您要給該欄位的名稱）。 |
      | 名稱 | 字串 | ./extended屬性/地理位置 |
      | renderReadOnly | 布林值 | true |
      | sling:resourceType | 字串 | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. 要為「字母」添加此頁籤，請在以下路徑上建立路徑/結構類似於以下項目資料夾的覆蓋資料夾：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   要為字母或其他資產建立覆蓋，請通過替換 [程式集類型] 包含文本、條件、清單、日期或片段：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾已建立。 按一下 **全部保存**。

1. 在新建立的項目資料夾中，使用以下步驟為資產中的自定義頁籤添加一個節點（此處為mytab — 此名稱不顯示在用戶介面中）:

   1. 按一下右鍵項目資料夾並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** mytab（或要給此屬性指定的名稱）

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處為mytab）。 CRX顯示節點的屬性。
   1. 將以下兩個屬性添加到節點（此處為customtab）:

      <table>
         <tbody>
         <tr>
           <td><strong>名稱</strong></td>
           <td><strong>類型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>路徑<br /> </td>
           <td>字串</td>
           <td>fd/cm/ma/gui/content/cmmetadataproperties/commontab<br /> </td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字串</td>
           <td>花崗岩/ui/元件/珊瑚/地基/包括<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 按一下 **全部保存**。

1. 要查看自定義，請將滑鼠懸停在相關資產（此處為字母）上，按一下「查看屬性」，然後按一下 **編輯**。 新頁籤（收件人）和欄位（收件人的位置）顯示在用戶介面中。

   >[!NOTE]
   >
   >在UI中顯示自定義項之前，可能需要清除瀏覽器快取。

   ![自定義頁籤添加到字母](assets/recipientstab-1.png)

### 方案：添加特定資產類型的自定義屬性 {#scenario-adding-custom-properties-for-specific-asset-types}

此方案顯示如何將屬性添加到特定資產類型，如將欄位添加到所有文本資產。 使用此過程，可向以下其中一項添加屬性：

* 文字
* 條件
* 清單
* 布局片段
* 資料字典
* 字母

例如，僅對文本資產，您需要添加屬性「收件人的位置」，以標識資產與哪個地理區域相關。  ![自定義屬性已添加到資產](assets/newtabui.png)

要將屬性添加到資產類型，請完成以下步驟：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 要在資產類型（如「文本」）中建立頁籤，請在「應用」資料夾中建立以下資料夾結構：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [資產類型] =文本、條件、清單、字母、日期或片段

   以下是建立此資料夾結構的步驟：

   1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例如，如果要為文本資產建立屬性，請選擇以下資料夾：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![覆蓋節點](assets/textitemstabsitemsoverlaynode1.png)

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmmetadatapropertys/properties//cmmetadataproperties/[資產類型]/items/tabs/items

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

      按一下 **全部保存**。

1. 在新建立的項目資料夾中，為資產中的自定義頁籤添加一個節點(示例：customtab)執行以下步驟：

   1. 按一下右鍵項目資料夾並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** customtab（或要賦給此屬性的名稱）

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處為custom頁籤）。 CRX顯示節點的屬性。
   1. 將以下兩個屬性添加到節點（此處為customtab）:

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | sling:resourceType | 字串 | 花崗岩/ui/元件/珊瑚/地基/集裝箱 |
      | jcr:title | 字串 | 用戶介面（此處為「我的」頁籤）上欄位的名稱 |

   1. 按一下 **全部保存**。

1. 在上一步中建立的節點（此處為customtab）中，使用以下步驟添加名為items的節點：

   1. 按一下右鍵節點（此處為custom頁籤），然後選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 項目

      **類型：** nt：非結構化

   1. 按一下 **全部保存**。

1. 在上一步中建立的項節點（在customtab下）中，使用以下步驟（要添加更多列，請重複此步驟），在自定義頁籤中添加用於建立列（此處為Column1）的節點：

   1. 按一下右鍵項目節點並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** Column1（或要給節點的名稱）

      **類型：** nt：非結構化

   1. 將以下屬性添加到節點（此處為列1），然後按一下 **全部保存**。

      <table>
         <tbody>
         <tr>
           <td><strong>名稱</strong></td>
           <td><strong>類型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>sling:resourceType</td>
           <td>字串</td>
           <td>花崗岩/ui/元件/珊瑚/地基/集裝箱<br /> </td>
         </tr>
         </tbody>
       </table>

1. 對於您建立的每列（如上一步中指定的 — 此處為Column1），使用以下步驟建立一個名為item的節點：

   1. 按一下右鍵相關列節點（此處為列1），然後選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 項目

      **類型：** nt：非結構化

   1. 按一下 **全部保存：**

1. 對於建立的每列，在「項目」節點下建立一個節點，以在「用戶介面」的「新」頁籤中建立欄位。 重複此步驟可在列中建立更多欄位：

   1. 按一下右鍵相關節點（此處列1下的項）並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 您選擇的名稱（此處為GeoLocation）

      **類型：** nt：非結構化

   1. 將以下屬性添加到節點，然後按一下 **全部保存**。

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 欄位標籤 | 字串 | 收件人的位置（或您要給該欄位的名稱）。 |
      | 名稱 | 字串 | `./extendedproperties/GeoLocation` |
      | renderReadOnly | 布林值 | true |
      | sling:resourceType | 字串 | 花崗岩/ui/元件/珊瑚/地基/表/文本 |

1. 要查看自定義，請將滑鼠懸停在相關資產（此處為文本）上，按一下「查看屬性」，然後按一下 **編輯**。 新頁籤和欄位（收件人的位置）顯示在用戶介面中。

   >[!NOTE]
   >
   >在UI中顯示自定義項之前，可能需要清除瀏覽器快取。

   ![自定義屬性添加到特定資產](assets/newtabui-1.png)

### 在「資產建立」頁上顯示自定義屬性 {#display-custom-properties-on-the-asset-creation-page}

預設情況下，添加到新頁籤的自定義屬性僅在屬性頁上可見，而不在資產建立頁上可見，因為資產建立頁沒有頁籤佈局。 要在資產建立頁面上顯示自定義屬性以及其他屬性，您需要執行以下操作：

1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 確保「覆蓋節點」對話框具有字母的以下值。 對於其他資產類型，下表中提供了路徑：

   **路徑：** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letter嚮導/items/properties/items/properties/items/letters/items

   **位置：** /apps/

   **匹配節點類型：** 已選擇

   根據資產類型，路徑應為：

   | **資產/單據類型** | **要添加的路徑** |
   |---|---|
   | 文字 | /libs/fd/cm/ma/cum/createasset/createtext/jcr:content/body/items/form/textwizard/items/editproperties/items/items/tabs/items/tabs/tabs/items/items/tab1/items |
   | 清單 | /libs/fd/cm/ma/cum/createst/createlist/jcr:content/body/items/form/items/listwizard/items/editproperties/items/properties/items/items/items/tabs/tab1/items |
   | 條件 | /libs/fd/cm/ma/cum/createst/createcondition/jcr:content/body/items/form/items/conditionwizard/items/properties/items/tabs/items/tabs/tabs/items/items/tab1/items |
   | 片段 | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr：內容/正文/項目/表單/項目/片段twizard/items/properties/items/properties/tabs2/items/tab1/items |
   | 字母 | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letter嚮導/items/properties/items/properties/items/letters/items |

1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

1. 在您建立的覆蓋項節點下，建立名稱為col4（或任何其他名稱）的節點，然後按一下 **全部保存**。

   例如，下面是為字母建立的覆蓋節點。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 將以下屬性添加到新建立的節點（此處為第4列），然後按一下 **全部保存**:

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>路徑</td>
   <td>字串</td>
   <td><p>此路徑是指向在以下位置建立的列的指針：</p>
    <ul>
     <li>對於所有資產類型的公用標籤：/apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>對於不同資產類型的不同屬性：/apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串</td>
   <td> 花崗岩/ui/元件/珊瑚/地基/包括<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappeinginmain屬性](assets/customfieldappearinginmainproperties.png)

自定義屬性，語言，顯示在用於建立字母的UI中

## 自定義清單視圖以顯示自定義屬性 {#customize-the-list-view-to-show-custom-properties}

在將自定義屬性添加到Tergement Management資產後，您需要在CRX/DE中做進一步更改，以確保自定義屬性顯示在Tergence Management UI中。

完成以下步驟以在Tergement Management的資產清單UI中顯示自定義屬性：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在apps資料夾中建立以下資料夾結構：

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   以下是建立此資料夾結構的步驟：

   1. 按一下右鍵以下路徑中的列資料夾並選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmassets/jcr：內容/視圖/清單/列

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

      按一下 **全部保存**。

1. 對於建立的每個屬性，在「列」節點下建立一個節點，以在「用戶介面」中建立列。 重複此步驟，在UI中建立更多列：

   1. 按一下右鍵相關節點（列）並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 您選擇的名稱（此處為GerolationLocation）

      **類型：** nt：非結構化

   1. 將以下屬性添加到節點，然後按一下 **全部保存**。

      <table>
         <tbody>
         <tr>
           <td><strong>名稱</strong></td>
           <td><strong>類型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>jcr:primaryType</td>
           <td>名稱</td>
           <td><p>nt:unstructured</p> </td>
         </tr>
         <tr>
           <td>jcr:title</td>
           <td>字串</td>
           <td><p>地理位置</p> <p>此值將作為UI中的列標題顯示。 </p> </td>
         </tr>
         <tr>
           <td>排序</td>
           <td>布林值</td>
           <td><p>true</p> <p>值為true表示用戶可以對此列中的值進行排序。 </p> </td>
         </tr>
         </tbody>
       </table>

1. 在apps資料夾中建立以下資料夾結構：

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   以下是建立此資料夾結構的步驟：

   1. 按一下右鍵以下路徑中的列資料夾並選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage//

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

      按一下 **全部保存**。

1. 從以下位置複製chilllistpage.jsp檔案：

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   將檔案貼上到以下位置：

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/

1. 開啟childlistpage.jsp檔案(/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp)並進行以下更改：

   1. 將以下內容添加到檔案第19行（版權聲明後）。

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. 將函式的以下代碼添加到檔案末尾，該代碼為每個自定義屬性獲取值：

      ```jsp
      <%!
          private String getCustomPropertyValue(Map<String, Object> extendedProperties, String propertyName) {
      
              String propertyValue = "";
              if (extendedProperties.containsKey(propertyName)) {
                  propertyValue = (String) extendedProperties.get(propertyName);
              }
      
              return propertyValue;
          }
      %>
      ```

   1. 在開始之前添加以下內容 &lt;tr> 標籤(&lt;tr attrs.build=&quot;&quot;>>):

      ```jsp
      <%
          String GeoLocation = "";
          if (asset != null) {
                  Map<String, Object> extendedProperties = asset.getExtendedProperties();
                  if (extendedProperties != null) {
                      GeoLocation = getCustomPropertyValue(extendedProperties,"GeoLocation");
                  }
          }
      %>
      ```

      在代碼中，GeoLocation是建立自定義節點/欄位時在name屬性中設定的值。 建立自定義節點/欄位時，已使用指定屬性名稱。/extendedproperties/前置詞：。/extendedproperties/GeoLocation。 在代碼中，不需要前置詞。

   1. 要在UI中顯示新屬性，請添加TD標籤，如下所示，在關閉tr(&lt;/tr>)標籤：

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      要添加更多列，請重複步驟6.3和6.4。

   1. 按一下 **全部保存**。

1. 要查看自定義，請開啟文檔片段或添加自定義屬性的字母的清單視圖。

   此過程中添加的UI列和屬性將針對所有資產類型顯示。 但是，這些屬性中的值只能輸入並顯示給最初為其添加自定義屬性的資產類型。

   例如，使用方案：添加特定資產類型的自定義屬性，將自定義屬性添加到文本資產中，您只能將自定義屬性輸入到文本資產中。 但是，如果在UI中顯示該自定義屬性，則所有資產類型都會顯示該列。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （可選）預設情況下，新列將作為UI中的最後一列顯示。 要使列顯示在特定位置，請將以下屬性添加到列節點：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>sling：排序之前</td>
   <td>字串</td>
   <td><p>路徑「/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list/columns」處的列節點的名稱，在此之前，自定義列需要在UI上顯示。</p> <p>如果希望「地理位置」列在「版本」列的前面（左側），請將屬性sling:orderBefore添加到路徑「」/apps/fd/cm/ma/gui/cmassets/jcr:content/views/list/columns/GeoLocation」的GeoLocation節點中，並將屬性值設定為版本。</p> </td>
  </tr>
 </tbody>
</table>

添加sling:orderBefore屬性以指定列位置時，還需要更新相應的 &lt;td> 在此過程的步驟6.4中指定的標籤。 例如，在本例中，您需要確保 &lt;td> 地理位置的標籤位於 &lt;td> 版本列的標籤：

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## 啟用自定義屬性的搜索 {#enable-search-for-custom-properties}

預設情況下，全文搜索不包括您使用CRX/DE添加到UI的自定義屬性。

要在搜索中包括自定義屬性，需要允許對自定義屬性進行索引。

要允許對自定義屬性進行索引，請完成以下步驟：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 轉到 `/oak:index/cmLucene`添加名為 **聚合** 下面。

   1. 按一下右鍵cmLucene資料夾並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 聚合

      **類型：** nt：非結構化

   1. 按一下 **全部保存**。

1. 在新建的聚合資料夾下，添加節點cm:resource。 在cm:resource下，添加名為include0的節點。

   1. 按一下右鍵聚合資料夾並選擇 **建立** > **建立節點**。 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** cm：資源

      **類型：** nt：非結構化

   1. 按一下右鍵cm:resource資料夾並選擇 **建立** > **建立節點**。 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 包括0

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處包括0）。 CRX顯示節點的屬性。
   1. 將以下屬性添加到節點（此處包括0）:

      <table>
         <tbody>
         <tr>
           <td><strong>名稱</strong></td>
           <td><strong>類型</strong></td>
           <td><strong>值</strong></td>
         </tr>
         <tr>
           <td>路徑</td>
           <td>字串</td>
           <td>擴展屬性<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 按一下 **全部保存**。

1. 轉到以下位置的屬性，並在其下添加節點位置： `/oak:index/cmLucene/indexRules/cm:resource/properties`

   對要添加到搜索的每個自定義屬性重複此步驟。

   1. 按一下右鍵屬性資料夾並選擇 **建立** > **建立節點**。
   1. 確保「建立節點」對話框具有以下值，然後按一下 **確定**:

      **名稱：** 位置（或要添加到搜索的自定義屬性的名稱）

      **類型：** nt：非結構化

   1. 按一下您建立的新節點（此處為位置）。 CRX顯示節點的屬性。
   1. 將以下屬性添加到節點（此處的位置）:

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 分析 | 字串 | true |
      | 名稱 | 字串 | extendedProperties/location（或要添加到搜索中的屬性的名稱） |
      | 屬性索引 | 布林值 | true |
      | useInSuggest | 布林值 | true |

   1. 按一下 **全部保存**。

1. 現在，您可以在全文搜索中使用自定義屬性值來查找相關資產。

>[!NOTE]
>
>如果仍無法搜索，則可能是由於索引問題。 要重新編製索引，請轉到以下節點，並將屬性「re-index」的值更改為true:
>
>/oak:index/cmLucene&quot;和屬性的更改值

## 更改搜索頁的預設視圖 {#change-default-view-of-the-search-page}

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在apps資料夾中，建立一個名為list的資料夾，其路徑/結構與/libs/granite/ui/content/shell/omnisearch/searchresults/singlersults/views中的list資料夾類似：

   1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/granite/ui/content/shell/omnisearch/searchress/singresults/views/list

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

   1. 按一下 **全部保存**。

1. 在新建立的節點中，清單，添加以下屬性，然後按一下 **全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling：排序之前<br /> </td>
      <td>字串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 自定義項在「清單」視圖中顯示所有控制台的搜索結果，包括「Forms」和「文檔」、「資產」和「站點」。

## 更改資產頁的預設視圖 {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>這些步驟更改所有控制台(如Forms和文檔、資產和站點)的預設視圖。

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在apps資料夾中，建立一個名為list的資料夾，其路徑/結構類似於位於以下位置的清單資料夾：

   /libs/fd/cm/ma/gui/content/cmassets/jcr/content/views/

   1. 按一下右鍵以下路徑上的項目資料夾並選擇 **覆蓋節點**:

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmassets/jcr/content/views/list

      **位置：** /apps/

      **匹配節點類型：** 已選擇

   1. 按一下&#x200B;**「確定」**。資料夾結構是在apps資料夾中建立的。

   1. 按一下 **全部保存**。

1. 在新建立的節點中，清單，添加以下屬性，然後按一下 **全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling：排序之前<br /> </td>
      <td>字串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 清除瀏覽器cookie或使用瀏覽器的隱藏模式查看資產。 預設情況下，資產頁面將出現在卡佈局中。

## 在「資產建立」和「屬性」頁上顯示/隱藏自定義屬性 {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

要顯示或隱藏自定義屬性，請完成以下步驟：

1. 在自定義屬性節點（如地理分配）下，建立一個名為「granite:rendercondition」的「nt:antrographic」類型的新節點。
1. 將以下屬性添加到節點，然後按一下 **全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling:resourceType<br /> </td>
      <td>字串</td>
      <td>fd/cm/ma/gui/元件/admin/asset屬性/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. 要在資產建立頁面中隱藏此屬性，請向其中添加以下屬性，然後按一下 **全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>隱藏OnCreate<br /> </td>
      <td>布林值</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. 要隱藏資產屬性頁上的自定義屬性，請向其中添加以下屬性，然後按一下 **全部保存**:

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>隱藏OnEdit<br /> </td>
      <td>布林值</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   要再次顯示值，請將屬性值重置為 `false` 或刪除屬性條目。
