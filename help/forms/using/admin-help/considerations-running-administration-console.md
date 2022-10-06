---
title: 運行AdministrationConsole時的考量事項
seo-title: Considerations when running AdministrationConsole
description: 本檔案列出執行管理控制台時要考慮的幾點。
seo-description: This document lists a few points to consider when running Administration Console.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# 執行管理控制台時的考量事項 {#considerations-when-running-administrationconsole}

以下是運行管理控制台時要考慮的事項：

* 如果您使用URL存取管理控制台 `https://[hostname]:'port'/adminui`，指定的主機名不能包含下划線字元。 否則，指向管理控制台某些區域的連結可能無法正常工作。
* 如果您在日文作業系統的Windows資源管理器中運行管理控制台，則可能會處理以下問題：

   * 按一下連結會將您傳回登入頁面，而非預期的連結。
   * 按一下連結會顯示權限錯誤。

   最佳作法是從其他瀏覽器（例如Mozilla Firefox）執行管理主控台，以確保不會有任何連結失敗。

* 在管理控制台中執行搜尋時，請勿使用反斜線字元()。
