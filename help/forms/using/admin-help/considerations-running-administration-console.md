---
title: 執行Administration Console時的注意事項
description: 本檔案列出執行Administration Console時應考量的幾點。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 執行Administration Console時的注意事項 {#considerations-when-running-administrationconsole}

執行Administration Console時，以下是一些要考量的事項：

* 如果您使用URL存取管理主控台 `https://[hostname]:'port'/adminui`，指定的主機名稱不可包含底線字元。 否則，連至管理主控台某些區域的連結可能無法正常運作。
* 如果您在日文作業系統上執行Windows檔案總管中的管理主控台，可能會遇到下列問題：

   * 按一下連結會返回登入頁面，而非預期的連結。
   * 按一下連結會顯示許可權錯誤。

  最佳實務是從其他瀏覽器（例如Mozilla Firefox）執行管理主控台，以確保沒有連結失敗。

* 在管理控制檯中執行搜尋時，請勿使用反斜線字元()。
