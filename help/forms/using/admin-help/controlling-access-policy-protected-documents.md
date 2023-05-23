---
title: 控制對策略保護文檔的訪問
seo-title: Controlling access to policy-protected documents
description: 瞭解您如何查看、管理和控制對受策略保護文檔的訪問。
seo-description: See how you can view, manage and control the access to your policy-protected documents.
uuid: 2d9f95e9-e4ee-47e2-988e-a191d1d1d264
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f34058c3-384a-4b73-a386-5bc9125acbf8
feature: Document Security
exl-id: 0eb6e769-97c1-41ee-8d12-91bece984947
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2169'
ht-degree: 0%

---

# 控制對策略保護文檔的訪問 {#controlling-access-to-policy-protected-documents}

無論您將受策略保護的文檔分發到多廣泛，您都可以控制收件人使用這些文檔的方式。

使用「文檔」頁，您可以執行以下任務：

* 搜索並查看受策略保護文檔的詳細資訊。 您可以查看有關文檔名稱、發佈者名稱、策略名稱和策略應用日期的資訊。 如果刪除了保護文檔的策略，您還可以在策略名稱下看到已刪除的策略ID。 用戶可以查看和管理自己的策略保護文檔。 管理員可以查看和管理所有受策略保護的文檔。
* 更改應用於文檔的策略的詳細資訊。 用戶可以編輯自己的策略，管理員可以編輯共用策略和個人策略，策略集協調員可以編輯他們具有權限的策略集中的共用策略。 您可以直接從「文檔詳細資訊」頁面訪問與文檔關聯的策略。
* 撤消和恢復對受策略保護文檔的訪問。 管理員可以撤消和恢復對任何文檔的訪問權限。 策略集協調員（具有管理文檔的權限）可以撤消和恢復對使用其策略集中共用策略的策略保護文檔的訪問權限。 如果用戶建立了保護文檔的策略，或者該策略是允許此功能的共用策略，則用戶可以撤消對其受策略保護文檔的訪問權限。
* 切換應用於文檔的策略。 如果將策略應用於文檔的用戶建立了策略，或者是啟用此功能的共用策略，則可以切換策略。 策略集協調員可以從其策略集切換策略。 管理員可以切換應用於任何文檔的策略。

當文檔受策略保護並且您撤消訪問權限或切換應用的策略時，更改將生效如下：

* 如果文檔處於聯機狀態，則除非用戶開啟了文檔，否則將立即應用更改。 在這種情況下，用戶必須關閉文檔，更改才能生效。
* 如果收件人離線使用文檔（例如，在膝上型電腦上），則更改將在收件人下次通過開啟任何受策略保護的文檔與文檔安全性同步時生效。

## 查看有關文檔的資訊 {#view-information-about-a-document}

對於「文檔」頁面上列出的每個文檔，您都可以看到文檔名稱、發佈者名稱、策略名稱以及文檔受保護的日期。 如果已刪除保護文檔的策略，則策略ID將列在「策略名稱」下。

您還可以在「文檔詳細資訊」頁面上查看有關特定文檔的詳細資訊（如下所述）:

>[!NOTE]
>
>您必須使用「文檔詳細資訊」頁面上的「策略名稱」連結來訪問在MicrosoftOutlook中為附加到電子郵件的文檔的收件人自動生成的策略。 這些策略不出現在策略頁上。

**文檔名稱：** 所選文檔的名稱。

**文檔ID:** 當將策略應用到文檔時，文檔安全性所分配的唯一標識符。 文檔安全性使用此編號來跟蹤文檔。

**文檔狀態：** 文檔的狀態（例如，活動或撤消）。

**發佈者：** 將策略附加到文檔的用戶的名稱。

**策略名稱：** 用於保護文檔的策略的名稱。 可以按一下該名稱以開啟策略。 您必須使用此連結訪問Acrobat為附加到Outlook中電子郵件的文檔的收件人生成的策略。 這些策略不顯示在「策略」頁上。

**策略類型：** 應用於文檔的策略類型。

**發佈日期：** 將策略應用於文檔的日期。

**相關小版本：** 如果文檔具有相關小版本，則此項目也會顯示在清單中。 按一下連結可查看文檔的相關小版本清單。

用戶可以查看有關其受保護文檔的資訊。 管理員可以查看有關任何用戶使用策略保護的文檔的資訊。 策略集協調員可以從策略集查看受策略保護的文檔資訊。

1. 在文檔安全頁面上，按一下「文檔」。
1. 在文檔清單中，按一下相應的文檔。 將開啟「文檔詳細資訊」頁面，其中顯示有關文檔的詳細資訊。 此頁還提供用於撤消文檔訪問、切換策略和查看與此文檔相關的事件的選項。

## 查看文檔的相關小版本 {#view-related-iterations-for-a-document}

如果啟用了跟蹤相關小版本，則可以跟蹤不同用戶保存的文檔版本。 此功能僅受某些應用程式（如PTC Pro/ENGINEER Wildfire）支援。

