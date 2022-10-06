---
title: 在PDF文檔中識別有效和過期的證書
seo-title: Recognizing valid and expired certificates in PDF documents
description: 了解如何辨識PDF檔案中的有效和過期憑證。
seo-description: Learn how to recognize valid and expired certificates in PDF documents.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# 在PDF文檔中識別有效和過期的證書 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中開啟具有由PDF擴展應用的使用權限的Reader文檔時，將顯示一個狀態欄，說明在PDF文檔中啟用的特定使用權限。

當指定PDF檔案使用權限的數位憑證過期，並在Adobe Reader中開啟PDF檔案時，會出現一個對話方塊，告知使用者PDF檔案具有使用權限，但這些權限會停用。 儘管該消息表示PDF文檔已被更改或篡改，但情況不一定如此。 Adobe Reader會在憑證過期或修改檔案時顯示此訊息。 在Adobe Reader 7.0.x或更新版本中，您無法判斷目前是哪個案例。

關閉對話方塊後，Adobe Reader會開啟PDF檔案。 無法使用使用Acrobat Reader DC擴充功能套用的使用權限，如預期。 如果PDF文檔是互動式表單，則表單欄位被鎖定，用戶無法更改表單資料。
