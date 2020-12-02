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
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---


# 使用AEM轉譯工作流程，將最適化表單和記錄檔案{#using-aem-translation-workflow-to-localize-adaptive-forms-and-document-of-record}當地語系化

本地化的表單可協助您為各地的廣大受眾提供服務。 Adobe Experience Manager翻譯工作流程可協助您將調適性表單及其記錄檔案當地語系化。 可以使用&#x200B;**機器翻譯**&#x200B;或&#x200B;**人類翻譯員**&#x200B;來本地化自適應表單。

本文說明將AEM翻譯工作流程與最適化表單和記錄檔案搭配使用的程式。

## 使用機器翻譯來定位自適應表單和記錄文檔{#localizing-an-adaptive-form-and-document-of-record-using-machine-translation}

機器翻譯服務會立即以最適化的形式和記錄檔案來翻譯您的內容。 AEM Forms已預先設定為使用Microsoft Translator試用版進行機器翻譯。 執行以下步驟，為自適應表單和記錄文檔啟用機器翻譯：

1. 在AEM Forms UI中，選取表單，然後點選「**新增字典**」選項。
1. 在&#x200B;**將字典添加到翻譯項目**&#x200B;螢幕中，選擇&#x200B;**建立新翻譯項目**&#x200B;或&#x200B;**添加到現有翻譯項目**&#x200B;選項。
1. 在&#x200B;**專案標題**&#x200B;欄位中，指定標題。 例如， `Government Reference Site - German locale.`
1. 在&#x200B;**目標語言**&#x200B;欄位中，指定地區（例如`German(de)`），然後按一下&#x200B;**Done**。 您可以指定多個地區設定。 表單會轉譯為&#x200B;**Target Languages**&#x200B;欄位中指定的所有地區設定。
1. 在「新增字典」對話方塊中，按一下「開啟專案」**。**&#x200B;在「專案」畫面中，開啟新建立的專案。
1. 按一下&#x200B;**翻譯摘要**&#x200B;表徵圖底部的&#x200B;**橢圓**。 將開啟「翻譯摘要」螢幕。
1. 按一下&#x200B;**翻譯摘要**&#x200B;螢幕頂部的&#x200B;**編輯**&#x200B;表徵圖。 開啟&#x200B;**Translation**&#x200B;頁籤，並在&#x200B;**Translation Method**&#x200B;螢幕中選擇Machine Translation。 選擇適當的&#x200B;**翻譯提供者**&#x200B;和&#x200B;**雲配置**。 按一下螢幕頂部的&#x200B;**Done**&#x200B;表徵圖。
1. 在&#x200B;**翻譯工作**&#x200B;表徵圖上，按一下![ aem62forms_downarrow](assets/aem62forms_downarrow.png)表徵圖，然後按一下&#x200B;**開始**。 表徵圖的狀態將更改為「草稿」。 翻譯完成後，狀態將更改為&#x200B;**Ready for review**。 幾分鐘後重新整理頁面並驗證狀態。
1. 在&#x200B;**翻譯工作**&#x200B;表徵圖上的狀態更改為&#x200B;**準備審核**&#x200B;後，在瀏覽器窗口中開啟表單。 此時會顯示表單的本地化版本。

   >[!NOTE]
   >
   >* 在瀏覽器視窗中開啟本地化版本的表單之前，請確定瀏覽器的地區設定與表單的地區設定相符。 例如，如果表單翻譯為德文(de)語言，則將瀏覽器的區域設定設定為德文(de)。
   >* 最適化表單元件不支援從右到左(RTL)語言。 例如，希伯來文。


   自動產生的記錄檔案也會與「最適化」表單一起本地化。

   有關記錄文檔設定和配置的詳細資訊，請參閱：

   [記錄範本文件配置](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-template-configuration-p)

   [記錄檔案設定](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#p-document-of-record-settings-p)

1. [自定義記錄文檔的品牌信](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) 息，並確保瀏覽器區域設定為使用機器語言本地化Adaptive Form的相同語言。瀏覽器地區設定可協助將品牌資訊當地化在記錄檔案中。
1. 若要檢視本地化的記錄檔案，請點選「產生預覽」。 記錄PDF的檔案會在您瀏覽器的新標籤中產生並開啟。

## 使用人工翻譯(Human Translation)定位最適化表單及其記錄文檔{#localizing-an-adaptive-form-and-its-document-of-record-using-human-translation}

在人文翻譯中，內容將發送給翻譯提供商，並由專業翻譯員翻譯。 完成時，會傳回翻譯的內容並匯入AEM。 當您的翻譯提供者與AEM整合時，內容會在AEM和翻譯提供者之間自動傳送。

對於翻譯，將與專業翻譯人員共用包含XLIFF格式檔案的字典。 字典包含每個地區設定的個別XLIFF檔案。 每個XLIFF檔案都包含將顯示給最終用戶的文本，以及對應本地化文本的佔位符。

使用Human Translators，執行以下步驟將表單及其記錄文檔本地化：

1. [將AEM與您的翻譯服務提供者](/help/sites-administering/tc-tic.md) 連接， [並建立翻譯整合架構設定](/help/sites-administering/tc-tic.md)。

1. [將您語言的首頁與翻](/help/sites-administering/tc-tic.md) 譯服務和框架配置相關聯。

1. [識別要翻譯的](/help/sites-administering/tc-rules.md) 內容類型。

1. [編寫語言主版](/help/sites-administering/tc-prep.md) 並建立語言副本的根頁面，以準備翻譯內容。

1. [建立轉](/help/sites-administering/tc-manage.md) 譯專案以收集要翻譯的內容並準備轉譯程式。

1. 使用翻譯項目到[管理內容翻譯流程](/help/sites-administering/tc-manage.md)。

>[!NOTE]
>
>* 最適化表單元件不支援從右到左(RTL)語言。 例如，希伯來文。

>



