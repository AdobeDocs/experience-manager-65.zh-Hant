---
title: 將自訂屬性新增至Correspondence Management資產
description: 瞭解如何將自訂屬性新增至通訊管理資產。
content-type: reference
topic-tags: correspondence-management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Correspondence Management
exl-id: ba2e145d-51ee-4844-a9e1-9927971d25a1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '4431'
ht-degree: 4%

---

# 將自訂屬性新增至Correspondence Management資產{#add-custom-properties-to-correspondence-management-assets}

## 概觀 {#overview}

您可以自訂「通訊管理」使用者介面，並以自訂的屬性和標籤集來呈現使用者。 此自訂包括將自訂欄位/屬性和標籤新增至特定資產型別/字母或所有資產型別和字母。

## 新增自訂屬性至Correspondence Management資產 {#adding-custom-properties-to-correspondence-management-assets}

下列案例顯示如何將屬性/標籤新增至「通訊管理」資產和信件：

* 新增通用屬性至所有資產型別
* 新增通用索引標籤至所有資產型別
* 將自訂屬性新增至特定資產型別

在這些案例中調整屬性、路徑和值，您就可以根據自己的需求，將自訂屬性和標籤新增到不同的資產集。

### 案例：新增通用欄位（屬性）至所有資產型別 {#scenario-adding-a-common-field-property-to-all-the-asset-types}

此案例顯示如何將自訂屬性新增至所有資產型別（文字、清單、條件和佈局片段）和字母。 使用此情境時，您可以將屬性收件者位置新增至所有資產和字母。 「收件者位置」屬性有助於識別資產或信函相關的傳送地理區域。

>[!NOTE]
>
>如果您已新增自訂屬性，屬性會開始出現在資產建立頁面上。 若要隱藏此類屬性，請參閱在資產建立和屬性頁面上顯示/隱藏自訂屬性。

![自訂屬性已新增至所有資產型別](assets/lcoationofrecipientsui.png)

完成下列步驟，將自訂屬性新增至所有資產型別和字母：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，使用下列步驟建立名為css的資料夾，其路徑/結構類似於css資料夾（在crui資料夾中）：

   1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

      ![覆蓋節點](assets/itemsoverlaynode.png)

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items

      **位置：** /apps/

      **符合節點型別：** 已選取

      ![覆蓋節點](assets/cmmetapropertiesoverlaynode.png)

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

   1. 按一下&#x200B;**「儲存全部」**。

1. 在新建立的專案資料夾下，使用下列步驟為所有資產中的自訂屬性新增節點（例如：GeoLocation）：

   1. 以滑鼠右鍵按一下專案資料夾並選取 **建立** > **建立節點**.

      ![在CRX中建立節點](assets/itemscreatenode.png)

   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 地理位置（或您要指定給此屬性的名稱）

      **型別：** nt：unstructured

      ![建立節點： GeoLocation](assets/geographicallocationcreatenode.png)

   1. 按一下您已建立的新節點（此處GeoLocation）。 CRX會顯示節點的屬性。
   1. 將下列屬性新增至節點（這裡是地理位置）：

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 欄位標籤 | 字串 | 您要為欄位/屬性指定的名稱。 （此處：收件者位置） |
      | 名稱 | 字串 | `./extendedproperties/GeoLocation` （保持與您在items節點下建立的欄位名稱相同的值） |
      | renderReadOnly | 布林值 | true |
      | sling:resourceType | 字串 | `granite/ui/components/coral/foundation/form/textfield` |

   1. 按一下&#x200B;**「儲存全部」**。

1. 若要檢視您的自訂，將滑鼠指標暫留在資產（文字、清單、條件或佈局片段）或信函上，請按一下 **檢視屬性**，然後按一下 **編輯**. 新欄位（收件者位置）會顯示在資產/信函屬性的「基本」索引標籤中。

   >[!NOTE]
   >
   >您可能需要在自訂出現在UI中之前清除瀏覽器快取。

   ![自訂屬性已新增至所有資產](assets/lcoationofrecipientsui-1.png)

   >[!NOTE]
   >
   >您新增之所有資產的通用屬性會顯示在資產屬性的基本標籤中。 依預設，為所有資產新增的共同屬性會顯示在屬性頁面和資產建立頁面上。 若要隱藏一般屬性，您必須 <!--link to show / hide properties]-->.

