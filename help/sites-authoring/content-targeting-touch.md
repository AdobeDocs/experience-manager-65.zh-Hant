---
title: 使用定位模式製作目標內容
seo-title: 使用定位模式製作目標內容
description: 定位模式和Target元件提供工具，以建立體驗內容
seo-description: 定位模式和Target元件提供工具，以建立體驗內容
uuid: cea85c1b-1bc3-4498-9eaa-4ad10dc58ea4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9d940744-3b00-4721-829a-96d17bb738e8
docset: aem65
translation-type: tm+mt
source-git-commit: 6853306d217809e05dbef4968c75bfef9d048f1c

---


# 使用定位模式製作目標內容{#authoring-targeted-content-using-targeting-mode}

使用AEM的「定位」模式來製作目標內容。 定位模式和Target元件提供工具，以建立體驗內容：

* 輕鬆辨識頁面上的目標內容。 虛線會圍繞所有目標內容形成邊框。
* 選擇品牌和活動以檢視體驗。
* 新增體驗至活動或移除體驗。
* 執行A/B測試並轉換得獎者（僅限Adobe Target）。
* 建立選件或使用資料庫中的選件，將選件新增至體驗。
* 設定目標並監控效能。
* 模擬使用者體驗。
* 如需更多自訂，請設定Target元件。

您可以使用AEM或Adobe Target作為定位引擎（您必須有有效的Adobe target帳戶才能使用Adobe Target）。 如果您使用Adobe Target，則必須先設定整合。 請參 [閱與Adobe Target整合的指示](/help/sites-administering/target.md)。

![chlimage_1-8](assets/chlimage_1-8.png)

您在Target模式中看到的活動和體驗反映了「活動」 [控制台](/help/sites-authoring/activitylib.md):

* 您使用定位模式對活動和體驗所做的變更會反映在「活動」主控台中。
* 在「活動」主控台中所做的變更會反映在「定位」模式中。

>[!NOTE]
>
>當您在Adobe target中建立促銷活動時，會指派一個名為的屬 `thirdPartyId`性給每個促銷活動。 當您在Adobe target中刪除促銷活動時，不會刪除thirdPartyId。 您無法針對不同類 `thirdPartyId` 型(AB、XT)的促銷活動重新使用，且無法手動移除。 為避免此問題，請為每個促銷活動命名一個唯一的名稱；因此，促銷活動名稱無法重複用於不同的促銷活動類型。
>
>如果您在相同的促銷活動類型中使用相同的名稱，您將會覆寫現有的促銷活動。
>
>如果在同步時，您會遇到「請求失敗」錯誤。 `thirdPartyId` 已存在」，請變更促銷活動的名稱，然後再次同步。

>[!NOTE]
>
>定位時，品牌和活動組合會持續存在於使用者層級，而非渠道層級。

## 切換至定位模式 {#switching-to-targeting-mode}

切換至Target模式，以存取製作目標內容的工具。

要切換到目標模式：

1. 開啟您要為其製作目標內容的頁面。
1. 在頁面頂端的工具列上，按一下或點選模式下拉式選單，以顯示可用的模式類型。

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. 按一下或點選「 **定位**」。 定位選項會顯示在頁面頂端。

   ![chlimage_1-10](assets/chlimage_1-10.png)

## 使用定位模式新增活動 {#adding-an-activity-using-targeting-mode}

使用定位模式將活動新增至品牌。 當您新增活動時，它會包含預設體驗。 新增活動後，您就會開始活動的內容定位程式。

您也可以從AEM建立和管理Adobe Target活動，並選擇目標引擎- AEM或Adobe Target —— 和選擇活動類型——體驗定位或A/B測試。

此外，您還可以管理所有Adobe target活動的目標和量度，並管理您的Adobe target受眾。 Adobe target活動報告也包含轉換A/B測試得獎者的功能。

添加活動時，該活動也會出現在「活動」控 [制台中](/help/sites-authoring/activitylib.md)。

要添加活動，請執行以下操作：

