---
title: 開發工具
description: 若要開發JCR、Apache Sling或Adobe Experience Manager應用程式，可使用數個工具集。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 開發工具{#development-tools}

若要開發JCR、Apache Sling或Adobe Experience Manager (AEM)應用程式，可使用下列工具集：

* 一組包含 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 和WebDAV。 CRXDE Lite內嵌至CRX/AEM，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄並與SVN整合時建立和編輯檔案(如.jsp和.java)、資料夾、範本、元件、對話方塊、節點、屬性和組合。

  如果您無法直接存取CRX/AEM伺服器，或是透過擴充或修改現成元件和Java™套件組合來開發應用程式，或是您不需要專用的除錯程式、程式碼完成和語法醒目提示，則建議使用CRXDE Lite。

* 一組包含下列專案：
   * 整合式開發環境。 例如， [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 或 [IntelliJ](/help/sites-developing/ht-intellij.md).
   * 建置工具。 例如， [Apache Maven](/help/sites-developing/ht-projects-maven.md).
   * FileVault，由Adobe開發，用於將存放庫對應到檔案系統（版本控制系統）。 例如，Subversion。
   * Bug追蹤系統。 例如，Jira。
   * 中央相依性管理系統。 例如，Apache Archiva。
   * 以及組建自動化系統。 例如，Apache Continuum。

  此設定可讓您將應用程式（內容、程式碼、設定）完全整合至任何開發環境和程式。 不同元素之間的連結是透過FileVault表示儲存庫的檔案系統，因為先前提到的所有開發工具都可以處理檔案。

## 整合式開發環境的擴充功能 {#extensions-for-integrated-development-environments}

Adobe發行了下列擴充功能：

* [AEM Eclipse擴充功能](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets擴充功能](/help/sites-developing/aem-brackets.md)

### 其他工具 {#other-tools}

AEM隨附其他有助於開發的工具：

* [對話方塊編輯器](/help/sites-developing/dialog-editor.md)
* [使用Translator管理字典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理套件](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse開發AEM專案](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven建置AEM專案](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA開發AEM專案](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用Proxy伺服器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 現代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

有助於建立新專案的工具：

* [AEM專案原型](https://github.com/adobe/aem-project-archetype)
* [AEM Lazybone範本](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>下列教學課程可能對開始新的AEM專案有幫助：
>[AEM Sites快速入門第1部分 — 專案設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
