---
title: Adobe Campaign元件
seo-title: Adobe Campaign元件
description: 當您與Adobe Campaign整合時，使用電子報和使用表單時，可使用元件。
seo-description: 當您與Adobe Campaign整合時，使用電子報和使用表單時，可使用元件。
uuid: cc9417c9-4cc1-4554-858e-2ecd682dc92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 5afe864d-5794-4ffa-99e7-a3233f982aff
docset: aem65
exl-id: eeff89c1-41b3-403d-b4bf-c79b09b24d4a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2555'
ht-degree: 5%

---

# Adobe Campaign元件{#adobe-campaign-components}

當您與Adobe Campaign整合時，使用電子報和使用表單時，可使用元件。 本檔案將對兩者進行說明。

>[!CAUTION]
>
>已棄用AEM電子郵件元件。 由於電子郵件的性質（可合併內容和樣式）,AEM提供的現成可用電子郵件元件對客戶的重複使用有限，因為需要將自訂樣式實施至專案所需的任何元件中。
>
>您可以在專案層級實作電子郵件元件，而過時的AEM電子郵件元件則說明如何達成此目標。 不過，這些已棄用的元件不應用於專案。

## Adobe Campaign電子報元件{#adobe-campaign-newsletter-components}

所有Campaign元件都遵循[電子郵件範本最佳實務](/help/sites-administering/best-practices-for-email-templates.md)中概述的最佳實務，且是以Adobe標籤語言[HTL](https://helpx.adobe.com/tw/experience-manager/htl/using/overview.html)為基礎。

當您開啟經設定以與Adobe Campaign整合的電子報/電子郵件時，應會在&#x200B;**Adobe Campaign電子報**&#x200B;區段中看到下列元件：

* 標題 (行銷活動)
* 影像 (行銷活動)
* 連結 (行銷活動)
* Scene7 影像範本 (行銷活動)
* 目標參考 (行銷活動)
* 文字與影像 (行銷活動)
* 文字與個人化 (行銷活動)

以下章節將介紹這些元件。

![chlimage_1-81](assets/chlimage_1-81.png)

### 標題 (行銷活動) {#heading-campaign}

標題元件可以：

* 將&#x200B;**Title**&#x200B;欄位留空，以顯示目前頁面的名稱。
* 顯示在&#x200B;**Title**&#x200B;欄位中指定的文本。

您可以直接編輯&#x200B;**標題（促銷活動）**&#x200B;元件。 留空將使用頁面標題。

![chlimage_1-82](assets/chlimage_1-82.png)

您可以設定下列項目：

* ****
標題如果您想使用頁面標題以外的名稱，請在此處輸入。

* **標題層級(1、2、3、4)**
根據HTML標題大小1-4的標題層級。

下列範例顯示要顯示的標題（促銷活動）元件。

![chlimage_1-83](assets/chlimage_1-83.png)

### 影像 (行銷活動) {#image-campaign}

影像（促銷活動）元件會根據指定的參數顯示影像和隨附的文字。

您可以上傳影像，然後編輯和操控影像（例如裁切、旋轉、新增連結/標題/文字）。

您可以上傳影像，然後編輯和操控影像（例如裁切、旋轉、新增連結/標題/文字）。 您可以直接將影像從[內容尋找器](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui)拖放至元件或其「編輯」對話方塊。 您也可以按兩下「編輯」對話方塊中央區域的，以瀏覽本機檔案系統並上傳影像。 「編輯」對話方塊的兩個索引標籤也控制影像的所有定義和操作：

![chlimage_1-84](assets/chlimage_1-84.png)

載入影像時，您可以設定下列項目：

* ****
映射要映射影像，請選擇映射。您可以指定要如何建立影像映射（矩形、多邊形等）以及區域應指向的位置。

* ****
裁切選取裁切以裁切影像。使用滑鼠來裁切影像。

* ****
旋轉要旋轉影像，請選擇「旋轉」。重複使用，直到影像以您想要的方式旋轉為止。

* ****
清除移除目前的影像。

* 縮放條（僅限傳統版）
要放大或縮小影像，請使用影像下方的幻燈片條（在「確定」和「取消」按鈕上）
* ****
標題影像的標題。

* **替代**
文字：建立可存取的內容時可使用的替代文字。

* **連**
結至建立連結至您網站內的資產或其他頁面。

* ****
說明影像的說明。

* ****
大小設定影像的高度和寬度。

>[!NOTE]
>
>您必須在&#x200B;**Advanced**&#x200B;標籤的&#x200B;**Alt Text**&#x200B;欄位中輸入資訊，否則影像無法儲存，您會看到下列錯誤訊息：
>
>`Validation failed. Verify the values of the marked fields.`


下列範例顯示要顯示的影像（促銷活動）元件。

![chlimage_1-85](assets/chlimage_1-85.png)

### 連結 (行銷活動) {#link-campaign}

連結（促銷活動）元件可讓您將連結新增至電子報。 雖然您可以在觸控最佳化使用者介面中新增元件，並在相容性模式中開啟，但此元件僅可在傳統使用者介面中使用。

![chlimage_1-86](assets/chlimage_1-86.png)

您可以在&#x200B;**Display**、**URL資訊**&#x200B;或&#x200B;**Advanced**&#x200B;標籤中配置以下內容：

* **連結**
標題連結的標題。這是用戶看到的文本。

* **連結**
工具提示添加有關如何使用連結的其他資訊。

* ****
LinkType在下拉式清單中，於 
**自訂** URL和最適 **化檔案**。此欄位為必填欄位. 如果您選取自訂URL，則可提供連結URL。 如果選擇「適用性文檔」，則可以提供文檔路徑。

* **其他URL參**
數新增任何其他URL參數。按一下「新增項目」以新增多個項目。

>[!NOTE]
>
>您必須在&#x200B;**URL資訊**&#x200B;索引標籤的&#x200B;**連結類型**&#x200B;欄位中輸入資訊，否則元件無法儲存，而您會看到下列錯誤訊息：
>
>`Validation failed. Verify the values of the marked fields.`


下列範例顯示要顯示的連結（促銷活動）元件。

![chlimage_1-87](assets/chlimage_1-87.png)

### 目標參考 (行銷活動) {#targeted-reference-campaign}

目標參考（促銷活動）元件可讓您建立目標段落的參考。

在此元件中，導航到目標段落以選擇它。

按一下下拉式功能表，導覽至您要參考的段落。 完成後，按一下&#x200B;**OK**。

### 文字與影像 (行銷活動) {#text-image-campaign}

文字與影像（促銷活動）元件會新增文字區塊和影像。

![chlimage_1-88](assets/chlimage_1-88.png)

和文字與個人化（促銷活動）和影像（促銷活動）元件一樣，您可以設定：

* ****
文字輸入文字。使用工具列來修改格式、建立清單和新增連結。

* ****
影像從內容尋找器拖曳影像，或按一下以瀏覽至影像。視需要裁切或旋轉。

* **影像屬性** (**進階影像屬性**)可讓您指定下列項目：

   * ****
標題區塊的標題；將以mouseover顯示。

   * **Alt**
TextAltine文本，如果無法顯示影像，則顯示該文本。

   * **連**
結至：建立網站內資產或其他頁面的連結。

   * ****
說明影像的說明。

   * ****
大小設定影像的高度和寬度。

>[!NOTE]
>
>**Advanced**&#x200B;標籤中的&#x200B;**Alt Text**&#x200B;欄位是必需的，否則元件無法保存，您會看到以下錯誤消息：
>
>`Validation failed. Verify the values of the marked fields.`


下列範例顯示要顯示的文字與影像（促銷活動）元件。

![chlimage_1-89](assets/chlimage_1-89.png)

### 文字與個人化 (行銷活動) {#text-personalization-campaign}

文字與個人化（促銷活動）元件可讓您使用WYSIWYG編輯器輸入文字區塊，並透過[RTF編輯器](/help/sites-authoring/rich-text-editor.md)提供的功能。 此外，此元件可讓您使用Adobe Campaign提供的內容欄位和個人化區塊；另請參閱[插入個人化](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization)。

通過選擇表徵圖，可以設定文本的格式，包括字型特性、對齊方式、連結、清單和縮進。

在RTF編輯器中新增文字的方式與一般相同。 選取Adobe Campaign下拉式清單並視需要選取欄位，以新增個人化。

![chlimage_1-90](assets/chlimage_1-90.png)

您可以新增文字和內容欄位或個人化區塊以建立內容。 接下來，選取「用戶端內容」 ，以測試角色設定檔中的資料。 選取角色後，個人化欄位會自動取代為所選設定檔中的資料。

>[!NOTE]
>
>只考慮&#x200B;**nms:seedMember**&#x200B;方案或其擴展之一中定義的欄位。 連結到`nms:seedMember`的表的屬性不可用。

## Adobe Campaign表單元件{#adobe-campaign-form-components}

您可以使用Adobe Campaign元件建立表單，讓使用者填寫表單以訂閱電子報、取消訂閱電子報，或更新其使用者設定檔。 如需詳細資訊，請參閱[建立Adobe Campaign Forms](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md) 。

每個元件欄位都可連結至Adobe Campaign資料庫欄位。 可用欄位會因其包含的資料類型而異，如[元件和資料類型](#components-and-data-type)一節所述。 如果您在Adobe Campaign中擴充收件者結構，新欄位將可在資料類型相符的元件中使用。

當您開啟已設定為與Adobe Campaign整合的表單時，您會在&#x200B;**Adobe Campaign**&#x200B;區段中看到下列元件：

* 核取方塊 (行銷活動)
* 日期欄位（促銷活動）和日期欄位/HTML5（促銷活動）
* 加密的主要金鑰 (行銷活動)
* 錯誤顯示 (行銷活動)
* 隱藏調解金鑰 (行銷活動)
* 數值欄位 (行銷活動)
* 選項欄位 (行銷活動)
* 訂閱檢查清單 (行銷活動)
* 測試欄位 (行銷活動)

本節詳細說明每個元件。

### 元件和資料類型{#components-and-data-type}

下表說明可用於顯示和修改Adobe Campaign設定檔資料的元件。 每個元件都可對應至Adobe Campaign設定檔欄位，以顯示其值，並在提交表單時更新欄位。 不同的元件只能與適當資料類型的欄位匹配。

<table>
 <tbody>
  <tr>
   <td><p><strong>元件</strong></p> </td>
   <td><p><strong>Adobe Campaign欄位的資料類型</strong></p> </td>
   <td><p><strong>範例欄位</strong></p> </td>
  </tr>
  <tr>
   <td><p>核取方塊 (行銷活動)</p> </td>
   <td><p>布林值</p> </td>
   <td><p>不再聯絡（透過任何管道）</p> </td>
  </tr>
  <tr>
   <td><p>日期欄位 (行銷活動)</p> <p>日期欄位/HTML 5 (行銷活動)</p> </td>
   <td><p>日期</p> </td>
   <td><p>出生日期</p> </td>
  </tr>
  <tr>
   <td><p>數值欄位 (行銷活動)</p> </td>
   <td><p>數值（位元組、短、長、雙）</p> </td>
   <td><p>年齡</p> </td>
  </tr>
  <tr>
   <td><p>選項欄位 (行銷活動)</p> </td>
   <td><p>關聯值的位元組</p> </td>
   <td><p>性別</p> </td>
  </tr>
  <tr>
   <td><p>測試欄位 (行銷活動)</p> </td>
   <td><p>字串</p> </td>
   <td><p>電子郵件</p> </td>
  </tr>
 </tbody>
</table>

### 大多數元件的常見設定{#settings-common-to-most-components}

Adobe Campaign元件具有所有元件中通用的設定（加密主鍵和隱藏協調鍵元件除外）。

在大部分元件中，您可以設定下列項目：

#### 標題和文字 {#title-and-text}

* ****
標題如果您想使用元素名稱以外的名稱，請在此處輸入。

* **隱藏**
標題如果不希望標題可見，請選中此複選框。

* ****
說明新增說明至欄位，以提供使用者的詳細資訊。

* **僅顯示**
valueOnly顯示值（如果有）

#### Adobe Campaign {#adobe-campaign}

您可以設定下列項目：

* ****
對應（如適用）選取Adobe Campaign個人化欄位。

* **調**
解密鑰如果此欄位是調解密鑰的一部分，則選中此複選框。

#### 限制 {#constraints}

* **必要**  — 選取此核取方塊，使此元件為必要項目；也就是說，使用者必須輸入值。
* **必填訊息**  — （可選）新增訊息，指出欄位為必填欄位。

#### 樣式 {#styling}

* ****
CSS輸入要用於此元件的CSS類。

### 核取方塊 (行銷活動) {#checkbox-campaign}

核取方塊（促銷活動）元件可讓使用者修改布林值資料類型的Adobe Campaign設定檔欄位。 例如，您可以有核取方塊（促銷活動）元件，讓收件者指定他/她不想透過任何管道聯絡。

您可以在核取方塊（促銷活動）元件中[設定大部分Adobe Campaign元件共同的設定](#settings-common-to-most-components)。

下列範例顯示要顯示的核取方塊（促銷活動）元件。

![chlimage_1-91](assets/chlimage_1-91.png)

### 日期欄位（促銷活動）和日期欄位/HTML 5（促銷活動）{#date-field-campaign-and-date-field-html-campaign}

使用日期欄位可讓收件者知道日期；例如，您可能希望收件者指定其出生日期。 日期格式符合您的Adobe Campaign例項中使用的格式。

除了大多數Adobe Campaign元件通用的[設定](#settings-common-to-most-components)外，您還可以配置以下設定：

* **約束 — 約束**  — 可以選擇 — 非 **** 或 **** 日期，以添加日期的約束或無約束。如果選擇日期，輸入欄位的答案用戶必須採用日期格式。

* **限制訊息**  — 此外，您可以新增限制訊息，讓使用者了解如何正確設定其答案的格式。
* **樣式 — 寬度**  — 按一下或點選+和 — 圖示或輸 **入數字** ，調 **整欄** 位的寬度。

下列範例顯示日期欄位（促銷活動）元件，並顯示調整寬度的元件。

![chlimage_1-92](assets/chlimage_1-92.png)

### 加密的主要金鑰 (行銷活動) {#encrypted-primary-key-campaign}

此元件定義將包含Adobe Campaign設定檔識別碼的URL參數名稱(分別在Adobe Campaign Standard和6.1中，包含&#x200B;**主要資源識別碼**&#x200B;或&#x200B;**加密的主鍵**)。

顯示和修改Adobe Campaign設定檔資料&#x200B;**的每個表單都必須**&#x200B;包含加密的主要金鑰元件。

您可以在加密的主要金鑰（促銷活動）元件中設定下列項目：

* **標題和文本 — 元素名稱**  — 預設為encryptedPK。只有當元素名稱與表單上其他元素的名稱衝突時，您才需要變更元素名稱。 沒有兩個表單欄位可以有相同的元素名稱。
* **Adobe Campaign - URL參數**  — 新增EPK的URL參數。例如，您可以使用值&#x200B;**epk**。

下列範例顯示加密的主要金鑰（促銷活動）元件。

![chlimage_1-93](assets/chlimage_1-93.png)

### 錯誤顯示 (行銷活動) {#error-display-campaign}

此元件可讓您顯示後端錯誤。 表單的錯誤處理必須設為「轉送」，才能讓元件正常運作。

下列範例顯示顯示的錯誤顯示（促銷活動）元件。

![chlimage_1-94](assets/chlimage_1-94.png)

### 隱藏調解金鑰 (行銷活動) {#hidden-reconciliation-key-campaign}

隱藏調解金鑰（促銷活動）元件可讓您將隱藏欄位新增為表單調解金鑰的一部分。

您可以在隱藏調解金鑰（促銷活動）元件中設定下列項目：

* **標題和文字 — 元素名稱**  — 預設為reconcilKey。只有當元素名稱與表單上其他元素的名稱衝突時，您才需要變更元素名稱。 沒有兩個表單欄位可以有相同的元素名稱。
* **Adobe Campaign — 對應**  — 對應至Adobe Campaign個人化欄位。

下列範例顯示隱藏調解金鑰（促銷活動）元件。

![chlimage_1-95](assets/chlimage_1-95.png)

### 數值欄位 (行銷活動) {#numeric-field-campaign}

使用數值欄位可讓收件者輸入數字，例如其年齡。

除了大多數Adobe Campaign元件通用的[設定](#settings-common-to-most-components)外，您還可以配置以下設定：

* **約束 —** 約束下拉式清單可以選擇 —  **** 非 **或數值 —** 來添加數字或無約束的約束。如果選擇數字，則在欄位中輸入的答案必須是數字。

* **限制訊息**  — 此外，您可以新增限制訊息，讓使用者了解如何正確設定其答案的格式。
* **樣式 — 寬度**  — 按一下或點選+和 — 圖示或輸 **入數字** ，調 **整欄** 位的寬度。

下列範例顯示數值欄位（促銷活動）元件，並顯示設定的寬度。

![chlimage_1-96](assets/chlimage_1-96.png)

### 選項欄位 (行銷活動) {#option-field-campaign}

此下拉式清單可讓您選取選項；例如，收件者的性別或狀態。

您可以在選項欄位（促銷活動）元件中[配置大多數Adobe Campaign元件共同的設定](#settings-common-to-most-components)。 若要填入下拉式清單，請按一下或點選Adobe Campaign符號，然後導覽至欄位，在Adobe Campaign個人化欄位中選取適當欄位。

下列範例顯示要顯示的選項欄位（促銷活動）元件。

![chlimage_1-97](assets/chlimage_1-97.png)

### 訂閱檢查清單 (行銷活動) {#subscriptions-checklist-campaign}

使用&#x200B;**訂閱檢查清單(Campaign)**&#x200B;元件來修改與Adobe Campaign設定檔相關聯的訂閱。

新增至表單時，此元件會將所有可用的訂閱顯示為核取方塊，並讓使用者選取所需的訂閱。 使用者提交表單時，此元件會根據表單動作類型(**Adobe Campaign:訂閱服務**&#x200B;或&#x200B;**Adobe Campaign:取消訂閱服務**)。

>[!NOTE]
>
>元件不會檢查使用者已訂閱/取消訂閱的服務。

您可以在訂閱檢查清單（促銷活動）元件中[配置大多數Adobe Campaign元件共同的設定](#settings-common-to-most-components)。 (此元件沒有可用的Adobe Campaign設定。)

下列範例顯示訂閱檢查清單（促銷活動）元件。

![chlimage_1-98](assets/chlimage_1-98.png)

### 測試欄位 (行銷活動) {#text-field-campaign}

文字欄位（促銷活動）元件可讓您輸入字串類型資料，例如名字、姓氏、地址、電子郵件地址等。

除了大多數Adobe Campaign元件通用的[設定](#settings-common-to-most-components)外，您還可以配置以下設定：

* **限制 — 限制**  — 下拉式清單 — 您可以選取 —  **無**、 **電子郵件**、 **名稱** （無變數），以新增電子郵件地址、名稱或無限制的限制。如果您選取電子郵件，使用者在欄位中輸入的答案必須是電子郵件地址。 如果您選取名稱，則必須是名稱（不允許變數）。

* **限制訊息**  — 此外，您可以新增限制訊息，讓使用者了解如何正確設定其答案的格式。
* **樣式 — 寬度**  — 按一下或點選+和 — 圖示或輸 **入數字** ，調 **整欄** 位的寬度。

下列範例顯示顯示的文字欄位（促銷活動）元件。

![chlimage_1-99](assets/chlimage_1-99.png)
