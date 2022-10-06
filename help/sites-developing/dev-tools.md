---
title: 開發工具
seo-title: Development Tools
description: 若要開發您的JCR、Apache Sling或AEM應用程式，可使用許多工具集
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 3%

---

# 開發工具{#development-tools}

若要開發您的JCR、Apache Sling或AEM應用程式，可使用下列工具集：

* 一組 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 和WebDAV。 CRXDE Lite內嵌於CRX/AEM中，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，可以在記錄和與SVN整合時建立和編輯檔案(如.jsp和.java)、資料夾、模板、元件、對話框、節點、屬性和包。

   如果您沒有CRX/AEM伺服器的直接存取權，或是透過擴充或修改現成可用的元件和Java套件組合來開發應用程式時，或是您不需要專用的除錯工具、程式碼完成和語法醒目提示時，建議使用CRXDE Lite。

* 一組由整合開發環境組成(例如： [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 或 [IntelliJ](/help/sites-developing/ht-intellij.md))、建置工具(例如： [阿帕奇·馬文](/help/sites-developing/ht-projects-maven.md))、 FileVault(由Adobe開發，可將儲存庫映射到檔案系統，即版本控制系統)(例如：Subversion)，錯誤追蹤器系統(例如：Jira)，一個中央依賴管理系統(例如：Apache Archiva)和組建自動化系統(例如：Apache Continuum)。

   此設定允許您將應用程式（內容、代碼、配置）完全整合到任何開發環境和進程中。不同元素之間的連結是通過FileVault對儲存庫的檔案系統表示，因為上述所有開發工具都可以使用檔案。

## 整合開發環境的擴充功能 {#extensions-for-integrated-development-environments}

Adobe發行下列擴充功能：

* [AEM Eclipse擴充功能](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets擴充功能](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ擴充功能](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) （從頭線）

### 其他工具 {#other-tools}

AEM隨附其他可促進開發的工具：

* [對話方塊編輯器](/help/sites-developing/dialog-editor.md)
* [使用翻譯工具管理字典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理套件](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse開發AEM專案](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven建立AEM專案](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA開發AEM專案](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用代理伺服器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 現代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

方便建立新項目的工具：

* [AEM 專案原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM懶骨模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>啟動新AEM專案可能需要下列教學課程：
>[AEM Sites快速入門第1部分 — 專案設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
