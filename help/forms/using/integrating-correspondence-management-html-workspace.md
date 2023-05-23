---
title: 在AEM Forms工作區中整合第三方應用程式
seo-title: Integrating third-party applications in AEM Forms workspace
description: 整合第三方應用程式，如AEM Forms工作區中的Tergement Management。
seo-description: How-to integrate third-party apps like Correspondence Management in AEM Forms workspace.
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
exl-id: 39a3f7db-549f-47f3-8d4f-42d583a4532d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# 在AEM Forms工作區中整合第三方應用程式{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms工作區支援對表單和文檔的任務分配和完成活動的管理。 這些表單和文檔可以是XDPForms、Flex®表單或參考線（已棄用），它們已以XDP、PDF、HTML或Flex格式呈現。

這些能力得到進一步增強。 AEM Forms現在支援與支援類似於AEM Forms工作區的功能的第三方應用程式協作。 此功能的一個常見部分是任務分配和後續審批的工作流。 AEM Forms為AEM Forms企業用戶提供單一的統一體驗，以便通過AEM Forms工作區處理支援應用程式的所有此類任務分配或批准。

例如，讓我們將Tergement Management視為與AEM Forms工作區整合的示例候選項。 Tergement Management的概念是「Letter」，它可以呈現並允許執行操作。

## 建立信件管理資產 {#create-correspondence-management-assets}

首先建立在AEM Forms工作區中呈現的示例Tergement Management模板。 有關詳細資訊，請參閱 [建立字母模板](../../forms/using/create-letter.md)。

訪問其URL上的「通信管理」模板，以驗證是否可以成功呈現「通信管理」模板。 URL的模式與 `https://'[server]:[port]'/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

何處 `encodedLetterId` 是URL編碼的字母Id。 在Workbench中為工作區任務定義呈現流程時，請指定相同的字母ID。

## 建立任務以在工作區中呈現和提交信AEM件 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

在執行這些步驟之前，請確保您是以下組的成員：

* cm代理用戶
* 工作區用戶

有關詳細資訊，請參見 [添加和配置用戶](/help/forms/using/admin-help/adding-configuring-users.md)。

使用以下步驟建立要在工作區中呈現和提交信函的任AEM務：

1. 啟動工作台。 以管理員身份登錄到localhost。
1. 按一下「檔案」>「新建」>「應用程式」。 在「應用程式名稱」欄位中，輸入 `CMDemoSample` 然後按一下「Finish（完成）」。
1. 選擇 `CMDemoSample/1.0` 並按一下右鍵 `NewProcess`。 在名稱欄位中，輸入 `CMRenderer` 然後按一下「Finish（完成）」。
1. 拖動「起點」活動選取器並配置它：

   1. 在演示資料中，選擇使用CRX資產。

      ![useacraxasset](assets/useacrxasset.png)

   1. 瀏覽資產。 在「選擇表單資產」對話框中，「字母」頁籤列出伺服器上的所有字母。

      ![字母頁籤](assets/letter_tab_new.png)

   1. 選擇相應的字母並按一下 **確定**。

1. 按一下管理操作配置檔案。 此時將顯示「管理操作配置檔案」對話框。 確保「渲染流程」和「提交流程」已適當選擇。
1. 要使用資料XML檔案開啟字母，請在準備資料處理中瀏覽並選擇相應的資料檔案。
1. 按一下「確定」。
1. 定義「起始點輸出」和「任務附件」的變數。 定義的變數將包含「起始點輸出」和「任務附件」資料。
1. （可選）要在工作流中添加其他用戶，請拖動活動選取器，對其進行配置，然後將其分配給用戶。 編寫自定義包裝器（下面給出示例），或下載並安裝DSC（下面給出）以擴展字母模板、起始點輸出和任務附件。

   下面列出了一個示例自定義包裝：

   ```javascript
   public LetterInstanceInfo getLetterInstanceInfo(Document dataXML) throws Exception {
   try {
   if(dataXML == null)
   throw new Exception("dataXML is missing");
   
   CoreService coreService = getRemoteCoreService();
   if (coreService == null)
   throw new Exception("Unable to retrive service. Please verify connection details.");
   Map<String, Object> result = coreService.getLetterInstanceInfo(IOUtils.toString(dataXML.getInputStream(), "UTF-8"));
   LetterInstanceInfo letterInstanceInfo = new LetterInstanceInfo();
   
   List<Document> attachmentDocs = new ArrayList<Document>();
   List<byte[]> attachments = (List<byte[]>)result.get(CoreService.ATTACHMENT_KEY);
   if (attachments != null){
   for (byte[] attachment : attachments)
   { attachmentDocs.add(new Document(attachment)); }
   
   }
   letterInstanceInfo.setLetterAttachments(attachmentDocs);
   
   byte[] updateLayout = (byte[])result.get(CoreService.LAYOUT_TEMPLATE_KEY);
   if (updateLayout != null)
   { letterInstanceInfo.setLetterTemplate(new Document(updateLayout)); }
   
   else
   { throw new Exception("template bytes missing while getting Letter instance Info."); }
   
   return letterInstanceInfo;
   } catch (Exception e)
   { throw new Exception(e); }
   
   }
   ```

   [獲取檔案](assets/dscsample.zip)
下載DSC:DSC示例DSC可在上面附加的DSCSample.zip檔案中找到。 下載並解壓縮DSCSample.zip檔案。 在使用DSC服務之前，需要配置它。 有關資訊，請參見 [配置DSC服務](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)。

   在「定義活動」對話框中，選擇相應的活動，如getLetterInstanceInfo，然後按一下 **確定**。

1. 部署應用程式。 如果系統提示，請簽入並保存資產。
1. 登錄到表AEM單工作區，網址為https://&#39;[伺服器]:[埠]「/lc/content/ws」。
1. 開啟您添加的任務，CMRender。 此時將顯示「Tergement Management（通信管理）」信函。

   ![CMINWORKSPACE](assets/cminworkspace.png)

1. 填寫所需資料並提交信函。 窗口關閉。 在此過程中，任務將分配給步驟9中工作流中指定的用戶。

   >[!NOTE]
   >
   >在填寫字母中的所有必需變數之前，不會啟用「提交」按鈕。
