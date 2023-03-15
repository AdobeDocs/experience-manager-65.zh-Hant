---
title: 使用AEM翻譯工作流程將最適化表單和記錄檔案當地化
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: 了解如何使用AEM翻譯工作流程將最適化表單和記錄檔案當地化。
seo-description: Learn to use AEM translation workflows to localize adaptive forms and document of record.
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: Adaptive Forms
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 15%

---

# 使用AEM翻譯工作流程將最適化表單和記錄檔案當地化 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可協助您跨地區為更多受眾服務。 Adobe Experience Manager翻譯工作流程可協助您將最適化表單及其記錄檔案當地化。 您可以使用 **機器翻譯** 或 **人類翻譯** 將最適化表單本地化。

本文說明如何搭配最適化表單和記錄檔案使用AEM翻譯工作流程。

## 使用機器翻譯將最適化表單和記錄檔案定位 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化格式和記錄檔案翻譯您的內容。 AEM Forms已預先設定為使用Microsoft Translator的試用版進行機器翻譯。 執行下列步驟以啟用最適化表單和記錄檔案的機器翻譯：

1. 在AEM Forms UI上，選取表單，然後點選 **新增字典** 選項。
1. 在 **在翻譯專案中新增字典** 螢幕上，選取 **建立新的翻譯專案** 或 **新增至現有的翻譯專案** 選項。
1. 在 **專案標題** 欄位，指定標題。 例如, `Government Reference Site - German locale.`
1. 在 **目標語言** 欄位，指定地區(例如 `German(de)`)，然後按一下 **完成**. 您可以指定多個地區設定。 表單會轉譯為 **目標語言** 欄位。
1. 在「新增字典」對話方塊中，按一下 **開啟專案**. 在「專案」畫面中，開啟新建立的專案。
1. 按一下 **橢圓** 在 **翻譯摘要** 方塊。 「翻譯摘要」畫面隨即開啟。
1. 按一下 **編輯** 圖示 **翻譯摘要** 螢幕。 開啟 **翻譯** 頁簽，然後在 **翻譯方法** 螢幕。 選取適當的 **翻譯提供者** 和 **雲端設定**. 按一下 **完成** 圖示。
1. 在 **翻譯工作** 並按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 按一下 **開始**. 圖磚的狀態會變更為「草稿」。 翻譯完成後，狀態會變更為 **準備審核**. 幾分鐘後重新整理頁面，並驗證狀態。
1. 狀態變更為 **準備審核** 在 **翻譯工作** 平鋪，在瀏覽器窗口中開啟表單。 此時會顯示表單的本地化版本。

   >[!NOTE]
   >
   >* 在瀏覽器窗口中開啟本地化版本的表單之前，請確保已將瀏覽器的區域設定與表單的區域設定相匹配。 例如，如果表單翻譯為德文(de)語言，則將瀏覽器的地區設定為德文(de)。
   >* 適用性表單元件不支援從右到左(RTL)語言。 例如，希伯來語。


   與適用性表單一起，自動產生的記錄檔案也會翻譯。

   有關「記錄文檔」設定和配置的詳細資訊，請參閱：

[記錄範本文件配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[記錄設定文檔](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定義記錄文檔的品牌資訊](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 並確認瀏覽器地區設定為您使用機器語言本地化適用性表單的相同語言。 瀏覽器區域設定有助於將品牌資訊本地化到記錄文檔中。
1. 要查看記錄的本地化文檔，請點選「生成預覽」。 記錄PDF的文檔將在瀏覽器中的新頁簽中生成和開啟。

## 使用人工翻譯將最適化表單及其記錄檔案翻譯為本地化 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人翻譯中，內容被發送給翻譯提供者，並由專業翻譯員翻譯。 完成後，翻譯後的內容將傳回並匯入到 AEM 中。如果您的翻譯提供商與 AEM 相整合，內容會在 AEM 和翻譯提供商之間自動傳送。

對於翻譯，與專業翻譯人員共用包含XLIFF格式檔案的字典。 字典包含每個區域設定的個別XLIFF檔案。 每個XLIFF檔案都包含將向最終用戶顯示的文本以及相應本地化文本的佔位符。

使用「人工翻譯員」執行以下步驟將表單及其記錄文檔本地化：

1. [將 AEM 與您的翻譯服務提供商連接](/help/sites-administering/tc-tic.md)並[建立翻譯整合框架設定](/help/sites-administering/tc-tic.md)。

1. [將您語言主版的頁面](/help/sites-administering/tc-tic.md) 與翻譯服務和框架設定相關聯。

1. [識別要翻譯的內容類型](/help/sites-administering/tc-rules.md)。

1. 編寫語言主版並建立語言副本的根頁面，[以備妥內容進行翻譯](/help/sites-administering/tc-prep.md)。

1. [建立翻譯專案](/help/sites-administering/tc-manage.md)以收集要翻譯的內容並準備翻譯流程。

1. 使用翻譯專案[管理內容翻譯流程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 適用性表單元件不支援從右到左(RTL)語言。 例如，希伯來語。
>

