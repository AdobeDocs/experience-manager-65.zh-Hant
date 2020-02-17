---
title: 使用AEM轉譯工作流程，將最適化表單和記錄檔案當地語系化
seo-title: 使用AEM轉譯工作流程，將最適化表單和記錄檔案當地語系化
description: 瞭解如何使用AEM轉譯工作流程，將最適化表單和記錄檔案當地語系化。
seo-description: 瞭解如何使用AEM轉譯工作流程，將最適化表單和記錄檔案當地語系化。
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
translation-type: tm+mt
source-git-commit: 5120bbdefea528ad6d07a9c99df565555b6a8444

---


# 使用AEM轉譯工作流程，將最適化表單和記錄檔案當地語系化 {#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}

本地化的表單可協助您為各地的廣大受眾提供服務。 Adobe Experience Manager翻譯工作流程可協助您將調適性表單及其記錄檔案當地語系化。 您可以使用 **機器翻譯** , **** 或人工翻譯器來本地化最適化表單。

本文說明將AEM翻譯工作流程與最適化表單和記錄檔案搭配使用的程式。

## 使用機器翻譯來定位自適應表單和記錄文檔 {#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化的形式和記錄檔案來翻譯您的內容。 AEM Forms已預先設定為使用Microsoft Translator試用版進行機器翻譯。 執行以下步驟，為自適應表單和記錄文檔啟用機器翻譯：

1. 在AEM Forms UI中，選取表單，然後點選「新增 **字典」選項** 。
1. 在「 **將字典添加到翻譯項目** 」螢幕中，選擇「創 **建新翻譯項目** 」或「 **添加到現有翻譯項目」選項** 。
1. 在「專 **案標題** 」欄位中，指定標題。 例如， `Government Reference Site - German locale.`
1. 在「目 **標語言** 」欄位中，指定地區設定(例如 `German(de)`)，然後按一下「 **完成」**。 您可以指定多個地區設定。 表單會轉譯為「目標語言」欄位中指定的所 **有地區** 。
1. 在「新增字典」對話方塊中，按一下「 **開啟專案**」。 在「專案」畫面中，開啟新建立的專案。
1. 按一下「 **Translation Summary** （翻譯摘要）」圖 **標底部的橢圓** 。 將開啟「翻譯摘要」螢幕。
1. 按一下「 **Translation Summary** 」（翻譯摘要）螢幕頂部的「Edit **」（編輯）表徵圖** 。 開啟「 **翻譯** 」頁籤，並在「翻譯方法」螢幕中選 **擇「機器翻譯** 」。 選擇適當的 **翻譯提供** 商 **和雲端設定**。 按一 **下畫面** 上方的「完成」圖示。
1. 在「轉 **譯工作** 」方塊上，按一 ![下aem62forms_downarrow](assets/aem62forms_downarrow.png) 圖示，然後按一下「 **開始**」。 表徵圖的狀態將更改為「草稿」。 翻譯完成後，狀態將更改為「 **Ready for review（準備審核）」**。 幾分鐘後重新整理頁面並驗證狀態。
1. 在「翻譯工作」圖 **格上** ，狀態變 **更為「準備審核」後** ，在瀏覽器視窗中開啟表格。 此時會顯示表單的本地化版本。

   >[!NOTE]
   >
   >* 在瀏覽器視窗中開啟本地化版本的表單之前，請確定瀏覽器的地區設定與表單的地區設定相符。 例如，如果表單翻譯為德文(de)語言，則將瀏覽器的區域設定設定為德文(de)。
   >* 最適化表單元件不支援從右到左(RTL)語言。 例如，希伯來文。


   自動產生的記錄檔案也會與「最適化」表單一起本地化。

   有關記錄文檔設定和配置的詳細資訊，請參閱：

   [記錄範本文件配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [記錄檔案設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自訂記錄檔案的品牌資訊](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) ，並確保瀏覽器地區設定為使用機器語言將最適化表單本地化的相同語言。 瀏覽器地區設定可協助將品牌資訊當地化在記錄檔案中。
1. 若要檢視本地化的記錄檔案，請點選「產生預覽」。 記錄PDF的檔案會在您瀏覽器的新標籤中產生並開啟。

## 使用人工翻譯定位自適應表單及其記錄文檔 {#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人文翻譯中，內容將發送給翻譯提供商，並由專業翻譯員翻譯。 完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會在AEM和翻譯提供者之間自動傳送。

對於翻譯，將與專業翻譯人員共用包含XLIFF格式檔案的字典。 字典包含每個地區設定的個別XLIFF檔案。 每個XLIFF檔案都包含將顯示給最終用戶的文本，以及對應本地化文本的佔位符。

使用Human Translators，執行以下步驟將表單及其記錄文檔本地化：

1. [將AEM與您的翻譯服務提供者連接](/help/sites-administering/tc-tic.md) ，並 [建立翻譯整合架構設定](/help/sites-administering/tc-tic.md)。

1. [將語言主版頁面與翻譯服務](/help/sites-administering/tc-tic.md) 和框架配置關聯。

1. [識別要翻譯的內容類型](/help/sites-administering/tc-rules.md) 。

1. [編寫語言主版](/help/sites-administering/tc-prep.md) ，並建立語言副本的根頁面，以準備翻譯內容。

1. [建立翻譯專案](/help/sites-administering/tc-manage.md) ，以收集要翻譯的內容並準備翻譯程式。

1. 使用翻譯專案來 [管理內容翻譯程式](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 最適化表單元件不支援從右到左(RTL)語言。 例如，希伯來文。
>



