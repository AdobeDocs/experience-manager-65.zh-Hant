---
title: 文檔安全產品
seo-title: Document security offerings
description: 了解AEM Document Security的各種工具和功能
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

Adobe Experience Manager Forms檔案安全性可確保只有獲授權的使用者才能使用您的檔案。 使用文檔安全性，您可以安全地分發以支援格式保存的任何資訊。 支援的檔案格式包括Adobe可移植文檔格式(PDF)和Microsoft Word、Excel和PowerPoint檔案。

您可以使用策略保護文檔。 您在策略中指定的機密設定決定了收件人如何使用應用策略的文檔。 例如，您可以指定收件者是否可以打印或複製文本、編輯文本，或向受保護的文檔添加簽名和注釋。

策略儲存在Document Security伺服器上；通過客戶端應用程式將策略應用到文檔。 將策略應用於文檔時，策略中指定的機密設定將保護文檔包含的資訊。 您可以將受策略保護的文檔分發給受策略授權的收件人。

下圖顯示AEM Forms檔案安全性的典型架構：

![檔案安全性 — 建議的架構](do-not-localize/document_security_architecture.png)

## 文檔安全客戶端 {#document-security-clients}

文檔安全性為各種客戶端提供了保護文檔、查看和編輯受保護文檔的功能，以及對受保護文檔進行全文搜索的索引器。 您可以根據您的需求和客戶端的功能選擇客戶端。

Document Security Server是Document Security執行事務（如用戶驗證、策略的即時管理和機密性應用）的中心元件。 伺服器還為策略、審核記錄和其他相關資訊提供一個中央儲存庫。

文檔安全伺服器提供基於Web的介面（網頁），用於建立策略、管理受策略保護的文檔，以及監視與受策略保護的文檔關聯的事件。 管理員還可以配置全局選項，如用戶驗證、審核和受邀用戶的消息傳送，以及管理受邀用戶帳戶。

伺服器包含在AEM Forms Document Security附加元件產品中。 您可以聯絡AEM Forms [銷售團隊](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) 購買Document Security附加元件。

### Protect檔案 {#protect-documents}

AEM Forms檔案安全性提供多種工具，可套用安全性原則。 您可以根據需求和規格選擇工具。

![document-security-offerings](assets/document-security-offerings.png)

您可以使用Document Security SDK、Adobe Acrobat、Document Security Extension for Microsoft Office或Portable Protection Library來套用及追蹤安全性原則：

* **檔案安全性SDK:** SDK是功能豐富的用戶端。 您可以使用Document Security SDK存取檔案伺服器功能、開啟受原則保護的檔案，以及開發自訂擴充功能、外掛程式或應用程式。 例如，您可以開發擴展來保護自定義檔案格式，或將SDK與資料丟失預防(DLP)解決方案整合。 使用Document Security SDK開發的擴充功能、應用程式和外掛程式會將檔案傳送至指定的AEM Forms伺服器，而原則會套用在伺服器上。 另請注意，AEM Forms檔案安全性用戶端SDK(CSDK)無法取消保護使用可攜式保護程式庫(PPL)保護的檔案，反之亦然。

   檔案安全性SDK可同時用於Java和C++。 AEM Forms Document Security產品包含Java SDK，且會安裝於部署JEE上的AEM表單時。 您可以聯絡 [AEM支援團隊](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html) 購買C++ SDK。 C++ SDK可用Microsoft Visual Studio 2013編譯。 您可以造訪 [檔案安全性API檔案](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) 網站以學習及使用SDK功能。

