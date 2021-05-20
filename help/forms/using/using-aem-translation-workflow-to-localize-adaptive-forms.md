---
title: 使用AEM翻譯工作流程將最適化表單和記錄檔案當地化
seo-title: 使用AEM翻譯工作流程將最適化表單和記錄檔案當地化
description: 了解如何使用AEM翻譯工作流程將最適化表單和記錄檔案當地化。
seo-description: 了解如何使用AEM翻譯工作流程將最適化表單和記錄檔案當地化。
uuid: 6c87a283-0203-4cf7-989a-3770ddbbbd6e
content-type: reference
topic-tags: develop
discoiquuid: f5642571-9657-4ca1-93c5-4ae2eb91e967
noindex: true
feature: 適用性表單
exl-id: ebec03a3-67a0-4ecd-84bb-8580388e048a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# 使用AEM翻譯工作流程將最適化表單和記錄檔案{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}當地化

本地化的表單可協助您跨地區為更多受眾服務。 Adobe Experience Manager翻譯工作流程可協助您將最適化表單及其記錄檔案當地化。 您可以使用&#x200B;**機器翻譯**&#x200B;或&#x200B;**人類翻譯員**&#x200B;將最適化表單本地化。

本文說明如何搭配最適化表單和記錄檔案使用AEM翻譯工作流程。

## 使用機器翻譯將最適化表單和記錄檔案定位{#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化格式和記錄檔案翻譯您的內容。 AEM Forms已預先設定為使用Microsoft Translator的試用版進行機器翻譯。 執行下列步驟以啟用最適化表單和記錄檔案的機器翻譯：

1. 在AEM Forms UI上，選取表單，然後點選&#x200B;**新增字典**&#x200B;選項。
1. 在&#x200B;**「將字典添加到翻譯項目」螢幕中，選擇「建立新翻譯項目」**&#x200B;或「添加到現有翻譯項目」**選項。******
1. 在&#x200B;**專案標題**&#x200B;欄位中，指定標題。 例如， `Government Reference Site - German locale.`
1. 在&#x200B;**目標語言**&#x200B;欄位中，指定地區（例如`German(de)`），然後按一下&#x200B;**Done**。 您可以指定多個地區設定。 表單將翻譯為&#x200B;**目標語言**&#x200B;欄位中指定的所有語言環境。
1. 在「新增字典」對話方塊中，按一下「**開啟專案**」。 在「專案」畫面中，開啟新建立的專案。
1. 按一下&#x200B;**翻譯摘要**&#x200B;方塊底部的&#x200B;**點**。 「翻譯摘要」畫面隨即開啟。
1. 按一下&#x200B;**翻譯摘要**&#x200B;螢幕頂部的&#x200B;**編輯**&#x200B;表徵圖。 開啟&#x200B;**Translation**&#x200B;頁簽，並在&#x200B;**Translation Method**&#x200B;螢幕中選擇Machine Translation。 選擇適當的&#x200B;**翻譯提供程式**&#x200B;和&#x200B;**雲配置**。 按一下螢幕頂端的&#x200B;**Done**&#x200B;圖示。
1. 在&#x200B;**翻譯工作**&#x200B;方塊中，按一下![aem62forms_downarrow](assets/aem62forms_downarrow.png)圖示，然後按一下&#x200B;**開始**。 圖磚的狀態會變更為「草稿」。 翻譯完成後，狀態會變更為「**準備審閱**」。 幾分鐘後重新整理頁面，並驗證狀態。
1. 狀態在&#x200B;**翻譯工作**&#x200B;方塊上變更為&#x200B;**準備檢閱**&#x200B;後，在瀏覽器視窗中開啟表單。 此時會顯示表單的本地化版本。

   >[!NOTE]
   >
   >* 在瀏覽器窗口中開啟本地化版本的表單之前，請確保已將瀏覽器的區域設定與表單的區域設定相匹配。 例如，如果表單翻譯為德文(de)語言，則將瀏覽器的地區設定為德文(de)。
   >* 適用性表單元件不支援從右到左(RTL)語言。 例如，希伯來語。


   與適用性表單一起，自動產生的記錄檔案也會翻譯。

   有關「記錄文檔」設定和配置的詳細資訊，請參閱：

[記錄範本文件配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

[記錄設定文檔](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定義記錄文檔的品牌資](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 訊，並確保瀏覽器區域設定設定為使用機器語言本地化適用性表單的相同語言。瀏覽器區域設定有助於將品牌資訊本地化到記錄文檔中。
1. 要查看記錄的本地化文檔，請點選「生成預覽」。 記錄PDF的檔案會在瀏覽器中的新索引標籤中產生和開啟。

## 使用人工翻譯將最適化表單及其記錄檔案定位{#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人翻譯中，內容被發送給翻譯提供者，並由專業翻譯員翻譯。 完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會自動在AEM和翻譯提供者之間傳送。

對於翻譯，與專業翻譯人員共用包含XLIFF格式檔案的字典。 字典包含每個區域設定的個別XLIFF檔案。 每個XLIFF檔案都包含將向最終用戶顯示的文本以及相應本地化文本的佔位符。

使用「人工翻譯員」執行以下步驟將表單及其記錄文檔本地化：

1. [將AEM與您的翻譯服務提供](/help/sites-administering/tc-tic.md) 商連 [接，並建立翻譯整合架構設定](/help/sites-administering/tc-tic.md)。

1. [將您語言首頁與翻](/help/sites-administering/tc-tic.md) 譯服務和框架配置相關聯。

1. [識別要翻譯的](/help/sites-administering/tc-rules.md) 內容類型。

1. [編寫語言主版](/help/sites-administering/tc-prep.md) 並建立語言副本的根頁面，以準備翻譯內容。

1. [建立翻](/help/sites-administering/tc-manage.md) 譯專案以收集要翻譯的內容並準備翻譯程式。

1. 使用翻譯專案至[管理內容翻譯程式](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 適用性表單元件不支援從右到左(RTL)語言。 例如，希伯來語。

>


