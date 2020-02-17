---
title: 運行AdministrationConsole時的注意事項
seo-title: 運行AdministrationConsole時的注意事項
description: 本檔案列出執行管理控制台時要考慮的幾點。
seo-description: 本檔案列出執行管理控制台時要考慮的幾點。
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 運行管理控制台時的注意事項 {#considerations-when-running-administrationconsole}

以下是運行管理控制台時要考慮的事項：

* 如果您使用URL存取管理控制台， `https://[hostname]:[port]/adminui`則指定的主機名稱不能包含底線字元。 否則，指向管理控制台某些區域的連結可能無法正常運作。
* 如果您在日文作業系統的Windows檔案總管中執行管理主控台，可能會遇到下列問題：

   * 按一下連結會返回登入頁面，而非預期的連結。
   * 按一下連結會顯示權限錯誤。
   最佳實務是從其他瀏覽器（例如Mozilla Firefox）執行管理控制台，以確保沒有連結會失敗。

* 在管理控制台中執行搜尋時，請勿使用反斜線字元()。