### 案例：新增自訂下拉式清單和值至自訂屬性/欄位 {#scenario-add-custom-drop-down-and-values-to-a-custom-property-field}

此案例顯示如何將自訂屬性新增至所有資產型別，並新增下拉式值至該屬性。

1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items`

1. 在新建立的覆蓋節點(/apps/fd/cm/ma/gui/content/cmmetadataproperties/commonproperties/col1/items)下，為需要建立下拉清單的每個屬性（欄位）建立節點（此處） `geographicallocation`nt：unstructured型別的)。
1. 將下列屬性新增至節點（這裡是地理配置），然後按一下 **全部儲存**：

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
      <td>您要為欄位/屬性指定的名稱。 （這裡：geographicallocation）</td>
   </tr>
   <tr>
      <td>名稱</td>
      <td>字串</td>
      <td>./extendedproperties/geographicallocation （讓值與您在items節點下建立的欄位名稱相同）</td>
   </tr>
   <tr>
      <td>renderReadOnly</td>
      <td>布林值</td>
      <td>true</td>
   </tr>
   <tr>
      <td>sling:resourceType</td>
      <td>字串</td>
      <td>granite/ui/components/coral/foundation/form/select<br /> </td>
   </tr>
   </tbody>
   </table>

1. 在屬性節點（此處為geographicallocation）底下，新增名為的新節點 `items`. 在專案節點底下，為下拉式清單中的值新增一個節點。 好的做法是將第一個節點新增為空白，作為下拉式清單的預設值，並新增選項讓使用者指定欄位無值。 若要新增多個選項/下拉式清單值，請重複下列步驟：

   1. 以滑鼠右鍵按一下屬性節點（這裡是地理配置），然後選取 **建立** > **建立節點**.
   1. 輸入欄位名稱為 `item1,` 將文字保留為nt：unstructured，然後按一下 **確定**.
   1. 將下列屬性新增至新建立的節點（此處item1），然後按一下 **全部儲存**：

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
          <td>這是使用者可見之下拉式選項的值。 請將其保留空白作為空白（預設）值，或輸入值，例如 <strong>國際</strong> 或 <strong>美國境內</strong>.<br /> </td>
         </tr>
         <tr>
          <td>值</td>
          <td>字串</td>
          <td>儲存在CRXDE中的文字值。 輸入任何唯一的關鍵字。 <br /> </td>
         </tr>
         </tbody>
   </table>

   ![customizationdropdownvaluescrxde](assets/customizationdropdownvaluescrxde.png)

自訂下拉式清單在資產屬性中顯示如下：

![drop-down_customization](assets/drop-down_customization.png)

### 案例：所有資產型別的通用標籤 {#scenario-common-tab-for-all-asset-types}

此案例顯示如何將自訂索引標籤「收件者」新增至所有資產型別（文字、清單、條件和佈局片段）和字母。 收件者索引標籤是您計畫放置與收件者相關的所有自訂屬性的位置。

![為所有資產型別新增自訂標籤](assets/recipientstab.png)

使用下列程式，您可以將含有欄位的索引標籤新增至所有資產：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，使用下列步驟建立名為cmmetadataproperties的資料夾，其路徑/結構類似於cmmetadataproperties資料夾（在內容資料夾中）：

   1. 以滑鼠右鍵按一下以下路徑的cmmetadataproperties資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties`

      ![覆蓋節點](assets/cmmetadatapropertiesoverlaynode.png)

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmmetadataproperties

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

      ![在CRX中建立的覆蓋資料夾結構](assets/cmmetadatapropertiesappsfolder.png)

      按一下&#x200B;**「儲存全部」**。

1. 在cmmetadataproperties資料夾下，使用下列步驟新增節點，以建立所有資產的自訂標籤（例如： commontab）：

   1. 以滑鼠右鍵按一下cmmetadataproperties資料夾，然後選取 **建立** > **建立節點**.

      ![建立節點](assets/cmmetadatapropertiescreatenode.png)

   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** commontab （或您要為此屬性指定的名稱）

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處為「共用標籤」）。 CRX會顯示節點的屬性。
   1. 將下列屬性新增至節點（此處為commontab）：

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
          <td>您要為欄指定的名稱。 （此處：收件者）</td>
         </tr>
         <tr>
          <td>sling:resourceType</td>
          <td>字串</td>
          <td>granite/ui/components/coral/foundation/container<br /> </td>
   </tr>
         </tbody>
       </table>

   1. 按一下&#x200B;**「儲存全部」**。

