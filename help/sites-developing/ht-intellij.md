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
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---


# 如何使用IntelliJ IDEA{#how-to-develop-aem-projects-using-intellij-idea}開發AEM專案

## 概覽 {#overview}

若要開始使用IntelliJ上的AEM開發，必須執行下列步驟。

在本「操作說明」的其餘章節中，將詳細說明每項說明。

* 安裝IntelliJ
* 根據Maven設定您的AEM專案
* 在Maven POM中準備IntelliJ的JSP支援
* 將Maven專案匯入IntelliJ

>[!NOTE]
>
>本指南以IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1為基礎。

### 安裝IntelliJ IDEA {#install-intellij-idea}

從JetBrains[的「下載」頁面下載IntelliJ IDEA。](https://www.jetbrains.com/idea/download/index.html)

然後，請依照該頁上的安裝指示進行。

### 根據Maven {#set-up-your-aem-project-based-on-maven}設定您的AEM專案

接著，使用Maven來設定專案，如[使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案中所述。

若要開始在IntelliJ IDEA中使用AEM專案，[Getting Started in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)中的基本設定已足夠。

### 準備IntelliJ IDEA {#prepare-jsp-support-for-intellij-idea}的JSP支援

此外，IntelliJ IDEA也可提供使用JSP的支援，例如

* 自動完成標籤庫
* 對`<cq:defineObjects />`和`<sling:defineObjects />`所定義對象的感知

為了讓AEM項目正常運作，請依照[使用Apache Maven](/help/sites-developing/ht-projects-maven.md)建立AEM專案中[使用JSP](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)的說明操作。

### 匯入Maven專案{#import-the-maven-project}

1. 在IntelliJ IDEA中開啟&#x200B;**Import**&#x200B;對話方塊，方式為

   * 如果尚未開啟任何項目，請在歡迎螢幕上選擇&#x200B;**導入項目**
   * 從主菜單中選擇&#x200B;**檔案->導入項目**

1. 在「導入」對話框中，選擇項目的POM檔案。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 繼續使用下列對話方塊中顯示的預設設定。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 按一下&#x200B;**Next**&#x200B;和&#x200B;**Finish**&#x200B;繼續進行以下對話框。
1. 您現在已設定使用IntelliJ IDEA進行AEM開發

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA {#debugging-jsps-with-intellij-idea}除錯JSP

使用IntelliJ IDEA除錯JSP時，必須執行下列步驟

* 在專案中設定Web Facet
* 安裝JSR45支援外掛程式
* 設定除錯設定檔
* 設定AEM的除錯模式

#### 在項目{#set-up-a-web-facet-in-the-project}中設定Web Facet

IntelliJ IDEA需要瞭解在何處尋找JSP以進行除錯。 由於IDEA無法解譯`content-package-maven-plugin`設定，因此需要手動設定。

1. 轉到&#x200B;**檔案->項目結構**
1. 選擇&#x200B;**Content**&#x200B;模組
1. 按一下模組清單上方的&#x200B;**+** ，然後選擇&#x200B;**Web**
1. 作為Web資源目錄，選擇項目的`content/src/main/content/jcr_root subdirectory`，如下面螢幕抓圖所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安裝JSR45支援插件{#install-the-jsr-support-plugin}

1. 前往IntelliJ IDEA設定的&#x200B;**Plugins**&#x200B;窗格
1. 導覽至&#x200B;**JSR45 Integration** Plugin並選取其旁的核取方塊
1. 按一下&#x200B;**Apply**
1. 當要求重新啟動IntelliJ IDEA時，請

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 配置調試配置檔案{#configure-a-debug-profile}

1. 轉至&#x200B;**運行->編輯配置**
1. 按一下&#x200B;**+**&#x200B;並選擇&#x200B;**JSR45 Remote**
1. 在配置對話框中，選擇&#x200B;**應用程式伺服器**&#x200B;旁邊的&#x200B;**配置** ，並配置通用伺服器
1. 如果您想在開始除錯時開啟瀏覽器，請將開始頁面設為適當的URL
1. 刪除所有&#x200B;**在啟動**&#x200B;任務之前（如果您使用vlt autosync），或在不使用vlt autosync時配置適當的Maven任務
1. 在&#x200B;**啟動／連接**&#x200B;窗格上，根據需要調整埠
1. 複製IntelliJ IDEA所建議的命令行參數

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 設定AEM進行除錯模式{#configure-aem-for-debug-mode}

最後一個必要步驟是使用IntelliJ IDEA建議的JVM選項來啟動AEM。

您可以直接啟動AEM jar檔案並新增這些選項，例如使用下列命令列：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart-5.6.1.jar`

您也可以將這些選項新增至`crx-quickstart/bin/start`的開始指令碼，如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -XX:MaxPermSize=256M -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 開始調試{#start-debugging}

您現在都已設定好在AEM中除錯JSP。

1. 選擇&#x200B;**運行->調試->調試配置檔案**
1. 在元件程式碼中設定中斷點
1. 在瀏覽器中存取頁面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA {#debugging-bundles-with-intellij-idea}除錯套件

使用標準的一般遠端除錯連線，可除錯組合中的程式碼。 您可依照[Jetbrain說明檔案進行遠端除錯](https://www.jetbrains.com/idea/webhelp/run-debug-configuration-remote.html)。
