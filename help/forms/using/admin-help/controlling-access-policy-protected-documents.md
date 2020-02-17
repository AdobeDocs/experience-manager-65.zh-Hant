---
title: 控制對受原則保護檔案的存取
seo-title: 控制對受原則保護檔案的存取
description: 瞭解您如何檢視、管理和控制對受原則保護檔案的存取。
seo-description: 瞭解您如何檢視、管理和控制對受原則保護檔案的存取。
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 控制對受原則保護檔案的存取 {#controlling-access-to-policy-protected-documents}

無論您散布檔案的範圍有多廣，您都可以控制收件者使用受原則保護檔案的方式。

使用「文檔」頁，您可以執行以下任務：

* 搜尋並檢視受原則保護檔案的詳細資訊。 您可以看到有關文檔名稱、發佈者名稱、策略名稱和策略應用日期的資訊。 如果刪除了保護文檔的策略，您也可以在策略名稱下看到已刪除的策略ID。 使用者可檢視並管理其受原則保護的檔案。 管理員可以檢視和管理所有受原則保護的檔案。
* 變更套用至檔案之原則的詳細資訊。 使用者可以編輯自己的原則、管理員可以編輯共用和個人原則，而原則集協調者則可以在擁有權限的原則集中編輯共用原則。 您可以直接從「文檔詳細資訊」頁訪問與文檔關聯的策略。
* 撤銷並重新建立受原則保護檔案的存取權。 管理員可以撤銷並重新建立任何檔案的存取權。 原則集協調者（具有管理檔案的權限）可以撤銷並重新建立對使用其原則集之共用原則之受原則保護檔案的存取權。 如果使用者建立了保護檔案的原則，或者原則是允許此功能的共用原則，就可以撤銷對受原則保護檔案的存取權。
* 切換套用至檔案的原則。 將原則套用至檔案的使用者可以在建立原則時或是啟用此功能的共用原則時，切換原則。 策略集協調者可以從其策略集切換策略。 管理員可切換套用至任何檔案的原則。

當檔案受原則保護，而您撤銷存取權限或切換套用的原則時，這些變更會生效如下：

* 如果檔案是線上的，則會立即套用變更，除非使用者已開啟檔案。 在這種情況下，用戶必須關閉文檔才能使更改生效。
* 如果收件者離線使用檔案（例如在膝上型電腦上），這些變更會在下次收件者透過開啟受原則保護的檔案與檔案安全性同步時生效。

## 檢視檔案的相關資訊 {#view-information-about-a-document}

對於「文檔」頁面上列出的每個文檔，您可以看到文檔名稱、發佈者名稱、策略名稱以及文檔受保護的日期。 如果保護文檔的策略已刪除，則策略ID將列在「策略名稱」下。

您也可以在「文檔詳細資訊」頁面上查看有關特定文檔的詳細資訊（如下所述）:

>[!NOTE]
>
>您必須使用「文檔詳細資訊」頁上的「策略名稱」連結，才能訪問在Microsoft outlook中為附加到電子郵件的文檔的收件人自動生成的策略。 這些策略不會顯示在策略頁上。

**** 檔案名稱：所選文檔的名稱。

**** 檔案ID:將原則套用至檔案時，檔案安全性會指派的唯一識別碼。 檔案安全性會使用此編號來追蹤檔案。

**** 檔案狀態：檔案的狀態（例如，活動或已撤銷）。

**** 發行者：將原則附加至檔案的使用者名稱。

**** 策略名稱：用於保護文檔的策略的名稱。 您可以按一下名稱以開啟原則。 您必須使用此連結來存取Acrobat為附加至Outlook電子郵件之檔案的收件者所產生的原則。 這些策略不會顯示在「策略」頁上。

**** 策略類型：套用至檔案的原則類型。

**** 發佈日期：將原則套用至檔案的日期。

**** 相關小版本：如果文檔具有相關小版本，則此項目也會出現在清單中。 按一下該連結可查看文檔的相關小版本清單。

使用者可檢視其受保護檔案的相關資訊。 管理員可檢視任何使用者使用原則所保護之檔案的相關資訊。 原則集協調者可從其原則集檢視受原則保護之檔案的相關資訊。

1. 在檔案安全性頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。 此時將開啟「文檔詳細資訊」頁，顯示有關文檔的詳細資訊。 本頁也提供廢止檔案存取權、切換原則以及檢視與本檔案相關事件的選項。

## 查看文檔的相關小版本 {#view-related-iterations-for-a-document}

如果啟用了跟蹤相關小版本，則可以跟蹤不同用戶保存的文檔版本。 此功能僅受某些應用程式（如PTC Pro/ENGINEER Wildfire）支援。

當多個使用者正在協作並儲存同一份檔案的不同版本時，此功能十分有用。 文檔安全可以跟蹤各種迭代；因此，您可以輕鬆檢視不同版本的檔案資訊。

如果啟用此功能，您可以從「文檔」(Documents)頁面查看文檔的相關小版本。

1. 查看文檔的「文檔詳細資訊」頁。 (請參 [閱檢視檔案的相關資訊](controlling-access-policy-protected-documents.md#view-information-about-a-document)。)
1. 按一下「查看相關小版本」(View Related Iterations)。 只有在啟用功能時，此選項才可用。 此時將顯示相關小版本的清單。 對於每個小版本，可以查看以下資訊：

   * **** 小版本：檔案名。 它可能與原始檔案名不同，並且其結尾附加了版本號。
   * **** 發行者：原始文檔的發佈者。
   * **** 建立者：保存小版本的用戶。
   * **** 建立日期：保存小版本的日期和時間。
   * **** 政策：保護小版本的策略。 不同的小版本可能受到不同原則的保護。

1. 要顯示該小版本的「文檔詳細資訊」(Document Detail)頁，請按一下小版本的檔案名。

## 廢止和恢復檔案存取權 {#revoking-and-reinstating-access-to-documents}

您可以撤銷並重新建立受原則保護檔案的存取權：

**** 使用者：可以撤銷或恢復對使用其個人原則或已針對套用原則之使用者啟用廢止功能之共用原則所保護檔案的存取權。 無法撤銷檔案存取權或切換原則的使用者，必須聯絡管理員。

**** 管理員：可以撤銷或重新建立任何受原則保護檔案的存取權限，包括受個人或共用原則保護的檔案。 如果管理員廢止使用共用原則保護之檔案的存取權，則只有管理員可以重新建立該檔案的存取權限。

**** 策略集協調者：可以撤消或恢復策略所保護的文檔的訪問權限。

當您撤銷或重新建立檔案存取權限時，變更會在下列時間生效：

* 如果檔案是線上並關閉的，則此變更會在收件人下次透過開啟受原則保護的檔案進行檔案保全同步時生效。
* 如果文檔處於聯機狀態並開啟，則當收件者關閉文檔時，更改將生效。
* 如果檔案離線（在使用中沒有網際網路連線，例如在膝上型電腦上），則變更會在收件人下次同步檔案保全時生效。

**廢止受原則保護檔案的存取權**

1. 在檔案安全性頁面上，按一下「檔案」。
1. 選擇適當文檔旁的複選框，然後按一下「撤銷」。 您可以一次撤銷對多份檔案的存取權。
1. 選擇要向嘗試在文檔被撤消後開啟該文檔的用戶顯示的消息：

   * **** 一般訊息：表示作者已撤銷檔案
   * **** 檔案終止：表示作者終止了文檔
   * **修訂檔案**:指出作者修訂了檔案

1. （可選）如果文檔有較新版本，請輸入URL並按一下測試以驗證URL。
1. 按一下「確定」，然後再次按一下「確定」返回「文檔」頁。

**恢復檔案存取權限**

1. 在檔案安全性頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。
1. 按一下「取消撤銷」，然後按一下「確定」。

## 切換套用至檔案的原則 {#switch-a-policy-that-is-applied-to-a-document}

使用者、原則集協調者和管理員可切換套用至受原則保護檔案的原則（一次只能套用一個原則至檔案）。 如果用戶建立了策略，或者策略是啟用了此功能的共用策略，則用戶可以切換應用到其自身受策略保護文檔的策略。 否則，管理員或策略集協調員必須切換策略。 管理員可針對任何使用者受原則保護的檔案切換原則。 策略集協調者可以從其策略集切換策略。

切換策略時，新策略的強制方式如下：

* 如果檔案是線上且已關閉，則此變更會在收件人下次透過線上開啟受原則保護的檔案進行檔案保全同步時生效。
* 如果文檔聯機並開啟，則更改在用戶關閉文檔時生效。
* 如果檔案離線（使用中未使用作用中的網際網路或網路連線，例如在膝上型電腦上），則在使用者下次透過線上開啟受原則保護的檔案以同步檔案保全時套用變更。

>[!NOTE]
>
>若要允許匿名存取目前沒有此存取權的受原則保護檔案，請移除用戶端應用程式中的現有原則，然後套用允許匿名存取的原則。 如果您切換原則，使用者仍必須登入才能存取檔案。

1. 在檔案安全性頁面上，按一下「檔案」。
1. 在檔案清單中，按一下適當的檔案。
1. 按一下「Switch Policy（切換策略）」。 最多會出現100個策略的清單。
1. 如果未顯示所需的策略，請從「查找」清單中選擇「策略名稱」或「策略ID」，鍵入名稱或ID，然後按一下「查找」。
1. 按一下清單中的新策略。
1. 按一下「切換策略」，然後按一下「確定」返回「文檔」頁。

## 搜尋檔案 {#search-for-a-document}

您可以使用清單中提供的日期範圍標準和搜索標準的組合，在「文檔」(Documents)頁面上搜索文檔。 這些條件包括檔案名稱、原則名稱或所有檔案。

有些額外的搜尋選項僅供管理員使用：

**** 檔案ID:套用原則時，檔案安全性會指派給檔案的唯一ID編號。

**** 檔案名稱：文檔的名稱。

**** 發行者名稱：將原則附加至檔案的使用者名稱。 您可以從所有網域或指定網域中選取使用者。

**** 原則ID:附加到文檔的策略的ID號。

**** 策略名稱：附加到文檔的策略的名稱。

**** 所有檔案：所有受管理員和使用者保護的檔案。 使用「所有文檔」選項進行搜索可能會返回文檔的長清單。

1. 在檔案安全性頁面上，按一下「檔案」。
1. 在「查找」(Find)清單中，選擇所需的搜索標準。

   您可以指定標準為檔案ID、檔案名稱、發佈者名稱、原則ID、原則名稱或所有檔案。

   如果您指定發行者名稱，請按一下「通訊錄」圖示並指定您要搜尋使用者的網域，然後按一下「確定」以返回「檔案」搜尋頁面。

1. （可選）在「日期」清單中，選取日期範圍選項。 如果您選取「自訂日期」，請在出現的方塊中輸入yyyy/mm/dd格式的日期，或使用「日期選擇器」來指定日期範圍：

   * 按一下日曆以開啟「日期選擇器」。
   * 使用箭頭尋找年份和月份。
   * 按一下日曆上當月的某天。
   * 按一下「確定」以關閉「日期選擇器」。

1. 按一下「尋找」。

## 排序文檔清單 {#sort-the-document-list}

您可以依欄標題來排序檔案清單。 欄標題旁的三角形圖示指出目前用來排序的欄。 向上三角形表示升序，向下三角形表示降序。

1. 在檔案安全性頁面上，按一下「檔案」。
1. 按一下適當的欄標題。
1. 要更改排序順序，請再次按一下列。

## 將封面頁面新增至受原則保護的檔案 {#add-cover-page-to-policy-protected-documents}

在大部分非Adobe PDF檢視器中，如果您開啟受檔案保全保護的檔案，第一頁會顯示為空白頁面，或應用程式會中止，而不會開啟檔案。

您可以使用「頁面0（包裝函式檔案）」支援，讓非Adobe PDF檢視器開啟受保護的檔案，並在檔案中顯示封面頁。

>[!NOTE]
>
>在Adobe Reader/Acrobat或Mobile Reader中檢視此類檔案（包含頁面0）時，預設會開啟受保護的檔案。

**若要將封面頁面新增至受原則保護的檔案**

在工作台中使用以下流程：

**** 使用封面頁面保護檔案：使用指定的原則保護PDF檔案，並新增封面至檔案

**** 擷取受保護的檔案：從含封面的PDF檔案擷取受原則保護的PDF檔案

使用下列檔案安全性API:

****`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` protectDocumentWithCoverPage:使用指定的原則保護指定的PDF，並傳回包含封面頁面的檔案，以及將受保護的檔案當成附件&#x200B;**** extractProtectedDocument:提取受保護的文檔，該文檔是帶有封面的文檔中的附件。 使用protectDocumentWithCoverPage方法可建立包含封面的檔案`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`