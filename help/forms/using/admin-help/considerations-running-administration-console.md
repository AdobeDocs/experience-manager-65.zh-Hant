---
title: 執行Administration Console時的注意事項
description: 本檔案列出執行Administration Console時應考量的幾點。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# 執行Administration Console時的注意事項 {#considerations-when-running-administrationconsole}

執行Administration Console時，以下是一些要考量的事項：

* 如果您使用URL `https://[hostname]:'port'/adminui`存取管理主控台，指定的主機名稱不能包含底線字元。 否則，連至管理主控台某些區域的連結可能無法正常運作。
* 如果您在日文作業系統上執行Windows檔案總管中的管理主控台，可能會遇到下列問題：

   * 按一下連結會返回登入頁面，而非預期的連結。
   * 按一下連結會顯示許可權錯誤。

  最佳實務是從其他瀏覽器（例如Mozilla Firefox）執行管理主控台，以確保沒有連結失敗。

* 在管理控制檯中執行搜尋時，請勿使用反斜線字元()。
