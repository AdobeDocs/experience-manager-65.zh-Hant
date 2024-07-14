---
title: 建立和管理最適化表單的A/B測試
description: AEM Forms與Adobe Target整合，可針對最適化表單執行A/B測試，以增強客戶體驗並提高轉換率。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '1558'
ht-degree: 0%

---

# 建立和管理最適化表單的A/B測試{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE 已終止]{type=negative tooltip="此功能現已終止服務"}

<div class="preview"> 調適型表單的A/B測試功能已終止服務，不再受支援。 </div>

## 概觀 {#overview-br}

如果表單提供的體驗不吸引人，您的客戶可能會捨棄表單。 雖然這會讓客戶感到挫折，但也可以提升貴組織的支援數量和成本。 識別並提供適當的客戶體驗以提高轉換率，這既重要又具有挑戰性。 Adobe Experience Manager Forms掌握此問題的關鍵所在。

AEM Forms與Adobe Experience Cloud解決方案Adobe Target整合，跨多個數位頻道提供個人化及吸引人的客戶體驗。 Target的一項重要功能是A/B測試，可讓您快速設定同時的A/B測試、向目標使用者呈現相關內容，以及識別可促進轉換率較高的體驗。

透過Adobe Experience Manager (AEM) Forms，您可以即時設定和執行最適化表單的A/B測試。 此外，還提供現成且可自訂的報告功能，將表單體驗的即時效能加以視覺化，並找出能最大程度提高使用者參與度和轉換率的體驗。

## 在AEM Forms中設定並整合Target {#set-up-and-integrate-target-in-aem-forms}

開始建立和分析適用性表單的A/B測試之前，您必須設定Target伺服器並將其整合到AEM Forms中。

### 設定Target {#set-up-target}

若要將AEM與Target整合，請確定您擁有有效的Adobe Target帳戶。 註冊Adobe Target時，您會收到使用者端代碼。 您需要使用者端代碼、與Target帳戶關聯的電子郵件，以及連線AEM與Target的密碼。

