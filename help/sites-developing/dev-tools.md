---
title: 開發工具
seo-title: 開發工具
description: 若要開發您的JCR、Apache Sling或應AEM用程式，有許多工具集可供使用
seo-description: 若要開發您的JCR、Apache Sling或應AEM用程式，有許多工具集可供使用
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 2%

---


# 開發工具{#development-tools}

若要開發您的JCR、Apache Sling或應AEM用程式，可使用下列工具集：

* 一組由[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)和WebDAV組成。 CRXDE Lite嵌入到CRX/AEM中，讓您在瀏覽器中執行標準開發工作。 使用CRXDE Lite，您可以在記錄和整合SVN時建立和編輯檔案（如。jsp和。java）、資料夾、模板、元件、對話框、節點、屬性和捆綁包。

   當您無法直接存取CRX/AEM伺服器、透過擴充或修改現成可用的元件和Java組合來開發應用程式，或當您不需要專用的除錯程式、程式碼完成和語法反白顯示時，建議使用CRXDE Lite。

* 一組由整合開發環境組成(例如：[Eclipse](/help/sites-developing/howto-projects-eclipse.md)或[IntelliJ](/help/sites-developing/ht-intellij.md))，建置工具(例如：[Apache Maven](/help/sites-developing/ht-projects-maven.md))，由Adobe開發的FileVault，將儲存庫映射到檔案系統、版本控制系統(例如：Subversion)，錯誤追蹤系統(例如：Jira)，一個中央相依性管理系統(例如：Apache Archiva)和建置自動化系統(例如：Apache Continuum)。

   此設定允許您將應用程式（內容、代碼、配置）完全整合到任何開發環境和流程中。不同元素之間的連結是通過FileVault對儲存庫的檔案系統表示，因為上述所有開發工具都可以使用檔案。

## 整合開發環境的擴展{#extensions-for-integrated-development-environments}

Adobe已發行下列擴充功能：

* [AEM Eclipse Extension](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ Extension](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf) （來自Headwire）

### 其他工具{#other-tools}

隨附AEM其他工具以利開發：

* [對話框編輯器](/help/sites-developing/dialog-editor.md)
* [使用翻譯工具管理字典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何使用EclipseAEM開發專案](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache AEM Maven建立專案](/help/sites-developing/ht-projects-maven.md)
* [如何使用IntelliJAEM IDEA開發專案](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用Proxy伺服器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 現代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

協助建立新專案的工具：

* [AEM 專案原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [拉濟AEM骨模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>下列教學課程可能是啟動新專案的AEM好用：
>[開始使用AEM Sites第1部分——項目設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

