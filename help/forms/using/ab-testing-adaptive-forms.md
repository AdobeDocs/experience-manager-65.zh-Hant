---
title: 建立和管理最適化表單的A/B測試
description: AEM Forms與Adobe Target整合，可針對最適化表單執行A/B測試，以增強客戶體驗並提高轉換率。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '1554'
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

使用者端代碼會識別Adobe Target客戶帳戶，並在呼叫Adobe Target伺服器時作為URL中的子網域。 繼續之前，請先登入 [https://experience.adobe.com/](https://experience.adobe.com/) 如果您有存取權，可檢視 [!DNL Adobe Target] 中的選項 [!UICONTROL 快速存取] 區段。

### 將執行中的Target伺服器與AEM Forms整合 {#integrate-target-in-aem-forms}

1. 在AEM伺服器上，前往https://&lt;*主機名稱*>：&lt;*連線埠*>/libs/cq/core/content/tools/cloudservices.html.

1. 在 **Adobe Target** 區段，按一下 **顯示設定** 然後 **+** 圖示以新增設定。
如果您是第一次設定目標，請按一下 **立即設定。**

1. 在建立組態對話方塊中，指定 **標題** 並可選擇使用 **名稱** 用於設定。

1. 按一下「**建立**」。「編輯元件」對話方塊開啟。
1. 指定您的Target帳戶詳細資料，例如使用者端代碼、電子郵件和密碼。
1. 選取 **Rest** 從「API型別」下拉式清單。

1. 按一下 **連線至Adobe Target** 以便初始化與Target的連線。 如果連線成功，則會顯示「連線成功」訊息。 按一下 **確定** 在訊息上，然後 **確定** 在對話方塊上。 已設定Target帳戶。

1. 建立Target架構，如所述 [新增框架](/help/sites-administering/target.md).

1. 前往https://&lt;*主機名稱*>：&lt;*連線埠*>/system/console/configMgr.

1. 按一下 **AEM Forms目標設定**.
1. 選取 **目標框架**.
1. 在 **目標URL** 欄位中，指定執行A/B測試的所有URL。 例如， https://&lt;*主機名稱*>：&lt;*連線埠*>/ (適用於OSGi上的AEM Forms伺服器)或https://&lt;*主機名稱*>：&lt;*連線埠*>/lc/適用於JEE上的AEM Forms Server。
假設您想為發佈執行個體設定Target URL，且您的客戶可使用主機名稱或IP位址進行存取。 在這種情況下，您必須使用主機名稱和IP位址，將兩者設定為Target URL。 如果您只設定其中一個URL，則不會針對來自其他URL的客戶執行A/B測試。 按一下 **+** 以指定多個URL。

1. 按一下「**儲存**」。

您的Target伺服器已與AEM Forms整合。 如果您擁有使用Adobe Target的完整授權，現在可以啟用A/B測試。

如果您有使用Adobe Target的完整授權，將Target與AEM Forms整合後，請使用下列引數啟動伺服器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果AEM執行個體在JBoss®上執行，則從以下的turnkey以服務形式啟動： `jboss\bin\standalone.conf.bat` 檔案，請在下列專案中新增 — Dabtesting.enabled=true引數：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了JBoss®伺服器之外，您也可以在任何應用程式伺服器的伺服器啟動指令碼中新增 — Dabtesting.enabled=true jvm引數。 現在您可以建立和執行最適化表單的A/B測試。

>[!NOTE]
>
>如果您稍後更新已設定的Target URL，請確定您更新任何執行中的A/B測試，使其指向目前的URL。 如需有關更新A/B測試的資訊，請參閱 [更新A/B測試](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p).
>

## 在AEM中建立對象 {#create-audiences-within-aem}

AEM可讓您建立對象，並將其用於A/B測試。 您在AEM中建立的對象可在AEM Forms中使用。 若要在AEM中建立對象，請執行下列動作：

1. 在編寫執行個體中，點選 **Adobe Experience Manager** > **個人化** > **受眾**.

1. 在「對象」頁面中，點選「 」 **建立對象>建立目標對象**.
1. 在Adobe Target設定對話方塊中，選取Target設定，然後按一下 **確定**.
1. 在建立新對象頁面中，建立規則。 規則可讓您分類對象。 例如，您想要根據作業系統將對象分類。 您的對象A來自Windows，而對象B來自Linux®。

   1. 若要根據Windows來分類對象，請在規則#1中，選取 **作業系統** 屬性型別。 從「時間」下拉式清單中，選取 **Windows。**

   1. 若要根據Linux®分類對象，請在規則#2中，選取 **作業系統** 屬性型別。 從 **時間** 下拉式清單，選取 **Linux®**，然後按一下 **下一個**.

1. 指定已建立對象的名稱，然後按一下 **儲存**.

當您設定表單的A/B測試時，可以選取對象，如下所示。

## 為最適化表單建立A/B測試 {#create-a-b-test}

1. 前往 **Forms與檔案** 在https://&lt;*主機名稱*>：&lt;*連線埠*>/aem/forms.html/content/dam/formsanddocuments.

1. 導覽至包含最適化表單的資料夾。
1. 按一下 **選取** 工具列並選取最適化表單。
1. 按一下 **更多** ，然後選取「 」 **設定A/B測試**. 隨即開啟設定A/B測試頁面。

[](assets/ab-test-configure-1.png)

1. 指定 **活動名稱** 用於A/B測試。

1. 從「對象」下拉式清單中，選取您要為其提供不同表單體驗的對象。 例如， **使用Chrome的訪客**. 對象清單是從已設定的Target伺服器填入。

1. 在 **體驗散佈** 體驗A和B的欄位中，以百分比的方式指定分佈，以決定體驗在總受眾中的分佈。 例如，如果您分別指定40、60給體驗A和B，則體驗A會提供給40%的對象，而其餘的60%則會看到體驗B。
1. 按一下 **設定**. 會出現一個對話方塊，確認建立A/B測試。
1. 按一下 **編輯體驗B** 以便您在編輯模式中開啟最適化表單。 建立與預設體驗A不同的體驗，以修改表單。體驗B中允許的可能變化為以下變更：

   * CSS或樣式
   * 不同面板或相同面板中的欄位順序
   * 面板版面配置
   * 面板標題
   * 欄位的說明、標籤和說明文字
   * 不會影響或中斷提交流程的指令碼
   * 驗證（使用者端和伺服器端）
   * 體驗B的主題。（您可以為體驗B選擇替代主題）

1. 前往Forms和檔案UI，選取最適化表單，然後按一下 **更多**，並選取 **開始A/B測試**.

您的A/B測試目前正在執行，而指定的對象會根據指定的分佈隨機提供體驗。

## 更新A/B測試 {#update-a-b-test}

您可以更新執行A/B測試的對象和體驗分佈。

若要更新A/B測試：

1. 在Forms和檔案UI中，導覽至包含執行A/B測試的最適化表單的資料夾。
1. 選取最適化表單。
1. 按一下 **更多** 然後選取 **編輯A/B測試**. 更新A/B測試頁面隨即開啟。

1. 視需要更新對象和體驗分佈。
1. 按一下&#x200B;**更新**。

## 檢視和分析A/B測試報告 {#view-and-analyze-a-b-test-report}

一旦您允許A/B測試在所需的期間執行，您就可以產生報告並檢查哪個體驗產生了更好的轉換。 您可以將表現較佳的體驗宣告為獲勝者，或選擇執行其他A/B測試。

若要檢視和分析A/B測試報告：

1. 選取最適化表單，按一下 **更多**，然後按一下 **A/B測試報告**. 報表隨即顯示。

[](assets/ab-test-report-3.png)

1. 分析報表，檢視是否有足夠的資料點將其中一個表現較佳的體驗宣告為獲勝者。 您可以選擇繼續相同的A/B測試以獲得更多時間或宣告獲勝者並結束A/B測試。
1. 若要宣告獲勝者並結束A/B測試，請按一下 **結束A/B測試** 按鈕來建立報告面板。 對話方塊會提示您宣告兩個體驗其中之一為獲勝者。 選擇獲勝者並確認結束A/B測試。
或者，您可以先按一下 **宣告贏家** 按鈕來顯示個別體驗。 它會提示您確認獲勝者。 按一下 **是** 以結束A/B測試。

如果您選擇體驗A作為獲勝者，A/B測試會結束，且往後只會提供體驗A給對象。