當多個用戶正在協作並正在保存同一文檔的不同版本時，此功能非常有用。 文檔安全可以跟蹤各種迭代；因此，您可以輕鬆查看不同版本的文檔資訊。

如果啟用了此功能，則可以從「文檔」頁面查看文檔的相關小版本。

1. 查看文檔的「文檔詳細資訊」頁面。 (請參閱 [查看有關文檔的資訊](controlling-access-policy-protected-documents.md#view-information-about-a-document)。)
1. 按一下「查看相關小版本」(View Related Iterations)。 此選項僅在啟用該功能時才可用。 出現相關小版本的清單。 對於每個小版本，可以查看以下資訊：

   * **迭代：** 檔案名。 它可能與原始檔案名不同，並且其結尾附有版本號。
   * **發佈者：** 原始文檔的發佈者。
   * **建立者：** 保存小版本的用戶。
   * **建立日期：** 保存小版本的日期和時間。
   * **策略：** 保護迭代的策略。 不同的迭代可能受不同策略的保護。

1. 要顯示該小版本的「文檔詳細資訊」(Document Detail)頁面，請按一下小版本的檔案名。

## 撤消和恢復對文檔的訪問 {#revoking-and-reinstating-access-to-documents}

您可以撤消和恢復對受策略保護文檔的訪問權限：

**用戶：** 可以撤消或恢復對文檔的訪問權，這些文檔使用其自己的個人策略或已為應用策略的用戶啟用了撤消功能的共用策略進行保護。 無法撤消對文檔的訪問或切換策略的用戶需要與管理員聯繫。

**管理員：** 可以撤消或恢復對任何受策略保護的文檔（包括受個人或共用策略保護的文檔）的訪問權限。 如果管理員撤消了對受共用策略保護的文檔的訪問權限，則只有管理員才能恢復該文檔的訪問權限。

**策略集協調員：** 可以撤消或恢復策略從其策略集保護的文檔的訪問權限。

撤消或恢復文檔訪問權限時，更改將在以下時間生效：

* 如果文檔處於聯機狀態並已關閉，則更改將在下次收件人通過開啟受策略保護的文檔與文檔安全性同步時生效。
* 如果文檔聯機並開啟，則當收件人關閉文檔時更改生效。
* 如果文檔處於離線狀態（在使用中沒有Internet連接，如在筆記型電腦上），則更改將在收件人下次與文檔安全性同步時生效。

**撤消對受策略保護文檔的訪問**

1. 在文檔安全頁面上，按一下「文檔」。
1. 選中相應文檔旁邊的複選框，然後按一下「撤消」。 您可以一次撤消對多個文檔的訪問權限。
1. 選擇要顯示給在撤消文檔後嘗試開啟文檔的用戶的消息：

   * **常規消息：** 指示作者吊銷了文檔
   * **文檔已終止：** 指示作者終止了文檔
   * **已修訂文檔**:指示作者修改了文檔

1. （可選）如果文檔的較新版本可用，請輸入URL並按一下Test以驗證URL。
1. 按一下「確定」，然後再次按一下「確定」以返回「文檔」頁面。

**恢復文檔訪問權限**

1. 在文檔安全頁面上，按一下「文檔」。
1. 在文檔清單中，按一下相應的文檔。
1. 按一下取消撤消，然後按一下確定。

## 切換應用於文檔的策略 {#switch-a-policy-that-is-applied-to-a-document}

用戶、策略集協調員和管理員可以切換應用於受策略保護的文檔的策略（一次只能對文檔應用一個策略）。 如果用戶建立了策略或策略是啟用了此功能的共用策略，則用戶可以切換應用於其自己受策略保護的文檔的策略。 否則，管理員或策略集協調員必須切換策略。 管理員可以切換任何用戶受策略保護的文檔的策略。 策略集協調員可以從其策略集切換策略。

切換策略時，新策略將按如下方式強制執行：

* 如果文檔處於聯機狀態並已關閉，則此更改將在下次收件人通過聯機開啟任何受策略保護的文檔與文檔安全性同步時生效。
* 如果文檔處於聯機狀態並處於開啟狀態，則更改將在用戶關閉文檔時生效。
* 如果文檔處於離線狀態（使用中沒有活動的Internet或網路連接，例如在膝上型電腦上），則在用戶下次通過聯機開啟受策略保護的文檔與文檔安全性同步時應用更改。

>[!NOTE]
>
>要允許匿名訪問當前沒有此訪問權限的受策略保護的文檔，請刪除客戶端應用程式中的現有策略，然後應用允許匿名訪問的策略。 如果切換策略，用戶仍必須登錄才能訪問文檔。

1. 在文檔安全頁面上，按一下「文檔」。
1. 在文檔清單中，按一下相應的文檔。
1. 按一下「Switch Policy（切換策略）」。 此時將顯示多達100個策略的清單。
1. 如果未顯示所需的策略，請從「查找」清單中選擇「策略名稱」或「策略ID」，鍵入名稱或ID，然後按一下「查找」。
1. 按一下清單中的新策略。
1. 按一下「切換策略」，然後按一下「確定」返回「文檔」頁。

## 搜索文檔 {#search-for-a-document}

您可以使用日期範圍標準和清單中可用的搜索標準的組合，在「文檔」(Documents)頁面上搜索文檔。 這些條件包括文檔名稱、策略名稱或所有文檔。

某些其他搜索選項僅供管理員使用：

**文檔ID:** 應用策略時文檔安全性為文檔分配的唯一ID號。

**文檔名稱：** 文檔的名稱。

**發佈者名稱：** 將策略附加到文檔的用戶的名稱。 可以從所有域或指定域中選擇用戶。

**策略ID:** 附加到文檔的策略的ID號。

**策略名稱：** 附加到文檔的策略的名稱。

**所有文檔：** 所有受管理員和用戶保護的文檔。 使用「所有文檔」選項進行搜索可能會返回一個長長的文檔清單。

1. 在文檔安全頁面上，按一下「文檔」。
1. 在「查找」(Find)清單中，選擇所需的搜索條件。

   您可以將條件指定為文檔ID、文檔名稱、發佈者名稱、策略ID、策略名稱或所有文檔。

   如果指定發佈者名稱，請按一下「通訊簿」表徵圖並指定要搜索用戶的域，然後按一下「確定」返回「文檔」搜索頁。

1. （可選）在「日期」清單中，選擇日期範圍選項。 如果選擇「自定義日期」，請在出現的框中鍵入格式為yyyy/mm/dd的日期，或使用日期選取器指定日期範圍：

   * 按一下日曆以開啟日期選取器。
   * 使用箭頭查找年和月。
   * 在日曆上按一下月份的某一天。
   * 按一下「確定」關閉日期選取器。

1. 按一下「查找」。

## 對文檔清單排序 {#sort-the-document-list}

您可以按列標題對文檔清單進行排序。 列標題旁邊的三角形表徵圖指示當前用於排序的列。 向上指向三角形表示升序，而向下指向三角形表示降序。

1. 在文檔安全頁面上，按一下「文檔」。
1. 按一下相應的列標題。
1. 要更改排序順序，請再次按一下列。

## 將封面添加到受策略保護的文檔 {#add-cover-page-to-policy-protected-documents}

對於大多數非Adobe PDF查看器，如果開啟文檔安全保護文檔，則第一頁將顯示為空白頁，或應用程式在不開啟文檔的情況下中止。

您可以使用頁0（包裝文檔）支援來允許非Adobe PDF查看者開啟受保護的文檔並在文檔中顯示封面。

>[!NOTE]
>
>在Adobe Reader/Acrobat或移動Reader中查看此類文檔（包含頁0）時，預設情況下會開啟受保護的文檔。

**將封面添加到受策略保護的文檔**

在工作台中使用以下流程：

**Protect封面文檔：** 使用指定策略保護PDF文檔，並向文檔添加封面

**提取受保護的文檔：** 從帶有封面的PDF文檔中提取受策略保護的PDF文檔

使用以下文檔安全API:

**protectDocumentWithCoverPage:** 使用指定策略保護給定PDF，並返回帶封面的文檔和受保護文檔作為附件
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a PDF document to which a policy is applied FileInputStream fileInputStream = new FileInputStream("C:\\testFile.pdf"); Document inPDF = new Document(fileInputStream); //Reference a Cover Page document FileInputStream coverPageInputStream = new FileInputStream("C:\\CoverPage.pdf"); Document inCoverDoc = new Document(coverPageInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document RMSecureDocumentResult rmSecureDocument = documentManager.protectDocumentWithCoverPage( inPDF, "ProtectedPDF.pdf", "PolicySetName", "PolicyName", null, null, inCoverDoc, true); //Retrieve the policy-protected PDF document Document protectPDF = rmSecureDocument.getProtectedDoc(); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); protectPDF.copyToFile(myFile);` **extractProtectedDocument:** 提取受保護文檔，該文檔是帶封面的文檔中的附件。 使用protectDocumentWithCoverPage方法可以建立包含封面的文檔
`//Create a ServiceClientFactory instance ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps); //Create a RightsManagementClient object RightsManagementClient rightsClient = new RightsManagementClient(factory); //Reference a protected PDF document with a Cover Page FileInputStream fileInputStream = new FileInputStream("C:\\policyProtectedDocWithCoverPage.pdf"); Document inPDF = new Document(fileInputStream); //Create a Document Manager object DocumentManager documentManager = rightsClient.getDocumentManager(); //Apply a policy to the PDF document Document extractedDoc = documentManager.extractProtectedDocument(inPDF); //Save the policy-protected PDF document File myFile = new File("C:\\PolicyProtectedDoc.pdf"); extractedDoc.copyToFile(myFile);`