1. 對於在上一步中建立的標籤節點（此處為commontab），請使用以下步驟建立稱為item的節點：

   1. 以滑鼠右鍵按一下相關節點（此處為「共用標籤」），然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 個專案

      **型別：** nt：unstructured

   1. 按一下 **全部儲存：**

1. 在上一個步驟中建立的專案節點（在commontab下）中，使用下列步驟在自訂標籤(commontab)中新增用於建立欄的節點（此處為Column1）（若要新增更多欄，請重複此步驟）：

   1. 以滑鼠右鍵按一下專案節點，然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** Column1 （或您要指定給節點的名稱 — 此名稱不會出現在使用者介面中。）

      **型別：** nt：unstructured

   1. 將下列屬性新增至節點（此處為Column1），然後按一下 **全部儲存**：

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
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 在上一步建立的節點（此處為Column1）中，使用下列步驟新增稱為專案的節點：

   1. 以滑鼠右鍵按一下節點（此處為Column1）並選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 個專案

      **型別：** nt：unstructured

   1. 按一下&#x200B;**「儲存全部」**。

1. 若要在自訂標籤中建立欄位（這裡是收件者），請新增節點（這裡是GeographicLocation）。 此屬性會對應至您建立的欄。 使用以下步驟建立欄位（若要建立更多欄位/節點，請重複這些步驟。）：

   1. 以滑鼠右鍵按一下專案節點，然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** GeographicLocation （或欄位屬性的其他名稱）

      **型別：** nt：unstructured

   1. 將以下屬性新增到欄位節點（此處為GeographicLocation），然後按一下 **全部儲存**.

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 欄位標籤 | 字串 | 收件者位置（或您要提供欄位的名稱）。 |
      | 名稱 | 字串 | ./extendedproperties/GeographicLocation |
      | renderReadOnly | 布林值 | true |
      | sling:resourceType | 字串 | `/libs/granite/ui/components/coral/foundation/form/textfield` |

1. 若要為Letters新增此索引標籤，請建立路徑/結構類似於以下專案資料夾的覆蓋資料夾，路徑如下：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   若要為字母或不同資產建立覆蓋，請使用以下路徑，方法是取代 [assettype] 包含文字、條件、清單、datadictionary或片段：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[assettype]/items/tabs/items`

   1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/letter/items/tabs/items`

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾隨即建立。 按一下&#x200B;**「儲存全部」**。

1. 在新建立的專案資料夾中，為資產中的自訂標籤新增節點（此處為mytab — 此名稱未顯示在使用者介面中），使用下列步驟：

   1. 以滑鼠右鍵按一下專案資料夾並選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** mytab （或您要為此屬性指定的名稱）

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處為「mytab」）。 CRX會顯示節點的屬性。
   1. 將下列兩個屬性新增至節點（此處為customtab）：

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
           <td>granite/ui/components/coral/foundation/include<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 按一下&#x200B;**「儲存全部」**。

1. 若要檢視您的自訂專案，請將滑鼠指標暫留在相關的資產（此處為字母）上，按一下「檢視屬性」，然後按一下 **編輯**. 新標籤（收件者）和欄位（收件者的位置）會顯示在使用者介面中。

   >[!NOTE]
   >
   >您可能需要在自訂出現在UI中之前清除瀏覽器快取。

   ![新增至字母的自訂標籤](assets/recipientstab-1.png)

### 案例：新增特定資產型別的自訂屬性 {#scenario-adding-custom-properties-for-specific-asset-types}

此案例顯示如何將屬性新增至特定資產型別，例如將欄位新增至所有文字資產。 使用此程式，您可以將屬性新增至下列其中一項：

* 文字
* 條件
* 清單
* 布局片段
* 資料字典
* 字母

例如，您只想對文字資產新增屬性「收件者位置」，以識別資產相關的地理區域。  ![自訂屬性已新增至資產](assets/newtabui.png)

