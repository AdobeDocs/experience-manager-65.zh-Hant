---
title: 如何利用IntelliJ IDEAAEM開發項目
description: 使用IntelliJ IDEA開發項AEM目
uuid: 382b5008-2aed-4e08-95be-03c48f2b549e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: df6410a2-794e-4fa2-ae8d-37271274d537
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# 如何利用IntelliJ IDEAAEM開發項目{#how-to-develop-aem-projects-using-intellij-idea}

## 概觀 {#overview}

要開始在AEMIntelliJ上開發，需要以下步驟。

本主題的其餘部分將更詳細地說明每個步驟。

* 安裝IntelliJ
* 基於Maven設AEM置項目
* 在Maven POM中為IntelliJ準備JSP支援
* 將Maven項目導入IntelliJ

>[!NOTE]
>
>本指南基於IntelliJ IDEA旗艦版12.1.4和5.6.1。

### 安裝IntelliJ IDEA {#install-intellij-idea}

從下載IntelliJ IDEA [JetBrains的下載頁面](https://www.jetbrains.com/idea/download/)。

然後，按照該頁上的安裝說明進行操作。

### 基於Maven設AEM置項目 {#set-up-your-aem-project-based-on-maven}

接下來，使用Maven設定項目，如中所述 [使用Apache Maven構建AEM項目的方法](/help/sites-developing/ht-projects-maven.md)。

要開始在AEMIntelliJ IDEA中使用項目， [5分鐘後開始](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 足夠了。

### 準備IntelliJ IDEA的JSP支援 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA還可以在使用JSP時提供支援，例如：

* 自動完成標籤庫
* 對由定義的對象的感知 `<cq:defineObjects />` 和 `<sling:defineObjects />`

要使其工作，請按照 [如何使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 在 [使用Apache Maven構建AEM項目的方法](/help/sites-developing/ht-projects-maven.md)。

### 導入Maven項目 {#import-the-maven-project}

1. 開啟 **導入** 對話框

   * 選擇 **導入項目** 在「歡迎」螢幕上，如果尚未開啟項目
   * 選擇 **檔案 — >導入項目** 菜單

1. 在「導入」對話框中，選擇項目的POM檔案。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 繼續使用以下對話框中顯示的預設設定。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 通過按一下 **下一個** 和 **完成**。
1. 現在，您已使用IntelliJ IDEAAEM設定為開發

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA調試JSP {#debugging-jsps-with-intellij-idea}

使用IntelliJ IDEA調試JSP時需要以下步驟

* 在項目中設定Web方面
* 安裝JSR45支援插件
* 配置調試配置檔案
* 配置AEM調試模式

#### 在項目中設定Web方面 {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA必須瞭解在何處查找用於調試的JSP。 因為IDEA無法解釋 `content-package-maven-plugin` 設定，必須手動配置。

1. 轉到 **檔案 — >項目結構**
1. 選擇 **內容** 模組
1. 按一下 **+** 並選擇 **Web**
1. 作為Web資源目錄，選擇 `content/src/main/content/jcr_root subdirectory` 螢幕截圖中顯示的。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安裝JSR45支援插件 {#install-the-jsr-support-plugin}

1. 轉到 **插件** IntelliJ IDEA設定中的窗格
1. 導航到 **JSR45整合** 插件，並選中它旁邊的複選框
1. 按一下 **應用**
1. 請求時重新啟動IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 配置調試配置檔案 {#configure-a-debug-profile}

1. 轉到 **運行 — >編輯配置**
1. 擊 **+** 選擇 **JSR45遠程**
1. 在配置對話框中，選擇 **配置** 下 **應用程式伺服器** 並配置通用伺服器
1. 如果要在開始調試時開啟瀏覽器，請將起始頁設定為相應的URL
1. 全部刪除 **啟動前** 任務（如果您使用vlt autosync），或配置相應的Maven任務（如果您不使用vlt autosync）
1. 在 **啟動/連接** 窗格，如有必要，調整埠
1. 複製IntelliJ IDEA建議的命令行參數

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 配置AEM調試模式 {#configure-aem-for-debug-mode}

最後一步是從IntelliJ IDEA提AEM議的JVM選項開始。

直接啟AEM動jar檔案並添加這些選項，例如使用以下命令行：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

您也可以將這些選項添加到中的開始指令碼 `crx-quickstart/bin/start` 如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 開始調試 {#start-debugging}

現在，您已設定為在中調試JSPAEM。

1. 選擇 **運行 — >調試 — >調試配置檔案**
1. 在元件代碼中設定斷點
1. 在瀏覽器中訪問頁面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA調試捆綁包 {#debugging-bundles-with-intellij-idea}

可以使用標準通用遠程調試連接調試捆綁包中的代碼。 您可以 [關於遠程調試的Jetbrain文檔](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter)。
