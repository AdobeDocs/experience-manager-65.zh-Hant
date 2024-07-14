---
title: Document Security方案
description: 瞭解AEM Document Security的各種工具和功能。
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Document Security
exl-id: d00ae232-b018-44e5-b04b-376d4cd9c6eb
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1161'
ht-degree: 0%

---

# Document Security方案{#document-security-offerings}

Adobe Experience Manager Forms document security可確保只有授權的使用者才能使用您的檔案。 使用Document Security，您可以安全地散發以支援格式儲存的任何資訊。 支援的檔案格式包括Adobe可攜式檔案格式(PDF)和Microsoft®Word、Excel和PowerPoint檔案。

您可以使用原則來保護檔案。 您在原則中指定的機密性設定可決定收件者如何使用您套用原則的檔案。 例如，您可以指定收件者是否可以列印或複製文字、編輯文字，或新增簽名和註解至受保護檔案。

原則儲存在Document Security伺服器上；您可以透過使用者端應用程式將原則套用至檔案。 當您套用原則至檔案時，原則中指定的機密性設定會保護檔案所包含的資訊。 您可以將受原則保護的檔案分發給受原則授權的收件者。

下圖顯示AEM Forms Document Security的典型架構：

![Document Security — 建議的架構](do-not-localize/document_security_architecture.png)

## Document Security使用者端 {#document-security-clients}

Document Security提供各種使用者端來保護檔案、檢視和編輯受保護的檔案，並提供索引器以啟用對受保護檔案的全文搜尋。 您可以根據您的需求和使用者端的功能來選擇使用者端。

Document Security伺服器是Document Security執行交易的中央元件，例如使用者驗證、政策的即時管理和機密性應用。 伺服器也提供原則、稽核記錄及其他相關資訊的中央存放庫。

Document Security伺服器提供網頁型介面（網頁），可建立原則、管理受原則保護的檔案，以及監控與受原則保護檔案相關聯的事件。 管理員也可以設定全域選項，例如受邀使用者的使用者驗證、稽核和傳訊，以及管理受邀的使用者帳戶。

