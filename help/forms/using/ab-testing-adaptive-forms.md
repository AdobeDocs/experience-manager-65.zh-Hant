---
title: 建立和管理自適應表單的A/Btest
seo-title: Create and manage A/B test for adaptive forms
description: AEM Forms公司與Adobe Target公司整合，允許運行A/Btest，以適應形式，以增強客戶體驗和提高轉換率。
seo-description: AEM Forms integrates with Adobe Target that allows running A/B tests for adaptive forms to enhance customer experience and improve conversion rates.
uuid: e258805c-4da8-4c5d-ae91-7bea78a6a71b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 8f776f30-ff93-4d19-94c6-c4bfe6f1fae2
docset: aem65
exl-id: be2444df-c772-4a8e-83f9-0f565c15a44e
source-git-commit: 294d12e7d1b5293f165a164ff1fcc624f7b2b648
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# 建立和管理自適應表單的A/Btest{#create-and-manage-a-b-test-for-adaptive-forms}

[!BADGE 已終止]{type=negative tooltip="此功能現在已過期"}

<div class="preview"> 自適應表單功能的A/B測試已到期，不再受支援。 </div>

## 概觀 {#overview-br}

如果您的客戶提供的體驗不吸引人，他們可能會放棄表單。 雖然這讓客戶感到沮喪，但也會增加您組織的支援量和成本。 確定並提供適當的客戶體驗，提高轉換率，這既是關鍵，也是挑戰。 Adobe Experience Manager Forms是這個問題的關鍵。

AEM Forms公司與Adobe Marketing Cloud解決方案Adobe Target公司整合，在多個數字渠道提供個性化和引人入勝的客戶體驗。 目標的關鍵功能之一是A/B測試，它允許您快速設定併發的A/Btest，向目標用戶顯示相關內容，並確定能夠提高轉換率的體驗。

使用AEM Forms，您可以即時設定和運行自適應表單上的A/Btest。 它還提供了現成的和可定製的報告功能，以可視化您的表單體驗的即時效能，並確定能夠最大限度地提高用戶參與和轉換的效能。

## 在AEM Forms建立和整合目標 {#set-up-and-integrate-target-in-aem-forms}

在開始建立和分析A/Btest以適應性表單之前，您需要設定目標伺服器並將其整合到AEM Forms。

### 設定目標 {#set-up-target}

要與目AEM標整合，請確保您有有效的Adobe Target帳戶。 在Adobe Target註冊時，您會收到客戶代碼。 您需要客戶端代碼、與目標帳戶關聯的電子郵件和密碼才能與AEM目標連接。

