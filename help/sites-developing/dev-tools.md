---
title: 開發工具
seo-title: Development Tools
description: 要開發JCR、Apache Sling或應用AEM程式，可使用許多工具集
seo-description: To develop your JCR, Apache Sling or AEM applications, a number of tool sets are available
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: 4967a6d9ad92272a1ff442456fe65de51cc46a73
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 3%

---

# 開發工具{#development-tools}

要開發JCR、Apache Sling或應用AEM程式，可使用以下工具集：

* 一組 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) 和WebDAV。 CRXDE Lite嵌入到CRX/AEM中，使您能夠在瀏覽器中執行標準開發任務。 使用CRXDE Lite，可以建立和編輯檔案(如.jsp和.java)、資料夾、模板、元件、對話框、節點、屬性和捆綁包，同時記錄和與SVN整合。

   當您沒有直接訪問CRX/AEM伺服器、通過擴展或修改現成元件和Java捆綁包開發應用程式或不需要專用調試器、代碼完成和語法突出顯示時，建議使用CRXDE Lite。

* 一組由整合開發環境組成(例如： [日蝕](/help/sites-developing/howto-projects-eclipse.md) 或 [智慧J](/help/sites-developing/ht-intellij.md))，生成工具(例如： [阿帕奇·馬文](/help/sites-developing/ht-projects-maven.md))，通過Adobe開發的FileVault，將儲存庫映射到檔案系統，即版本控制系統(例如：Subversion)，錯誤跟蹤器系統(例如：Jira)，一個中央依賴關係管理系統(例如：Apache Archiva)和生成自動化系統(例如：Apache Continuum)。

   此安裝程式允許您將應用程式（內容、代碼、配置）完全整合到任何開發環境和流程中。不同元素之間的連結是通過FileVault對儲存庫進行檔案系統表示，因為上述所有開發工具都可以使用檔案。

## 整合開發環境的擴展 {#extensions-for-integrated-development-environments}

Adobe發佈了以下擴展：

* [Eclipse擴AEM展](/help/sites-developing/aem-eclipse.md)
* [括弧AEM擴展](/help/sites-developing/aem-brackets.md)

### 其他工具 {#other-tools}

AEM與其他促進發展的工具一起：

* [對話框編輯器](/help/sites-developing/dialog-editor.md)
* [使用翻譯器管理詞典](/help/sites-developing/i18n-translator.md)
* [使用Maven管理包](/help/sites-developing/vlt-mavenplugin.md)
* [如何利用EclipseAEM開發項目](/help/sites-developing/howto-projects-eclipse.md)
* [如何使用Apache AEM Maven生成項目](/help/sites-developing/ht-projects-maven.md)
* [如何利用IntelliJ IDEAAEM開發項目](/help/sites-developing/ht-intellij.md)
* [如何使用VLT工具](/help/sites-developing/ht-vlttool.md)
* [如何使用代理伺服器工具](/help/sites-developing/ht-proxy-server.md)
* [AEM 現代化工具](/help/sites-developing/modernization-tools.md)
* [AEM Repo Tool](/help/sites-developing/aem-repo-tool.md)

方便建立新項目的工具：

* [AEM 專案原型](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [拉濟AEM骨模板](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>下面的教程可能對啟動新項目AEM有意義：
>[AEM Sites入門第1部分 — 項目設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
