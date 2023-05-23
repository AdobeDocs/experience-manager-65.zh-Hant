---
title: 文檔安全產品
seo-title: Document security offerings
description: 瞭解文檔安全的各種工具AEM和功能
seo-description: Learn about various tools and features of AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
source-git-commit: 18c180a491af10b41393ad841f2fa74d02ec9cd9
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# 文檔安全產品{#document-security-offerings}

Adobe Experience Manager Forms文檔安全性確保只有授權用戶才能使用您的文檔。 使用文檔安全性，您可以安全地分發以支援格式保存的任何資訊。 支援的檔案格式包括Adobe可移植文檔格式(PDF)和MicrosoftWord、Excel和PowerPoint檔案。

可以使用策略保護文檔。 在策略中指定的機密性設定決定了收件人如何使用您應用策略的文檔。 例如，您可以指定收件人是否可以打印或複製文本、編輯文本，或向受保護文檔添加簽名和注釋。

策略儲存在Document Security伺服器上；通過客戶端應用程式將策略應用於文檔。 將策略應用於文檔時，策略中指定的機密性設定會保護文檔包含的資訊。 您可以將受策略保護的文檔分發給受策略授權的收件人。

下圖顯示了AEM Forms文檔安全的典型體系結構：

![文檔安全性 — 推薦的體系結構](do-not-localize/document_security_architecture.png)

## 文檔安全客戶端 {#document-security-clients}

文檔安全性提供各種客戶端來保護文檔、查看和編輯受保護的文檔，以及索引器以啟用受保護文檔的全文搜索。 您可以根據您的要求和客戶機的功能選擇客戶機。

文檔安全伺服器是文檔安全執行事務的核心元件，如用戶驗證、策略的即時管理和機密性應用。 伺服器還為策略、審計記錄和其他相關資訊提供了中央儲存庫。

文檔安全伺服器提供基於Web的介面（網頁），用於建立策略、管理受策略保護的文檔以及監視與受策略保護的文檔相關聯的事件。 管理員還可以為受邀用戶配置全局選項，如用戶驗證、審核和消息傳遞，並管理受邀用戶帳戶。

伺服器包含在AEM Forms文檔安全附加產品中。 你可以聯繫AEM Forms [銷售團隊](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) 購買「文檔安全性」載入項。

### Protect檔案 {#protect-documents}

AEM Forms文檔安全性提供了各種工具來應用安全策略。 您可以根據您的要求和規格選擇工具。

![文檔安全產品](assets/document-security-offerings.png)

您可以使用Document Security SDK、Adobe Acrobat、Document Security Extension for Decument Office或Portable Protection Library來應用和跟蹤安全策略：

* **文檔安全SDK:** SDK是功能豐富的客戶端。 您可以使用Document Security SDK訪問文檔伺服器功能、開啟受策略保護的文檔，以及開發自定義擴展、插件或應用程式。 例如，您可以開發擴展來保護自定義檔案格式，或將SDK與資料丟失防範(DLP)解決方案整合。 使用Document Security SDK開發的擴展、應用程式和插件將文檔發送到指定的AEM Forms伺服器，並且策略應用在伺服器上。 另請注意，AEM Forms文檔安全客戶端SDK(CSDK)無法取消保護使用攜帶型保護庫(PPL)保護的文檔，反之亦然。

   Document Security SDK可用於Java和C++。 Java SDK包含在AEM Forms文檔安全產品中，並安裝在JEE上AEM的部署表單上。 您可以聯繫 [AEM支援團隊](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html) 購買C++ SDK。 C++ SDK可以用MicrosoftVisual Studio 2013編譯。 你可以去 [文檔安全API文檔](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) 站點以學習和使用SDK的功能。

