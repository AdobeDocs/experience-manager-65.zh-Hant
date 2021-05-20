---
title: 識別PDF檔案中的有效和過期憑證
seo-title: 識別PDF檔案中的有效和過期憑證
description: 了解如何辨識PDF檔案中的有效和過期憑證。
seo-description: 了解如何辨識PDF檔案中的有效和過期憑證。
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# 識別PDF文檔{#recognizing-valid-and-expired-certificates-in-pdf-documents}中的有效證書和過期證書

在Adobe Reader中開啟具有「Reader擴充功能」所套用之使用權限的PDF檔案時，會出現狀態列，說明PDF檔案中啟用的特定使用權限。

當指定PDF檔案使用權限的數位憑證過期，以及在Adobe Reader中開啟PDF檔案時，會出現一個對話方塊，告知使用者PDF檔案具有使用權限，但這些權限會停用。 儘管該消息表示PDF文檔已被更改或篡改，但情況不一定如此。 Adobe Reader會在憑證過期或修改檔案時顯示此訊息。 在Adobe Reader 7.0.x或更新版本中，您無法判斷目前是哪個案例。

關閉對話框後，Adobe Reader將開啟PDF文檔。 無法使用使用Acrobat Reader DC擴充功能套用的使用權限，如預期。 如果PDF文檔是互動式表單，則表單欄位被鎖定，用戶無法更改表單資料。