伺服器包含在AEM Forms Document Security附加元件產品中。 您可以聯絡AEM Forms [銷售團隊](https://business.adobe.com/request-consultation/experience-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG)以購買Document Security附加元件。

### Protect檔案 {#protect-documents}

AEM Forms Document Security提供多種工具來套用安全性原則。 您可以根據需求和規格選擇工具。

![document-security-offers](assets/document-security-offerings.png)

您可以使用Document Security SDK、Adobe Acrobat、Microsoft適用的Document Security Extension®Office或可攜式保護資料庫來套用及追蹤安全性原則：

* **Document Security SDK：** SDK是功能豐富的使用者端。 您可以使用Document Security SDK來存取檔案伺服器功能、開啟受原則保護的檔案，以及開發自訂擴充功能、外掛程式或應用程式。 例如，您可以開發擴充功能以保護自訂檔案格式，或整合SDK與資料損失防護(DLP)解決方案。 使用Document Security SDK開發的擴充功能、應用程式和外掛程式，可將檔案傳送至指定的AEM Forms伺服器，且原則會套用至伺服器。 AEM Forms Document Security使用者端SDK (CSDK)無法取消保護使用可攜式保護程式庫(PPL)保護的檔案，反之亦然。

  Document Security SDK可同時用於Java™和C++。 Java™ SDK包含在AEM Forms Document Security產品中，並安裝在JEE上部署AEM Forms上。 聯絡[AEM客戶支援](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)以取得C++ SDK。 C++ SDK可以使用Microsoft® Visual Studio 2013進行編譯。 造訪[Document Security API檔案](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html)網站，瞭解並使用SDK的功能。

* **Adobe Acrobat：**&#x200B;您可以使用Adobe Acrobat將安全性原則套用至PDF使用熱門案頭應用程式(例如Microsoft®Office、網頁瀏覽器或任何支援PDF格式列印的應用程式)建立的檔案。

  您可以從[Adobe網站](https://www.adobe.com/acrobat/free-trial-download.html)購買及下載Adobe Acrobat。 Adobe Acrobat文章[為PDF設定安全性原則](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html)提供在Adobe Acrobat中建立和套用原則的詳細資訊。

* **Microsoft® Office適用的Document Security Extension**：您可以使用Microsoft® Office適用的Document Security Extension，從Microsoft® Office程式將預先定義的原則套用至Microsoft® Office檔案。 此擴充功能可確保只有授權人員才能使用受原則保護的Microsoft®Word、Excel和PowerPoint檔案。 只有已安裝外掛程式的授權使用者才能使用受原則保護的檔案。

  Document Security Extension可作為Microsoft® Office外掛程式使用。 請連絡[AEM客戶支援](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html)以取得擴充功能。 稍後您可以造訪[Microsoft適用的Document Security Extension® Office](https://experienceleague.adobe.com/docs/experience-manager-document-security/using/download-installer.html?lang=en)說明，瞭解安裝、設定和使用擴充功能的相關資訊。

* **可攜式保護庫：** PPL會在本機保護檔案，不會將檔案傳送至AEM Forms伺服器。 只有安全性認證和原則詳細資料會透過網路傳遞。 PPL也可讓您將原則擷取存取許可權製為只有登入的使用者。 您可以根據登入AEM使用者的內容擷取原則。

  除了上述功能，PPL還具備Document Security SDK的所有功能。 您可以使用Document Security SDK來存取檔案伺服器功能、開啟受原則保護的檔案，以及開發自訂擴充功能、外掛程式或應用程式。 PPL無法取消保護使用AEM Forms Document Security使用者端SDK (CSDK)受保護的檔案，反之亦然。

  PPL適用於32位元和64位元版本的Java™和C++語言。 它也可作為OSGi上AEM Forms的OSGi套件組合提供。 C++ PPL可以使用Microsoft® Visual Studio 2013進行編譯。 如果您已授權AEM Forms Document Security附加元件，您可以聯絡[AEM Forms Document Security](https://experienceleague.adobe.com/?support-solution=General&amp;support-tab=home#support)支援團隊以取得PPL。 稍後，您可以使用PPL說明（與程式庫整合）來設定及使用PPL。

### 檢視或編輯受保護的檔案 {#view-or-edit-protected-documents}

* 對於&#x200B;**PDF檔案**，您可以使用Adobe Acrobat DC、Acrobat Reader和Acrobat Reader Mobile來檢視受保護的PDF檔案。 大部分使用者已在裝置上安裝Acrobat Reader，因此他們不需要取得或學習其他軟體即可檢視受保護檔案。 您也可以從[Acrobat Reader下載網站](https://get.adobe.com/reader/)下載Acrobat Reader。

* 若為&#x200B;**Microsoft® Office檔案**，您需要使用Microsoft® Office適用的Microsoft® Office和AEM Forms Document Security Extension。 Document Security Extension可作為Microsoft® Office外掛程式使用。 您可以從Adobe網站下載擴充功能。

### 受保護檔案索引 {#index-protected-documents}

Microsoft® Windows全文檢索搜尋引擎(SharePoint Index server)和Adobe Experience Manager (AEM)可以對常用的檔案格式(例如純文字檔、Microsoft® Office檔案和PDF檔案)執行全文檢索。 您可以使用Document Security索引子來啟用全文檢索搜尋引擎，以搜尋受保護的PDF檔案：

* **iFilter索引子：**&#x200B;您可以使用iFilter索引子來索引受保護的PDF檔案，並啟用Microsoft® Windows全文檢索搜尋引擎(案頭索引服務和SharePoint索引伺服器)來搜尋受保護的PDF檔案。 如需詳細資訊，請參閱[AEM SharePoint IFilter for Protected Documents](assets/sharepoint-ifilter-doc-security.pdf)。

* **AEM Forms Document Security Indexer：**&#x200B;您可以使用AEM Forms Document Security Indexer為受保護的PDF檔案編制索引，以及讓Adobe Experience Manager搜尋受保護的PDF檔案。 索引器是AEM Forms Document Security產品的一部分。 這些包含在JEE安裝程式的AEM Forms中。
