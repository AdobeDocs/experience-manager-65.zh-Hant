---
title: 在PDF檔案中辨識有效及過期的憑證
description: 瞭解如何在PDF檔案中識別有效及過期的憑證。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# 在PDF檔案中辨識有效及過期的憑證 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中開啟具有由PDF擴充功能套用之使用許可權的Reader檔案時，會出現一個狀態列，說明PDF檔案中啟用的特定使用許可權。

當指定PDF檔案使用許可權的數位憑證過期且PDF檔案在Adobe Reader中開啟時，對話方塊會建議使用者該PDF檔案具有使用許可權，但這些許可權已停用。 雖然訊息指出PDF檔案被更改或竄改，但情況不一定如此。 當憑證過期或修改檔案時，Adobe Reader會顯示此訊息。 在Adobe Reader 7.0.x或更新版本中，您無法判斷目前是問題的案例。

關閉對話方塊後，Adobe Reader會開啟PDF檔案。 使用Acrobat Reader DC擴充功能套用的使用許可權無法如預期使用。 如果PDF檔案是互動式表單，則表單欄位會鎖定，使用者無法變更表單資料。
