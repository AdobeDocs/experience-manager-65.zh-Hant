---
title: 如何使用IntelliJ IDEA開發AEM專案
description: 瞭解如何使用IntelliJ IDEA開發Adobe Experience Manager專案。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 5a79c79b-df65-4cb2-b9d4-eda994c992ec
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 2%

---

# 如何使用IntelliJ IDEA開發AEM專案{#how-to-develop-aem-projects-using-intellij-idea}

## 概觀 {#overview}

若要開始使用IntelliJ上的AEM開發，必須執行下列步驟。

本主題的其餘部分將更詳細地說明每個步驟。

* 安裝IntelliJ
* 根據Maven設定您的AEM專案
* 在Maven POM中為IntelliJ準備JSP支援
* 將Maven專案匯入IntelliJ

>[!NOTE]
>
>本指南以IntelliJ IDEA Ultimate Edition 12.1.4和AEM 5.6.1為基礎。

### 安裝IntelliJ IDEA {#install-intellij-idea}

從[JetBrains](https://www.jetbrains.com/idea/download/)的「下載」頁面下載IntelliJ IDEA。

然後，請依照該頁面上的安裝指示操作。

### 根據Maven設定您的AEM專案 {#set-up-your-aem-project-based-on-maven}

接下來，使用Maven設定您的專案，如[使用Apache Maven建置AEM專案的方法](/help/sites-developing/ht-projects-maven.md)中所述。

若要在IntelliJ IDEA中開始使用AEM專案，[在5分鐘後開始使用](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html)中的基本設定已足夠。

### 為IntelliJ IDEA準備JSP支援 {#prepare-jsp-support-for-intellij-idea}

IntelliJ IDEA也支援使用JSP，例如：

* 自動完成標籤程式庫
* `<cq:defineObjects />`與`<sling:defineObjects />`所定義的物件感知

若要讓此功能發揮作用，請依照[使用Apache Maven建置AEM專案的方法](/help/sites-developing/ht-projects-maven.md)中[使用JSP的方法](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)的指示。

### 匯入Maven專案 {#import-the-maven-project}

1. 開啟IntelliJ IDEA中的&#x200B;**匯入**&#x200B;對話方塊，方法為

   * 在歡迎熒幕上選取&#x200B;**匯入專案** （如果您尚未開啟專案）
   * 從主功能表選取&#x200B;**檔案>匯入專案**

1. 在「匯入」對話方塊中，選取專案的POM檔案。

   ![chlimage_1-45](assets/chlimage_1-45a.png)

1. 繼續使用預設設定，如下方對話方塊所示。

   ![chlimage_1-46](assets/chlimage_1-46a.png)

1. 按一下&#x200B;**下一步**&#x200B;和&#x200B;**完成**，繼續下列對話方塊。
1. 您現在已使用IntelliJ IDEA設定AEM開發

   ![chlimage_1-47](assets/chlimage_1-47a.png)

### 使用IntelliJ IDEA除錯JSP {#debugging-jsps-with-intellij-idea}

使用IntelliJ IDEA偵錯JSP時，必須執行下列步驟

* 在專案中設定Web Facet
* 安裝JSR45支援外掛程式
* 設定除錯設定檔
* 針對偵錯模式設定AEM

#### 在專案中設定Web Facet {#set-up-a-web-facet-in-the-project}

IntelliJ IDEA必須瞭解在哪裡可以找到JSP以進行偵錯。 由於IDEA無法解譯`content-package-maven-plugin`設定，因此必須手動設定。

1. 移至&#x200B;**檔案>專案結構**
1. 選取&#x200B;**內容**&#x200B;模組
1. 按一下模組清單上方的&#x200B;**+**，然後選取&#x200B;**網頁**
1. 在Web資源目錄中，選取專案的`content/src/main/content/jcr_root subdirectory`，如下方熒幕擷圖所示。

![chlimage_1-48](assets/chlimage_1-48a.png)

#### 安裝JSR45支援外掛程式 {#install-the-jsr-support-plugin}

1. 移至IntelliJ IDEA設定中的&#x200B;**外掛程式**&#x200B;窗格
1. 導覽至&#x200B;**JSR45整合**&#x200B;外掛程式，並選取其旁邊的核取方塊
1. 按一下&#x200B;**套用**
1. 請求時重新啟動IntelliJ IDEA

![chlimage_1-49](assets/chlimage_1-49a.png)

#### 設定除錯設定檔 {#configure-a-debug-profile}

1. 移至&#x200B;**執行>編輯設定**
1. 點選&#x200B;**+**&#x200B;並選取&#x200B;**JSR45 Remote**
1. 在設定對話方塊中，選取&#x200B;**應用程式伺服器**&#x200B;旁的&#x200B;**設定**&#x200B;並設定一般伺服器
1. 如果您要在開始偵錯時開啟瀏覽器，請將起始頁面設定為適當的URL
1. 如果您使用vlt autosync，請移除所有&#x200B;**啟動前**&#x200B;工作；如果您未使用，請設定適當的Maven工作
1. 在&#x200B;**啟動/連線**&#x200B;窗格中，視需要調整連線埠
1. 複製IntelliJ IDEA建議的命令列引數

![chlimage_1-50](assets/chlimage_1-50a.png) ![chlimage_1-51](assets/chlimage_1-51a.png)

#### 針對偵錯模式設定AEM {#configure-aem-for-debug-mode}

最後一個必要步驟是使用IntelliJ IDEA建議的JVM選項啟動AEM。

直接啟動AEM jar檔案並新增這些選項，例如，使用下列命令列：

`java -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y -Xmx1024m -jar cq-quickstart-6.5.0.jar`

您也可以將這些選項新增到`crx-quickstart/bin/start`中的啟動指令碼，如下所示。

```shell
# ...

# default JVM options
if [ -z "$CQ_JVM_OPTS" ]; then
 CQ_JVM_OPTS='-server -Xmx1024m -Djava.awt.headless=true'
fi

CQ_JVM_OPTS="$CQ_JVM_OPTS -Xdebug -Xrunjdwp:transport=dt_socket,address=58242,suspend=n,server=y"

# ...
```

#### 開始偵錯 {#start-debugging}

您現在已準備好在AEM中偵錯JSP。

1. 選取&#x200B;**執行>偵錯>您的偵錯設定檔**
1. 在元件程式碼中設定中斷點
1. 存取瀏覽器中的頁面

![chlimage_1-52](assets/chlimage_1-52a.png)

### 使用IntelliJ IDEA偵錯套件組合 {#debugging-bundles-with-intellij-idea}

您可以使用標準的通用遠端偵錯連線來偵錯套件中的程式碼。 您可以在遠端偵錯](https://www.jetbrains.com/help/idea/remote-debugging-with-product.html#remote-interpreter)上遵循[Jetbrain檔案。
