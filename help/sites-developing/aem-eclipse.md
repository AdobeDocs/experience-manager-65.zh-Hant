---
title: Eclipse 適用的 AEM 開發人員工具
description: 瞭解Adobe Experience Manager的Eclipse開發人員工具。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 00473769-c447-4966-a71e-117c669e0151
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 5bd621b14e3bcd21431c1df5629fe4669b14052c
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 2%

---


# Eclipse 適用的 AEM 開發人員工具 {#aem-developer-tools-for-eclipse}

![適用於Eclipse標誌的Experience Manager Developer Tools](assets/eclipse-logo.png)

## 概觀 {#overview}

_適用於Eclipse的Experience Manager Developer Tools_&#x200B;是以Apache授權2所發行適用於Apache Sling[的](https://sling.apache.org/documentation/development/ide-tooling.html)Eclipse外掛程式為基礎的Eclipse外掛程式。

它提供數項功能，讓AEM開發更容易：

* 透過Eclipse伺服器聯結器與AEM執行個體緊密整合
* 內容和OSGi套件組合的同步
* 使用程式碼熱交換功能提供除錯支援
* AEM專案的簡單Bootstrap，透過特定專案建立精靈
* 輕鬆編輯JCR屬性

## 要求 {#requirements}

使用AEM開發人員工具之前，您需要：

