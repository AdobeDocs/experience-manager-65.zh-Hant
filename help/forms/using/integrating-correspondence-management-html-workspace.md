---
title: 將協力廠商應用程式整合在AEM Forms工作區
seo-title: 將協力廠商應用程式整合在AEM Forms工作區
description: 在AEM Forms工作區中整合協力廠商應用程式，例如「對應管理」。
seo-description: 如何在AEM Forms工作區中整合協力廠商應用程式，例如「對應管理」。
uuid: 7654cf86-b896-4db2-8f5d-6c1b2e6c229f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: f70f21e3-3bec-490d-889e-faf496fb738b
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 將協力廠商應用程式整合在AEM Forms工作區{#integrating-third-party-applications-in-aem-forms-workspace}

AEM Forms工作區支援管理表單和檔案的任務指派和完成活動。 這些表單和檔案可以是XDP表單、Flex®表單或已轉換為XDP、PDF、HTML或Flex格式的參考線（已過時）。

這些功能進一步增強。 AEM Forms現在支援與支援類似AEM Forms工作區功能的協作協作協力廠商應用程式。 此功能的常見部分是指派工作流程和後續核准工作。 AEM Forms為AEM Forms企業使用者提供單一的統一體驗，讓支援應用程式的所有此類工作指派或核准都可透過AEM Forms工作區處理。

例如，讓我們將「通信管理」視為與AEM Forms工作區整合的範例候選項。 「信件管理」的概念是「信件」，可轉譯並允許執行動作。

## 建立對應管理資產 {#create-correspondence-management-assets}

首先，建立在AEM Forms工作區中轉譯的範例「對應管理」範本。 如需詳細資訊，請參 [閱建立信函範本](../../forms/using/create-letter.md)。

在其URL中存取「對應管理」範本，以驗證「對應管理」範本是否可成功轉譯。 URL的模式類似於 `https://[server]:[port]/lc/content/cm/createcorrespondence.html?cmLetterId=encodedLetterId&cmUseTestData=1&cmPreview=0;`

其中 `encodedLetterId` 是URL編碼的字母Id。 在「工作台」中定義工作區任務的演算程式時，請指定相同的字母Id。

## 在AEM Workspace中建立要演算和送出信函的工作 {#create-a-task-to-render-and-submit-a-letter-in-aem-workspace}

在執行這些步驟之前，請確定您是下列群組的成員：

* cm-agent-users
* 工作區使用者

如需詳細資訊，請參 [閱新增和設定使用者](/help/forms/using/admin-help/adding-configuring-users.md)。

使用下列步驟建立要在AEM工作區中演算和送出信函的工作：

1. 啟動工作台。 以管理員身份登錄到localhost。
1. 按一下「檔案>新增>應用程式」。 在「應用程式名稱」欄位中，輸入， `CMDemoSample` 然後按一下「完成」。
1. 選 `CMDemoSample/1.0` 取並按一下滑鼠右鍵 `NewProcess`。 在名稱欄位中，輸入，然 `CMRenderer` 後按一下完成。
1. 拖曳「起始點」活動選擇器並加以設定：

   1. 在簡報資料中，選取「使用CRX資產」。

      ![useacrxasset](assets/useacrxasset.png)

   1. 瀏覽資產。 在「選擇表單資產」對話框中，「字母」頁籤列出伺服器上的所有字母。

      ![字母標籤](assets/letter_tab_new.png)

   1. 選擇適當的字母，然後按一下「 **確定」**。

1. 按一下「管理動作設定檔」。 此時將顯示「管理操作配置檔案」對話框。 請確定已適當選取「演算程式」和「提交程式」。
1. 若要使用資料XML檔案開啟字母，請瀏覽並選取「準備資料處理」中的適當資料檔案。
1. 按一下「確定」。
1. 定義「起始點輸出」和「任務附件」的變數。 定義的變數將包含「起始點輸出」和「任務附件」資料。
1. （可選）若要在工作流程中新增其他使用者，請拖曳活動選擇器、進行設定，並指派給使用者。 撰寫自訂包裝函式（範例如下），或下載並安裝DSC（如下所述），以擴充Letter範本、Start Point Output和Task Attachment。

   自訂包裝函式範例如下：

   ```java
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

   [獲取檔案](assets/dscsample.zip)下載DSC:上述DSCSample.zip檔案中提供範例DSC。 下載並解壓縮DSCSample.zip檔案。 在使用DSC服務之前，您需要對其進行配置。 有關資訊，請參 [閱配置DSC服務](../../forms/using/add-action-button-in-create-correspondence-ui.md#p-configure-the-dsc-service-p)。

   在「定義活動」對話方塊中，選取適當的活動，例如getLetterInstanceInfo，然後按一下「 **確定**」。

1. 部署應用程式。 如果出現提示登入並儲存資產。
1. 登入AEM表單工作區，網址為https://[server]:[port]/lc/content/ws。
1. 開啟您新增的工作，CMRender。 此時將出現「Correportence Management（通信管理）」信函。

   ![cminworkspace](assets/cminworkspace.png)

1. 填寫所需資料並提交信件。 窗口關閉。 在此過程中，任務將被分配給步驟9中工作流中指定的用戶。

   >[!NOTE]
   >
   >填入字母中的所有必要變數後，「提交」按鈕才會啟用。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