若要將屬性新增至資產型別，請完成下列步驟：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 若要在資產型別（例如文字）中建立索引標籤，請在apps資料夾中建立下列資料夾結構：

   `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

   [資產型別] =文字、條件、清單、信件、datadictionary或片段

   以下是建立此資料夾結構的步驟：

   1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[AssetType]/items/tabs/items`

      例如，如果您想要建立文字資產的屬性，請選取下列資料夾：

      `/libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/text/items/tabs/items`

      ![覆蓋節點](assets/textitemstabsitemsoverlaynode1.png)

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmmetadataproperties/properties/[資產型別]/items/tabs/items

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

      按一下&#x200B;**「儲存全部」**。

1. 在新建立的專案資料夾中，使用下列步驟為資產中的自訂標籤新增節點（例如：customtab）：

   1. 以滑鼠右鍵按一下專案資料夾並選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** customtab （或您要指定給此屬性的名稱）

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處為「自訂」標籤）。 CRX會顯示節點的屬性。
   1. 將下列兩個屬性新增至節點（此處為customtab）：

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | sling:resourceType | 字串 | granite/ui/components/coral/foundation/container |
      | jcr:title | 字串 | 使用者介面上的欄位名稱（此處為「我的」標籤） |

   1. 按一下&#x200B;**「儲存全部」**。

1. 在上一步建立的節點中（此處為「自訂」標籤），使用下列步驟新增稱為專案的節點：

   1. 以滑鼠右鍵按一下節點（此處為「自訂」標籤），然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 個專案

      **型別：** nt：unstructured

   1. 按一下&#x200B;**「儲存全部」**。

1. 在上一個步驟中建立的專案節點（在「自訂」標籤下）中，使用下列步驟在自訂標籤中新增用於建立欄的節點（此處為Column1）（若要新增更多欄，請重複此步驟）：

   1. 以滑鼠右鍵按一下專案節點，然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** Column1 （或您要指定給節點的名稱）

      **型別：** nt：unstructured

   1. 將下列屬性新增至節點（此處為Column1），然後按一下 **全部儲存**.

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
           <td>granite/ui/components/coral/foundation/container<br /> </td>
         </tr>
         </tbody>
       </table>

1. 對於您建立的每個欄（如上一個步驟 — 此處Column1所指定），使用下列步驟建立稱為item的節點：

   1. 以滑鼠右鍵按一下相關的欄節點（此處為Column1），然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 個專案

      **型別：** nt：unstructured

   1. 按一下 **全部儲存：**

1. 對於建立的每個欄，在專案節點下建立一個節點，以在使用者介面的新索引標籤中建立欄位。 重複此步驟以在欄中建立更多欄位：

   1. 以滑鼠右鍵按一下相關節點（此處為Column1下的專案），然後選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 您選擇的名稱（這裡是地理位置）

      **型別：** nt：unstructured

   1. 將下列屬性新增至節點，然後按一下 **全部儲存**.

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 欄位標籤 | 字串 | 收件者位置（或您要提供欄位的名稱）。 |
      | 名稱 | 字串 | `./extendedproperties/GeoLocation` |
      | renderReadOnly | 布林值 | true |
      | sling:resourceType | 字串 | granite/ui/components/coral/foundation/form/textfield |

1. 若要檢視您的自訂內容，請將滑鼠指標暫留在相關的資產（此處為文字）上，按一下「檢視屬性」，然後按一下 **編輯**. 新索引標籤和欄位（收件者的位置）會顯示在使用者介面中。

   >[!NOTE]
   >
   >您可能需要在自訂出現在UI中之前清除瀏覽器快取。

   ![新增至特定資產的自訂屬性](assets/newtabui-1.png)

### 在資產建立頁面上顯示自訂屬性 {#display-custom-properties-on-the-asset-creation-page}

依預設，新增到新索引標籤的自訂屬性僅會顯示在屬性頁面上，不會顯示在資產建立頁面上，因為資產建立頁面沒有索引標籤配置。 若要在資產建立頁面上顯示自訂屬性以及其他屬性，您需要執行以下操作：

