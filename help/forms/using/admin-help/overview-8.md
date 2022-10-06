---
title: 輸出服務概述
seo-title: Overview of output service
description: Output允許您將XML表單資料與在Designer中建立的表單設計合併，以建立各種格式的文檔輸出流。
seo-description: Output lets you merge XML form data with a form design created in Designer to create a document output stream in various formats.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 輸出服務概述 {#overview-of-output-service}

Output允許您將XML表單資料與在Designer中建立的表單設計合併，以建立各種格式的文檔輸出流。 輸出流可被發送到網路打印機、本地打印機或磁碟檔案

您可以使用管理控制台中的「輸出」頁面來管理輸出服務。 未透過AEM Forms API指定對等設定時，會在執行時使用您設定的設定。 透過AEM Forms SDK完成的設定會覆寫使用管理控制台所設定的設定。

有關輸出服務的其他資訊，請參見 [服務參考](https://www.adobe.com/go/learn_aemforms_services_61).

在管理控制台的「輸出」頁上，您可以執行數個任務：

* 指定國際化的字元集。 (請參閱 [更改字元集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* 指定URL、URI、XCI和檔案位置的絕對路徑和相對路徑。 (請參閱 [指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* 配置快取大小和策略。 (請參閱 [指定快取模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 和 [配置快取設定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* 讓字型在應用程式伺服器上可用。 (請參閱 [使字型可用](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* 指定要嵌入的字型。 (請參閱 [指定要嵌入的字型](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* 指定XCI設定選項。 (請參閱 [指定XCI配置選項](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* 指定安全設定。 (請參閱 [指定安全設定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

變更設定後，按一下「儲存」 ，將其套用至「輸出」。 您不需要重新啟動伺服器，變更才會生效，但在設定快取設定時，您可能需要重新啟動輸出服務。