* **Adobe Acrobat:** 您可以使用Adobe Acrobat將安全性原則套用至使用常用案頭應用程式(如Microsoft Office、Web瀏覽器或任何支援以PDF格式列印的應用程式)建立的PDF檔案。

   您可以從購買及下載Adobe Acrobat [Adobe網站](https://acrobat.adobe.com/us/en/free-trial-download.html). Adobe Acrobat文章 [為PDF設定安全策略](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) 提供在Adobe Acrobat中建立和套用原則的詳細資訊。

* **Microsoft Office的Document Security Extension**:您可以使用Microsoft Office的Document Security Extension，從Microsoft Office程式內將預先定義的原則套用至您的Microsoft Office檔案。 此擴充功能可確保只有授權人員才能使用受原則保護的Microsoft Word、Excel和PowerPoint檔案。 只有安裝了插件的授權用戶才能使用受策略保護的檔案。

   Document Security擴充功能可作為Microsoft Office外掛程式使用。 您可以聯絡 [AEM支援團隊](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) 購買擴充功能。 稍後，您可以造訪 [Microsoft Office的Document Security Extension](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) 協助您了解如何安裝、設定和使用擴充功能。

* **可移植保護庫：** 可移植保護庫(PPL)可在本地保護文檔，而不將文檔發送到AEM Forms伺服器。 只有安全憑據和策略詳細資訊才能通過網路傳輸。 PPL還允許您僅限登錄用戶訪問策略檢索。 您可以使用登入AEM使用者的使用者內容擷取原則。

   除了上述功能外，可比例保護庫還具有Document Security SDK的所有功能。 您可以使用Document Security SDK存取檔案伺服器功能、開啟受原則保護的檔案，以及開發自訂擴充功能、外掛程式或應用程式。 另請注意，可攜式保護程式庫(PPL)無法取消保護使用AEM Forms檔案安全性用戶端SDK(CSDK)保護的檔案，反之亦然。

   可移植保護庫適用於32位和64位版本的Java和C++語言。 OSGi上也提供AEM Forms適用的OSGi套件組合。 C++ PPL可用Microsoft Visual Studio 2013編譯。 如果您已授權AEM Forms Document Security附加元件，您可以聯絡 [AEM Forms檔案安全性](https://helpx.adobe.com/marketing-cloud/contact-support.html) 支援團隊採購Portable Protection Library。 稍後，您可以使用「Portable Protection Library幫助」（隨庫一起提供）來設定和使用「Portable Protection Library」。

### 查看或編輯受保護的文檔 {#view-or-edit-protected-documents}

* 針對 **PDF檔案**，您可以使用Adobe Acrobat DC、Acrobat Reader和Acrobat Reader Mobile來檢視受保護的PDF檔案。 大部分的使用者在裝置上皆已安裝Acrobat Reader，因此他們不需要取得或了解其他軟體即可檢視受保護的檔案。 您也可以從下載Acrobat Reader [Acrobat Reader下載網站](https://get.adobe.com/reader/).

* 針對 **Microsoft Office檔案**，您需要Microsoft Office和Microsoft Office的AEM Forms Document Security擴充功能。 Document Security擴充功能可作為Microsoft Office外掛程式使用。 您可以從Adobe網站下載擴充功能。

### 為受保護的文檔編製索引 {#index-protected-documents}

Microsoft Windows全文搜索引擎(SharePoint Index Server)和Adobe Experience Manager(AEM)可以對常用的文檔格式(如，純文字檔案檔案、Microsoft Office文檔和PDF文檔)執行全文搜索。 您可以使用Document Security索引器來啟用全文搜索引擎以搜索受保護的PDF文檔：

* **iFilter索引器：** 您可以使用iFilter索引器為受保護的PDF文檔建立索引，並使Microsoft Windows全文搜索引擎(案頭索引服務和SharePoint索引伺服器)能夠搜索受保護的PDF文檔。 如需詳細資訊，請參閱 [AEM SharePoint IFilter for Protected Documents](assets/sharepoint-ifilter-doc-security.pdf).

* **AEM Forms Document Security Indexer:** 您可以使用AEM Forms Document Security索引器來索引受保護的PDF檔案，並啟用Adobe Experience Manager來搜尋受保護的PDF檔案。 索引器是AEM Forms Document Security產品的一部分。 這些功能包含在JEE安裝程式的AEM Forms中。
