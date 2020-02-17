---
title: 開發工具
seo-title: 開發工具
description: 若要開發您的JCR、Apache Sling或AEM應用程式，有許多工具集可供使用
seo-description: 若要開發您的JCR、Apache Sling或AEM應用程式，有許多工具集可供使用
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 開發工具{#development-tools}

若要開發您的JCR、Apache Sling或AEM應用程式，可使用下列工具集：

* 一組由 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 和WebDAV組成。 CRXDE Lite已內嵌在CRX/AEM中，可讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄和整合SVN時，建立和編輯檔案（例如。jsp和。java）、檔案夾、範本、元件、對話方塊、節點、屬性和組合。

   當您無法直接存取CRX/AEM伺服器、透過擴充或修改現成可用的元件和Java套件來開發應用程式時，或當您不需要專用的除錯程式、程式碼完成和反白顯示語法時，建議使用CRXDE Lite。

* 一組由整合開發環境組成(例如： [Eclipse](/help/sites-developing/howto-projects-eclipse.md) 或 [IntelliJ](/help/sites-developing/ht-intellij.md))，建置工具(例如：Apache Maven [](/help/sites-developing/ht-projects-maven.md)),FileVault，由Adobe開發以將儲存庫對應至檔案系統、版本控制系統(例如：Subversion)，錯誤追蹤系統(例如：Jira)，一個中央相依性管理系統(例如：Apache Archiva)和建置自動化系統(例如：Apache Continuum)。

   此設定允許您將應用程式（內容、代碼、配置）完全整合到任何開發環境和流程中。不同元素之間的連結是通過FileVault對儲存庫的檔案系統表示，因為上述所有開發工具都可以使用檔案。

## 整合開發環境的擴充功能 {#extensions-for-integrated-development-environments}

Adobe已發行下列擴充功能：

* [AEM Eclipse Extension](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets延伸功能](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ Extension](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) （來自Headwire）

### 其他工具 {#other-tools}

AEM隨附其他可協助開發的工具：

* [對話框編輯器](/help/sites-developing/dialog-editor.md)
* [使用翻譯工具管理字典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用Eclipse開發AEM專案](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache Maven建立AEM專案](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJ IDEA開發AEM專案](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用Proxy伺服器工具](/help/sites-developing/ht-proxy-server.md)
* [對話方塊轉換工具](/help/sites-developing/dialog-conversion.md)
* [AEM Repo工具](/help/sites-developing/aem-repo-tool.md)

協助建立新專案的工具：

* [AEM Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones範本](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>下列教學課程可能會對啟動新AEM專案有興趣：
>[AEM Sites快速入門第1部份——專案設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

