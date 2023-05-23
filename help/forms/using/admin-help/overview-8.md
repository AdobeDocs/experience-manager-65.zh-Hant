---
title: 輸出服務概述
seo-title: Overview of output service
description: 「輸出」(Output)允許您將XML表單資料與在設計器中建立的表單設計合併，以建立各種格式的文檔輸出流。
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

「輸出」(Output)允許您將XML表單資料與在設計器中建立的表單設計合併，以建立各種格式的文檔輸出流。 輸出流可以發送到網路打印機、本地打印機或磁碟檔案

可以使用管理控制台中的「輸出」頁管理「輸出」服務。 未通過表單API指定對等設定時，將在運行時使用您配置AEM的設定。 通過表單SDKAEM完成的配置將覆蓋使用管理控制台配置的設定。

有關輸出服務的其他資訊，請參見 [服務參考](https://www.adobe.com/go/learn_aemforms_services_61)。

在管理控制台的「輸出」頁上，可以執行以下幾項任務：

* 指定用於國際化的字元集。 (請參閱 [更改字元集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)。)
* 為URL、URI、XCI和檔案位置指定絕對路徑和相對路徑。 (請參閱 [為輸出指定檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)
* 配置快取大小和策略。 (請參閱 [指定快取模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 和 [配置快取設定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)。)
* 使字型在應用伺服器上可用。 (請參閱 [使字型可用](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)。)
* 指定要嵌入的字型。 (請參閱 [指定要嵌入的字型](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)。)
* 指定XCI配置選項。 (請參閱 [指定XCI配置選項](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)。)
* 指定安全設定。 (請參閱 [指定安全設定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)。)

更改設定後，按一下「保存」(Save)將其應用於「輸出」(Output)。 您不需要重新啟動伺服器以使更改生效，但在配置快取設定時可能需要重新啟動輸出服務。
