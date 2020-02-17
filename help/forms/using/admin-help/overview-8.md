---
title: 輸出服務概觀
seo-title: 輸出服務概觀
description: 輸出功能可讓您將XML表單資料與在設計工具中建立的表單設計合併，以建立各種格式的檔案輸出串流。
seo-description: 輸出功能可讓您將XML表單資料與在設計工具中建立的表單設計合併，以建立各種格式的檔案輸出串流。
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 輸出服務概觀 {#overview-of-output-service}

輸出功能可讓您將XML表單資料與在設計工具中建立的表單設計合併，以建立各種格式的檔案輸出串流。 輸出流可以發送到網路打印機、本地打印機或磁碟檔案

您可以使用管理控制台中的「輸出」頁來管理「輸出」服務。 您設定的設定會在執行時期使用，當等同的設定未透過AEM表單API指定時。 透過AEM Forms SDK完成的設定會覆寫使用管理控制台所設定的設定。

有關輸出服務的其他資訊，請參閱服 [務參考](https://www.adobe.com/go/learn_aemforms_services_61)。

在管理控制台的「輸出」頁面上，您可以執行數項工作：

* 指定國際化的字元集。 (請參 [閱更改字元集](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)。)
* 指定URL、URI、XCI和檔案位置的絕對和相對路徑。 (請參 [閱指定輸出的檔案位置](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)。)
* 配置快取大小和策略。 (請參 [閱指定快取模式](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode)[和設定快取設定](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)。)
* 讓字型在應用程式伺服器上可用。 (請參 [閱「提供字型](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)」。)
* 指定要內嵌的字型。 (請參 [閱指定要內嵌的字型](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)。)
* 指定XCI配置選項。 (請參 [閱指定XCI配置選項](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)。)
* 指定安全性設定。 (請參 [閱指定安全性設定](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)。)

變更設定後，按一下「儲存」，將它們套用至「輸出」。 您不需要重新啟動伺服器，更改才能生效，但在配置快取設定時可能需要重新啟動輸出服務。
