---
title: 使用AEM翻譯工作流本地化記錄的自適應表單和文檔
seo-title: Using AEM translation workflow to localize adaptive forms and document of record
description: 學習使用翻AEM譯工作流來本地化自適應表單和記錄文檔。
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

# 使用AEM翻譯工作流本地化記錄的自適應表單和文檔 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可幫助您為不同地區的更多受眾提供服務。 Adobe Experience Manager翻譯工作流幫助您本地化自適應表單及其記錄文檔。 您可以使用 **機器翻譯** 或 **人類翻譯** 來定位自適應窗體。

本文介紹了翻譯工作流AEM與自適應表單和文檔記錄的使用過程。

## 使用機器翻譯來定位記錄的自適應形式和文檔 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務立即以自適應形式和記錄文檔來翻譯您的內容。 AEM Forms已預配置為使用Microsoft翻譯器的試用版進行機器翻譯。 執行以下步驟，為自適應表單和記錄文檔啟用機器翻譯：

1. 在AEM FormsUI上，選擇一個表單，然後點擊 **添加詞典** 的雙曲餘切值。
1. 在 **將詞典添加到翻譯項目** ，選擇 **新建翻譯項目** 或 **添加到現有翻譯項目** 的雙曲餘切值。
1. 在 **項目標題** 的子菜單。 例如 `Government Reference Site - German locale.`
1. 在 **目標語言** 欄位，指定區域設定(例如， `German(de)`)，然後按一下 **完成**。 可以指定多個區域設定。 表單將翻譯為在 **目標語言** 的子菜單。
1. 在「添加的字典」對話框中，按一下 **開啟項目**。 在「項目」螢幕中，開啟新建立的項目。
1. 按一下 **橢圓** 在 **翻譯摘要** 平鋪。 將開啟「翻譯摘要」螢幕。
1. 按一下 **編輯** 表徵圖 **翻譯摘要** 的上界。 開啟 **翻譯** ，然後在 **翻譯方法** 的上界。 選擇相應的 **翻譯提供程式** 和 **雲配置**。 按一下 **完成** 表徵圖。
1. 在 **翻譯作業** 平鋪，按一下 ![aem62forms_downarrow](assets/aem62forms_downarrow.png) 表徵圖，然後按一下 **開始**。 磁貼的狀態將更改為「草稿」。 完成翻譯後，狀態將更改為 **準備審閱**。 幾分鐘後刷新頁面並驗證狀態。
1. 狀態更改為 **準備審閱** 的 **翻譯作業** 平鋪，在瀏覽器窗口中開啟窗體。 將顯示表單的本地化版本。

   >[!NOTE]
   >
   >* 在瀏覽器窗口中開啟表單的本地化版本之前，請確保將瀏覽器的區域設定設定為與表單的區域設定匹配。 例如，如果表單被翻譯為德語(de)語言，則將瀏覽器的區域設定設定為德語(de)。
   >* 自適應表單元件不支援從右到左(RTL)語言。 例如，希伯來語。


   與「自適應」窗體一起，自動生成的記錄文檔也會進行本地化。

   有關「記錄文檔」設定和配置的詳細資訊，請參閱：

[記錄範本文件配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[記錄設定的文檔](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定義記錄文檔的品牌資訊](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 並確保瀏覽器區域設定設定為與使用機器語言本地化自適應表單的語言相同的語言。 瀏覽器區域設定有助於在記錄文檔中本地化品牌資訊。
1. 要查看記錄的本地化文檔，請點擊「生成預覽」。 記錄PDF的文檔在瀏覽器的新頁籤中生成並開啟。

## 使用人類翻譯來定位自適應表單及其記錄文檔 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人文翻譯中，內容將發送給翻譯提供商，並由專業翻譯員翻譯。 完成後，翻譯後的內容將傳回並匯入到 AEM 中。如果您的翻譯提供商與 AEM 相整合，內容會在 AEM 和翻譯提供商之間自動傳送。

對於翻譯，包含XLIFF格式的檔案的字典與專業翻譯員共用。 字典為每個區域設定包括一個單獨的XLIFF檔案。 每個XLIFF檔案都包含將顯示給最終用戶的文本和相應本地化文本的佔位符。

使用Human Translators對表單及其記錄文檔進行本地化，請執行以下步驟：

1. [將 AEM 與您的翻譯服務提供商連接](/help/sites-administering/tc-tic.md)並[建立翻譯整合框架設定](/help/sites-administering/tc-tic.md)。

1. [將您語言主版的頁面](/help/sites-administering/tc-tic.md) 與翻譯服務和框架設定相關聯。

1. [識別要翻譯的內容類型](/help/sites-administering/tc-rules.md)。

1. 編寫語言主版並建立語言副本的根頁面，[以備妥內容進行翻譯](/help/sites-administering/tc-prep.md)。

1. [建立翻譯專案](/help/sites-administering/tc-manage.md)以收集要翻譯的內容並準備翻譯流程。

1. 使用翻譯專案[管理內容翻譯流程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 自適應表單元件不支援從右到左(RTL)語言。 例如，希伯來語。
>