1. 使用「 **品牌** 」下拉式選單，選取您要為其建立活動的品牌。

   >[!NOTE]
   >
   >建議您透過活 [動主控台建立品牌](/help/sites-authoring/activitylib.md#creating-a-brand-using-the-activities-console)。
   >
   >
   >如果您以任何其他方式建立品牌，請確定節點存 `/campaigns/<brand>/master` 在，或者當您嘗試建立活動時會產生錯誤。

1. 按一下或點選「活動」下拉 **式功能表旁** ，再按+。
1. 鍵入活動的名稱。

   >[!NOTE]
   >
   >當您建立新活動並將Adobe Target雲端設定附加至頁面或其父項時，AEM會自動假設Adobe Target為引擎。

1. 在「定 **位引擎** 」下拉式功能表中，選取您的定位引擎。

   * 如果您選 **取ContextHub AEM**，其餘欄位會呈暗灰色且不可用。 按一下或點選「 **建立**」。

   * 如果您選 **取Adobe Target**，則可以選取設定(依預設，這是您設定帳戶時提供 [的設定](/help/sites-administering/opt-in.md))和活動類型。

   * 如果您使用AEM/Adobe Campaign整合併傳送目標內容（電子報），請選取「 **Adobe Campaign**」。 如需 [詳細資訊，請參閱與Adobe Campaign整合](/help/sites-administering/campaign.md) 。

1. 在「活動」功能表中，選 **取「體驗定位** 」 **或「A/B測試」**。

   * 體驗定位——從AEM管理Adobe Target活動。
   * A/B測試——從AEM在Adobe Target中建立／管理A/B測試活動。

## 定位程式：建立、定位及目標與設定 {#the-targeting-process-create-target-and-goals-settings}

定位模式可讓您設定活動的多個方面。 使用下列三步驟程式，建立品牌活動的目標內容：

1. [建立](#create-authoring-the-experiences):新增或移除體驗，並新增每個體驗的選件。
1. [目標](#diagramtargetconfiguringtheaudiences):指定每個體驗目標的對象。 您可以定位特定對象，如果使用A/B測試決定哪一個體驗的流量百分比。
1. [目標與設定](#settingsgoalssettingsconfiguringtheactivityandsettinggoals):排程活動並設定優先順序。 您也可以設定成功度量目標。

請依照下列程式，開始活動的內容定位程式。

>[!NOTE]
>
>若要使用定位程式，您必須是「定位活動作者」使用者群組的成員。

要添加活動，請執行以下操作：

1. 在「品 **牌** 」下拉式選單中，選取包含您正在處理之活動的品牌。
1. 在「活 **動** 」下拉式選單中，選取您要為其製作目標內容的活動。
1. 若要顯示引導您完成定位程式的控制項，請按一下或點選「開始 **定位」**。

   ![chlimage_1-11](assets/chlimage_1-11.png)

   >[!NOTE]
   >
   >若要變更您所使用的活動，請按一下或點選「上 **一步」**。

## 建立：製作體驗 {#create-authoring-the-experiences}

建立內容定位的步驟包括建立體驗。 在此步驟中，您可以建立或刪除活動的體驗，並新增選件至每個體驗。

### 在定位模式中檢視體驗選件 {#seeing-experience-offers-in-targeting-mode}

開始定 [位程式後](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)，請選取體驗，以查看為該體驗提供的選件。 當您選擇體驗時，頁面上的目標元件會變更，以顯示該體驗的選件。

>[!CAUTION]
>
>停用已在作者例項中定位的元件定位時請務必小心。 個別活動也會自動從發佈例項中刪除。

>[!NOTE]
>
>選件是目標元件的內容。

體驗會顯示在「對象」窗格中。 在下列範例中，體驗包 **括Default**、 **Femole**、 **Femole 30歲以上，******&#x200B;以及Femole 30歲以下。 此範例顯示目標影像元件的「預設 **」選件** 。

![chlimage_1-12](assets/chlimage_1-12.png)

選取不同的體驗時，影像元件會顯示該體驗的選件。

![chlimage_1-13](assets/chlimage_1-13.png)

當選取體驗且目標元件不包含該體驗的選件時，元件會顯示疊加在半透明預設選件上的「新增選件 **** 」。 當未建立任何體驗的選件時，會針對對應至 **體驗的區段顯示** 「預設」選件。

![chlimage_1-14](assets/chlimage_1-14.png)

當訪客屬性與映射至體驗的任何區段不符時，也會顯示預設體驗。 請參閱 [使用定位模式新增體驗](#adding-and-removing-experiences-using-targeting-mode)。

### 自訂選件和資料庫選件 {#custom-offers-and-library-offers}

在頁面上 [撰寫並用於單一體驗](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) 的選件稱為自訂選件。 下列影像會疊加在自訂選件的內容上：

![chlimage_1-15](assets/chlimage_1-15.png)

從選件程 [式庫新增的選件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library) ，會與下列影像重疊：

![chlimage_1-16](assets/chlimage_1-16.png)

如果您決定要重複使用自訂選件，可將自訂選件儲存至選件程式庫。 如果您想要修改體驗的內容，也可以將資料庫選件轉換為自訂選件。 編輯後，您可以再次將選件儲存回程式庫。

### 使用定位模式新增和移除體驗 {#adding-and-removing-experiences-using-targeting-mode}

使用定位程式的「 [建立」步驟](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)，您可以新增和移除體驗。 此外，您也可以複製體驗並重新命名體驗。

#### 使用定位模式新增體驗 {#adding-experiences-using-targeting-mode}

若要新增體驗：

1. 若要新增體驗，請按一下或點選「 **觀眾」窗格中** 現有體驗下方的「新增體驗定位」(Add Experience Targeting ******** )。
1. 選擇和對象。 依預設，該名稱是體驗的名稱。 您可以視需要輸入其他名稱。 按一下或點選「 **確定**」。

#### 使用定位模式移除體驗 {#removing-experiences-using-targeting-mode}

若要刪除體驗：

1. 按一下或點選體驗名稱旁的箭頭。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 按一 **下刪除**。

#### 使用定位模式重新命名體驗 {#renaming-experiences-using-targeting-mode}

若要使用定位模式重新命名體驗：

1. 按一下或點選體驗名稱旁的箭頭。
1. 按一 **下「重新命名體驗** 」，然後輸入新名稱。
1. 按一下或點選畫面上的其他位置，以儲存變更。

#### 使用定位模式編輯對象 {#editing-audiences-using-targeting-mode}

若要使用定位模式編輯對象：

1. 按一下或點選體驗名稱旁的箭頭。
1. 按一 **下「編輯對象** 」並選取新對象。
1. 按一下 **確定**。

#### 使用定位模式複製體驗 {#duplicating-experiences-using-targeting-mode}

若要使用定位模式複製體驗：

1. 按一下或點選體驗名稱旁的箭頭。
1. 按一 **下「複製** 」並選擇對象。
1. 視需要重新命名體驗，然後按一下「 **確定**」。

### 使用定位模式建立選件 {#creating-offers-using-targeting-mode}

定位元件以建立體驗的選件。 目標元件提供用作體驗選件的內容。

* [定位現有元件](/help/sites-authoring/content-targeting-touch.md#creating-a-default-offer-by-targeting-an-existing-component)。 內容會變成預設體驗的選件。
* [新增Target元件](/help/sites-authoring/content-targeting-touch.md#creating-an-offer-by-adding-a-target-component)，然後新增內容至元件。

定位元件後，您可以新增每個體驗的選件：

* [新增自訂選件](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer)。
* [從資料庫新增選件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

下列工具可用於處理選件：

* [新增自訂選件至選件程式庫](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library)。
* [將資料庫選件轉換為自訂選件](/help/sites-authoring/content-targeting-touch.md#converting-a-library-offer-to-a-custom-library)。
* [開啟資料庫選件並編輯內容](/help/sites-authoring/content-targeting-touch.md#editing-a-library-offer)。

#### 定位現有元件以建立預設選件 {#creating-a-default-offer-by-targeting-an-existing-component}

定位頁面上的元件，以用作活動的預設體驗選件。 當您定位元件時，它會封裝在Target元件中，其內容會變成預設體驗的選件。

當您定位元件時，選件中只能使用該元件。 您無法從選件移除元件或將其他元件新增至選件。

啟動定位程式後， [請執行下列程式](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings)。

1. 按一下或點選要定位的元件。 此時將顯示元件的工具欄，與以下示例類似。

   ![chlimage_1-18](assets/chlimage_1-18.png)

1. 按一下或點選「目標」圖示。

   ![](do-not-localize/chlimage_1.png)

   元件內容是預設體驗的選件。 定位元件時，會針對每個體驗複製其預設節點。 在體驗特定製作期間，編輯正確的內容節點時需要這個選項。 對於這些非預設體驗，請新 [增自訂選件](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer) , [或新增資料庫選件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

#### 新增Target元件以建立選件 {#creating-an-offer-by-adding-a-target-component}

新增Target元件以建立預設體驗的選件。 Target元件是其他元件的容器，而放置在其中的元件會成為目標。 當您使用Target元件時，可以新增數個元件來建立選件。 此外，您也可以在每個體驗中使用不同的元件來建立不同的選件。

如需自 [訂此元件的詳細資訊](/help/sites-authoring/content-targeting-touch.md#configuring-target-component-options) ，請參閱設定Target元件選項。

>[!NOTE]
>
>您使用選件主控台建立的選 [件](/help/sites-authoring/offerlib.md) ，也可以包含數個元件。 這些選件屬於選件程式庫，可用於多個體驗。

由於Target元件是容器，因此會顯示為其他元件的放置區域。

在Target模式中，Target元件有藍色邊框，而drop-target訊息會指出目標性質。

![chlimage_1-19](assets/chlimage_1-19.png)

在「編輯」模式中，Target元件具有bullseye圖示。

![](do-not-localize/chlimage_1-1.png)

將元件拖曳至Target元件時，這些元件就是目標元件。

![chlimage_1-20](assets/chlimage_1-20.png)

將元件新增至Target元件時，會提供特定體驗的內容。 若要指定體驗，請在新增元件前先選取體驗。

您可以在「編輯」模式或「目標」模式中，將Target元件新增至頁面。 您只能在Target模式中，將元件新增至Target元件。 Target元件屬於Personalization元件群組。

如果編輯目標內容，您必須先按一下或點選「 **開始定位** 」，才能這麼做。

1. 將Target元件拖曳至您希望選件出現的頁面。
1. 依預設，未設定任何位置ID。 按一下或點選設定齒輪以設定位置。

   >[!NOTE]
   >
   >如果由管理員設定，您可能需要明確設定位置。
   >
   >
   >管理員可以決定是否需要在 **https://&lt;host>:&lt;port>/system/console/configMgr/com.day.cq.personalization.impl.servlets.TargetingConfigurationServlet中設定此組態**
   要要求用戶輸入位置，請選擇**強制位置**複選框。

1. 選擇您要建立選件的體驗。
1. 建立選件：

   * 對於「預設」體驗，將元件拖曳至目標拖放區域，並照常編輯元件屬性，以建立選件的內容。
   * 對於非預設體驗，請新 [增自訂選件](#adding-a-custom-offer) , [或新增資料庫選件](/help/sites-authoring/content-targeting-touch.md#adding-an-offer-from-an-offer-library)。

#### 新增自訂選件 {#adding-a-custom-offer}

在「定位」模式中撰寫定位元件的內容，以建立選件。 當您建立自訂選件時，它會用作單一體驗的選件。

如果您決定該選件可用於其他體驗，則可建立自訂選件並 [將其新增至程式庫](/help/sites-authoring/content-targeting-touch.md#adding-a-custom-offer-to-a-library)。 如需使用選件主控台建立可重複使用選件的詳細資訊，請參 [閱新增選件至選件程式庫](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library)。

1. 選擇您要新增選件的體驗。
1. 若要顯現元件選單，請按一下或點選您要新增選件的目標元件。

   ![chlimage_1-21](assets/chlimage_1-21.png)

1. 按一下或點選+圖示。

   預設選件的內容會用作目前體驗的選件。

1. 按一下或點選選件以顯示選件選單，然後按一下或點選編輯圖示。

   ![](do-not-localize/chlimage_1-2.png)

1. 編輯元件的內容。

#### 從選件程式庫新增選件 {#adding-an-offer-from-an-offer-library}

從選件程式庫 [新增選件](/help/sites-authoring/offerlib.md) 至體驗。 您可以從目前鎖定的品牌資料庫新增任何選件。

您無法將程式庫選件新增至預設體驗。

1. 選擇您要新增選件的體驗。
1. 若要顯現元件選單，請按一下或點選您要新增選件的目標元件。

   ![chlimage_1-22](assets/chlimage_1-22.png)

1. 按一下或點選資料夾圖示。

   ![](do-not-localize/chlimage_1-3.png)

1. 從資料庫選取選件，然後按一下或點選核取標籤圖示。

   ![chlimage_1-23](assets/chlimage_1-23.png)

   選件選擇器可讓您瀏覽或篩選選件。 當瀏覽或篩選時，您也可能想要排序選件，並變更檢視選件的方式。 右上方的數字表示目前資料庫中有多少選件可用。

   * 按一下或點選「 **瀏覽** 」以導覽至其他資料夾。 導覽窗格隨即開啟，您按一下箭頭即可深入檢視資料夾。 再按一下或點 **選「瀏覽** 」以關閉導覽窗格。
   ![chlimage_1-24](assets/chlimage_1-24.png)

   * 按一下或點選「 **篩選** 」，以針對關鍵字或標籤篩選選件。 您輸入關鍵字，然後從下拉式選單中選取標籤。 再按一下或點 **選「篩選** 」，以關閉篩選窗格。
   ![chlimage_1-25](assets/chlimage_1-25.png)

   * 按一下或點選「最新至最舊」旁的箭頭，以變更選件 **的排序方式**。 選件可以從最新到最舊，或從最舊到最新。
   ![chlimage_1-26](assets/chlimage_1-26.png)

   按一下或點選「檢視方式」旁 **的圖示** ，即可將選件檢視為拼貼或清單。

   ![chlimage_1-27](assets/chlimage_1-27.png)

#### 新增自訂選件至程式庫 {#adding-a-custom-offer-to-a-library}

當您想要將自訂選件重新 [用作多個體驗的選件](/help/sites-authoring/offerlib.md) ，請將它新增至選件程式庫。 您可以將選件新增至目前所定位之品牌的資料庫。

如需使用選件主控台建立可重複使用選件的詳細資訊，請參 [閱新增選件至選件程式庫](/help/sites-authoring/offerlib.md#add-an-offer-to-an-offer-library)。

1. 選取體驗以顯示自訂選件。
1. 按一下或點選自訂選件以顯示選件選單，然後按一下或點選「將選 **件儲存至選件程式庫** 」圖示。

   ![](do-not-localize/chlimage_1-4.png)

1. 輸入選件的名稱，並選取您要新增選件的程式庫，然後按一下或點選核取標籤圖示。

#### 將資料庫選件轉換為自訂資料庫 {#converting-a-library-offer-to-a-custom-library}

將資料庫選件轉換為自訂選件，以變更目前體驗的選件，而不變更其他體驗中的選件。

1. 選取體驗以顯示程式庫選件。
1. 按一下或點選程式庫選件以顯示選件選單，然後按一下或點選「轉換為內嵌選件」圖示。

   ![](do-not-localize/chlimage_1-5.png)

#### 編輯資料庫選件 {#editing-a-library-offer}

從「目標」模式的體驗開啟資料庫選件，以編輯選件。 您所做的變更會顯示在使用選件的所有體驗中。

1. 選取體驗以顯示程式庫選件。
1. 將資料庫選件轉換為本機／自訂選件。 請參 [閱將資料庫選件轉換為自訂資料庫](#converting-a-library-offer-to-a-custom-library)。
1. 編輯選件的內容。

1. 將它儲存回資料庫。 請參 [閱新增自訂選件至資料庫](#adding-a-custom-offer-to-a-library)。

## 目標：設定觀眾 {#target-configuring-the-audiences}

定位程式的「 [目標」步驟](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) ，包括將觀眾與您在「建立」步驟中使用的體驗對應。 「目標」頁面顯示每個體驗所定位的對象。 您可以指定或變更每個體驗的對象。 如果您使用Adobe Target，也可以建立A/B測試，讓您針對特定體驗的對象流量百分比進行定位。

### 如果您使用AEM定位或Adobe Target（體驗定位）。.. {#if-you-are-using-aem-targeting-or-adobe-target-experience-targeting}

對象會顯示在對應圖的左側，體驗會顯示在右側。

![chlimage_1-28](assets/chlimage_1-28.png)

使用區隔定義對象。 頁面偵測的雲端設定會決定您可用的區段。 當頁面未與Adobe Target雲端設定關聯時，AEM區段可用於定義觀眾。 當頁面與Adobe Target雲端設定相關聯時，您會使用Target區段。

如需定位引擎的資訊，請參閱 [定位引擎](/help/sites-authoring/personalization.md#targeting-engine)。

一個對象不得被多個體驗使用。 當體驗對應至對應至其他體驗的對象時，警告符號會出現在體驗旁。

![](do-not-localize/chlimage_1-6.png)

### 將體驗與觀眾建立關聯（AEM或Adobe Target） {#associating-experiences-with-audiences-aem-or-adobe-target}

使用AEM定位（或Adobe Target體驗定位）時，請依照下列程式將體驗與對象建立關聯：

1. 按一下或點選對應至體驗的觀眾方塊中旁的下拉箭頭。
1. （可選）按一下或點選「 **編輯** 」，然後輸入關鍵字以搜尋所要的區段。
1. 在對象清單中，選取對象，然後按一下或點選「確 **定」**。

### 如果您使用A/B測試(Adobe Target)。.. {#if-you-are-using-a-b-testing-adobe-target}

如果您有A/B測試活動，觀眾在您的左側，每個體驗的檢視百分比在中間，體驗在右側。

只要百分比加起來達到100%，您就可以變更百分比。 在A/B測試中，多個體驗可以使用對象。

![chlimage_1-29](assets/chlimage_1-29.png)

### 將觀眾和流量百分比與A/B測試關聯 {#associating-audiences-and-traffic-percentages-with-a-b-testing}

1. 按一下或點選對應至體驗之對象旁的下拉式方塊。
1. （可選）按一 **下「編輯**」，然後輸入關鍵字以搜尋所要的區段。
1. 按一下或點選「 **確定」。**
1. 輸入百分比，以設定將觀眾流量路由至每個體驗的方式。 總數必須等於100。
1. （可選）按一下體驗名稱旁的下拉式選單，編輯體驗名稱。

## 目標與設定：設定活動和設定目標 {#goals-settings-configuring-the-activity-and-setting-goals}

定位程式的「目標與 [設定」步驟](/help/sites-authoring/content-targeting-touch.md#the-targeting-process-create-target-and-goals-settings) ，包括設定品牌活動的行為。 指定活動的開始和結束時間，以及活動優先順序。 此外，您也可追蹤目標。 具體來說，您可以決定要測量哪些活動。

目標量度僅在您將Adobe target用於目標引擎時可用。 您必須至少定義一個目標量度。 如果您已設定Adobe Analytics，且有A4T Analytics雲端設定，則可以選取報表來源是Adobe target還是Adobe Analytics。

目標量度僅會針對已發佈的促銷活動進行測量。

如果使用AEM做為定位引擎：

![chlimage_1-30](assets/chlimage_1-30.png)

如果使用Adobe target做為定位引擎：

![chlimage_1-31](assets/chlimage_1-31.png)

如果使用Adobe target做為定位引擎，而您已為帳戶設定了A4T Analytics，則您會有其他的「 **Reporting Source** 」下拉式選單：

![chlimage_1-32](assets/chlimage_1-32.png)

下列成功度量可用（僅用於發佈）:

<table>
 <tbody>
  <tr>
   <td><strong>轉換</strong></td>
   <td><p>點按測試體驗任何部分的訪客百分比。 每個訪客或任何訪客每次完成轉換時，都可計算一次轉換。 轉換量度會設為下列其中一項：</p>
    <ul>
     <li><strong>已檢視頁面</strong> -您可以定義觀眾檢視的頁面，方法是選擇 <strong>URL，然後定義URL或多個URL，或選擇</strong> URL包含 <strong></strong> ，然後新增路徑或關鍵字。</li>
     <li><strong>已檢視mbox</strong> —— 您可以輸入mbox的名稱，以定義您的觀眾檢視的mbox。 您可以按一下「新增mbox」 <strong>來輸入多個mbox</strong>。</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>收入</strong></td>
   <td><p>瀏覽產生的收入。 您可以從下列收入量度中選擇：</p>
    <ul>
     <li>每位訪客的收入(RPV)</li>
     <li>平均訂購值 (AOV)</li>
     <li>銷售總額 </li>
     <li>訂購</li>
    </ul> <p>對於其中任何選項，是否檢視mbox表示已達到目標。 您可以定義mbox或多個mbox。</p> </td>
  </tr>
  <tr>
   <td><strong>參與</strong></td>
   <td><p>您可以測量三種類型的參與：</p>
    <ul>
     <li>頁面檢視</li>
     <li>自訂得分</li>
     <li>網站逗留時間</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

此外，還有進階設定可讓您決定如何計算成功度量。 選項包括計算每個曝光或每個訪客一次的量度，並選擇是否將使用者留在活動中或移除。

使用進階設定來判斷使用者遇 **到目標量度** 後會發生什麼。 下表顯示了可用選項。

<table>
 <tbody>
  <tr>
   <td><strong>使用者遇到此目標量度後……</strong></td>
   <td><strong>您選擇要進行的下列操作……</strong></td>
  </tr>
  <tr>
   <td><strong>增加計數以及讓使用者留在活動中</strong></td>
   <td>指定計數的遞增方式：
    <ul>
     <li>每個參加者一次</li>
     <li>在每次曝光時，排除頁面重新整理</li>
     <li>在每一印象中</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>增加計數、釋出使用者以及允許重新進入</strong></td>
   <td>選取訪客在重新輸入活動時所看到的體驗：
    <ul>
     <li>相同體驗</li>
     <li>隨機體驗</li>
     <li>不可見的體驗</li>
    </ul> </td>
  </tr>
  <tr>
   <td><strong>增量計數、釋放用戶和條返回</strong></td>
   <td>判斷使用者所看到的內容，而非活動內容：
    <ul>
     <li>相同的體驗，不需追蹤</li>
     <li>預設內容或其他活動內容</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

如需 [成功度量的詳細資訊](https://marketing.adobe.com/resources/help/en_US/target/target/r_success_metrics.html) ，請參閱Adobe Target檔案。

### 設定設定（AEM定位） {#configuring-settings-aem-targeting}

若要設定使用AEM定位時的設定：

1. 若要指定活動何時啟動，請使用「 **開始** 」下拉式功能表來選取下列值之一：

   * **啟動時**:活動會在包含目標內容的頁面被啟用時開始。
   * **指定的日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 要指定活動何時結束，請使用「結 **束** 」(End)下拉菜單選擇以下值之一：

   * **停用時**:當包含目標內容的頁面停用時，活動便會結束。
   * **指定的日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑塊選擇「低 **」**、「 **正常**」或「 **高」**。

### 設定目標與設定(Adobe Target) {#configuring-goals-settings-adobe-target}

若要在使用Adobe Target時設定目標和設定：

1. 若要指定活動何時啟動，請使用「 **開始** 」下拉式功能表來選取下列值之一：

   * **啟動時**:活動會在包含目標內容的頁面被啟用時開始。
   * **指定的日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定啟動活動的時間。

1. 要指定活動何時結束，請使用「結 **束** 」(End)下拉菜單選擇以下值之一：

   * **停用時**:當包含目標內容的頁面停用時，活動便會結束。
   * **指定的日期和時間**:特定時間。 選取此選項時，按一下或點選日曆圖示，選取日期，並指定結束活動的時間。

1. 要指定活動的優先順序，請使用滑塊選擇「低 **」**、「 **正常**」或「 **高」**。
1. 如果您已使用Adobe target帳戶設定Adobe Analytics，則會看到「報 **告來源** 」下拉式功能表。 選取 **Adobe Target****或** Adobe Analytics做為來源。

   如果您選 **取Adobe Analytics**，請選取公司和報表套裝。 如果您選 **取Adobe Target**，則不需執行任何動作。

   ![chlimage_1-33](assets/chlimage_1-33.png)

1. 在「目 **標量度** 」區域的「我的主要目標 **** 」下方，選取您要追蹤的成功量度——轉換、收入、參與——並輸入量度的測量方式（或觀眾採取哪些動作來指出已達成目標）。 請參閱上表中目標量度的定義，並參閱 [Adobe Target成功量度的相關檔案](https://marketing.adobe.com/resources/help/en_US/target/target/r_success_metrics.html) 。

   您可以按一下右上角的三個點並選取「重新命名」，以重新命名目 **標**。

   如果您需要清除所有欄位，請按一下右上角的三個點，然後選取「清除所 **有欄位」**。

   所有量度也有進階設定，您可加以定義。 選取 **進階設定** ，以存取這些設定。 請參閱上表中如何計算成功度量的定義，並參閱 [Adobe Target檔案](https://marketing.adobe.com/resources/help/en_US/target/target/r_success_metrics.html)。

   >[!NOTE]
   您必須至少定義一個目標。

   ![chlimage_1-34](assets/chlimage_1-34.png)

   >[!NOTE]
   如果量度中遺失資訊，則量度周圍會有紅線。

1. 按一 **下新增量度** ，以設定其他成功量度。

   ![chlimage_1-35](assets/chlimage_1-35.png)

   >[!NOTE]
   您可以按一下或點選三個點，然後按一下或點選「刪除」，以移除其他 **目標**。 AEM要求您至少已定義一個目標。

1. 如果您想要對成功度量的計數方式有更多控制，請按一下或點選「進階 **設定** 」以存取這些度量。
1. 按一下&#x200B;**「儲存」**。

設定後，您可 [以檢視使用Adobe Target](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test) （體驗或A/B測試定位）的活動效能。 此外，透過A/B測試定位，您可以轉 [換得獎者。](/help/sites-authoring/activitylib.md#viewing-performance-and-converting-winning-experiences-a-b-test)

## 模擬體驗 {#simulating-an-experience}

模擬訪客的體驗，以驗證頁面內容是否如預期般根據您的目標內容設計顯示。 在模擬時，載入不同的使用者描述檔，並查看該使用者的目標內容。

下列條件會決定模擬訪客體驗時顯示的內容：

* 使用者作業儲存區（透過內容中樞）中的資料。
* 開啟 [的活動](/help/sites-authoring/activitylib.md)。
* 定 [義區段的規則](/help/sites-administering/campaign-segmentation.md)。
* Target元件中的體驗內容。
* 定 [位引擎的設定](/help/sites-authoring/activitylib.md)。

如果載入描述檔時頁面上出現非預期的內容，請檢查此清單中每個項目的設定。

>[!NOTE]
如果您使用A/B測試，則模擬體驗時會根據流量百分比顯示。 這由Adobe target控制，可能會導致作者出現意外結果。 （_author活動會與允許在模擬期間重新評估的特定設定同步。）作者可能需要重新整理，才能根據其流量設定來檢視其他體驗。

若要模擬訪客的體驗，請使用下列工具：

* 定位模式下的模擬活動：該頁面會顯示目前在Context Hub中選取之使用者的選件。 您可以編輯以使用者為目標的選件。
* 預覽模式：使用內容中樞來選取符合體驗所依據之區段標準的使用者和位置。 當您的「內容中樞」選項變更時，目標內容會隨之變更。

1. 若要切換至「預覽」模式，請在工具列上按一下或點選「預 **覽」**。
1. 在工具列上，按一下或點選「內容中樞」圖示。

   ![](do-not-localize/chlimage_1-7.png)

1. 使用Context Hub來變更內容屬性。 例如，按一下或點選「人物」屬性以選取不同的使用者。

   ![chlimage_1-36](assets/chlimage_1-36.png)

   頁面會變更為顯示目前內容的定位內容。

1. 若要變更顯示的選件，請切換至「定位」模式。 在選取模擬活動後，編輯您在「預覽」模式中設定之上下文的選件。

## 配置目標元件選項 {#configuring-target-component-options}

您可以透過下列兩種方式之一存取元件的選項來自訂Target元件：

1. 定位元件後，在Target元件中按一下或點選元件，然後再按設定圖示(cog)。

   ![](do-not-localize/chlimage_1-8.png)

   AEM會顯示Target元件選項視窗。

   ![chlimage_1-37](assets/chlimage_1-37.png)

1. 或者，若要以全螢幕模式存取這些設定，請在「目標元件選項」視窗中按一下或點選全螢幕圖示。

   ![](do-not-localize/chlimage_1-9.png)

   AEM會顯示全螢幕的Target元件選項視窗。

   ![chlimage_1-38](assets/chlimage_1-38.png)

1. 按照下表所述配置Target元件設定。

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>位置</strong></td>
   <td><p>此位置是字串，可為目標內容位置提供名稱，並將選件與應放置這些選件之頁面上的位置（或位置或元件）連接。</p> <p>此欄位是一般值。</p> <p>如果您將選件放入元件中，選件會記住位置ID。 執行頁面時，引擎會評估使用者的區段，並據此解析應顯示之作用中促銷活動的體驗。 然後，它會檢查頁面上的位置ID，並嘗試將選件與這些位置ID相符。</p> </td>
  </tr>
  <tr>
   <td><strong>引擎</strong></td>
   <td>根據您 <strong>要使用的引擎，在「用戶端規則」（無追蹤）、Adobe Target </strong><strong> 、ContextHub和 </strong>Adobe Campaign之間進行選擇。</td>
  </tr>
 </tbody>
</table>

如果您選取Adobe Target做為引擎：

![chlimage_1-39](assets/chlimage_1-39.png)

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>準確定位</strong></td>
   <td><p>啟用正確定位可讓元件等候用戶端內容或上下文中心資料可用，再將請求傳送至Adobe Target。 它可能會增載入入時間。 製作時，一律會啟用精確定位。</p> <p>如果您選取「準 <strong>確定位</strong> 」核取方塊，mbox會先執行一個 <code>mboxDefine</code> Ajax請求，然後 <code>mboxUpdate</code> 在資料可用時產生Ajax請求。</p> <p>如果您未選取「精確定位 <strong>」核取方塊，mbox會立即執行</strong><code>mboxCreate</code> 導致同步請求的動作（在此例中，並非所有上下文資料都可用）。</p> <p><strong></strong> 注意：對特定元件啟用或停用精確定位不會影響您已全域設定的設定。 您永遠可以在元件中選取「精確定位」來覆寫全域設定。</p> </td>
  </tr>
  <tr>
   <td><strong>包括已解析的區段</strong></td>
   <td><p>選取此核取方塊會包含mbox呼叫中所有已解析的區段，以及頁面和架構中所設定的任何參數。</p> <p>這僅適用於您正在同步AEM區段的XML API。 如果您的AEM中有未由Adobe Target處理的區段（如指令碼區段），則此選項可讓您解析AEM中的區段，並傳送區段作用中的資訊給Adobe Target。</p> </td>
  </tr>
  <tr>
   <td><strong>繼承的內容參數</strong></td>
   <td>列出從Adobe Target架構繼承的與所選頁面關聯的上下文參數（如果有）。</td>
  </tr>
  <tr>
   <td><strong>上下文參數</strong></td>
   <td>按一下或點 <strong>選「新增欄位</strong> 」，以設定其他上下文參數（與Target架構中可用的參數相同）。 新增至元件的上下文參 <i>數</i> ，只會套用至元件，而不會套用至其他元件，如果直接新增內容參數至架構則會如此。</td>
  </tr>
  <tr>
   <td><strong>靜態參數</strong></td>
   <td>按一下或點 <strong>選「新增欄位</strong> 」，以設定其他靜態參數（與Target架構中可用的參數相同）。 添加到元件的靜態參 <i>數僅應用於</i> ，而不應用於其它元件，如果直接將靜態參數添加到框架，則會如此。 靜態參數不來自上下文（內容中樞的用戶端上下文）。</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
當您選取元件並將其設為可定位時，AEM也會取代元件並插入Adobe Target元件。 （Adobe Target元件不僅會在您手動新增至頁面時使用，也會在您定位現有元件時使用。）

如果您選取「用戶端內容（用戶端）」做為引擎：

![chlimage_1-40](assets/chlimage_1-40.png)

<table>
 <tbody>
  <tr>
   <td><strong>選項</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td><strong>用戶端選項——策略</strong></td>
   <td><p>從以下選項中選擇：</p>
    <ul>
     <li><strong>第一</strong>:清單中最上層的體驗，如促銷活動中的順序。</li>
     <li><strong>隨機</strong>:任何體驗都會使用。</li>
     <li><strong>點按流分數</strong>:使用用戶端內容中追蹤的標籤和相關標籤點擊。 比較摘要頁面上定義之標籤的點擊率。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

如果您 **要整合AEM與Adobe Campaign** ，請選取Adobe Campaign作為引擎。 如需詳 [細資訊，請參閱「整合AEM與Adobe Campaign](/help/sites-administering/campaign.md) 」。

如果您 **使用ContextHub進行定位，請選取ContextHub** 作為引擎。 請參 [閱設定ContextHub。](/help/sites-administering/contexthub-config.md)

