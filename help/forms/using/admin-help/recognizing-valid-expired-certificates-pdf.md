---
title: 識別PDF文檔中的有效和過期證書
seo-title: Recognizing valid and expired certificates in PDF documents
description: 瞭解如何識別PDF文檔中的有效和過期的證書。
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

# 識別PDF文檔中的有效和過期證書 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader開啟具有由PDF擴展應用的使用權限的Reader文檔時，將顯示一個狀態欄，描述在PDF文檔中啟用的特定使用權限。

當指定PDF文檔的使用權限的數字證書過期且PDF文檔在Adobe Reader開啟時，將出現一個對話框，通知用戶PDF文檔具有使用權限，但是這些權限被禁用。 儘管該消息表示PDF文檔已被更改或篡改，但情況不一定如此。 Adobe Reader在證書過期或文檔被修改時顯示此消息。 在Adobe Reader7.0.x或更高版本中，您無法確定當前問題出在哪個案例上。

關閉對話框後，Adobe Reader開啟PDF文檔。 使用Acrobat Reader DC擴展應用的使用權限不可用，如預期。 如果PDF文檔是互動式表單，則表單域將被鎖定，用戶無法更改表單資料。
