---
title: Eclipse 適用的 AEM 開發人員工具
seo-title: AEM Developer Tools for Eclipse
description: Eclipse 適用的 AEM 開發人員工具
seo-description: null
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
exl-id: 00473769-c447-4966-a71e-117c669e0151
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 4%

---

# Eclipse 適用的 AEM 開發人員工具{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概觀 {#overview}

「AEM開發人員工具」是以 [適用於Apache Sling的Eclipse外掛程式](https://sling.apache.org/documentation/development/ide-tooling.html) 依Apache授權2發行。

它提供數種可讓AEM開發更輕鬆的功能：

* 透過Eclipse Server Connector與AEM執行個體緊密整合。
* 內容和OSGI套件組合的同步。
* 使用程式碼熱交換功能進行除錯支援。
* 透過特定專案建立精靈，輕鬆BootstrapAEM專案。
* 輕鬆編輯JCR屬性。

## 要求 {#requirements}

使用AEM開發人員工具之前，請執行下列操作：

* 下載並安裝 [適用於Java™ EE開發人員的Eclipse IDE](https://www.eclipse.org/downloads/packages/release/luna/r/eclipse-ide-java-ee-developers). AEM開發人員工具目前支援Eclipse Kepler或更新版本

* 可與AEM 5.6.1版或更新版本搭配使用
* 通過編輯您的 `eclipse.ini` 組態檔，如 [Eclipse常見問題集](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F).

>[!NOTE]
>
>在macOS上，按一下滑鼠右鍵 **Eclipse.app**，然後選取 **顯示包內容** 找到 `eclipse.ini`.

## 如何安裝AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

完成 [需求](#requirements) 如上所述，您可以依照下列方式安裝外掛程式：

1. 瀏覽 **AEM開發人員工具** 網站 `https://eclipse.adobe.com/aem/dev-tools/`.

1. 複製 **安裝連結**.

   或者，您也可以下載封存，而不是使用安裝連結。 這樣可允許離線安裝，但您遺漏了自動更新通知。

1. 在Eclipse中，開啟 **說明** 功能表。
1. 按一下 **安裝新軟體**.
1. 按一下 **添加……**.
1. 在 **名稱** 輸入AEM開發人員工具。
1. 在 **位置** 複製安裝URL。
1. 按一下 **確定**.
1. 檢查兩者 **AEM** 和 **Sling** 外掛程式。
1. 按一下&#x200B;**下一步**。
1. 按一下&#x200B;**下一步**。
1. 接受這些協定，然後按一下 **完成**.
1. 按一下 **是** 重新啟動Eclipse。

## 如何匯入現有專案 {#how-to-import-existing-projects}

>[!NOTE]
>
>請參閱 [如何從AEM下載套件組合時，在Eclipse中加以運作](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407).

## AEM透視 {#the-aem-perspective}

Eclipse適用的AEM開發工具隨附透視，可讓您完全控制AEM專案和例項。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 多模組專案範例 {#sample-multi-module-project}

「AEM開發人員工具」包含範例、多模組專案，可協助您快速上手，在Eclipse中設定專案。 此外，也是數種AEM功能的最佳實務指南。 [深入了解專案原型](https://github.com/adobe/aem-project-archetype).

若要建立範例專案，請完成下列步驟：

1. 在 **檔案** > **新增** > **專案** 菜單，瀏覽到 **AEM** 區段，然後選取 **AEM範例多模組專案**.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 按一下&#x200B;**下一步**。

   >[!NOTE]
   >
   >此步驟可能需要一些時間，因為m2eclipse必須掃描原型目錄。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 選擇 **com.adobe.granite.archetypes :sample-project-archetype :（最高數）** 按一下功能表中的 **下一個**.

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 填入 **名稱**, **群組ID**，和 **工件ID** ，以取得範例專案。 您也可以選擇設定一些進階屬性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 現在設定AEM伺服器，讓Eclipse可以連線至。

   若要使用除錯程式功能，請務必在除錯模式中啟動AEM，這可借由將下列項目新增至命令列來達成：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 按一下 **完成**. 項目結構隨即建立。

   >[!NOTE]
   >
   >在全新安裝上(具體說明：從未下載maven相依性時)，您可能會獲得建立的專案並發生錯誤。 在此情況下，請依照 [解決無效的項目定義](#resolving-invalid-project-definition).

## 疑難排解 {#troubleshooting}

### 解決無效的項目定義 {#resolving-invalid-project-definition}

要解析無效的依賴項，項目定義將按以下步驟進行：

1. 選取所有已建立的專案。
1. 按一下右鍵。 在功能表中 **馬文**，選取 **更新專案**.
1. 檢查 **強制更新快照/版本**.
1. 按一下&#x200B;**「確定」**。Eclipse會嘗試下載所需的相依性。

### 在JSP檔案中啟用標籤庫自動完成 {#enabling-tag-library-autocompletion-in-jsp-files}

在專案中新增了適當的相依性時，標籤程式庫自動完成功能會立即運作。 使用AEM Uber Jar時有一個已知問題，其中不包含所需的tld和TagExtraInfo檔案。

若要解決此問題，請確定org.apache.sling.scripting.jsp.taglib工件位於AEM Uber Jar之前的類路徑中。 若為Maven專案，請將下列相依性放入pom.xml中，放在Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

請務必為部署的AEM新增正確版本。

## 詳細資訊 {#more-information}

適用於Eclipse網站的官方Apache Sling IDE工具可提供您實用的資訊：

* 此 [**適用於Eclipse的Apache Sling IDE工具** 使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)，本檔案會逐步引導您了解AEM開發工具所支援的整體概念、伺服器整合和部署功能。
* 此 [疑難排解區段](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* 此 [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

以下官員 [Eclipse](https://www.eclipse.org/) 說明檔案可協助您設定環境：

* [Eclipse快速入門](https://www.eclipse.org/getting-started/)
* [Eclipse Luna幫助系統](https://help.eclipse.org/latest/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