客戶端代碼標識Adobe Target客戶帳戶，並在調用Adobe Target伺服器時用作URL中的子域。 繼續之前，請登錄到 [https://experience.adobe.com/](https://experience.adobe.com/) 如果您有權訪問，請查看 [!DNL Adobe Target] 的上界 [!UICONTROL 快速訪問] 的子菜單。

### 整合目標在AEM Forms {#integrate-target-in-aem-forms}

執行以下步驟將正在運行的目標伺服器與AEM Forms整合：

1. 在服AEM務器上，轉到https://&lt;*主機名*>:&lt;*埠*>/libs/cq/core/content/tools/cloudservices.html。

1. 在 **Adobe Target** ，按一下 **顯示配置** 然後 **+** 表徵圖以添加新配置。
如果是首次配置目標，請按一下 **立即配置。**

1. 在「建立配置」對話框中，指定 **標題** （可選） **名稱** 的子菜單。

1. 按一下&#x200B;**建立**。「編輯」(Edit)元件對話框開啟。
1. 指定目標帳戶詳細資訊，如客戶端代碼、電子郵件和密碼。
1. 選擇 **休息** 從「API類型」下拉清單中。

1. 按一下 **連接到Adobe Target** 初始化與目標的連接。 如果連接成功，則顯示「連接成功」消息。 按一下 **確定** 在留言上，然後 **確定** 對話框。 已配置目標帳戶。

1. 建立目標框架（如所述） [添加框架](/help/sites-administering/target.md)。

1. 請訪問https://&lt;*主機名*>:&lt;*埠*>/system/console/configMgr。

1. 按一下 **AEM Forms目標配置**。
1. 選擇 **目標框架**。
1. 在 **目標URL** 欄位中，指定將運行A/Btest的所有URL。 例如，https://&lt;*主機名*>:&lt;*埠*>/用於OSGi或https://上的AEM Forms伺服器&lt;*主機名*>:&lt;*埠*>/lc/，用於JEE上的AEM Forms伺服器。
請考慮您要為發佈實例配置目標URL，並且您的客戶可以使用主機名或IP地址訪問該URL，您需要將兩者都配置為目標URL — 使用主機名和IP地址。 如果只配置其中一個URL，則A/Btest將不會為來自另一個URL的客戶運行。 按一下 **+** 指定多個URL。

1. 按一下「**儲存**」。

您的目標伺服器已與AEM Forms整合。 如果您擁有使用Adobe Target的完整許可證，則現在可以啟用A/B測試。

如果您擁有使用Adobe Target的完整許可證，請在將Target與AEM Forms整合後使用以下參數啟動伺服器：

`parameter -Dabtesting.enabled=true java -Xmx2048m -XX:MaxPermSize=512M -jar -Dabtesting.enabled=true`

如果實AEM例在JBoss上運行，則作為從交鑰匙開始的服務在 `jboss\bin\standalone.conf.bat` 檔案，在以下條目中添加 — dabtesting.enabled=true參數：

`set "JAVA_OPTS=%JAVA_OPTS% -Dadobeidp.serverName=server1 -Dfile.encoding=utf8 -Djava.net.preferIPv4Stack=true -Dabtesting.enabled=true"`

除了jboss伺服器外，您還可以在任何應用程式伺服器的伺服器啟動指令碼中添加 — Dabtesting.enabled=true jvm參數。 現在，您可以建立並運行適應表單的A/Btest。

>[!NOTE]
>
>如果稍後更新已配置的目標URL，請確保更新任何正在運行的A/Btest，以便它們指向當前URL。 有關更新A/Btest的資訊，請參見 [更新A/Btest](/help/forms/using/ab-testing-adaptive-forms.md#p-update-a-b-test-p)。

## 在內部建立受眾AEM {#create-audiences-within-aem}

用AEM於建立受眾，並將其用於A/Btest。 您在其中建立的AEM受眾在AEM Forms。 執行以下步驟以在中建立受眾AEM:

1. 在創作實例中，點擊 **Adobe Experience Manager** > **個性化** > **觀眾**。

1. 在「受眾」頁中，按一下 **建立受眾>建立目標受眾**。
1. 在「Adobe Target配置」對話框中，選擇目標配置，然後按一下 **確定**。
1. 在「建立新受眾」頁中，建立規則。 規則允許您對受眾進行分類。 例如，您要根據作業系統對受眾進行分類。 您的觀眾A來自Windows，而觀眾B來自Linux。

   1. 要根據Windows對受眾進行分類，請在規則#1中選擇 **作業系統** 屬性類型。 從「時間」(When)下拉清單中，選擇 **窗口。**

   1. 要根據Linux對受眾進行分類，請在規則#2中選擇 **作業系統** 屬性類型。 從 **當** 下拉，選擇 **Linux**，然後按一下 **下一個**。

1. 指定建立的受眾的名稱，然後按一下 **保存**。

在為表單配置A/B測試時，可以選擇受眾，如下所示。

## 建立A/Btest {#create-a-b-test}

執行以下步驟為自適應表單建立A/Btest。

1. 轉到 **Forms和文檔** https://&lt;*主機名*>:&lt;*埠*>/aem/forms.html/content/dam/formsanddocuments。

1. 導航到包含自適應表單的資料夾。
1. 按一下 **選擇** 的子菜單。
1. 按一下 **更多** 中，選擇 **配置A/B測試**。 將開啟「配置A/B測試」頁。

[ ](assets/ab-test-configure-1.png)

1. 指定 **活動名稱** A/Btest。

1. 從「受眾」下拉清單中，選擇要為其提供窗體不同體驗的受眾。 比如說， **使用Chrome的訪問者**。 從配置的目標伺服器填充訪問群體清單。

1. 在 **經驗分配** A和B的欄位中，指定以百分比表示的分佈，以確定在總受眾中的經驗分佈。 例如，如果您分別為經驗A和B指定40、60，則經驗A將提供給40%的受眾，其餘60%將看到經驗B。
1. 按一下 **配置**。 將出現一個對話框，確認A/Btest的建立。
1. 按一下 **編輯體驗B** 的子菜單。 修改表單以建立與預設體驗A不同的體驗。經驗B中允許的可能變化為：

   * CSS或樣式
   * 不同面板或同一面板中的欄位順序
   * 面板版面配置
   * 面板標題
   * 欄位的說明、標籤和幫助文本
   * 不影響或中斷提交流的指令碼
   * 驗證（客戶端和伺服器端）
   * 經驗B的主題。（您可以選擇經驗B的備選主題）

1. 轉至「Forms和文檔」UI，選擇自適應表單，按一下 **更多**，然後選擇 **開始A/B測試**。

您的A/Btest現在正在運行，指定的受眾將根據指定的分佈隨機獲得體驗。

## 更新A/Btest {#update-a-b-test}

您可以更新運行的A/Btest的受眾和體驗分佈。 為此：

1. 在「Forms和文檔」UI中，導航到包含A/Btest正在運行的自適應表單的資料夾。
1. 選擇自適應窗體。
1. 按一下 **更多** ，然後選擇 **編輯A/B測試**。 將開啟「更新A/B」測試頁。

1. 根據需要更新受眾和體驗分發。
1. 按一下&#x200B;**更新**。

## 查看和分析A/Btest報表 {#view-and-analyze-a-b-test-report}

一旦您允許A/Btest在所需期間運行，您就可以生成報告並檢查哪些經驗導致了更好的轉換。 您可以宣佈獲獎者獲得效能更好的體驗，或選擇運行另一個A/Btest。 為此，請執行以下步驟：

1. 選擇自適應窗體，按一下 **更多**，然後按一下 **A/B測試報告**。 顯示報告。

[ ](assets/ab-test-report-3.png)

1. 分析報告並查看是否有足夠的資料點，以便將效能更好的體驗之一宣佈為贏家。 您可以選擇繼續使用同一A/Btest更長時間，或者聲明贏家並結束A/Btest。
1. 要聲明贏家並結束A/Btest，請按一下 **結束A/Btest** 按鈕。 對話框將提示您聲明兩種體驗中的一種是贏家。 選擇獲勝者並確認結束A/Btest。
或者，您可以通過按一下 **聲明贏家** 按鈕 提示您確認獲勝者。 按一下 **是** 結束A/Btest。

如果你選擇經驗A作為贏家，A/Btest將結束，而且向前，只有經驗A將提供給所有觀眾。
