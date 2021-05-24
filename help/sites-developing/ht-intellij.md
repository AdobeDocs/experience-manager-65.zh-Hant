---
title: 如何使用IntelliJ IDEA開發AEM專案
seo-title: 如何使用IntelliJ IDEA開發AEM專案
description: 使用IntelliJ IDEA開發AEM專案
seo-description: 使用IntelliJ IDEA開發AEM專案
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# 如何使用IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}開發AEM專案

## 概覽 {#overview}

若要開始使用IntelliJ上的AEM開發，需執行下列步驟。

在本作法的其餘部分中，會更詳細地說明每個選項。

* 安裝IntelliJ
* 根據Maven設定AEM專案
* 在Maven POM中準備IntelliJ的JSP支援
* 將Maven專案匯入IntelliJ

>[!NOTE]
>
>本指南以IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1為基礎。

### 安裝IntelliJ IDEA {#install-intellij-idea}

從JetBrains](https://www.jetbrains.com/idea/download/index.html)的「下載」頁面下載IntelliJ IDEA。[

接著，請依照該頁面上的安裝指示操作。

### 根據Maven {#set-up-your-aem-project-based-on-maven}設定AEM專案

接下來，使用Maven設定專案，如[How-To Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md)中所述。

若要開始在IntelliJ IDEA中使用AEM專案，[5分鐘後快速入門](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)中的基本設定已足夠。

### 準備IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}的JSP支援

IntelliJ IDEA也可提供使用JSP的支援，例如

* 自動完成標籤庫
* 對`<cq:defineObjects />`和`<sling:defineObjects />`所定義對象的感知

為了讓此功能發揮作用，請按照[How-To With JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)中的[說明，使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案。

### 導入Maven項目{#import-the-maven-project}

1. 開啟IntelliJ IDEA中的&#x200B;**Import**&#x200B;對話框，方法為

   * 如果您尚未開啟任何專案，請在歡迎畫面上選取&#x200B;**匯入專案**
   * 從主菜單中選擇&#x200B;**檔案 — >導入項目**

1. 在「匯入」對話方塊中，選取專案的POM檔案。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 繼續進行下列對話方塊中顯示的預設設定。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 按一下&#x200B;**Next**&#x200B;和&#x200B;**Finish**，繼續進行以下對話。
1. 您現在已透過IntelliJ IDEA設定為AEM開發

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA {#debugging-jsps-with-intellij-idea}調試JSP

使用IntelliJ IDEA調試JSP時需要執行以下步驟

* 在專案中設定Web面向
* 安裝JSR45支援外掛程式
* 設定除錯設定檔
* 設定AEM以進行除錯模式

#### 在項目{#set-up-a-web-facet-in-the-project}中設定Web面

IntelliJ IDEA需要了解在何處查找用於調試的JSP。 由於IDEA無法解譯`content-package-maven-plugin`設定，因此需要手動配置。

1. 轉至&#x200B;**檔案 — >項目結構**
1. 選擇&#x200B;**Content**&#x200B;模組
1. 按一下模組清單上方的&#x200B;**+**&#x200B;並選擇&#x200B;**Web**
1. 作為Web資源目錄，選擇項目的`content/src/main/content/jcr_root subdirectory`，如下面螢幕快照所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安裝JSR45支援插件{#install-the-jsr-support-plugin}

1. 轉到IntelliJ IDEA設定中的&#x200B;**插件**&#x200B;窗格
1. 導覽至&#x200B;**JSR45 Integration** Plugin ，並選取其旁的核取方塊
1. 按一下&#x200B;**Apply**
1. 請求重新啟動IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 配置調試配置檔案{#configure-a-debug-profile}

1. 轉至&#x200B;**Run -> Edit Configurations**
1. 點擊&#x200B;**+**&#x200B;並選擇&#x200B;**JSR45 Remote**
1. 在配置對話框中，選擇&#x200B;**應用程式伺服器**&#x200B;旁邊的&#x200B;**配置**&#x200B;並配置通用伺服器
1. 如果您想在開始偵錯時開啟瀏覽器，請將啟動頁面設為適當的URL
1. 如果使用vlt autosync，請刪除所有&#x200B;**啟動前**&#x200B;任務；如果不使用vlt autosync，請配置適當的Maven任務
1. 在&#x200B;**啟動/連接**&#x200B;窗格上，根據需要調整埠
1. 複製IntelliJ IDEA提出的命令行參數

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 配置AEM的調試模式{#configure-aem-for-debug-mode}

最後一個步驟是使用IntelliJ IDEA提議的JVM選項啟動AEM。

您可以直接啟動AEM jar檔案並新增這些選項（例如使用下列命令列）來執行此操作：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

您也可以將這些選項新增至`crx-quickstart/bin/start`中的開始指令碼，如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 啟動調試{#start-debugging}

現在，您都已設定為在AEM中調試JSP。

1. 選擇&#x200B;**運行 — >調試 — >您的調試配置檔案**
1. 在元件代碼中設定斷點
1. 在瀏覽器中存取頁面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA {#debugging-bundles-with-intellij-idea}調試套件組合

可以使用標準通用遠程調試連接調試套件中的代碼。 您可以依照[Jetbrain檔案進行遠端除錯](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)。