1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

   `/libs/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 確定「覆蓋節點」對話方塊包含以下字母值。 對於其他資產型別，路徑如下表所示：

   **路徑：** /libs/fd/cm/ma/gui/content/createasset/createletter/jcr：content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items

   **位置：** /apps/

   **符合節點型別：** 已選取

   根據資產型別，路徑必須為下列：

   | **資產/檔案型別** | **要新增的路徑** |
   |---|---|
   | 文字 | /libs/fd/cm/ma/gui/content/createasset/createtext/jcr：content/body/items/form/items/textwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | 清單 | /libs/fd/cm/ma/gui/content/createasset/createlist/jcr：content/body/items/form/items/listwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | 條件 | /libs/fd/cm/ma/gui/content/createasset/createcondition/jcr：content/body/items/form/items/conditionwizard/items/editproperties/items/properties/items/tabs/items/tab1/items |
   | 片段 | /libs/fd/cm/ma/gui/content/createasset/createfragment/jcr：content/body/items/form/items/fragmentwizard/items/properties/items/properties/items/tabs2/items/tab1/items |
   | 字母 | /libs/fd/cm/ma/gui/content/createasset/createletter/jcr：content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items |

1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

1. 在您建立的覆蓋專案節點下，建立名稱為col4 （或任何其他名稱）的節點，然後按一下 **全部儲存**.

   例如，下面是為字母建立的覆蓋節點。

   `/apps/fd/cm/ma/gui/content/createasset/createletter/jcr:content/body/items/form/items/letterWizard/items/properties/items/properties/items/letterproperties/items`

1. 將下列屬性新增至新建立的節點（此處為col4），然後按一下 **全部儲存**：

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
   <td><p>此路徑是指向在中建立的欄的指標：</p>
    <ul>
     <li>適用於所有資產型別的通用標籤： /apps/fd/cm/ma/gui/content/cmmetadataproperties/commontab/items/col1</li>
     <li>針對不同資產型別的不同屬性： /apps/fd/cm/ma/gui/content/cmmetadataproperties/properties//items/tabs/items/customtab/items/col1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>sling:resourceType</td>
   <td>字串</td>
   <td> granite/ui/components/coral/foundation/include<br /> </td>
  </tr>
 </tbody>
</table>

![customfieldappearinginmainproperties](assets/customfieldappearinginmainproperties.png)

自訂屬性，語言，出現在UI中以建立字母

## 自訂清單檢視以顯示自訂屬性 {#customize-the-list-view-to-show-custom-properties}

將自訂屬性新增至通訊管理資產後，您需要在CRX/DE中進行進一步變更，以確保自訂屬性顯示在通訊管理UI中。

完成下列步驟，在通訊管理的資產清單UI中顯示自訂屬性：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中建立下列資料夾結構：

   `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   以下是建立此資料夾結構的步驟：

   1. 以滑鼠右鍵按一下以下路徑的columns資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/lists/columns`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/lists/columns

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

      按一下&#x200B;**「儲存全部」**。

1. 針對所建立的每個屬性，在欄節點下建立一個節點，以在使用者介面中建立欄。 重複此步驟以在UI中建立更多欄：

   1. 以滑鼠右鍵按一下相關節點（欄）並選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 您選擇的名稱（此處為GeographicLocation）

      **型別：** nt：unstructured

   1. 將下列屬性新增至節點，然後按一下 **全部儲存**.

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
           <td><p>地理位置</p> <p>此值會顯示為UI中的欄標題。 </p> </td>
         </tr>
         <tr>
           <td>可排序</td>
           <td>布林值</td>
           <td><p>true</p> <p>值為true表示使用者可以排序此欄中的值。 </p> </td>
         </tr>
         </tbody>
       </table>

1. 在apps資料夾中建立下列資料夾結構：

   `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   以下是建立此資料夾結構的步驟：

   1. 以滑鼠右鍵按一下以下路徑的columns資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

      按一下&#x200B;**「儲存全部」**。

1. 從下列位置複製childlistpage.jsp檔案：

   /libs/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp

   將檔案貼到下列位置：

   /apps//fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/。

1. 開啟childlistpage.jsp檔案(/apps/fd/cm/ma/gui/components/admin/childpagerenderer/childlistpage/childlistpage.jsp)並進行下列變更：

   1. 將下列內容加入檔案的第19行（在著作權宣告之後）。

      ```jsp
      <%@page import="java.util.Map"%>
      ```

   1. 將取得每個自訂屬性之值的函式的下列程式碼新增至檔案結尾：

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

   1. 在開始之前，新增以下內容 &lt;tr> 標籤(&lt;tr attrs.build=&quot;&quot;>>)：

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

      在程式碼中，GeoLocation是您在建立自訂節點/欄位時，於name屬性中設定的值。 建立自訂節點/欄位時，您指定屬性的名稱給。/extendedproperties/前置詞： 。/extendedproperties/GeoLocation。 在程式碼中，首碼並非必要。

   1. 若要在UI中顯示新屬性，請在結尾的tr (&lt;/tr>)標籤：

      ```jsp
      <td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
      ```

      若要新增更多欄，請重複步驟6.3和6.4。

   1. 按一下&#x200B;**「儲存全部」**。

