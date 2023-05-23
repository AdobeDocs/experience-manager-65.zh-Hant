---
title: 配置OSGi
seo-title: Configuring OSGi
description: OSGi是Adobe Experience Manager技術棧中的一個基AEM本要素。 它用於控制複合束及其AEM結構。 本文詳細介紹了如何管理此類捆綁包的配置設定。
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 2981f11565db957fac323f81014af83cab2c0a12
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 0%

---

# 配置OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) 是Adobe Experience Manager(M)技術中的一個基本AEM要素。 它用於控制複合束及其AEM結構。

OSGi &quot;*提供了標準化基元，允許應用程式由小型、可重用和協作的元件構建。 這些元件可以組合成應用程式並部署*。

這樣可以輕鬆管理捆綁包，因為可以單獨停止、安裝和啟動捆綁包。 互依關係將自動處理。 每個OSGi元件(請參見 [OSGi規範](https://docs.osgi.org/specification/))包含在各種捆綁包中。

您可以通過以下任一方法管理此類捆綁包的配置設定：

* 使用 [Adobe CQWeb控制台](#osgi-configuration-with-the-web-console)
* 使用 [配置檔案](#osgi-configuration-with-configuration-files)
* 配置 [內容節點( `sling:OsgiConfig`)](#osgi-configuration-in-the-repository)

儘管存在細微差異，但可以使用兩種方法，主要與 [運行模式](/help/sites-deploying/configure-runmodes.md):

* [Adobe CQWeb控制台](#osgi-configuration-with-the-web-console)

   * Web控制台是OSGi配置的標準介面。 它提供了用於編輯各種屬性的UI，在這些屬性中可以從預定義清單中選擇可能的值。

      因此，它是最容易使用的方法。

   * 使用Web控制台進行的任何配置都會立即應用並適用於當前實例，而不管當前運行模式或後續對運行模式的任何更改。

* [配置檔案](#osgi-configuration-with-configuration-files)

   * 包含在Web控制台中定義的設定。
   * 可以包含在內容包中，以用於其他實例。

* [儲存庫中的內容節點(sling:osgiConfig)](#osgi-configuration-in-the-repository)

   * 需要使用CRXDE Lite進行手動配置。
   * 由於 `sling:OsgiConfig` 節點，您可以將配置與特定 [運行模式](/help/sites-deploying/configure-runmodes.md)。 您甚至可以在同一儲存庫中保存多個運行模式的配置。
   * 將立即應用任何適當的配置（取決於運行模式）。

無論您使用哪種方法，所有這些配置方法：

* 確保複製或複製儲存庫內容會重新建立相同的配置。
* 允許您將配置檢出到FileVault或Subversion;用於安全或進一步更新。
* 可以保存在包中，以便在設定其他實例時使用。
* 允許您使用指令碼來傳播配置詳細資訊來執行配置部署。

>[!NOTE]
>
>某些重要設定的詳細資訊列於 [OSGi配置設定。](/help/sites-deploying/osgi-configuration-settings.md)

## OSGi與Web控制台的配置 {#osgi-configuration-with-the-web-console}

的 [Web控制台](/help/sites-deploying/web-console.md) 中提供AEM了用於配置捆綁包的標準化介面。 的 **配置** 頁籤用於配置OSGi捆綁包，因此是配置系統參數的基礎AEM機制。

對相關OSGi配置所做的任何更改都會立即應用，無需重新啟動。

>[!NOTE]
>
>在Web控制台中所做的更改將保存在儲存庫中， [配置檔案](#osgi-configuration-with-configuration-files)。 這些檔案可以包含在內容包中，以便在進一步安裝中重新使用。

>[!NOTE]
>
>在Web控制台上，任何提及預設設定的說明都與Sling預設值相關。
>
>Adobe Experience Manager有其自己的預設值，因此設定的預設值可能與控制台上記錄的預設值不同。

要使用Web控制台更新配置：

1. 訪問 **配置** 的子菜單：

   * 從上的連結開啟Web控制台 **工具 — >操作** 的子菜單。 登錄到控制台後，可以使用下列下拉菜單：

      **OSGi >**

   * 直接URL;例如：

      `http://localhost:4502/system/console/configMgr`
   將顯示一個清單。

1. 選擇要通過以下任一方式配置的包：

   * 按一下 **編輯** 表徵圖
   * 按一下 **名稱** 的

1. 開啟對話框。 在此，您可以根據需要進行編輯。 例如，設定 **日誌級別** 至 `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新將保存在儲存庫中 [配置檔案](#osgi-configuration-with-configuration-files)。 以後要查找這些檔案以包括在內容包中以供其他實例使用，例如，記下永久標識( `PID`)。

1. 按一下「**儲存**」。

   您所做的更改將立即應用於正在運行的系統的相關OSGi配置，無需重新啟動。

   >[!NOTE]
   >
   >您現在可以找到相關 [配置檔案](#osgi-configuration-with-configuration-files)。 例如，要包括在內容包中以用於另一個實例。

## OSGi配置，包含配置檔案 {#osgi-configuration-with-configuration-files}

使用Web控制台進行的配置更改作為配置檔案保留在儲存庫中( `.config`)下：

`/apps`

這些檔案可以包含在內容包中，並可在其他實例上重用。

>[!NOTE]
>
>配置檔案的格式是特定的 — 請參見 [Sling Apache文檔](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) 的雙曲餘切值。
>
>因此，建議通過在Web控制台中進行實際更改來建立和維護配置檔案。

Web控制台不顯示儲存庫中保存了更改的位置，但可以輕鬆找到更改：

1. 建立配置檔案的方法 [在web控制台中進行初始更改](#osgi-configuration-with-the-web-console)。
1. 開啟CRXDE Lite。
1. 在 **工具** 菜單，選擇 **查詢……** 。
1. 要搜索已更新的配置的PID，請提交 **類型** `SQL`。

   比如說， **Apache Felix OSGi管理控制台** 具有以下項的持久標識(PID):

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此SQL查詢可以是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 將顯示配置檔案節點。

   對於上例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以開啟此檔案以查看您所做的更改，但為避免鍵入錯誤，建議使用控制台進行實際更改。

1. 現在，您可以生成包含此節點的內容包，並根據需要在其他實例上使用。

## 儲存庫中的OSGi配置 {#osgi-configuration-in-the-repository}

除了使用Web控制台外，您還可以在儲存庫中定義配置詳細資訊。 這樣，您可以輕鬆配置不同的運行模式。

這些配置是通過建立 `sling:OsgiConfig` 儲存庫中的節點，供系統引用。 這些節點鏡像OSGi配置，並形成用戶介面。 要更新配置資料，請更新節點屬性。

如果修改儲存庫中的配置資料，則這些更改將立即應用於相關OSGi配置。 這就好像是使用Web控制台進行了更改，並進行了適當的驗證和一致性檢查。 此工作流還適用於從複製配置的操作 `/libs/` 至 `/apps/`。

由於同一配置參數在多個位置，因此系統：

* 搜索所有類型的節點 `sling:OsgiConfig`
* 根據服務名篩選
* 根據運行模式篩選

>[!NOTE]
>
>另請閱讀 [如何僅為特定實例定義基於儲存庫的配置](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=en)。

### 將新配置添加到儲存庫 {#adding-a-new-configuration-to-the-repository}

#### 你需要知道的 {#what-you-need-to-know}

要將配置添加到儲存庫，您必須知道以下內容：

1. 的 **持久標識** (PID)。

   引用 **配置** 的子菜單。 名稱在束名稱后方括弧中顯示(或 **配置資訊** 頁面底部)。

   例如，建立節點 `com.day.cq.wcm.core.impl.VersionManagerImpl.` 配置 **WCM版AEM本管理器**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是特定 [運行模式](/help/sites-deploying/configure-runmodes.md) 需要？ 建立資料夾：

   * `config`  — 所有運行模式
   * `config.author`  — 針對作者環境
   * `config.publish`  — 對於發佈環境
   * `config.<run-mode>` - 依需要

1. 是 **配置** 或 **工廠配置** 必要嗎？
1. 要配置的各個參數，包括必須重新建立的任何現有參數定義。

   引用Web控制台中的單個參數欄位。 每個參數的名稱都以括弧顯示。

   例如，建立屬性
   `versionmanager.createVersionOnActivation` 配置 **激活時建立版本**。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. 中是否存在配置 `/libs`? 要列出實例中的所有配置，請使用 **查詢** CRXDE Lite中的工具以提交以下SQL查詢：

   `select * from sling:OsgiConfig`

   如果是，可將此配置複製到 ` /apps/<yourProject>/`，然後在新位置自定義。

#### 在儲存庫中建立配置 {#creating-the-configuration-in-the-repository}

要將新配置實際添加到儲存庫，請執行以下操作：

1. 使用CRXDE Lite導航至：

   ` /apps/<yourProject>`

1. 如果不存在，請建立 `config` 資料夾(F) `sling:Folder`):

   * `config`  — 適用於所有運行模式
   * `config.<run-mode>`  — 特定於特定運行模式

1. 在此資料夾下，建立一個節點：

   * 類型: `sling:OsgiConfig`
   * 名稱：持久身份(PID);

      例如，AEM WCM版本管理器使用 `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >追加出廠配置時 `-<identifier>` 的名稱。
   >
   >如： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >位置 `<identifier>` 替換為自由文本，您（必須輸入該文本）才能標識實例（您不能忽略此資訊）;例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 對於要配置的每個參數，在此節點上建立一個屬性：

   * 名稱：參數名稱，如Web控制台所示；名稱在欄位說明末尾的括弧中顯示。 例如， `Create Version on Activation` 使用 `versionmanager.createVersionOnActivation`
   * 類型：視情況而定。
   * 值：按需要。

   您只能為要配置的參數建立屬性，其他參數仍採用由設定的預設值AEM。

1. 保存所有更改。

   當通過重新啟動服務來更新節點時，將應用更改（與在Web控制台中所做的更改一樣）。

>[!CAUTION]
>
>不更改 `/libs` 路徑。

>[!CAUTION]
>
>配置的完整路徑必須正確，才能在啟動時讀取。

## 配置詳細資訊 {#configuration-details}

### 啟動時的解析順序 {#resolution-order-at-startup}

使用以下優先順序：

1. 下的儲存庫節點 `/apps/*/config...`.或 `sling:OsgiConfig` 或屬性檔案。

1. 具有類型的儲存庫節點 `sling:OsgiConfig` 在 `/libs/*/config...`。 （現成定義）。

1. 任意 `.config` 檔案 `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`。 在本地檔案系統上。

中的泛型配置 `/libs` 可通過中的項目特定配置進行屏蔽 `/apps`。

### 運行時的解析度順序 {#resolution-order-at-runtime}

在系統運行時所做的配置更改會觸發具有修改的配置的重新載入。

然後，優先順序如下：

1. 在Web控制台中修改配置會立即生效，因為它在運行時優先。
1. 修改中的配置 `/apps` 立即生效。
1. 修改中的配置 `/libs` 立即生效，除非它被中的配置屏蔽 `/apps`。

### 多運行模式的解析 {#resolution-of-multiple-run-modes}

對於特定於運行模式的配置，可以組合多個運行模式。 例如，可以按以下樣式建立配置資料夾：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有運行模式都與啟動時定義的運行模式匹配，則應用此類資料夾中的配置。

例如，如果實例是使用運行模式啟動的 `author,dev,emea`，配置節點 `/apps/*/config.emea`。 `/apps/*/config.author.dev/`, `/apps/*/config.author.emea.dev/` 應用時，配置節點 `/apps/*/config.author.asean/` 和 `/config/author.dev.emea.noldap/` 的子菜單。

如果同一PID的多個配置可用，則應用具有最大數量匹配運行模式的配置。

例如，如果實例是使用運行模式啟動的 `author,dev,emea`的 `/apps/*/config.author/` 和 `/apps/*/config.emea.author/` 定義配置
`com.day.cq.wcm.core.impl.VersionManagerImpl`，中的配置 `/apps/*/config.emea.author/` 的子菜單。

此規則的粒度處於PID級別。
不能為中的同一PID定義某些屬性 `/apps/*/config.author/` 更具體的 `/apps/*/config.emea.author/` 同一PID。
對於整個PID，具有最大匹配運行模式數的配置是有效的。

### 標準配置 {#standard-configurations}

以下清單顯示了儲存庫中可用配置的一小部分（在標準安裝中）:

* 作者 — AEM WCM篩選器：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 發佈 — AEM WCM篩選器：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 發佈 — AEM WCM頁統計資訊：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>由於這些配置位於 `/libs` 不能直接編輯，而是複製到您的應用程式區域( `/apps`)。

要列出實例中的所有配置節點，請使用 **查詢** CRXDE Lite中的功能，以提交以下SQL查詢：

`select * from sling:OsgiConfig`

### 配置持久性 {#configuration-persistence}

* 如果通過Web控制台更改配置，則（通常）會在以下位置寫入儲存庫：

   `/apps/{somewhere}`

   * 預設情況下 `{somewhere}` 是 `system/config` 因此將配置寫入

      `/apps/system/config`

   * 但是，如果您正在編輯最初來自儲存庫中其他位置的配置：例如：

      /libs/foo/config/someconfig

      然後將更新後的配置寫入原始位置；例如：

      `/apps/foo/config/someconfig`

* 更改者的設定 `admin` 保存 `*.config` 檔案位於：

   ```
      /crx-quickstart/launchpad/config
   ```

   * 此區域是OSGi配置管理員的專用資料，並包含由 `admin`，不管他們是如何進入系統的。
   * 此區域是實現詳細資訊，您決不能直接編輯此目錄。
   * 但是，瞭解這些配置檔案的位置非常有用，以便可以為備份或多次安裝或同時進行以下兩種操作建立副本：

      * Apache Felix OSGi管理控制台

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling客戶端儲存庫

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>切勿編輯以下資料夾或檔案：
>
>`/crx-quickstart/launchpad/config`
