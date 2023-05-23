---
title: 使用定位模式編寫目標內容
seo-title: Authoring Targeted Content Using Targeting Mode
description: 目標模式和目標元件提供了為體驗建立內容的工具
seo-description: Targeting mode and the Target component provide tools for creating content for experiences
uuid: cea85c1b-1bc3-4498-9eaa-4ad10dc58ea4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9d940744-3b00-4721-829a-96d17bb738e8
docset: aem65
exl-id: edde225d-0be7-4306-8dda-d18d46fae977
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '5349'
ht-degree: 6%

---

# 使用定位模式編寫目標內容{#authoring-targeted-content-using-targeting-mode}

使用的「目標」模式建立目標內AEM容。 目標模式和目標元件提供了建立體驗內容的工具：

* 輕鬆識別頁面上的目標內容。 虛線在所有目標內容周圍形成邊框。
* 選擇品牌和活動以查看體驗。
* 將體驗添加到活動或刪除體驗。
* 執行A/B測試並轉換獲獎者(僅限Adobe Target)。
* 通過建立優惠或使用庫提供的優惠來添加優惠。
* 配置目標並監控效能。
* 模擬用戶體驗。
* 要進行更多自定義，請配置目標元件。

您可以使用AEM或Adobe Target作為目標引擎(您必須具有有效的Adobe Target帳戶才能使用Adobe Target)。 如果使用Adobe Target，則必須先配置整合。 請參閱 [與Adobe Target整合的指示](/help/sites-administering/target.md)。

![chlimage_1-8](assets/chlimage_1-8.png)

您在「目標」模式下看到的活動和體驗反映了 [活動控制台](/help/sites-authoring/activitylib.md):

* 使用「目標」模式對活動和體驗所做的更改將反映在「活動」控制台中。
* 在「活動」控制台中所做的更改將反映在「目標」模式中。

>[!NOTE]
>
>當您在Adobe Target建立市場活動時，它會指定一個名為 `thirdPartyId`每次競選。 刪除Adobe Target市場活動時，不會刪除thirdPartyId。 您不能重新使用 `thirdPartyId` 對於不同類型的市場活動(AB、XT)，不能手動刪除它。 為避免此問題，請為每個活動指定一個唯一的名稱；因此，不能在不同的市場活動類型中重新使用市場活動名稱。
>
>如果在同一市場活動類型中使用相同的名稱，則將改寫現有市場活動。
>
>如果同步時遇到錯誤「請求失敗」。 `thirdPartyId` 已存在」，更改市場活動的名稱並再次同步。

>[!NOTE]
>
>當目標鎖定時，品牌和活動組合將保留在用戶級別而不是渠道級別。

## 切換到目標模式 {#switching-to-targeting-mode}

切換到目標模式以訪問用於創作目標內容的工具。

切換到目標模式：

1. 開啟要為其建立目標內容的頁面。
1. 在頁面頂部的工具欄上，按一下或點擊模式下拉菜單以顯示可用模式類型。

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 按一下或點擊 **目標**。 目標選項顯示在頁面頂部。

   ![chlimage_1-10](assets/chlimage_1-10.png)

## 使用目標模式添加活動 {#adding-an-activity-using-targeting-mode}

使用目標模式將活動添加到品牌。 添加活動時，它包含預設體驗。 添加活動後，將啟動該活動的內容目標化進程。

您還可以通過選擇目標引AEM擎(可選為Adobe Target)和選擇活動類型(體驗目標或A/BTest)來建立和管理Adobe Target活動。

此外，您還可以管理所有Adobe Target活動的目標和指標，並管理Adobe Target觀眾。 Adobe Target的活動報告也包括A/B測試的獲獎者轉換。

添加活動時，該活動也顯示在 [活動控制台](/help/sites-authoring/activitylib.md)。

要添加活動，請執行以下操作：

1. 使用 **品牌** 下拉菜單，以選擇要為其建立活動的品牌。

   >[!NOTE]
   >
   >建議 [通過活動控制台建立品牌](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console)。
   >
   >
   >如果以其他方式建立品牌，請確保節點 `/campaigns/<brand>/master` 存在，或嘗試建立活動時將導致錯誤。

1. 按一下或點擊「 **活動** 的下界。
1. 鍵入活動的名稱。

   >[!NOTE]
   >
   >當您建立新活動並將Adobe Target雲配置附加到頁面或其父項之一時，將自動AEM假定Adobe Target為引擎。

