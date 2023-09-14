---
title: Eclipse 適用的 AEM 開發人員工具
description: Eclipse 適用的 AEM 開發人員工具
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 8336a7257d3c5e75cd37381b0124c227c2d55dca
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 4%

---

# Eclipse 適用的 AEM 開發人員工具{#aem-developer-tools-for-eclipse}

![適用於Eclipse的AEM開發人員工具的圓形影像主題。](do-not-localize/chlimage_1-9.png)

## 概觀 {#overview}

「AEM Developer Tools」是一個以 [Apache Sling的Eclipse外掛程式](https://sling.apache.org/documentation/development/ide-tooling.html) 以Apache授權2發行。

它提供數項功能，讓AEM開發更容易：

* 透過Eclipse伺服器聯結器與AEM執行個體緊密整合。
* 內容和OSGI套件組合的同步。
* 使用程式碼熱交換功能提供除錯支援。
* 透過特定專案建立精靈，簡單BootstrapAEM專案。
* 輕鬆編輯JCR屬性。

## 要求 {#requirements}

使用AEM開發人員工具之前，請先執行下列動作：

* 下載並安裝 [適用於Java™ EE開發人員的Eclipse IDE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). AEM開發人員工具目前支援Eclipse Kepler或更新版本

* 可搭配AEM 5.6.1或更新版本使用
* 設定eclipse安裝，透過編輯您的檔案，確保您至少有1 GB的棧積記憶體 `eclipse.ini` 組態檔，如 [Eclipse常見問題集](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>在macOS上按一下右鍵 **Eclipse.app**，然後選取 **顯示封裝內容** 以尋找您的 `eclipse.ini`.

## 如何安裝適用於Eclipse的AEM開發人員工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

當您完成 [需求](#requirements) 如上所示，您可以安裝外掛程式：

1. 瀏覽 **AEM Developer Tools** 網站位置 `https://eclipse.adobe.com/aem/dev-tools/`.

1. 複製 **安裝連結**.

   或者，您也可以下載封存，而不使用安裝連結。 這樣做允許離線安裝，但您會遺漏自動更新通知。

1. 在Eclipse中，開啟 **說明** 功能表。
1. 按一下 **安裝新軟體**.
1. 按一下 **新增……**.
1. 在 **名稱** 輸入AEM Developer Tools。
1. 在 **位置** 複製安裝URL
1. 按一下 **確定**.
1. 檢查兩者 **AEM** 和 **Sling** 外掛程式。
1. 按一下「**下一步**」。
1. 按一下「**下一步**」。
1. 接受線上合約，然後按一下 **完成**.
1. 按一下 **是** 以重新啟動Eclipse。

## 如何匯入現有的專案 {#how-to-import-existing-projects}

>[!NOTE]
>
>另請參閱 [如何在Eclipse中使用從AEM下載的套件組合](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM觀點 {#the-aem-perspective}

Eclipse適用的AEM開發工具隨附的透視功能可讓您完全控制AEM專案和執行個體。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 多模組專案範例 {#sample-multi-module-project}

「AEM開發人員工具」包含範例、多模組專案，可幫助您在Eclipse中快速完成專案設定。 它也是幾項AEM功能的最佳實務指南。 [進一步瞭解專案原型](https://github.com/adobe/aem-project-archetype).

若要建立範例專案，請完成以下步驟：

1. 在 **檔案** > **新增** > **專案** 功能表，瀏覽至 **AEM** 區段並選取 **AEM範例多模組專案**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 按一下「**下一步**」。

   >[!NOTE]
   >
   >此步驟可能需要一點時間，因為m2eclipse必須掃描原型目錄。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 選擇 **com.adobe.granite.archetypes ： sample-project-archetype ： （最高數字）** 在功能表中，然後按一下 **下一個**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 填入 **名稱**， **群組ID**，以及 **成品ID** 以取得範例專案。 您也可以選擇設定一些進階屬性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 現在設定Eclipse可連線的AEM伺服器。

   若要使用偵錯工具功能，請確定您是以偵錯模式啟動AEM，方法是在命令列新增下列內容：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 按一下 **完成**. 專案結構隨即建立。

   >[!NOTE]
   >
   >在全新安裝中（更具體地說：從未下載過maven相依性時），您可能會收到建立專案的錯誤。 在這種情況下，請遵循中所述的程式 [解析無效的專案定義](#resolving-invalid-project-definition).

## 疑難排解 {#troubleshooting}

### 解析無效的專案定義 {#resolving-invalid-project-definition}

若要解決無效的相依性和專案定義，請依照下列步驟進行：

1. 選取所有已建立的專案。
1. 按一下滑鼠右鍵。 在功能表中 **Maven**，選取 **更新專案**.
1. 檢查 **強制更新快照/版本**.
1. 按一下&#x200B;**「確定」**。Eclipse會嘗試下載必要的相依性。

### 在JSP檔案中啟用標籤庫自動完成 {#enabling-tag-library-autocompletion-in-jsp-files}

只要將適當的相依性新增至專案，標籤程式庫自動完成功能即可立即運作。 使用AEM Uber Jar時，有一個已知問題，其中不包含所需的tld和TagExtraInfo檔案。

若要解決此問題，請確保org.apache.sling.scripting.jsp.taglib成品在AEM Uber Jar之前的類別路徑中。 對於Maven專案，請將以下相依性放在pom.xml中的Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

請務必新增正確版本的AEM部署。

## 詳細資訊 {#more-information}

Eclipse網站的官方Apache Sling IDE工具提供您實用資訊：

* 此 [**適用於Eclipse的Apache Sling IDE工具** 使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)，本檔案會引導您瞭解AEM開發工具支援的整體概念、伺服器整合和部署功能。
* 此 [疑難排解章節](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* 此 [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

下列官方 [Eclipse](https://www.eclipse.org/) 說明檔案有助於設定您的環境：

* [Eclipse快速入門](https://eclipseide.org/getting-started/)
* [Eclipse Luna說明系統](https://help.eclipse.org/latest/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
