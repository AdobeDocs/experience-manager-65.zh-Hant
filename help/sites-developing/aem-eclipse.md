---
title: AEM Developer Tools for Eclipse
seo-title: AEM Developer Tools for Eclipse
description: 'null'
seo-description: 'null'
uuid: 566e49f2-6f28-4aa7-bfe0-b5f9675310bf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: a2ae76a8-50b0-4e43-b791-ad3be25b8582
translation-type: tm+mt
source-git-commit: 6d216e7521432468a01a29ad2879f8708110d970
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](do-not-localize/chlimage_1-9.png)

## 概覽 {#overview}

AEM Developer Tools for Eclipse是Eclipse外掛程式，以Apache License 2下發行的[Eclipse plugin for Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html)為基礎。

它提供數種功能，讓AEM開發更輕鬆：

* 透過Eclipse Server Connector與AEM例項緊密整合。
* 內容與OSGI組合的同步化。
* 使用程式碼熱交換功能進行除錯支援。
* 透過特定專案建立精靈，簡單引導AEM專案。
* 輕鬆編輯JCR屬性。

## 要求{#requirements}

在使用AEM開發人員工具之前，您必須：

* 下載並安裝[適用於Java EE開發人員的Eclipse IDE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar)。 AEM Developer Tools目前支援Eclipse Kepler或更新版本

* 可與AEM 5.6.1版或更新版本一起使用
* 按照[Eclipse常見問答集](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)中所述，編輯您的`eclipse.ini`設定檔，以設定您的Eclipse安裝以確保您至少擁有1GB的堆積記憶體。

>[!NOTE]
>
>在macOS上，您必須在&#x200B;**Eclipse.app**&#x200B;上按一下滑鼠右鍵，然後選取&#x200B;**顯示封裝內容**，才能找到您的&#x200B;`eclipse.ini`**。**

## 如何安裝AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

完成上述[要求](#requirements)後，您可以按如下方式安裝插件：

1. 瀏覽&#x200B;[**AEM**&#x200B;開發人員工具網站](https://eclipse.adobe.com/aem/dev-tools/)。

1. 複製&#x200B;**安裝連結**。

   請注意，您也可以下載封存檔，而不是使用安裝連結。 這允許離線安裝，但您會漏掉自動更新通知。

1. 在Eclipse中，開啟&#x200B;**Help**&#x200B;功能表。
1. 按一下「安裝新軟體」 ****。
1. 按一下&#x200B;**添加……**。
1. 在&#x200B;**Name**&#x200B;中，輸入AEM Developer Tools。
1. 在&#x200B;**Location**&#x200B;中複製安裝URL。
1. 按一下&#x200B;**確定**。
1. 同時檢查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;增效模組。
1. 按一下&#x200B;**下一步**。
1. 按一下&#x200B;**下一步**。
1. 接受這些線上合約，然後按一下「完成」**。**
1. 按一下&#x200B;**是**&#x200B;以重新啟動Eclipse。

## 如何導入現有項目{#how-to-import-existing-projects}

>[!NOTE]
>
>請參閱[如何從AEM](https://stackoverflow.com/questions/29699726/how-to-work-with-a-bundle-in-eclipse-when-it-was-downloaded-from-aem/29705407#29705407)下載Eclipse中的搭售套件。

## AEM Perspective {#the-aem-perspective}

AEM Development Tools for Eclipse隨附「透視」功能，可讓您完全控制AEM專案和例項。

![chlimage_1-2](assets/chlimage_1-2a.jpeg)

## 多模組項目示例{#sample-multi-module-project}

AEM Developer Tools for Eclipse隨附範例、多模組專案，可協助您快速上手使用Eclipse中的專案設定，並提供數種AEM功能的最佳實務指南。 [進一步瞭解Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)。

請依照下列步驟建立範例專案：

1. 在&#x200B;**File** > **New** > **Project**&#x200B;功能表中，瀏覽至&#x200B;**AEM**&#x200B;區段並選取&#x200B;**AEM Sample Multi-Module Project**。

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. 按一下&#x200B;**下一步**。

   >[!NOTE]
   >
   >這個步驟可能需要一段時間，因為m2eclipse需要掃描原型型錄。

   ![chlimage_1-70](assets/chlimage_1-70a.png)

1. 選擇&#x200B;**com.adobe.granite.archetypes:樣本——項目——原型：（最高數）**，然後按一下&#x200B;**Next**。

   ![chlimage_1-71](assets/chlimage_1-71a.png)

1. 填入範例專案的&#x200B;**名稱**、**群組ID**&#x200B;和&#x200B;**工件ID**。 您也可以選擇設定一些進階屬性。

   ![chlimage_1-72](assets/chlimage_1-72a.png)

1. 然後，您應設定Eclipse將連線至的AEM伺服器。

   若要使用除錯程式功能，您必須在除錯模式中啟動AEM —— 這可透過將下列項目新增至命令列來達成：

   ```
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![chlimage_1-73](assets/chlimage_1-73a.png)

1. 按一下&#x200B;**完成**。 將建立項目結構。

   >[!NOTE]
   >
   >在全新安裝中(更具體而言：從未下載過依賴項時)，您可能會建立出錯誤的項目。 在這種情況下，請遵循[解決無效項目定義](#resolving-invalid-project-definition)中描述的過程。

## 疑難排解 {#troubleshooting}

### 解決無效的項目定義{#resolving-invalid-project-definition}

要解決無效的從屬關係和項目定義，請按如下步驟進行：

1. 選取所有已建立的專案。
1. 按一下右鍵。 在菜單&#x200B;**Maven**&#x200B;中，選擇&#x200B;**更新項目**。
1. 檢查&#x200B;**強制更新快照／版本**。
1. 按一下&#x200B;**「確定」**。Eclipse會嘗試下載所需的相依性。

### 在JSP檔案{#enabling-tag-library-autocompletion-in-jsp-files}中啟用標籤庫自動完成

標籤庫自動完成功能不會立即生效，因為專案中已新增適當的相依性。 使用AEM Uber Jar時有一個已知問題，其中不包含所需的tld和TagExtraInfo檔案。

若要解決這個問題，請確定org.apache.sling.scripting.jsp.taglib工件位於AEM Uber Jar之前的類路徑中。 對於Maven項目，請在pom.xml中將下列相依性置於Uber Jar之前。

```xml
<dependency>
  <groupId>org.apache.sling</groupId>
  <artifactId>org.apache.sling.scripting.jsp.taglib</artifactId>
  <scope>provided</scope>
</dependency>
```

請確定新增適合您部署AEM的版本。

## 更多資訊{#more-information}

Eclipse網站的Apache Sling IDE官方工具提供您有用的資訊：

* [**Apache Sling IDE工具的Eclipse**&#x200B;使用指南](https://sling.apache.org/documentation/development/ide-tooling.html)，本檔案將引導您瞭解AEM Development Tools支援的整體概念、伺服器整合和部署功能。
* [疑難排解部分](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)。
* [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)。

以下正式的[Eclipse](https://eclipse.org/)文檔可幫助設定環境：

* [Eclipse快速入門](https://eclipse.org/users/)
* [Eclipse Luna幫助系統](https://help.eclipse.org/luna/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)