* 下載並安裝適用於Enterprise Java和Web開發人員的[Eclipse IDE。](https://www.eclipse.org/downloads/packages/)
   * 適用於Eclipse的AEM Developer Tools 1.4.0版相容於Eclipse 2022-12 (4.26)或更新版本，且需要Java 17或更新版本才能執行。
* 依照`eclipse.ini`Eclipse常見問答集[的說明，編輯您的](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)設定檔，設定Eclipse安裝以確保您至少有1 GB的棧積記憶體。

>[!NOTE]
>
>在macOS上，您必須用滑鼠右鍵按一下&#x200B;**Eclipse.app**，然後選取&#x200B;**顯示封裝內容**&#x200B;以尋找您的`eclipse.ini`。

## 如何安裝適用於Eclipse的AEM開發人員工具 {#how-to-install-the-aem-developer-tools-for-eclipse}

當您符合上述[需求](#requirements)時，您可以依照下列方式安裝開發人員工具外掛程式：

1. 開啟[AEM Developer Tools網站。](https://eclipse.adobe.com/)

1. 複製&#x200B;**安裝連結**。

   * 您也可以下載封存，而不使用安裝連結。
   * 此方法允許離線安裝，但您不會收到自動更新通知。

1. 在Eclipse中，開啟&#x200B;**說明**&#x200B;功能表。
1. 按一下&#x200B;**安裝新軟體**。
1. 按一下&#x200B;**新增……**。
1. 在&#x200B;**名稱**&#x200B;欄位中，輸入`AEM Developer Tools`。
1. 在&#x200B;**位置**&#x200B;欄位中，複製安裝URL。
1. 按一下&#x200B;**新增**。
1. 檢查&#x200B;**AEM**&#x200B;和&#x200B;**Sling**&#x200B;外掛程式。
1. 按一下「**下一步**」。
1. 在&#x200B;**安裝詳細資料**&#x200B;視窗中，檢閱要安裝的專案，然後再次按一下&#x200B;**下一步**。
1. 接受授權合約，然後按一下&#x200B;**完成**。
1. 在出現的&#x200B;**信任授權單位**&#x200B;對話方塊中，選取授權單位/網站`https://eclipse.adobe.com`並按一下&#x200B;**信任選取的專案**。
1. 在出現的&#x200B;**信任成品**&#x200B;對話方塊中，選取程式碼簽署者，然後按一下&#x200B;**信任選取的專案**。
1. 按一下&#x200B;**立即重新啟動**&#x200B;以重新啟動Eclipse。

## AEM觀點 {#the-aem-perspective}

在Eclipse中，**透視**&#x200B;會決定視窗中可用的動作和檢視，並可與Eclipse中的資源進行以工作為導向的互動。 如需有關檢視方式的詳細資訊，請參閱[Eclipse檔案。](https://help.eclipse.org/latest/index.jsp)。

適用於Eclipse的&#x200B;_Experience Manager開發工具_&#x200B;提供AEM觀點，讓您完全控制您的AEM專案和執行個體。 若要開啟AEM觀點：

1. 從Eclipse功能表列選取&#x200B;**視窗** > **透視** > **開啟透視** > **其他**。
1. 在對話方塊中選取&#x200B;**AEM**，然後按一下&#x200B;**開啟**。

![Eclipse中的AEM觀點](assets/eclipse-aem-perspective.png)

## 多模組專案範例 {#sample-multi-module-project}

適用於Eclipse的&#x200B;_Experience Manager開發人員工具_&#x200B;隨附範例多模組專案，可協助您快速上手Eclipse中的專案設定。 它也可當作數個AEM功能的最佳實務指南，運用[AEM專案原型。](https://github.com/adobe/aem-project-archetype)

請依照下列步驟建立範例專案：

1. 在&#x200B;**檔案** > **新增** > **專案**&#x200B;功能表中，瀏覽至&#x200B;**AEM**&#x200B;區段並選取&#x200B;**AEM範例多模組專案**。

   ![AEM範例多模組專案](assets/aem-sample-project.png)

1. 按一下「**下一步**」。

   >[!NOTE]
   >
   >此步驟可能需要一些時間，因為[m2eclipse](https://eclipse.dev/m2e/)必須掃描原型目錄。

1. `com.adobe.aem : aem-project-archetype : <highest-number>`應在&#x200B;**Archetype**&#x200B;下拉式清單中自動選取。 視需要選取先前版本。 按一下「**下一步**」。

   ![選取原型版本](assets/select-archetype.png)

1. 為範例專案提供下列欄位：

   * **名稱**
   * **群組識別碼**
   * **成品ID**
   * **appId** — 您可能需要展開&#x200B;**進階**&#x200B;選項才能設定此值。
   * **appTitle** — 您可能需要展開&#x200B;**進階**&#x200B;選項以設定此值。
   * **封裝** — 您可能需要展開&#x200B;**進階**&#x200B;選項以設定此值。

   ![定義原型屬性](assets/archetype-properties.png)

1. 按一下「**下一步**」。

1. 選取&#x200B;**設定新伺服器**，並提供伺服器名稱和必要的連線詳細資料，以設定Eclipse連線的AEM伺服器。

   ![連線到AEM伺服器](assets/connect-server.png)

   * 若要使用偵錯工具功能，您必須藉由提供`-agentlib`引數在偵錯模式下啟動AEM，例如：

   ```text
   $ java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:5005 -jar aem-author-p4502.jar
   ```

   >[!TIP]
   >
   >如需有關在本機AEM SDK上執行專案的偵錯的詳細資訊，請參閱檔案[遠端偵錯AEM SDK。](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-sdk/remote-debugging)

1. 按一下&#x200B;**完成**。

專案結構隨即建立。 下載必要的成品至專案可能需要一些時間。

>[!NOTE]
>
>全新安裝時或先前未下載Maven相依性時，Eclipse可能會報告專案建立時發生錯誤。 在此情況下，請依照[解決無效的專案定義一節中所述的程式進行。](#resolving-invalid-project-definition)

## 如何匯入現有的專案 {#how-to-import-existing-projects}

使用&#x200B;**新專案**&#x200B;功能建立基本專案結構。

1. 請依照指示建立[範例多模組專案，](#sample-multi-module-project)，這會建立基本專案結構，並包含健全的關注點分離：

   * `PROJECT.ui.apps`和`/apps`內容的`/etc`
   * 已編寫之`PROJECT.ui.content`的`/content`
   * Java套件組合的`PROJECT.core`
   * 整合測試的`PROJECT.it.launcher`和`PROJECT.it.tests`

1. 將`PROJECT.ui.apps`專案的內容取代為您的封裝的`apps`和`etc`資料夾：

   1. 在&#x200B;**專案總管**&#x200B;面板中，展開`PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`。
   1. 在`apps`資料夾上按一下滑鼠右鍵，然後選擇&#x200B;**顯示於** > **系統總管**。
   1. 刪除那裡的`apps`和`etc`資料夾。
   1. 將內容封裝的`apps`和`etc`資料夾放置到相同位置。
   1. 在Eclipse中，以滑鼠右鍵按一下`PROJECT.ui.apps`專案，然後選擇&#x200B;**重新整理**。

1. 然後對`PROJECT.ui.content`執行相同操作，並將其內容資料夾取代為您其中一個封裝：

   1. 在&#x200B;**專案總管**&#x200B;面板中，展開`PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`。
   1. 用滑鼠右鍵按一下較深的內容資料夾，然後選擇&#x200B;**顯示於** > **系統總管**。
   1. 在該處刪除內容資料夾。
   1. 將內容封裝的內容資料夾放在相同位置。
   1. 在Eclipse中，以滑鼠右鍵按一下`PROJECT.ui.content`專案，然後選擇&#x200B;**重新整理**。

1. 透過在單獨的文字/程式碼編輯器中開啟內容套件的`filter.xml`檔案，更新這兩個專案的`META-INF/vault/filter.xml`檔案，以對應至您的內容套件內容。

   * 以下範例說明您的`filter.xml`檔案外觀：

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. 至於您分割為兩個專案的套件內容，您也必須將這些篩選規則分割為兩個，並相應地更新兩個專案的`filter.xml`檔案。

   1. 在Eclipse中，開啟`PROJECT.ui.apps/src/main/content/META-INF/filter.xml`。
   1. 將`<workspaceFilter>`元素的內容取代為您以`/apps`和`/etc`開頭的封裝規則
      * 例如：

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. 然後開啟`PROJECT.ui.content/src/main/content/META-INF/filter.xml`。
   1. 將規則取代為您以`/content`開頭的套件規則。
      * 例如：

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. 請務必儲存所有變更。 您現在可以將新內容同步至您的AEM執行個體。

1. 在&#x200B;**伺服器**&#x200B;面板中，確定您的連線已啟動，若未啟動，則確定已啟動。

1. 按一下&#x200B;**清除並發佈**&#x200B;圖示。

完成後，您的套件應該會在執行個體上執行。 儲存時，所有變更都會自動同步至執行個體。

如果您想要從專案重新建置套件，請在`PROJECT.ui.apps`或`PROJECT.ui.content`上按一下滑鼠右鍵，然後選擇&#x200B;**執行身分** > **Maven安裝**。

您現在已建立目標資料夾，內含套件（例如`PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`）。

## 疑難排解 {#troubleshooting}

### 解析無效的專案定義 {#resolving-invalid-project-definition}

若要解決無效的相依性和專案定義，請依照下列步驟進行：

1. 選取所有已建立的專案。
1. 按一下滑鼠右鍵。
1. 在內容功能表中，選取&#x200B;**Maven** > **更新專案**。
1. 檢查&#x200B;**強制更新快照/版本**。
1. 按一下&#x200B;**「確定」**。

Eclipse會下載必要的相依性。 這可能需要一段時間。

## 詳細資訊 {#more-information}

Eclipse網站的官方Apache Sling IDE工具提供有用的其他資訊：

* 適用於Eclipse [**的** Apache Sling IDE工具使用手冊](https://sling.apache.org/documentation/development/ide-tooling.html)會引導您瞭解AEM開發工具支援的整體概念、伺服器整合和部署功能。
* [疑難排解Apache Sling IDE工具](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting)
* [已知問題清單](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues)

下列正式[Eclipse](https://www.eclipse.org/)檔案可協助您設定環境：

* [開始使用Eclipse](https://eclipseide.org/getting-started/)
* [Eclipse Luna說明系統](https://help.eclipse.org/latest/index.jsp)
* [Maven整合(m2eclipse)](https://www.eclipse.org/m2e/)
