---
title: 建立和管理最適化表單的A/B測試
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms與Adobe Target整合，可執行最適化表單的A/B測試，以增強客戶體驗並改善轉換率。
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 1def8ff7bc90e2ab82ce8b50277a97da9709c78c
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# 建立和管理最適化表單的A/B測試{#create-and-manage-a-b-test-for-adaptive-forms}

## 概覽 {#overview-br}

如果您的客戶提供的體驗不吸引人，他們可能會放棄表單。 雖然讓客戶感到沮喪，但它還可以提高貴組織的支援量和成本。 識別並提供適當的客戶體驗以提高轉換率既重要又具挑戰性。 Adobe Experience Manager Forms是這個問題的關鍵。

AEM Forms與Adobe Marketing Cloud解決方案Adobe Target整合，可跨多個數位頻道提供個人化且吸引人的客戶體驗。 Target的其中一項主要功能是A/B測試，可讓您快速設定同時進行的A/B測試、向目標使用者呈現相關內容，以及識別可帶來更高轉換率的體驗。

透過AEM Forms，您可以即時在適用性表單上設定和執行A/B測試。 此外，它還提供現成可用且可自訂的報表功能，以視覺化您的表單體驗的即時效能，並找出可將使用者互動和轉換最大化的體驗。

## 在AEM Forms中設定和整合Target {#set-up-and-integrate-target-in-aem-forms}

開始建立和分析最適化表單的A/B測試之前，您需要設定Target伺服器，並將其整合至AEM Forms。

### 設定Target {#set-up-target}

若要將AEM與Target整合，請確定您擁有有效的Adobe Target帳戶。 向Adobe Target註冊時，您會收到用戶端代碼。 您需要用戶端代碼、與Target帳戶相關聯的電子郵件，以及密碼，才能將AEM與Target連線。