1. 若要檢視您的自訂，請開啟檔案片段清單檢視，或您已新增自訂屬性的字母。

   此程式中新增的UI欄和屬性會針對所有資產型別顯示。 不過，您只能針對您最初新增自訂屬性的資產型別，輸入及顯示這些屬性中的值。

   例如，使用「案例：為特定資產型別新增自訂屬性」時，若將自訂屬性新增至文字資產，您只能為文字資產輸入自訂屬性。 但是，如果您在UI中顯示該自訂屬性，則所有資產型別都會出現該欄。

   ![custompropertyinlistview](assets/custompropertyinlistview.png)

1. （選擇性）依預設，新欄會顯示為UI中的最後一欄。 若要讓欄出現在特定位置，請將下列屬性新增至欄節點：

<table>
 <tbody>
  <tr>
   <td><strong>名稱</strong></td>
   <td><strong>類型</strong></td>
   <td><strong>值</strong></td>
  </tr>
  <tr>
   <td>sling：orderBefore</td>
   <td>字串</td>
   <td><p>位於路徑「/libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/list/columns」的欄節點名稱，在該路徑之前，自訂欄需要出現在UI上。</p> <p>如果您想要地理位置欄顯示在「版本」欄之前（左側），請將sling：orderBefore屬性新增至位於路徑「/apps/fd/cm/ma/gui/content/cmassets/jcr：content/views/list/columns/GeoLocation」的GeoLocation節點，並將屬性的值設定為version。</p> </td>
  </tr>
 </tbody>
</table>

新增sling：orderBefore屬性以指定欄位置時，您也需要更新對應位置的順序 &lt;td> 此程式的步驟6.4中指定的標籤。 例如，在此情況下，您需要確保 &lt;td> 地理位置的標籤會放在之前 &lt;td> 「版本」欄的標籤：

```xml
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(geographicalLocation) %>"><%= xssAPI.encodeForHTML(geographicalLocation) %></td>
<td is="coral-td" value="<%= xssAPI.encodeForHTMLAttr(version) %>"><%= xssAPI.encodeForHTML(version) %></td>
```

## 啟用自訂屬性搜尋 {#enable-search-for-custom-properties}

依預設，全文檢索搜尋不包含您使用CRX/DE新增到UI的自訂屬性。

若要在搜尋中包含自訂屬性，您必須允許建立自訂屬性的索引。

若要允許建立自訂屬性的索引，請完成以下步驟：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 前往 `/oak:index/cmLucene`並新增名為的節點 **彙總** 在其下方。

   1. 以滑鼠右鍵按一下cmLucene資料夾並選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 彙總

      **型別：** nt：unstructured

   1. 按一下&#x200B;**「儲存全部」**。

1. 在新建立的彙總資料夾下，新增節點cm：resource。 在cm：resource底下，新增名為include0的節點。

   1. 在彙總資料夾上按一下滑鼠右鍵，然後選取 **建立** > **建立節點**. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** cm：resource

      **型別：** nt：unstructured

   1. 以滑鼠右鍵按一下cm：resource資料夾並選取 **建立** > **建立節點**. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** include0

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處為include0）。 CRX會顯示節點的屬性。
   1. 將下列屬性新增至節點（此處為include0）：

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
           <td>extendedProperties<br /> </td>
         </tr>
         </tbody>
       </table>

   1. 按一下&#x200B;**「儲存全部」**。

