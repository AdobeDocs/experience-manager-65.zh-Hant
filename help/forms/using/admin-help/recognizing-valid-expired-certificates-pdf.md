---
title: 識別PDF檔案中的有效及過期憑證
seo-title: 識別PDF檔案中的有效及過期憑證
description: 瞭解如何辨識PDF檔案中有效和過期的憑證。
seo-description: 瞭解如何辨識PDF檔案中有效和過期的憑證。
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 識別PDF檔案中的有效及過期憑證 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

當在Adobe Reader中開啟具有Reader Extensions套用之使用權限的PDF檔案時，會出現狀態列，說明PDF檔案中啟用的特定使用權限。

當指定PDF檔案使用權限的數位憑證過期，而PDF檔案在Adobe Reader中開啟時，會出現對話方塊，告知使用者PDF檔案具有使用權限，但是這些權限已停用。 雖然訊息指出PDF檔案已遭變更或竄改，但不一定如此。 當憑證過期或檔案被修改時，Adobe Reader會顯示此訊息。 在Adobe Reader 7.0.x或更新版本中，您無法判斷目前是哪個案例。

關閉對話方塊後，Adobe Reader會開啟PDF檔案。 使用Acrobat Reader DC擴充功能套用的使用權限無法如預期般使用。 如果PDF檔案是互動式表單，表單欄位會鎖定，使用者無法變更表單資料。
