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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%
---
# 在PDF檔案中辨識有效及過期的憑證 {#recognizing-valid-and-expired-certificates-in-pdf-documents}

在Adobe Reader中開啟具有Reader擴充功能套用之使用許可權的PDF檔案時，會顯示一個狀態列，說明PDF檔案中啟用的特定使用許可權。

當指定PDF檔案使用許可權的數位憑證到期，且PDF檔案在Adobe Reader中開啟時，對話方塊會建議使用者該PDF檔案具有使用許可權，但這些許可權已停用。 雖然訊息指出PDF檔案遭到更改或竄改，但情況未必如此。 Adobe Reader會在憑證過期或修改檔案時顯示此訊息。 在Adobe Reader 7.0.x或更新版本中，您無法判斷目前是哪個案例的問題。

關閉對話方塊後，Adobe Reader會開啟PDF檔案。 使用Acrobat Reader DC擴充功能套用的使用許可權無法如預期使用。 如果PDF檔案是互動式表單，則表單欄位會鎖定，使用者無法變更表單資料。