1. 前往下列位置的屬性，並在其下方新增節點位置： `/oak:index/cmLucene/indexRules/cm:resource/properties`

   針對您想要新增至搜尋的每個自訂屬性重複此步驟。

   1. 以滑鼠右鍵按一下屬性資料夾並選取 **建立** > **建立節點**.
   1. 確定「建立節點」對話方塊具有下列值，然後按一下 **確定**：

      **名稱：** 位置（或您要新增至搜尋的自訂屬性名稱）

      **型別：** nt：unstructured

   1. 按一下您已建立的新節點（此處為位置）。 CRX會顯示節點的屬性。
   1. 將下列屬性新增至節點（此處為位置）：

      | **名稱** | **類型** | **值** |
      |---|---|---|
      | 已分析 | 字串 | true |
      | 名稱 | 字串 | extendedProperties/location （或您要新增至搜尋的屬性名稱） |
      | propertyIndex | 布林值 | true |
      | useInSuggest | 布林值 | true |

   1. 按一下&#x200B;**「儲存全部」**。

1. 現在，您可以在全文檢索搜尋中使用自訂屬性值，以找出相關資產。

>[!NOTE]
>
>如果您還是無法搜尋，可能是因為索引問題。 若要重新索引，請前往以下節點並將屬性「重新索引」的值變更為true：
>
>/oak：index/cmLucene&quot;並變更屬性的值

## 變更搜尋頁面的預設檢視 {#change-default-view-of-the-search-page}

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，建立名為的資料夾，其路徑/結構類似於/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views中的清單資料夾：

   1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

      `/libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/granite/ui/content/shell/omnisearch/searchresults/singleresults/views/list

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

   1. 按一下&#x200B;**「儲存全部」**。

1. 在新建立的節點清單中，新增以下屬性並按一下 **全部儲存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling：orderBefore<br /> </td>
      <td>字串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 自訂功能會在清單檢視中顯示所有主控台的搜尋結果，包括Forms以及檔案、資產和網站。

## 變更資產頁面的預設檢視 {#change-default-view-of-the-assets-page}

>[!NOTE]
>
>這些步驟會變更所有主控台的預設檢視，例如Forms和檔案、資產和網站。

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在apps資料夾中，建立名為list的資料夾，其路徑/結構類似於中的清單資料夾：

   /libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/

   1. 以滑鼠右鍵按一下下列路徑的專案資料夾，然後選取 **覆蓋節點**：

      `/libs/fd/cm/ma/gui/content/cmassets/jcr:content/views/list`

   1. 請確定「覆蓋節點」對話方塊是否具備下列值：

      **路徑：** /libs/fd/cm/ma/gui/content/cmassets/jcr：content/views/list

      **位置：** /apps/

      **符合節點型別：** 已選取

   1. 按一下 **確定**. 資料夾結構會在apps資料夾中建立。

   1. 按一下&#x200B;**「儲存全部」**。

1. 在新建立的節點清單中，新增以下屬性並按一下 **全部儲存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling：orderBefore<br /> </td>
      <td>字串</td>
      <td>卡片</td>
   </tr>
   </tbody>
   </table>

1. 清除瀏覽器Cookie或使用瀏覽器的無痕模式來檢視資產。 預設情況下，資產頁面會顯示在卡片配置中。

## 在「資產建立」和「屬性」頁面上顯示/隱藏自訂屬性 {#show-hide-custom-properties-on-asset-creation-and-properties-pages}

若要顯示或隱藏自訂屬性，請完成下列步驟：

1. 在自訂屬性節點（例如geographicallocation）底下，建立名稱為「granite：rendercondition」且型別為「nt：unstructured」的節點。
1. 將下列屬性新增至節點，然後按一下 **全部儲存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>sling：resourceType<br /> </td>
      <td>字串</td>
      <td>fd/cm/ma/gui/components/admin/assetsproperties/custompropertyconfig<br /> </td>
   </tr>
   </tbody>
   </table>

1. 若要在資產建立頁面上隱藏此屬性，請在其中新增以下屬性，然後按一下 **全部儲存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>hideOnCreate<br /> </td>
      <td>布林值</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

1. 若要隱藏資產屬性頁面上的自訂屬性，請新增以下屬性至其中，然後按一下 **全部儲存**：

   <table>
   <tbody>
   <tr>
      <td><strong>名稱</strong></td>
      <td><strong>類型</strong></td>
      <td><strong>值</strong></td>
   </tr>
   <tr>
      <td>hideOnedit<br /> </td>
      <td>布林值</td>
      <td>true<br /> </td>
   </tr>
   </tbody>
   </table>

   若要再次顯示值，請將屬性值重設為 `false` 或刪除屬性專案。
