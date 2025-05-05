---
title: 產生最適化表單的記錄檔案
description: 說明如何為最適化表單產生記錄檔案(DoR)。
content-type: reference
topic-tags: adaptive_forms, develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 7240897f-6b3a-427a-abc6-66310c2998f3
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '4308'
ht-degree: 3%

---

# 產生最適化表單或最適化表單片段的記錄檔案 {#generate-document-of-record-for-adaptive-forms}

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=zh-Hant)，用來[建立新的最適化表單](/help/forms/using/create-an-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |


## 概觀 {#overview}

提交表單後，您的客戶通常希望以列印或檔案格式來記錄他們在表單中填寫的資訊，以供日後參考。 這稱為記錄檔案。

本文說明如何產生Adaptive Forms或Adaptive Form片段的記錄檔案。

>[!NOTE]
>
> AEM 6.5 Forms Service Pack 19 (6.5.19.0)引進自訂最適化表單片段及其在最適化表單編輯器中欄位的支援。


>[!NOTE]
>
>XFA型調適型表單不支援自動產生記錄檔案。 不過，您可以使用用來建立最適化表單作為記錄檔案的XDP。

## 最適化表單型別及其記錄檔案 {#adaptive-form-types-and-their-documents-of-record}

建立最適化表單時，您可以選取表單模型。 您的選項有：

* [表單範本](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-an-xfa-form-template)
可讓您為最適化表單選取XFA範本。 當您選取XFA範本時，您可以使用關聯的XDP檔案作為記錄檔案，如上所述。

* [XML結構描述](../../forms/using/creating-adaptive-form.md#create-an-adaptive-form-based-on-xml-or-json-schema)
讓您為最適化表單選取XML結構描述定義。 當您為最適化表單選取XML結構描述時，您可以：

   * 為記錄檔案建立XFA範本的關聯。 確保關聯的XFA範本使用與您的調適型表單相同的XML結構描述
   * 自動生成記錄檔案

* 無
讓您建立不含表單模型的最適化表單。 系統會自動為您的最適化表單產生記錄檔案。

當您選取表單模型時，請使用「記錄檔案範本組態」下可用的選項來設定記錄檔案。 請參閱[記錄範本檔案組態](#document-of-record-template-configuration)。

## 自動產生的記錄檔案 {#automatically-generated-document-of-record}

記錄檔案可讓您的客戶保留已提交表單的復本以供列印。 當您自動產生記錄檔案時，每次變更表單時，其記錄檔案都會立即更新。 例如，您會為選取美國作為其國家/地區的客戶移除年齡欄位。 當這類客戶產生記錄檔案時，他們無法在記錄檔案中看到年齡欄位。

自動產生的記錄檔案具有以下優點：

* 它會處理資料繫結。
* 它會自動隱藏在提交時標籤為從記錄檔案中排除的欄位。 不需要額外付出。
* 這樣可節省設計記錄範本檔案的時間。
* 它可讓您使用不同的基本範本嘗試不同的樣式和外觀，並為記錄檔案選擇最佳的樣式和外觀。 造型外觀是選用的，如果您未指定造型，系統樣式會設定為預設值。
* 它可確保表單中的任何變更都立即反映在記錄檔案中。

## 自動產生記錄檔案的元件 {#components-to-automatically-generate-a-document-of-record}

若要產生最適化表單的記錄檔案，您需要下列元件：

**最適化表單**&#x200B;您要為其產生記錄檔案的最適化表單。

您要產生記錄檔案的&#x200B;**最適化表單片段**&#x200B;最適化表單片段。

在AEM Designer中建立的&#x200B;**Base範本（建議）** XFA範本（XDP檔案）。 基礎範本用於指定記錄檔案範本的樣式和品牌資訊。

檢視記錄檔案的[基底範本](#base-template-of-a-document-of-record)

>[!NOTE]
>
>記錄檔案的基礎範本也稱為記錄檔案的中繼範本。

從最適化表單產生的&#x200B;**記錄檔案範本** XFA範本（XDP檔案）。

請參閱[記錄範本檔案組態](#document-of-record-template-configuration)。

**表單資料**&#x200B;使用者以最適化表單填寫的資訊。 它與記錄檔案範本合併以產生記錄檔案。

## 最適化表單元素的對應 {#mapping-of-adaptive-form-elements}

以下章節說明最適化表單元素在記錄檔案中的顯示方式。

### 欄位 {#fields}

<table>
 <tbody>
  <tr>
   <th>最適化表單元件</th>
   <th>對應的XFA元件</th>
   <th>預設包含在記錄檔案範本中？</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>按鈕</td>
   <td>按鈕</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>核取方塊</td>
   <td>核取方塊</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>日期挑選器</td>
   <td>日期/時間欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>下拉式清單</td>
   <td>下拉式清單</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>草寫簽名</td>
   <td>手寫簽名</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>數值方塊</td>
   <td>數值欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>密碼方塊</td>
   <td>密碼欄位</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>選項按鈕</td>
   <td>選項按鈕</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>文字方塊</td>
   <td>文字欄位</td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>重設按鈕</td>
   <td>重設按鈕</td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>提交按鈕</td>
   <td><p>電子郵件提交按鈕</p> <p>HTTP提交按鈕</p> </td>
   <td>false</td>
   <td> </td>
  </tr>
  <tr>
   <td>條款與條件</td>
   <td> </td>
   <td>true</td>
   <td> </td>
  </tr>
  <tr>
   <td>檔案附件</td>
   <td> </td>
   <td>false</td>
   <td>在記錄範本檔案中無法使用。 只能透過附件在記錄檔案中使用。</td>
  </tr>
 </tbody>
</table>

### 容器 {#containers}

<table>
 <tbody>
  <tr>
   <th>最適化表單元件</th>
   <th>對應的XFA元件</th>
   <th>附註</th>
  </tr>
  <tr>
   <td>面板<br /> </td>
   <td>子表單<br /> </td>
   <td>可重複面板對應至可重複的子表單。</td>
  </tr>
 </tbody>
</table>

### 靜態元件 {#static-components}

| 最適化表單元件 | 對應的XFA元件 | 附註 |
|---|---|---|
| 影像 | 影像 | 除非使用記錄檔案設定加以排除，否則TextDraw和Image元件（無論已繫結或未繫結）一律會出現在XSD型調適型表單的記錄檔案中。 |
| 文字 | 文字 |

>[!NOTE]
>
>在傳統UI中，您會獲得不同的索引標籤來編輯欄位屬性。

### 表格 {#tables}

最適化表單元件（例如頁首、頁尾和列）對應到對應的XFA元件。 您可以將可重複面板對應至記錄檔案中的表格。

## 記錄檔案的基礎範本 {#base-template-of-a-document-of-record}

基礎範本為記錄檔案提供樣式和外觀資訊。 它可讓您自訂自動產生記錄檔案的預設外觀。 例如，您想要在檔案的頁首中新增公司標誌，並在頁尾中新增版權資訊。 基礎範本的主版頁面會作為記錄檔案範本的主版頁面。 主版頁面可以包含頁首、頁尾和頁碼等資訊，您可以將這些資訊套用至記錄檔案。 您可以使用基礎範本將此類資訊套用至記錄檔案，以自動產生記錄檔案。 使用基礎範本可讓您變更欄位的預設屬性。

設計基本範本時，請務必遵循[基本範本慣例](#base-template-conventions)。

## 基礎範本慣例 {#base-template-conventions}

基礎範本用於定義記錄檔案的頁首、頁尾、樣式和外觀。 頁首和頁尾可包含公司標誌和版權文字等資訊。 基礎範本中的第一個主版頁面會被複製並用作記錄檔案的主版頁面，其中包含頁首、頁尾、頁碼或應出現在記錄檔案所有頁面上的任何其他資訊。 如果您使用的基底範本不符合基底範本慣例，則基底範本中的第一個主版頁面仍會用於記錄檔案範本中。 強烈建議您依照其慣例設計基礎範本，並用於自動產生記錄檔案。

**主版頁面慣例**

* 在基底範本中，您應該將根子表單命名為`AF_METATEMPLATE`，並將主版頁面命名為`AF_MASTERPAGE`。

* 名稱為`AF_MASTERPAGE`的主版頁面位於`AF_METATEMPLATE`根子表單下，其優先選項為擷取頁首、頁尾和樣式資訊。

* 如果`AF_MASTERPAGE`不存在，則會使用基底範本中存在的第一個主版頁面。

**欄位的樣式慣例**

* 若要在記錄檔案中的欄位套用樣式，基底範本會提供`AF_METATEMPLATE`根子表單下`AF_FIELDSSUBFORM`子表單中的欄位。

* 這些欄位的屬性會套用至記錄檔案中的欄位。 這些欄位應遵循`AF_<name of field in all caps>_XFO`命名慣例。 例如，核取方塊的欄位名稱應該是`AF_CHECKBOX_XFO`。

若要建立基礎範本，請在AEM Designer中執行下列動作。

1. 按一下&#x200B;**檔案>新增**。
1. 選取&#x200B;**根據範本**&#x200B;選項。

1. 選取&#x200B;**Forms — 記錄檔案**&#x200B;類別。
1. 選取&#x200B;**DoR基底範本**。
1. 按一下[下一步]&#x200B;**&#x200B;**&#x200B;並提供必要的資訊。

1. （選擇性）修改您要在記錄檔案中欄位上套用的欄位樣式和外觀。
1. 儲存表單。

您現在可以使用儲存的表單作為記錄檔案的基礎範本。
請勿修改或移除基礎範本中存在的任何指令碼。

**正在修改基底範本**

* 如果您未在基礎範本的欄位上套用任何樣式，建議您從基礎範本中移除這些欄位，以便自動擷取對基礎範本的任何升級。
* 修改基底範本時，請勿移除、新增或修改指令碼。

>[!NOTE]
>
>使用慣例並嚴格遵循上述步驟來設計基礎範本。

## 記錄範本文件配置 {#document-of-record-template-configuration}

設定表單的記錄檔案範本，讓客戶下載已提交表單的易列印復本。 XDP檔案可作為記錄檔案範本。 客戶下載的記錄檔案會根據XDP檔案中指定的版面進行格式化。

執行以下步驟來設定最適化表單的記錄檔案：

1. 在AEM編寫執行個體中，按一下&#x200B;**Forms > Forms和檔案。**
1. 選取表單，然後按一下&#x200B;**檢視內容**。
1. 在[內容]視窗中，選取&#x200B;**表單模型**。
您也可以在建立表單時選取表單模型。

   >[!NOTE]
   >
   >在[表單模型]索引標籤中，確定您從&#x200B;**從**&#x200B;選取下拉式清單中選取&#x200B;**結構描述**&#x200B;或&#x200B;**無**。 **[!UICONTROL 以表單範本作為表單模型的XFA式或調適型表單不支援記錄檔案。]**

1. 在「表單模型」標籤的「記錄檔案範本組態」區段中，選取下列其中一個選項：

   **無**&#x200B;如果您不想設定表單的記錄檔案，請選取此選項。

   **將表單範本關聯為記錄檔案範本**&#x200B;如果您有要做為記錄檔案範本使用的XDP檔案，請選取此選項。 選取此選項時，會顯示AEM Forms存放庫中可用的所有XDP檔案。 選取適當的檔案。

   選取的XDP檔案會與最適化表單建立關聯。

   **產生記錄檔案**&#x200B;選取此選項以使用XDP檔案作為定義記錄檔案樣式和外觀的基礎範本。 選取此選項時，會顯示AEM Forms存放庫中可用的所有XDP檔案。 選取適當的檔案。

   >[!NOTE]
   >
   >在下列情況下，請確定用來建立調適型表單的結構描述與XFA表單的結構描述（資料結構描述）相同：
   >
   >
   >
   >    * 您的最適化表單是以結構描述為基礎
   >    * 您正在使用&#x200B;**關聯表單範本作為記錄檔案的記錄檔案範本**&#x200B;選項
   >
   >

1. 按一下&#x200B;**完成。**

## 自訂記錄檔案中的品牌資訊 {#customize-the-branding-information-in-document-of-record}

產生記錄檔案時，您可以在記錄檔案索引標籤上變更記錄檔案的品牌資訊。 「記錄檔案」索引標籤包括如標誌、外觀、版面、頁首和頁尾、免責宣告等選項，以及您是否要包含未選取的核取方塊和選項按鈕選項。

若要將您在「記錄檔案」標籤中輸入的品牌資訊當地語系化，您必須確保已正確設定瀏覽器的地區設定。 若要自訂記錄檔案的品牌資訊，請完成下列步驟：

1. 選取記錄檔案中的面板（根面板），然後選取![設定](assets/configure.png)。
1. 選取![多標籤](/help/forms/using/assets/dortab.png)。 記錄檔案索引標籤隨即顯示。
1. 選取呈現記錄檔案的預設範本或自訂範本。 如果您選取預設範本，記錄檔案的縮圖預覽會顯示在「範本」下拉式清單下方。

   ![brandingtemplate](/help/forms/using/assets/brandingtemplateupdate.png)

   如果您選擇選取自訂範本，請在AEM Forms伺服器上瀏覽並選取XDP。 如果您想使用AEM Forms伺服器上尚未存在的範本，您必須先將XDP上傳至AEM Forms伺服器。

### 主版頁面屬性(#master-page-properties)

根據您選取預設或自訂範本，下列部分或全部主版頁面屬性會顯示在「記錄檔案」標籤中，如上圖所示。 適當地指定下列專案：

* **標誌影像**：您可以選擇使用最適化表單的標誌影像、從DAM中選擇標誌影像，或從您的電腦上傳標誌影像。
* **表單標題**
* **標頭文字**
* **免責宣告標籤**
* **免責宣告**
* **免責宣告文字**

  <!--
    * **Accent Color**: The color in which header text and separator lines are rendered in the document or record PDF
    * **Font Family**: Font family of the text in the document of record PDF
    * **For Check Box and Radio Button components, show only the selected values**
    * **Separator for multiple selected value(s)**
    * **Include form objects that are not bound to data model**
    * **Exclude hidden fields from the document of record**
    * **Hide description of panels**
    -->

  如果您選取的自訂XDP範本包含多個主版頁面，則這些頁面的屬性會顯示在&#x200B;**[!UICONTROL 記錄檔案]**&#x200B;索引標籤的&#x200B;**[!UICONTROL 內容]**&#x200B;區段中。

  ![主版頁面屬性](assets/master-page-properties.png)

  主版頁面的屬性包括標誌影像、頁首文字、表單標題、免責宣告標籤和免責宣告文字。 您可以將最適化表單或XDP範本屬性套用至記錄檔案。 AEM Forms預設會將範本屬性套用至記錄檔案。 您也可以定義主版頁面屬性的自訂值。 如需如何在記錄檔案中套用多個主版頁面的詳細資訊，請參閱[將多個主版頁面套用至記錄檔案](#apply-multiple-master-pages-dor)。

  >[!NOTE]
  >
  >如果您使用以6.3版之前的Designer版本建立的調適型表單範本，為了使輔色和字型系列屬性發揮作用，請確定根子表單下的調適型表單範本中存在下列專案：

  ```xml
  <proto>
  <font typeface="Arial"/>
  <fill>
  <color value="4,166,203"/>
  </fill>
  <edge>
  <color value="4,166,203"/>
  </edge>
  </proto>
  ```

1. 若要儲存品牌變更，請選取「完成」。

## 記錄檔案中面板的表格和欄配置 {#table-and-column-layouts-for-panels-in-document-of-record}

您的最適化表單可能會很長，包含多個表單欄位。 您可能不想將記錄檔案儲存為最適化表單的精確副本。 現在您可以選擇表格或欄版面配置，以將一或多個最適化表單面板儲存在記錄檔案PDF中。

在產生記錄檔案之前，在面板的設定中，選取該面板的「記錄檔案配置」(Layout For the Document Of Record for the Panel)，作為「表格」或「欄」。 面板中的欄位會在記錄檔案中進行相應的組織。

![面板中的欄位在記錄檔案中以資料表配置呈現](assets/dortablelayout.png)

面板中的欄位在記錄檔案中以表格佈局呈現

![在記錄檔案中以欄配置呈現的面板欄位](assets/dorcolumnlayout.png)

面板中的欄位在記錄檔案中的欄配置中轉譯

## 記錄檔案設定 {#document-of-record-settings}

記錄檔案設定可讓您選擇要包含在記錄檔案中的選項。 例如，銀行可接受表單中的姓名、年齡、社保號碼和電話號碼。 此表單會產生銀行帳號及分行詳細資訊。 您可以選擇在記錄檔案中只顯示名稱、社會安全號碼、銀行帳戶和分行詳細資訊。

元件的記錄檔案設定可在其屬性下使用。 若要存取元件的屬性，請選取該元件，然後按一下覆蓋圖中的![cmppr](assets/cmppr.png)。 屬性會列在側邊欄中，您可在其中找到下列設定。

**欄位層級設定**

* **從記錄檔案排除**：設定屬性True會從記錄檔案排除欄位。 這是名為`excludeFromDoR`的指令碼屬性。 其行為取決於若隱藏&#x200B;**表單層級屬性，則從DoR排除**&#x200B;欄位。

* **將面板顯示為表格：**&#x200B;如果面板中有少於6個欄位，則設定屬性將面板顯示為記錄檔案中的表格。 僅適用於面板。
* **從記錄檔案排除標題：**&#x200B;設定屬性會從記錄檔案排除面板/表格的標題。 僅適用於面板和表格。
* **從記錄檔案排除描述：**&#x200B;設定屬性會從記錄檔案排除面板/表格的描述。 僅適用於面板和表格。
* **[!UICONTROL 分頁]** > **[!UICONTROL 置入]**：決定您要置入面板的位置。
   * **[!UICONTROL 置入]** > **[!UICONTROL 先前專案]**：將面板置於父面板中的前一個物件之後。
   * **[!UICONTROL 放置]** > **[!UICONTROL 在內容區域中]** >內容區域的名稱：將面板放置在指定的內容區域中。
   * **[!UICONTROL 放置]** > **[!UICONTROL 置於下一個內容區域頂端]**：將面板置於下一個內容區域頂端。
   * **[!UICONTROL 放置]** > **[!UICONTROL 內容區域頂端]** >內容區域名稱：將面板放置在指定內容區域的頂端。
   * **[!UICONTROL 放置]** > **[!UICONTROL 在頁面]** >主版頁面的名稱：將面板放置在指定的頁面上。 如果未自動插入分頁，[!DNL AEM Forms]會新增分頁。
   * **[!UICONTROL 置入]** > **[!UICONTROL 下一頁頂端]**：將面板置於下一頁頂端。 如果未自動插入分頁，[!DNL AEM Forms]會新增分頁。
   * **[!UICONTROL 置入]** > **[!UICONTROL 頁面頂端]** >主版頁面的名稱：呈現指定的頁面時，將面板置於頁面頂端。 如果未自動插入分頁，[!DNL AEM Forms]會新增分頁。
* **[!UICONTROL 分頁]** > **[!UICONTROL After]**：決定置入面板後要填滿的區域。**[!UICONTROL After]**&#x200B;區段中可用的欄位如下：
   * **[!UICONTROL After]** > **[!UICONTROL 繼續填滿上層]**：繼續合併上層面板中剩餘要填滿之所有物件的資料。
   * **[!UICONTROL After]** > **[!UICONTROL 移至下一個內容區域]**：在放置面板後，開始填入下一個內容區域。
   * **[!UICONTROL After]** > **[!UICONTROL 移至內容區域]** >內容區域名稱：在放置面板後，開始填入指定的內容區域。
   * **[!UICONTROL After]** > **[!UICONTROL 移至下一頁]**：在放置面板後開始填入下一頁。
   * **[!UICONTROL After]** > **[!UICONTROL 移至頁面]** >頁面名稱：開始填入指定的頁面。
* **[!UICONTROL 分頁]** > **[!UICONTROL 溢位]**：設定跨頁面的面板或資料表的溢位。 **[!UICONTROL 溢位]**&#x200B;區段中有下列欄位：
   * **[!UICONTROL 溢位]** > **[!UICONTROL 無]**：開始填入下一頁。 如果未自動插入分頁，[!DNL AEM Forms]會新增分頁。
   * **[!UICONTROL 溢位]** > **[!UICONTROL 移至內容區域]** >內容區域名稱：開始填入指定的內容區域。
   * **[!UICONTROL 溢位]** > **[!UICONTROL 移至頁面]** >頁面名稱：開始填入指定的頁面。

  >[!NOTE]
  >
  > 分頁屬性不適用於最適化表單片段。

如需如何在記錄檔案中套用分頁符號和套用多個主版頁面的詳細資訊，請參閱[在記錄檔案中套用分頁符號](#apply-page-breaks-in-dor)和[將多個主版頁面套用至記錄檔案](#apply-multiple-master-pages-dor)。

**表單層級設定**

* **[!UICONTROL 基本]**
   * **範本：**&#x200B;您可以選取[預設]或[自訂]範本。

     ![替代文字](image.png)
   * **強調色：**&#x200B;您可以預先定義[!UICONTROL 記錄檔案]的範本顏色。
   * **字型系列：**&#x200B;為[!UICONTROL 記錄檔案]文字選取字型型別。
   * **包含未繫結欄位於DoR：**&#x200B;設定屬性包含來自[!UICONTROL 記錄檔案]中結構描述型最適化表單的未繫結欄位。 預設為true。
   * **若隱藏則從DoR排除欄位：**&#x200B;設定屬性以在表單提交時從[!UICONTROL 記錄檔案]排除隱藏欄位。 當您在伺服器[&#128279;](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form-server-side-revalidation-in-adaptive-form)上啟用重新驗證時，伺服器會先重新計算隱藏的欄位，然後再從[!UICONTROL 記錄檔案]中排除這些欄位
* **[!UICONTROL 表單欄位屬性]**
   * 如果勾選選項&#x200B;**對於核取方塊與選項按鈕元件，只顯示選取的值**，它將只產生具有選取值的DoR輸出。
   * 您可以為多個選取的值選取「分隔符號」，也可以選擇任何其他分隔符號型別。
   * 選項對齊方式
      * 垂直
      * 水平
      * 與自適應表單相同

     >[!NOTE]
     > 「垂直」和「水準」對齊方式僅適用於     選項按鈕與核取方塊
* **[!UICONTROL 主版頁面屬性]**&#x200B;按一下以取得有關[主版頁面屬性](#master-page-properties-master-page-properties)的詳細資訊

## 在記錄檔案中套用分頁符號 {#apply-page-breaks-in-dor}

您可以使用多種方法在記錄檔案中套用分頁符號。

若要將分頁套用至記錄檔案：

1. 選取面板並選取![設定](/help/forms/using/assets/configure.png)
1. 展開&#x200B;**[!UICONTROL 記錄檔案]**&#x200B;以檢視內容。

1. 在&#x200B;**[!UICONTROL 分頁]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 位置]**&#x200B;欄位中的![資料夾](/help/forms/using/assets/folder-icon.png)。
1. 選取&#x200B;**[!UICONTROL 下一頁頂端]**&#x200B;並選取&#x200B;**[!UICONTROL 選取]**。 您也可以選取&#x200B;**[!UICONTROL 頁面頂端]**，選取主版頁面，然後選取&#x200B;**[!UICONTROL 選取]**&#x200B;以套用分頁符號。
1. 選取![儲存](/help/forms/using/assets/save_icon.png)以儲存屬性。

選取的面板會移至下一頁。

## 套用多個主版頁面至記錄檔案 {#apply-multiple-master-pages-dor}

如果您選取的自訂XDP範本包含多個主版頁面，則這些頁面的屬性會顯示在[!UICONTROL 記錄檔案]索引標籤的[!UICONTROL 內容]區段中。 如需詳細資訊，請參閱[自訂記錄檔案](#customize-the-branding-information-in-document-of-record)中的品牌資訊。

您可以將不同的主版頁面套用至最適化表單的元件，以將多個主版頁面套用至記錄檔案。 使用記錄檔案屬性的[分頁](#document-of-record-settings)區段來套用多個主版頁面。

以下是如何將多個主版頁面套用至記錄檔案的範例：
您上傳包含四個主版頁面的XDP範本至[!DNL AEM Forms]伺服器。 [!DNL AEM Forms]預設會將範本屬性套用至記錄檔案。 [!DNL AEM Forms]也會將範本中的第一個主版頁面屬性套用至記錄檔案。

若要將第二個主版頁面屬性套用至面板，並將第三個主版頁面屬性套用至後續面板，請執行下列步驟：

1. 選取要套用第二個主版頁面的面板，然後選取![設定](assets/cmppr.png)。
1. 在&#x200B;**[!UICONTROL 分頁]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 位置]**&#x200B;欄位中的![資料夾](/help/forms/using/assets/folder-icon.png)。
1. 選取&#x200B;**[!UICONTROL 在頁面]**&#x200B;上，選取第二個主版頁面並選取&#x200B;**[!UICONTROL 選取]**。
AEM Forms會套用第二個主版頁面至面板，以及最適化表單中的所有後續面板。
1. 在&#x200B;**[!UICONTROL 分頁]**&#x200B;區段中，選取&#x200B;**[!UICONTROL After]**&#x200B;欄位中的![資料夾](/help/forms/using/assets/folder-icon.png)。
1. 選取&#x200B;**[!UICONTROL 移至頁面]**，選取第三個主版頁面，然後選取&#x200B;**[!UICONTROL 選取]**。
1. 選取![儲存](/help/forms/using/assets/save_icon.png)以儲存屬性。
AEM Forms會套用第三個主版頁面至面板，以及最適化表單中的所有後續面板。

>[!NOTE]
>
> 您無法將多個主版頁面套用至最適化表單片段的記錄檔案。

## 使用記錄檔案時的主要考量事項 {#key-considerations-when-working-with-document-of-record}

處理最適化表單的記錄檔案時，請謹記下列考量事項和限制。

* 記錄範本的檔案不支援RTF文字。 因此，靜態最適化表單中或一般使用者填入的資訊中的任何RTF文字都會在記錄檔案中顯示為純文字。
* 最適化表單中的檔案片段未出現在記錄檔案中。 不過，也支援最適化表單片段。
* 不支援根據XML結構描述的最適化表單產生的記錄檔案中的內容繫結。
* 當使用者請求轉譯記錄檔案時，會根據地區設定的需求建立記錄檔案的當地語系化版本。 記錄檔案本地化與最適化表單本地化同時發生。 如需記錄檔案和最適化表單本地化的詳細資訊，請參閱[使用AEM翻譯工作流程將最適化表單和記錄檔案本地化](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md)。

## 使用自訂XCI檔案

XCI檔案可協助您設定檔案的各種屬性。 <!-- Forms as a Cloud Service has a master XCI file.-->您可以使用自訂XCI檔案來覆寫在現有XCI檔案中指定的一個或多個預設屬性。 例如，您可以選擇將字型內嵌到檔案中，或是為所有檔案啟用標籤屬性。 下表指定XCI選項：

| XCI選項 | 說明 |
|--- |--- |
| config/present/pdf/creator | 使用檔案資訊字典中的建立者專案來識別檔案建立者。 如需此字典的相關資訊，請參閱[PDF參考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)。 |
| config/present/pdf/producer | 使用檔案資訊字典中的製作者專案來識別檔案製作者。 如需此字典的相關資訊，請參閱[PDF參考指南](https://opensource.adobe.com/dc-acrobat-sdk-docs/acrobatsdk/)。 |
| config/present/layout | 控制輸出是單一面板還是分頁。 |
| config/present/pdf/compression/level | 指定產生PDF檔案時要使用的壓縮程度。 |
| config/present/pdf/fontInfo/embed | 控制輸出檔案中的字型內嵌。 |
| config/present/pdf/scriptModel | 控制輸出PDF檔案中是否包含XFA特定資訊。 |
| config/present/common/data/adjustData | 控制XFA應用程式是否會在合併後調整資料。 |
| config/present/pdf/renderPolicy | 控制頁面內容的產生是在伺服器上完成，還是延後至使用者端。 |
| config/present/common/locale | 指定輸出檔案中使用的預設地區設定。 |
| config/present/destination | 當由目前元素包含時，指定輸出格式。 當由openAction元素包含時，會指定在互動式使用者端中開啟檔案時要執行的動作。 |
| config/present/output/type | 指定要套用至檔案的壓縮型別，或是要產生的輸出型別。 |
| config/present/common/temp/uri | 指定表單URI。 |
| config/present/common/template/base | 提供表單設計中基本的URI位置。 當此元素不存在或空白時，會使用表單設計的位置作為基礎。 |
| config/present/common/log/to | 控制記錄資料或輸出資料寫入的位置。 |
| config/present/output/to | 控制記錄資料或輸出資料寫入的位置。 |
| config/present/script/currentPage | 指定開啟檔案時的初始頁面。 |
| config/present/script/exclude | 通知Formsas a Cloud Service忽略哪些事件。 |
| config/present/pdf/linearized | 控制是否將輸出PDF檔案線性化。 |
| config/present/script/runScripts | 控制Forms as a Cloud Service執行的指令碼集。 |
| config/present/pdf/tagged | 控制標籤在輸出PDF檔案中是否包含。 在PDF的內容中，標籤是包含在檔案中的其他資訊，用於公開檔案的邏輯結構。 標籤有助於協助協助工具及重新格式化。 例如，頁碼可能會被標籤為成品，這樣熒幕閱讀器就不會在文字中間朗讀它。 雖然標籤讓檔案變得更實用，但它們也會增加檔案的大小，以及建立檔案的處理時間。 |
| config/present/pdf/fontInfo/alwaysEmbed | 指定內嵌在輸出檔案中的字型。 |
| config/present/pdf/fontInfo/neverEmbed | 指定不得嵌入至輸出檔案的字型。 |
| config/present/pdf/pdfa/part | 指定檔案符合的PDF/A規格的版本號碼。 |
| config/present/pdf/pdfa/amd | 指定PDF/A規格的修訂層次。 |
| config/present/pdf/pdfa/conformance | 指定符合PDF/A規格的等級。 |
| config/present/pdf/version | 指定要產生的PDF檔案版本 |
| config/present/pdf/version/map | 指定檔案的回覆字型 |


<!--

### Use a custom XCI file in your AEM Forms environment

  1. Add the custom XCI file to your development project.
  1. Specify the following inline property:(/help/implementing/deploying/configuring-osgi.md)
  1. Deploy the project to your AEM Forms environment. <!--Cloud Service environment
  
-->

### 在本機Forms開發環境中使用自訂XCI檔案

1. 上傳XCI檔案至您的本機開發環境。
1. 開啟<!--Cloud Service SDK-->組態管理員。<!--The default URL is: <http://localhost:4502/system/console/configMgr>.-->
1. 找到並開啟&#x200B;**[!UICONTROL 最適化Forms和互動式通訊Web Channel]**&#x200B;設定。
1. 指定XCI檔案的路徑，然後按一下&#x200B;**[!UICONTROL 儲存]**。