1. 在 **目標** 引擎下拉菜單，選擇目標引擎。

   * 如果選擇 **上下文集AEM線**，其餘欄位將變灰且不可用。 按一下或點擊 **建立**。

   * 如果選擇 **Adobe Target**，可以選擇配置(預設情況下，它是您在 [已配置帳戶](/help/sites-administering/opt-in.md))和活動類型。

   * 如果您正在使用AEM/Adobe Campaign整合併正在發送目標內容（新聞稿），請選擇 **Adobe Campaign**。 請參閱 [與Adobe Campaign整合](/help/sites-administering/campaign.md) 的子菜單。

1. 在「活動」菜單中，選擇 **體驗目標** 或 **A/BTest**。

   * 經驗目標 — 管理Adobe Target活動AEM。
   * A/BTest — 從Adobe Target建立/管理A/Btest活AEM動。

## 目標流程：建立、目標、目標和設定 {#the-targeting-process-create-target-and-goals-settings}

目標模式使您能夠配置活動的多個方面。 使用以下三步流程為品牌活動建立目標內容：

1. [建立](#create-authoring-the-experiences):添加或刪除體驗，並為每個體驗添加優惠。
1. [目標](#diagramtargetconfiguringtheaudiences):指定每個體驗所針對的受眾。 您可以針對特定的受眾，如果使用A/B測試確定哪一流量百分比將用於哪種體驗。
1. [目標和設定](#settingsgoalssettingsconfiguringtheactivityandsettinggoals):安排活動並設定優先順序。 您還可以設定成功度量目標。

請按下列步驟啟動活動的內容目標化進程。

>[!NOTE]
>
>要使用目標進程，您必須是「目標活動作者」用戶組的成員。

要添加活動，請執行以下操作：

1. 在 **品牌** 下拉菜單，選擇包含您正在處理的活動的品牌。
1. 在 **活動** 下拉菜單，選擇您正在為其創作目標內容的活動。
1. 要顯示指導您完成目標過程的控制項，請按一下或點擊 **開始目標**。

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >要更改您正在使用的活動，請按一下或點擊 **後退**。

## 建立：創作體驗 {#create-authoring-the-experiences}

內容目標的「建立」步驟涉及建立體驗。 在此步驟中，您可以建立或刪除活動的體驗，並向每個體驗添加優惠。

### 在目標模式下查看體驗產品 {#seeing-experience-offers-in-targeting-mode}

在你之後 [啟動目標化進程](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)，選擇體驗以查看為該體驗提供的優惠。 選擇體驗後，頁面上的目標元件將更改以顯示該體驗的優惠。

>[!CAUTION]
>
>禁用已在作者實例中目標的元件的目標時，請小心。 相應的活動也將自動從發佈實例中刪除。

>[!NOTE]
>
>優惠是目標元件的內容。

體驗會顯示在「對象」窗格中。在下列範例中，體驗包 **括Default**、 **Femole**、 **Femole 30歲以上，******&#x200B;以及Femole 30歲以下。此範例顯示目標影像元件的「預設 **」選件** 。

![chlimage_1-12](assets/chlimage_1-12.png)

當選擇了其他體驗時，影像元件將顯示該體驗的提供。

![chlimage_1-13](assets/chlimage_1-13.png)

當選取體驗且目標元件不包含該體驗的選件時，元件會顯示疊加在半透明預設選件上的「新增選件 **** 」。當未建立任何體驗的選件時，會針對對應至 **體驗的區段顯示** 「預設」選件。

![chlimage_1-14](assets/chlimage_1-14.png)

當訪問者屬性與映射到體驗的任何段不匹配時，也會顯示「預設體驗」。 請參閱 [使用目標模式添加體驗](#adding-and-removing-experiences-using-targeting-mode)。

### 自定義優惠和庫優惠 {#custom-offers-and-library-offers}

優惠 [在頁面上創作](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) 用於單一體驗的產品稱為定制優惠。 以下影像疊加在自定義優惠的內容上：

![chlimage_1-15](assets/chlimage_1-15.png)

優惠 [從優惠庫添加](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library) 與以下影像疊加：

![chlimage_1-16](assets/chlimage_1-16.png)

如果您決定要重新使用自定義優惠，則可以將其保存到優惠庫。 如果要修改體驗內容，還可以將庫服務轉換為自定義服務。 編輯後，您可以再次將優惠保存回庫。

### 使用目標模式添加和刪除體驗 {#adding-and-removing-experiences-using-targeting-mode}

使用的「建立」步驟 [瞄準過程](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)，可以添加和刪除體驗。 此外，您還可以複製體驗並更名它。

#### 使用目標模式添加體驗 {#adding-experiences-using-targeting-mode}

要添加體驗：

1. 要添加體驗，請按一下或點擊 **+** **添加體驗目標** 顯示在 **觀眾** 的子菜單。
1. 選擇和受眾。 預設情況下，該名稱是體驗的名稱。 如果需要，可鍵入其他名稱。 按一下或點擊 **確定**。

#### 使用目標模式刪除體驗 {#removing-experiences-using-targeting-mode}

要刪除體驗，請執行以下操作：

1. 按一下或點擊體驗名稱旁邊的箭頭。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 按一下&#x200B;**刪除**。

#### 使用目標模式更名體驗 {#renaming-experiences-using-targeting-mode}

要使用目標模式更名體驗：

1. 按一下或點擊體驗名稱旁邊的箭頭。
1. 按一下 **更名體驗** 鍵入新名稱。
1. 按一下或點擊螢幕上的其他位置以保存更改。

#### 使用目標模式編輯受眾 {#editing-audiences-using-targeting-mode}

要使用目標模式編輯受眾：

1. 按一下或點擊體驗名稱旁邊的箭頭。
1. 按一下 **編輯受眾** 並選擇新受眾。
1. 按一下&#x200B;**「確定」**。

#### 使用目標模式複製體驗 {#duplicating-experiences-using-targeting-mode}

要使用目標模式複製體驗，請執行以下操作：

1. 按一下或點擊體驗名稱旁邊的箭頭。
1. 按一下 **重複** 選擇觀眾。
1. 根據需要更名體驗，然後按一下 **確定**。

### 使用目標模式建立優惠 {#creating-offers-using-targeting-mode}

瞄準元件以建立體驗服務。 目標元件提供用作體驗的內容。

* [瞄準現有元件](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component)。 內容成為預設體驗的提供。
* [添加目標元件](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component)，然後將內容添加到元件。

在將元件定為目標後，您可以為每種體驗添加優惠：

* [添加自定義優惠](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer)。
* [從庫添加優惠](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

以下工具可用於使用優惠：

* [將自定義優惠添加到優惠庫](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library)。
* [將庫服務轉換為自定義服務](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library)。
* [開啟庫服務並編輯內容](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer)。

#### 通過目標現有元件建立預設優惠 {#creating-a-default-offer-by-targeting-an-existing-component}

將頁面上的元件作為活動預設體驗的提供對象。 當您瞄準某個元件時，該元件被封裝在一個目標元件中，其內容將成為預設體驗的提供。

當您瞄準某個元件時，只有該元件才能用在提供中。 您不能從聘用中刪除該元件或將其他元件添加到聘用中。

在以下步驟之後 [啟動目標進程](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)。

1. 按一下或點擊要目標的元件。 此時將出現元件工具欄，與以下示例類似。

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 按一下或點擊「目標」表徵圖。

   ![](do-not-localize/chlimage_1.png)

   元件內容是預設體驗的服務。 當某個元件成為目標時，將為每個體驗複製其預設節點。 在體驗特定創作期間編輯正確的內容節點時需要這樣做。 對於這些非預設體驗， [添加自定義優惠](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) 或 [添加庫服務](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

#### 通過添加目標元件建立聘用 {#creating-an-offer-by-adding-a-target-component}

添加目標元件以建立預設體驗的服務。 「目標」元件是其他元件的容器，放置在其中的元件成為目標。 使用「目標」元件時，可以添加多個元件以建立優惠。 此外，您可以在每個體驗中使用不同的元件來建立不同的優惠。

請參閱 [配置目標元件選項](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options) 的子菜單。

>[!NOTE]
>
>您使用 [提供控制台](/help/sites-authoring/offerlib.md) 也可包含幾個元件。 這些服務屬於一個服務庫，可用於多種體驗。

由於目標元件是容器，因此它顯示為其它元件的放置區域。

在「目標」模式下，「目標」元件具有藍色邊框，而「目標」消息則指明目標性質。

![chlimage_1-19](assets/chlimage_1-19.png)

在「編輯」模式下，「目標」元件具有「牛眼」表徵圖。

![](do-not-localize/chlimage_1-1.png)

將元件拖動到「目標」元件中時，它們是目標元件。

![chlimage_1-20](assets/chlimage_1-20.png)

將元件添加到目標元件時，它將提供特定體驗的內容。 要指定體驗，請在添加元件之前選擇體驗。

可以在「編輯」模式或「目標」模式下將「目標」元件添加到頁面。 只能在「目標」模式下將元件添加到「目標」元件。 目標元件屬於個性化元件組。

如果編輯目標內容，則必須按一下或點擊 **開始目標** 才能實現。

1. 將「目標」元件拖到要顯示優惠的頁面。
1. 預設情況下，未設定位置ID。 按一下或點擊配置輪圈以設定位置。

   >[!NOTE]
   >
   >如果由管理員設定，則可能需要顯式設定位置。
   >
   >
   >管理員可以決定是否需要在 **https://&lt;host>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlet.TargetingConfigurationServlet**
   要要求用戶輸入位置，請選中**Force location **複選框。

1. 選擇要為其建立優惠的體驗。
1. 建立優惠：

   * 對於預設體驗，將元件拖到目標拖放區，並像往常一樣編輯元件屬性以建立服務內容。
   * 對於非預設體驗， [添加自定義優惠](#adding-a-custom-offer) 或 [添加庫服務](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

#### 添加自定義優惠 {#adding-a-custom-offer}

通過在「目標」模式下創作目標元件的內容來建立優惠。 在您建立自定義優惠時，它將用作單一體驗的優惠。

如果您決定此優惠可用於其他體驗，則可以建立自定義優惠， [將其添加到庫](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library)。 有關使用「優惠」控制台建立可重用優惠的資訊，請參見 [將聘用添加到聘用庫](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library)。

1. 選擇要添加優惠的體驗。
1. 要顯示元件菜單，請按一下或點擊要向其添加優惠的目標元件。

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. 按一下或點擊+表徵圖。

   預設優惠的內容用作當前體驗的優惠。

1. 按一下或點擊聘用以顯示聘用菜單，然後按一下或點擊編輯表徵圖。

   ![](do-not-localize/chlimage_1-2.png)

1. 編輯元件的內容。

#### 從優惠庫添加優惠 {#adding-an-offer-from-an-offer-library}

添加來自 [提供庫](/help/sites-authoring/offerlib.md) 體驗。 您可以從當前目標的品牌庫添加任何優惠。

無法將庫服務添加到預設體驗。

1. 選擇要添加優惠的體驗。
1. 要顯示元件菜單，請按一下或點擊要向其添加優惠的目標元件。

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 按一下或點擊資料夾表徵圖。

   ![](do-not-localize/chlimage_1-3.png)

1. 從庫中選擇優惠，然後按一下或點擊複選標籤表徵圖。

   ![chlimage_1-23](assets/chlimage_1-23.png)

   通過聘用選擇器，您可以瀏覽或篩選聘用。 瀏覽或篩選時，您可能還希望對優惠進行排序並更改查看優惠的方式。 右上角的數字表示當前庫中有多少項服務可用。

   * 按一下或點擊 **瀏覽** 導航到其他資料夾。 將開啟導航窗格，然後按一下箭頭可深入到資料夾。 按一下或點擊 **瀏覽** 的子菜單。

   ![chlimage_1-24](assets/chlimage_1-24.png)

   * 按一下或點擊 **篩選** 按關鍵字或標籤篩選優惠。 輸入關鍵字，然後從下拉菜單中選擇標籤。 按一下或點擊 **篩選** 按鈕。

   ![chlimage_1-25](assets/chlimage_1-25.png)

   * 通過按一下或點擊旁邊的箭頭更改對優惠的排序方式 **最新到最舊**。 可以將優惠按最新到最舊或從最早到最新進行排序。

   ![chlimage_1-26](assets/chlimage_1-26.png)

   按一下或點擊旁邊的表徵圖 **視為** 以磁貼形式或清單形式查看優惠。

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### 向庫添加自定義優惠 {#adding-a-custom-offer-to-a-library}

將自定義優惠添加到 [提供庫](/help/sites-authoring/offerlib.md) 當您希望將它重新用作提供多種體驗時。 您可以將優惠添加到您所針對的當前品牌的庫中。

有關使用「優惠」控制台建立可重用優惠的資訊，請參見 [將聘用添加到聘用庫](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library)。

1. 選擇顯示自定義優惠的體驗。
1. 按一下或點擊自定義優惠以顯示優惠菜單，然後按一下或點擊 **保存優惠以提供庫** 表徵圖

   ![](do-not-localize/chlimage_1-4.png)

1. 鍵入聘用的名稱，然後選擇要向其中添加聘用的庫，然後按一下或點擊複選標籤表徵圖。

#### 將庫服務轉換為自定義庫 {#converting-a-library-offer-to-a-custom-library}

將庫服務轉換為定制服務，以更改當前體驗的服務，而不更改其他體驗中的服務。

1. 選擇顯示庫服務的體驗。
1. 按一下或點擊庫優惠以顯示優惠菜單，然後按一下或點擊「轉換為內聯優惠」表徵圖。

   ![](do-not-localize/chlimage_1-5.png)

#### 編輯庫服務 {#editing-a-library-offer}

以「目標」模式開啟庫服務以編輯服務。 您所做的更改將顯示在使用此優惠的所有體驗中。

1. 選擇顯示庫服務的體驗。
1. 將庫服務轉換為本地/自定義服務。 請參閱 [將庫服務轉換為自定義庫](#converting-a-library-offer-to-a-custom-library)。
1. 編輯優惠內容。

1. 保存回庫。 請參閱 [向庫添加自定義優惠](#adding-a-custom-offer-to-a-library)。

## 目標：配置受眾 {#target-configuring-the-audiences}

的目標步驟 [瞄準過程](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) 涉及用您在「建立」步驟中使用的體驗映射受眾。 「目標」頁顯示每個體驗所針對的受眾。 您可以為每個體驗指定或更改受眾。 如果您使用Adobe Target，還可以建立A/Btest，以便您針對特定體驗的受眾確定流量百分比。

### 如果您正在使AEM用目標或Adobe Target（經驗目標）。.. {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

觀眾顯示在映射圖的左側，體驗顯示在右側。

![chlimage_1-28](assets/chlimage_1-28.png)

使用段定義受眾。 頁面檢測器的雲配置確定了可用的段。 當頁面未與Adobe Target雲配置關聯時，AEM可用段定義受眾。 當頁面與Adobe Target雲配置關聯時，您將使用目標段。

有關資訊目標引擎，請參見 [目標引擎](/help/sites-authoring/personalization.md#targeting-engine)。

一個受眾不能被多個體驗使用。 當一個體驗映射到映射到另一個體驗的受眾時，該體驗旁會顯示一個警告符號。

![](do-not-localize/chlimage_1-6.png)

### 將體驗與觀眾(或AEMAdobe Target)關聯 {#associating-experiences-with-audiences-aem-or-adobe-target}

使用目標(或Adobe Target經驗目標)時，請按以下步驟將AEM體驗與受眾關聯：

1. 按一下或點擊映射到體驗的觀眾框中旁邊的下拉箭頭。
1. （可選）按一下或點擊 **編輯** 然後鍵入關鍵字以搜索所需的段。
1. 在受眾清單中，選擇受眾，然後按一下或點擊 **確定**。

### 如果您正在使用A/B測試(Adobe Target)。.. {#if-you-are-using-a-b-testing-adobe-target}

如果您有A/Btest活動，觀眾在您的左側，每個體驗的查看百分比在中間，體驗在右側。

只要百分比加起來達到100%，就可以更改百分比。 在A/B測試中，受眾可以被多種體驗使用。

![chlimage_1-29](assets/chlimage_1-29.png)

### 將受眾和流量百分比與A/B測試關聯 {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. 按一下或點擊映射到體驗的觀眾旁邊的下拉清單框。
1. （可選）按一下 **編輯**，然後鍵入關鍵字以搜索所需的段。
1. 按一下或點擊 **好。**
1. 以百分比輸入以配置如何將受眾流量路由到每個體驗。 總數必須等於100。
1. （可選）通過按一下體驗名稱旁邊的下拉菜單來編輯體驗名稱。

## 目標和設定：配置活動和設定目標 {#goals-settings-configuring-the-activity-and-setting-goals}

的「目標和設定」步驟 [瞄準過程](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) 包括配置品牌活動的行為。 指定活動的開始和結束時間以及活動優先順序。 另外，你還跟蹤目標。 具體來說，您可以決定要測量的活動。

僅當將Adobe Target用於目標引擎時，目標度量才可用。 必須至少定義一個目標度量。 如果您已配置Adobe Analytics並且擁有A4T Analytics雲配置，則可以選擇是希望報告源是Adobe Target還是Adobe Analytics。

目標度量僅針對已發佈的市場活動進行度量。

如果AEM用作目標引擎：

![chlimage_1-30](assets/chlimage_1-30.png)

如果使用Adobe Target作為目標引擎：

![chlimage_1-31](assets/chlimage_1-31.png)

如果使用Adobe target做為定位引擎，而您已為帳戶設定了A4T Analytics，則您會有其他的「 **Reporting Source** 」下拉式選單：

![chlimage_1-32](assets/chlimage_1-32.png)

以下成功度量可用（僅用於發佈）:

<table>
 <tbody>
  <tr>
   <td><strong>轉換</strong></td>
   <td><p>點擊所測試體驗任何部分的訪問者百分比。 每個訪問者或每次訪問者完成轉換時，都可以計算一次轉換。 轉換度量設定為以下之一：</p>
    <ul>
     <li><strong>已查看頁面</strong>  — 通過選擇以下任一選項，您可以定義查看的受眾頁 <strong>URL是</strong> 然後定義URL或多個URL，或通過選擇 <strong>URL包含</strong> 然後添加路徑或關鍵字。</li>
     <li><strong>已查看框</strong>  — 您可以通過輸入框的名稱來定義觀眾查看的框。 通過按一下 <strong>添加Mbox</strong>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>收入</strong></td>
   <td><p>訪問產生的收入。 您可以從以下收入指標中進行選擇：</p>
    <ul>
     <li>每訪客收入(RPV)</li>
     <li>平均訂購值 (AOV)</li>
     <li>銷售總額 </li>
     <li>訂購</li>
    </ul> <p>對於這些選項中的任何一個，是否查看了框表示已達到目標。 可以定義框或多個框。</p> </td>
  </tr>
  <tr>
   <td><strong>參與</strong></td>
   <td><p>您可以測量三種類型的預訂：</p>
    <ul>
     <li>頁面檢視</li>
     <li>自訂得分</li>
     <li>網站逗留時間</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

此外，還有高級設定，允許您確定如何計算成功度量。 選項包括按印象或每個訪問者計算一次度量，以及選擇是保留用戶參與活動還是刪除它們。

使用高級設定確定發生的情況 **後** 用戶遇到目標度量。 下表顯示了可用選項。

<table>
 <tbody>
  <tr>
   <td><strong>用戶遇到此目標度量後……</strong></td>
   <td><strong>您選擇以下項……</strong></td>
  </tr>
  <tr>
   <td><strong>增加計數以及讓使用者留在活動中</strong></td>
   <td>指定計數的遞增方式：
    <ul>
     <li>每個參與者一次</li>
     <li>在每個印象中，排除頁面刷新</li>
     <li>每個印象</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>增加計數、釋出使用者以及允許重新進入</strong></td>
   <td>選擇訪問者是否重新進入活動時看到的體驗：
    <ul>
     <li>相同的體驗</li>
     <li>隨機體驗</li>
     <li>看不見的體驗</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>增量計數、釋放用戶和條重新入門</strong></td>
   <td>確定用戶看到的內容，而不是活動內容：
    <ul>
     <li>相同的體驗，不跟蹤</li>
     <li>預設內容或其他活動內容</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

請參閱 [Adobe Target文檔](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) 的子菜單。

### 配置設定(AEM目標) {#configuring-settings-aem-targeting}

配置使用目標時的AEM設定：

1. 要指定活動何時啟動，請使用 **開始** 下拉菜單，以選擇以下值之一：

   * **激活時**:活動在包含目標內容的頁面被激活時開始。
   * **指定日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 要指定活動結束的時間，請使用 **結束** 下拉菜單，以選擇以下值之一：

   * **停用時**:當包含目標內容的頁面被停用時，活動將結束。
   * **指定日期和時間**:特定時間。 選擇此選項後，按一下或點擊日曆表徵圖，選擇日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑塊選擇 **低**。 **正常**&#x200B;或 **高**。

### 配置目標和設定(Adobe Target) {#configuring-goals-settings-adobe-target}

要配置目標和設定(如果使用Adobe Target):

1. 要指定活動何時啟動，請使用 **開始** 下拉菜單，以選擇以下值之一：

   * **激活時**:活動在包含目標內容的頁面被激活時開始。
   * **指定日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 要指定活動結束的時間，請使用 **結束** 下拉菜單，以選擇以下值之一：

   * **停用時**:當包含目標內容的頁面被停用時，活動將結束。
   * **指定日期和時間**:特定時間。 選擇此選項後，按一下或點擊日曆表徵圖，選擇日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑塊選擇 **低**。 **正常**&#x200B;或 **高**。
1. 如果您已使用Adobe Target帳戶配置了Adobe分析，則 **報告源** 的下界。 選取 **Adobe Target****或** Adobe Analytics做為來源。

   如果選擇 **Adobe Analytics**，選擇公司和報表套件。 如果選擇 **Adobe Target**，不需要任何操作。

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. 在「目 **標量度** 」區域的「我的主要目標 **** 」下方，選取您要追蹤的成功量度——轉換、收入、參與——並輸入量度的測量方式 (或觀眾採取哪些動作來指出已達成目標)。請參閱上表中目標量度的定義，並參閱 [Adobe Target成功量度的相關檔案](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) 。

   您可以按一下右上角的三個點並選取「重新命名」，以重新命名目 **標**。

   如果您需要清除所有欄位，請按一下右上角的三個點，然後選取「清除所 **有欄位」**。

   所有度量還具有可定義的高級設定。 選擇 **高級設定** 來獲取這些。 請參閱上表中對成功度量計數的定義，並參見 [Adobe Target文檔](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)。

   >[!NOTE]
   必須至少定義一個目標。

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   如果度量中缺少資訊，則度量周圍會有一條紅線。

1. 按一下 **添加新度量** 配置其他成功度量。

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   通過按一下或點擊三個點，然後按一下或點擊，可以刪除其他目標 **刪除**。 要AEM求至少定義一個目標。

1. 如果希望對成功度量的計數方式有更多控制，請按一下或點擊 **高級設定** 來獲取這些。
1. 按一下「**儲存**」。

配置後，您可以 [查看活動的績效](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) 使用Adobe Target(經驗或A/Btest瞄準)。 另外，通過A/Btest目標， [將獲勝者轉化。](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## 模擬體驗 {#simulating-an-experience}

模擬訪問者的體驗，以驗證頁面內容是否根據目標內容的設計按預期顯示。 模擬時，載入不同的用戶配置檔案並查看該用戶的目標內容。

以下標準確定模擬訪問者體驗時顯示的內容：

* 用戶會話儲存中的資料（通過上下文中心）。
* 的 [正在進行的活動](/help/sites-authoring/activitylib.md)。
* 的 [定義段的規則](/help/sites-administering/campaign-segmentation.md)。
* 目標元件中的體驗內容。
* 的 [目標引擎的配置](/help/sites-authoring/activitylib.md)。

如果載入配置檔案時頁面上出現意外內容，請檢查此清單中每個項的配置。

>[!NOTE]
如果使用A/B測試，則模擬體驗時會根據通信量百分比顯示。 這由Adobe Target控制，可能給作者帶來意想不到的結果。 （_author活動與允許在模擬期間重新評估的特定設定同步。） 作者可能需要刷新才能根據其流量設定查看其他體驗。

要模擬訪問者的體驗，請使用以下工具：

* 在「目標」模式下的模擬活動：該頁顯示當前在上下文中心中選擇的用戶的優惠。 您可以編輯針對用戶的優惠。
* 預覽模式：使用上下文中心選擇滿足您的體驗所基於的段標準的用戶和位置。 當您的「上下文中心」選擇發生更改時，目標內容會相應更改。

1. 要切換到「預覽」模式，請在工具欄上按一下或點擊 **預覽**。
1. 在工具欄上，按一下或點擊「上下文中心」表徵圖。

   ![](do-not-localize/chlimage_1-7.png)

1. 使用上下文中心更改上下文屬性。 例如，按一下或點擊「Persona」屬性以選擇其他用戶。

   ![chlimage_1-36](assets/chlimage_1-36.png)

   頁面將更改以顯示當前上下文的目標內容。

1. 要更改顯示的優惠，請切換到目標模式。 選擇模擬活動後，編輯在「預覽」模式下配置的上下文的優惠。

## 配置目標元件選項 {#configuring-target-component-options}

可通過以下兩種方式之一訪問元件的選項來定制目標元件：

1. 在目標元件後，在「目標」元件中按一下或點擊該元件，然後按一下設定表徵圖(cog)。

   ![](do-not-localize/chlimage_1-8.png)

   顯AEM示「目標元件選項」窗口。

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 或者，要以全屏模式訪問這些設定，請在「目標元件選項」窗口中按一下或點擊全屏表徵圖。

   ![](do-not-localize/chlimage_1-9.png)

   顯AEM示全屏「目標」元件選項窗口。

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. 按照下表中所述配置目標元件設定。

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>位置</strong></td>
   <td><p>該位置是一個字串，它為目標內容位置指定名稱，並將提供與頁面上應放置這些提供的位置（或位置或元件）連接。</p> <p>此欄位是泛型值。</p> <p>如果將聘用放入元件，則聘用將記住位置ID。 執行頁面時，引擎會評估用戶的段，並基於此，它將解析應顯示的活動中的體驗。 然後，檢查頁面上的位置ID，並嘗試將提供與這些位置ID匹配。</p> </td>
  </tr>
  <tr>
   <td><strong>引擎</strong></td>
   <td>在 <strong>客戶端規則（不跟蹤）、Adobe Target、ContextHub、 </strong>和<strong> Adobe Campaign </strong>取決於你想使用哪個引擎。</td>
  </tr>
 </tbody>
</table>

如果選擇Adobe Target作為引擎：

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>準確定位</strong></td>
   <td><p>啟用準確目標會告訴元件在將請求發送到Adobe Target之前，等待客戶端上下文或上下文中心資料可用。 這樣可以增加負載時間。 對於創作，始終啟用準確的目標。</p> <p>如果選擇 <strong>精確瞄準</strong> 框中 <code>mboxDefine</code> 第一個 <code>mboxUpdate</code> 稍後，在資料可用後，會生成Ajax請求。</p> <p>如果未選擇 <strong>精確瞄準</strong> 框中 <code>mboxCreate</code> 立即生成同步請求（在本例中，並非所有上下文資料都可用）。</p> <p><strong>注：</strong> 對特定元件啟用或禁用精確目標不會影響已全局設定的設定。 通過在元件中選擇「準確目標」(Accurate Targing)，始終可以覆蓋全局設定。</p> </td>
  </tr>
  <tr>
   <td><strong>包括已解析的區段</strong></td>
   <td><p>選中此複選框將包含框調用中的所有已解析段以及在頁面和框架中配置的任何參數。</p> <p>這隻適用於同步段的XML API的情AEM況。 如果中的段AEM未由Adobe Target處理（如指令碼段），則此選項允許您解析中的段，並將該段處於活動狀態AEM的資訊發送到Adobe Target。</p> </td>
  </tr>
  <tr>
   <td><strong>繼承的內容參數</strong></td>
   <td>列出從Adobe Target框架繼承的與所選頁面關聯的上下文參數（如果有）。</td>
  </tr>
  <tr>
   <td><strong>上下文參數</strong></td>
   <td>按一下或點擊 <strong>添加欄位</strong> 配置其他上下文參數（與目標框架中可用的內容相同）。 添加到元件的上下文參數應用 <i>僅</i> 將上下文參數直接添加到框架時，將其添加到元件，而不是添加到其他元件。</td>
  </tr>
  <tr>
   <td><strong>靜態參數</strong></td>
   <td>按一下或點擊 <strong>添加欄位</strong> 配置其他靜態參數（與目標框架中可用的參數相同）。 添加到元件的靜態參數應用 <i>僅</i> 直接將靜態參數添加到框架時，不會像其它元件那樣添加到元件。 靜態參數不來自上下文（內容中心的客戶端上下文）。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
選擇元件並使其成為目標元件時，還AEM會替換元件並彈出Adobe Target元件。 (Adobe Target元件不僅在您將其手動添加到頁面時使用，而且在您針對現有元件時也使用。)

如果選擇「客戶端上下文」（客戶端）作為引擎：

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>客戶端選項 — 策略</strong></td>
   <td><p>從以下選項中選擇：</p>
    <ul>
     <li><strong>第一個</strong>:在市場活動中排序的清單中最高體驗。</li>
     <li><strong>隨機</strong>:任何經驗都會使用。</li>
     <li><strong>按一下流分數</strong>:使用在客戶端上下文中跟蹤的標籤和相關標籤命中。 比較在預告頁上定義的標籤的命中率。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

您選擇 **Adobe Campaign** 作為引擎，如果你和AEMAdobe Campaign。 請參閱 [與AEMAdobe Campaign](/help/sites-administering/campaign.md) 的子菜單。

選擇 **上下文中心** 作為引擎。 請參閱 [正在配置ContextHub。](/help/sites-developing/ch-configuring.md)