使用者端代碼會識別Adobe Target客戶帳戶，並在呼叫Adobe Target伺服器時作為URL中的子網域。 在繼續之前，請先登入[https://experience.adobe.com/](https://experience.adobe.com/)，如果您有存取權，請檢視[!UICONTROL 快速存取]區段中的[!DNL Adobe Target]選項。

### 將執行中的Target伺服器與AEM Forms整合 {#integrate-target-in-aem-forms}

1. 在AEM伺服器上，移至https://&lt;*主機名稱*>：&lt;*連線埠*>/libs/cq/core/content/tools/cloudservices.html。

1. 在&#x200B;**Adobe Target**&#x200B;區段中，按一下&#x200B;**顯示組態**，然後按一下&#x200B;**+**圖示以新增組態。
如果您是第一次設定目標，請按一下[立即設定]。****

1. 在[建立組態]對話方塊中，指定組態的&#x200B;**Title**&#x200B;以及選擇性的&#x200B;**Name**。

1. 按一下「**建立**」。「編輯元件」對話方塊開啟。
1. 指定您的Target帳戶詳細資料，例如使用者端代碼、電子郵件和密碼。
1. 從API型別下拉式清單中選取&#x200B;**Rest**。

1. 按一下&#x200B;**連線至Adobe Target**，以便初始化與Target的連線。 如果連線成功，則會顯示「連線成功」訊息。 在訊息上按一下&#x200B;**[確定]**，然後在對話方塊上按一下&#x200B;**[確定]**。 已設定Target帳戶。

1. 建立Target框架，如[新增框架](/help/sites-administering/target.md)中所述。

1. 移至https://&lt;*主機名稱*>：&lt;*連線埠*>/system/console/configMgr。

1. 按一下&#x200B;**AEM Forms目標組態**。
1. 選取&#x200B;**目標架構**。
1. 在&#x200B;**目標URL**&#x200B;欄位中，指定執行A/B測試的所有URL。 例如，OSGi上AEM Forms伺服器的https://&lt;*主機名稱*>：&lt;*連線埠*>/，或JEE上AEM Forms伺服器的https://&lt;*主機名稱*>：&lt;*連線埠*>/lc/。
假設您要為Publish執行個體設定Target URL，且您的客戶可使用主機名稱或IP位址進行存取。 在這種情況下，您必須使用主機名稱和IP位址，將兩者設定為Target URL。 如果您只設定其中一個URL，則不會針對來自其他URL的客戶執行A/B測試。 按一下**+**&#x200B;以指定多個URL。

1. 按一下「**儲存**」。

您的Target伺服器已與AEM Forms整合。 如果您擁有使用Adobe Target的完整授權，現在可以啟用A/B測試。

如果您有使用Adobe Target的完整授權，將Target與AEM Forms整合後，請使用下列引數啟動伺服器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM執行個體在JBoss®上執行，從turnkey以服務方式啟動，在`jboss\bin\standalone.conf.bat`檔案中，將 — Dabtesting.enabled=true引數新增到下列專案中：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了JBoss®伺服器之外，您也可以在任何應用程式伺服器的伺服器啟動指令碼中新增 — Dabtesting.enabled=true jvm引數。 現在您可以建立和執行最適化表單的A/B測試。

>[!NOTE]
>
>如果您稍後更新已設定的Target URL，請確定您更新任何執行中的A/B測試，使其指向目前的URL。 如需有關更新A/B測試的資訊，請參閱[更新A/B測試](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)。
>

## 在AEM中建立對象 {#create-audiences-within-aem}

AEM可讓您建立對象，並將其用於A/B測試。 您在AEM中建立的對象可在AEM Forms中使用。 若要在AEM中建立對象，請執行下列動作：

1. 在編寫執行個體中，選取&#x200B;**Adobe Experience Manager** > **Personalization** > **對象**。

1. 在「對象」頁面中，選取&#x200B;**建立對象>建立目標對象**。
1. 在Adobe Target設定對話方塊中，選取Target設定，然後按一下&#x200B;**確定**。
1. 在建立新對象頁面中，建立規則。 規則可讓您分類對象。 例如，您想要根據作業系統將對象分類。 您的對象A來自Windows，而對象B來自Linux®。

   1. 若要根據Windows來分類對象，請在規則#1中，選取&#x200B;**OS**&#x200B;屬性型別。 從[When]下拉式清單中，選取&#x200B;**Windows.**

   1. 若要根據Linux®來分類對象，請在規則#2中，選取&#x200B;**OS**&#x200B;屬性型別。 從&#x200B;**When**&#x200B;下拉式清單中，選取&#x200B;**Linux®**，然後按一下&#x200B;**下一步**。

1. 指定已建立對象的名稱，然後按一下[儲存]。****

當您設定表單的A/B測試時，可以選取對象，如下所示。

## 為最適化表單建立A/B測試 {#create-a-b-test}

1. 前往&#x200B;**Forms &amp; Documents**，網址為https://&lt;*主機名稱*>：&lt;*連線埠*>/aem/forms.html/content/dam/formsanddocuments。

1. 導覽至包含最適化表單的資料夾。
1. 按一下工具列中的&#x200B;**選取**&#x200B;工具並選取最適化表單。
1. 按一下工具列中的&#x200B;**更多**，然後選取&#x200B;**設定A/B測試**。 隨即開啟設定A/B測試頁面。

[](assets/ab-test-configure-1.png)

1. 指定A/B測試的&#x200B;**活動名稱**。

1. 從「對象」下拉式清單中，選取您要為其提供不同表單體驗的對象。 例如，**位使用Chrome**&#x200B;的訪客。 對象清單是從已設定的Target伺服器填入。

1. 在體驗A和B的&#x200B;**體驗分佈**&#x200B;欄位中，指定分佈（以百分比表示）以決定體驗在總對象中的分佈。 例如，如果您分別指定40、60給體驗A和B，則體驗A會提供給40%的對象，而其餘的60%則會看到體驗B。
1. 按一下&#x200B;**設定**。 會出現一個對話方塊，確認建立A/B測試。
1. 按一下「**編輯體驗B**」，以便您可以在編輯模式中開啟最適化表單。 建立與預設體驗A不同的體驗，以修改表單。體驗B中允許的可能變化為以下變更：

   * CSS或樣式
   * 不同面板或相同面板中的欄位順序
   * 面板版面配置
   * 面板標題
   * 欄位的說明、標籤和說明文字
   * 不會影響或中斷提交流程的指令碼
   * 驗證（使用者端和伺服器端）
   * 體驗B的主題。（您可以為體驗B選擇替代主題）

1. 前往Forms和檔案UI，選取最適化表單，按一下&#x200B;**更多**，然後選取&#x200B;**開始A/B測試**。

您的A/B測試目前正在執行，而指定的對象會根據指定的分佈隨機提供體驗。

## 更新A/B測試 {#update-a-b-test}

您可以更新執行A/B測試的對象和體驗分佈。

若要更新A/B測試：

1. 在Forms和檔案UI中，導覽至包含執行A/B測試的最適化表單的資料夾。
1. 選取最適化表單。
1. 按一下&#x200B;**更多**，然後選取&#x200B;**編輯A/B測試**。 更新A/B測試頁面隨即開啟。

1. 視需要更新對象和體驗分佈。
1. 按一下&#x200B;**更新**。

## 檢視和分析A/B測試報告 {#view-and-analyze-a-b-test-report}

一旦您允許A/B測試在所需的期間執行，您就可以產生報告並檢查哪個體驗產生了更好的轉換。 您可以將表現較佳的體驗宣告為獲勝者，或選擇執行其他A/B測試。

若要檢視和分析A/B測試報告：

1. 選取最適化表單，按一下&#x200B;**更多**，然後按一下&#x200B;**A/B測試報告**。 報表隨即顯示。

[](assets/ab-test-report-3.png)

1. 分析報表，檢視是否有足夠的資料點將其中一個表現較佳的體驗宣告為獲勝者。 您可以選擇繼續相同的A/B測試以獲得更多時間或宣告獲勝者並結束A/B測試。
1. 若要宣告獲勝者並結束A/B測試，請按一下報告控制面板上的&#x200B;**結束A/B測試**按鈕。 對話方塊會提示您宣告兩個體驗其中之一為獲勝者。 選擇獲勝者並確認結束A/B測試。
或者，您可以先按一下個別體驗的「**宣告獲勝者**」按鈕來宣告獲勝者。 它會提示您確認獲勝者。 按一下&#x200B;**是**&#x200B;結束A/B測試。

如果您選擇體驗A作為獲勝者，A/B測試會結束，且往後只會提供體驗A給對象。