用戶端代碼可識別Adobe Target客戶帳戶，並在呼叫Adobe Target伺服器時作為URL中的子網域使用。 在繼續操作之前，登錄[https://experience.adobe.com/](https://experience.adobe.com/)，如果您有訪問權限，請查看[!UICONTROL 快速訪問]部分中的[!DNL Adobe Target]選項。

### 在AEM Forms中整合Target {#integrate-target-in-aem-forms}

執行下列步驟來整合執行中的Target伺服器與AEM Forms:

1. 在AEM伺服器上，轉至https://&lt;*hostname*:&lt;*port*>/libs/cq/core/content/tools/cloudservices.html。

1. 在&#x200B;**Adobe Target**&#x200B;區段中，按一下&#x200B;**顯示配置**，然後按一下&#x200B;**+**圖示以新增配置。
如果您是第一次配置目標，請按一下「立即配置」。****

1. 在「建立配置」對話框中，指定配置的&#x200B;**標題**&#x200B;和可選的&#x200B;**名稱**。

1. 按一下&#x200B;**建立**。「編輯元件」(Edit component)對話框開啟。
1. 指定您的Target帳戶詳細資訊，例如用戶端代碼、電子郵件和密碼。
1. 從「API類型」下拉式清單中選取「**Rest**」。

1. 按一下&#x200B;**連線至Adobe Target**&#x200B;以初始化與Target的連線。 如果連接成功，則顯示「Connection successful（連接成功）」消息。 按一下消息上的&#x200B;**OK**，然後在對話框上按一下&#x200B;**OK**。 已設定Target帳戶。

1. 如[新增架構](/help/sites-administering/target.md)中所述，建立Target架構。

1. 轉到https://&lt;*hostname*>:&lt;*port*>/system/console/configMgr。

1. 按一下&#x200B;**AEM Forms Target設定**。
1. 選擇&#x200B;**目標框架**。
1. 在&#x200B;**目標URL**&#x200B;欄位中，指定將執行A/B測試的所有URL。 例如，OSGi上的AEM Forms伺服器https://&lt;*hostname*>:&lt;*port*>/，或https://*hostname*>:&lt;*port*/lc/,JEE上的AEM Forms伺服器。
請考慮您要為發佈執行個體設定Target URL，而您的客戶可以使用主機名稱或IP位址存取，您需要將兩者設為Target URL — 使用主機名稱及IP位址。 如果您只設定其中一個URL，則不會對來自其他URL的客戶執行A/B測試。 按一下**+**&#x200B;以指定多個URL。

1. 按一下「**儲存**」。

您的Target伺服器已與AEM Forms整合。 如果您擁有使用Adobe Target的完整授權，現在可以啟用A/B測試。

如果您有使用Adobe Target的完整授權，請在將Target與AEM Forms整合後，使用下列參數啟動伺服器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM執行個體在JBoss上執行，從統包服務開始，請在`jboss\bin\standalone.conf.bat`檔案中，在下列項目中新增 — Dabtesting.enabled=true參數：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss伺服器之外，您還可以在任何應用程式伺服器的伺服器啟動指令碼中添加 — Dabtesting.enabled=true jvm參數。 現在您可以建立並執行最適化表單的A/B測試。

>[!NOTE]
>
>如果您稍後更新已設定的Target URL，請務必更新任何執行中的A/B測試，使其指向目前的URL。 有關更新A/B測試的資訊，請參閱[更新A/B測試](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)。

## 在AEM中建立對象 {#create-audiences-within-aem}

AEM可讓您建立對象，並用於A/B測試。 您在AEM中建立的對象可在AEM Forms中使用。 執行下列步驟以在AEM中建立對象：

1. 在製作例項中，點選&#x200B;**Adobe Experience Manager** > **個人化** > **對象**。

1. 在「對象」頁面中，點選&#x200B;**建立對象>建立目標對象**。
1. 在「Adobe Target設定」對話方塊中，選取Target設定，然後按一下&#x200B;**確定**。
1. 在建立新受眾頁面中，建立規則。 規則可讓您將對象分類。 例如，您想要根據作業系統來分類對象。 您的對象A來自Windows，而對象B來自Linux。

   1. 若要根據Windows來分類受眾，請在規則#1中選取&#x200B;**OS**&#x200B;屬性類型。 從「時間」下拉式清單中，選擇&#x200B;**Windows.**

   1. 若要根據Linux對受眾分類，請在規則#2中選取&#x200B;**OS**&#x200B;屬性類型。 從&#x200B;**When**&#x200B;下拉式清單中，選擇&#x200B;**Linux**，然後按一下&#x200B;**Next**。

1. 指定已建立對象的名稱，然後按一下「**儲存**」。

您可以在為表單設定A/B測試時選取對象，如下所示。

## 建立A/B測試 {#create-a-b-test}

執行下列步驟以建立最適化表單的A/B測試。

1. 前往&#x200B;**Forms與檔案**(https://*hostname*>:*port*>/aem/forms.html/content/dam/formsanddocuments)。

1. 導覽至包含最適化表單的資料夾。
1. 按一下工具列中的&#x200B;**選取**&#x200B;工具，然後選取最適化表單。
1. 按一下工具列中的&#x200B;**More** ，然後選取&#x200B;**Configure A/B Testing**。 「設定A/B」測試頁面隨即開啟。

[ ](assets/ab-test-configure-1.png)

1. 指定A/B測試的&#x200B;**活動名稱**。

1. 從「對象」下拉式清單中，選取您要為其提供不同表單體驗的對象。 例如，**使用Chrome**&#x200B;的訪客。 對象清單會從設定的Target伺服器填入。

1. 在體驗A和B的&#x200B;**體驗分送**&#x200B;欄位中，以百分比指定分送，以決定體驗在總受眾中的分送。 例如，如果您分別為體驗A和B指定40、60，體驗A將提供給40%的對象，其餘60%將看到體驗B。
1. 按一下&#x200B;**配置**。 出現對話方塊，確認A/B測試的建立。
1. 按一下「**編輯體驗B**」以在編輯模式中開啟最適化表單。 修改表單以建立與預設體驗A不同的體驗。體驗B中允許的可能變數為：

   * CSS或樣式
   * 不同面板或相同面板中的欄位順序
   * 面板布局
   * 面板標題
   * 欄位的說明、標籤和說明文字
   * 不影響或中斷提交流程的指令碼
   * 驗證（客戶端和伺服器端）
   * 體驗B的主題。（您可以為體驗B選取替代主題）

1. 前往Forms和檔案UI，選取最適化表單，按一下&#x200B;**更多**，然後選取&#x200B;**開始A/B測試**。

您的A/B測試現在正在執行，系統會根據指定的分送，隨機提供指定的對象。

## 更新A/B測試 {#update-a-b-test}

您可以更新執行中A/B測試的對象和體驗分配。 若要這麼做：

1. 在Forms與檔案UI中，導覽至包含執行A/B測試的最適化表單的資料夾。
1. 選取最適化表單。
1. 按一下「**更多**」，然後選擇「**編輯A/B測試**」。 「更新A/B」測試頁面隨即開啟。

1. 視需要更新對象和體驗分送。
1. 按一下&#x200B;**更新**。

## 檢視和分析A/B測試報表 {#view-and-analyze-a-b-test-report}

在您允許A/B測試在所需期間執行後，您就可以產生報表，並檢查哪個體驗已導致更好的轉換。 您可以宣告效能較佳的體驗為獲勝者，或選擇執行其他A/B測試。 要執行此操作，請執行以下步驟：

1. 選取最適化表單，按一下&#x200B;**更多**，然後按一下&#x200B;**A/B測試報表**。 報表隨即顯示。

[ ](assets/ab-test-report-3.png)

1. 分析報表，查看您是否有足夠的資料點將其中一個表現較佳的體驗宣告為獲勝者。 您可以選擇繼續執行相同的A/B測試更久，或宣告獲勝者並結束A/B測試。
1. 若要宣告獲勝者並結束A/B測試，請按一下報表控制面板上的&#x200B;**結束A/B測試**按鈕。 對話方塊會提示您將兩個體驗其中之一宣告為獲勝者。 選擇獲勝者並確認以結束A/B測試。
或者，您也可以按一下個別體驗的**宣告獲勝者**&#x200B;按鈕，以先宣告獲勝者。 提示您確認獲勝者。 按一下「**是**」結束A/B測試。

如果您挑選體驗A作為獲勝者，A/B測試將會結束，並且隨後，只會向所有對象提供體驗A。