* **Adobe Acrobat:** 您可以使用Adobe Acrobat將安全策略應用於PDF使用常用案頭應用程式建立的文檔，如Microsoft辦公室、Web瀏覽器或任何支援以PDF格式打印的應用程式。

   您可以從以下網站購買和下載Adobe Acrobat [Adobe網站](https://acrobat.adobe.com/us/en/free-trial-download.html)。 Adobe Acrobat文章 [為PDF設定安全策略](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) 提供了有關在Adobe Acrobat建立和應用策略的詳細資訊。

* **Microsoft辦事處檔案安全擴展**:您可以使用Microsoft辦事處的文檔安全擴展，從Microsoft辦事處程式內將預定義的策略應用到Microsoft辦事處檔案。 該擴展可確保只有已授權的人員才能使用受策略保護的MicrosoftWord、Excel和PowerPoint檔案。 只有安裝了插件的授權用戶才能使用受策略保護的檔案。

   文檔安全擴展可作為Microsoft辦公室插件使用。 您可以聯繫 [AEM支援團隊](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) 來取得延期。 稍後，您可以訪問 [Microsoft辦事處檔案安全擴展](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) 有關安裝、配置和使用擴展的幫助。

* **攜帶型保護庫：** 可移植保護庫(PPL)在本地保護文檔，而不將文檔發送到AEM Forms伺服器。 只有安全憑據和策略詳細資訊才能通過網路傳輸。 PPL還允許您將策略檢索訪問限制為僅登錄用戶。 您可以使用登錄用戶的上下文獲取策AEM略。

   除上述功能外，可寫程式保護庫還具有Document Security SDK的所有功能。 您可以使用Document Security SDK訪問文檔伺服器功能、開啟受策略保護的文檔，以及開發自定義擴展、插件或應用程式。 另請注意，攜帶型保護庫(PPL)無法取消保護使用AEM Forms文檔安全客戶端SDK(CSDK)保護的文檔，反之亦然。

   可移植保護庫可用於32位和64位版本的Java和C++語言。 它還作為OSGi上的AEM Forms的OSGi捆綁包提供。 C++ PPL可以用MicrosoftVisual Studio 2013編譯。 如果您已獲得AEM Forms文檔安全附加模組的許可，您可以聯繫 [AEM Forms文檔安全](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html) 支援團隊購買攜帶型保護庫。 稍後，您可以使用「Portable Protection Library Help（隨庫捆綁）」來設定和使用「Portable Protection Library（便攜保護庫）」。

### 查看或編輯受保護的文檔 {#view-or-edit-protected-documents}

* 對於 **PDF文檔**，您可以使用Adobe AcrobatDC、Acrobat Reader和Acrobat Reader移動查看受保護的PDF文檔。 大多數用戶已在其設備上安裝了Acrobat Reader，因此他們不需要獲取或學習其他軟體來查看受保護的文檔。 您也可以從以下網站下載Acrobat Reader [Acrobat Reader下載網站](https://get.adobe.com/reader/)。

* 對於 **Microsoft辦公室檔案**，您需要Microsoft辦公室和AEM Forms文檔安全擴展，以便Microsoft辦公室。 文檔安全擴展可作為Microsoft辦公室插件使用。 您可以從Adobe網站下載分機。

### 為受保護的文檔編製索引 {#index-protected-documents}

MicrosoftWindows全文搜索引擎(SharePoint索引伺服器)和Adobe Experience Manager(AEM)可以對常用文檔格式(如純文字檔案檔案、Microsoft Office文檔和PDF文檔)執行全文搜索。 您可以使用文檔安全索引器啟用全文搜索引擎來搜索受保護的PDF文檔：

* **iFilter索引器：** 您可以使用iFilter索引器為受保護的PDF文檔編製索引，並啟用MicrosoftWindows全文搜索引擎(案頭索引服務和SharePoint索引伺服器)來搜索受保護的PDF文檔。 有關詳細資訊，請參見 [SharePointAEM IFilter保護文檔](assets/sharepoint-ifilter-doc-security.pdf)。

* **AEM Forms文檔安全索引器：** 您可以使用AEM Forms文檔安全索引器為受保護的PDF文檔編製索引，並使Adobe Experience Manager能夠搜索受保護的PDF文檔。 索引器是AEM Forms文檔安全產品的一部分。 這些內容包含在AEM Forms的JEE安裝程式中。
