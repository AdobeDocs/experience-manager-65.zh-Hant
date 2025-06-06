---
title: 設定OSGi
description: OSGi是Adobe Experience Manager (AEM)技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。 本文詳細說明如何管理這類套裝的組態設定。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 0%

---

# 設定OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/)是Adobe Experience Manager (AEM)技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

OSGi「*」提供標準化的原語，允許使用小型、可重複使用且協同合作的元件來建構應用程式。 這些元件可組成應用程式並部署*。

如此一來，就能輕鬆地管理套件組合，因為套件組合可以個別停止、安裝和啟動。 系統會自動處理相依性。 每個OSGi元件（請參閱[OSGi規格](https://docs.osgi.org/specification/)）都包含在其中一個不同套件組合中。

您可以透過以下任一方式管理此類套裝的組態設定：

* 使用[Adobe CQ Web主控台](#osgi-configuration-with-the-web-console)
* 使用[組態檔](#osgi-configuration-with-configuration-files)
* 正在設定存放庫[&#128279;](#osgi-configuration-in-the-repository)中的內容節點( `sling:OsgiConfig`)

雖然有細微的差異（主要與[執行模式](/help/sites-deploying/configure-runmodes.md)有關），但可以使用其中一種方法：

* [Adobe CQ Web主控台](#osgi-configuration-with-the-web-console)

   * Web控制檯是OSGi設定的標準介面。 它提供用於編輯各種屬性的UI，其中可以從預先定義的清單中選擇可能的值。

     因此，這是最簡單的方法。

   * 使用Web主控台進行的所有設定都會立即套用並適用於目前的執行個體，無論目前的執行模式或後續對執行模式的任何變更為何。

* [組態檔](#osgi-configuration-with-configuration-files)

   * 包含在Web主控台中定義的設定。
   * 可以包含在內容套件中，以供在其他執行個體上使用。

* [存放庫中的content-nodes (sling：osgiConfig)](#osgi-configuration-in-the-repository)

   * 需要使用CRXDE Lite進行手動設定。
   * 由於`sling:OsgiConfig`節點的命名慣例，您可以將組態連結至特定的[執行模式](/help/sites-deploying/configure-runmodes.md)。 您甚至可以在同一存放庫中儲存多個執行模式的設定。
   * 任何適當的設定都會立即套用（取決於執行模式）。

無論您使用哪種方法，這些設定方法皆有：

* 請確定複製或復寫存放庫內容會重新建立相同的設定。
* 可讓您將組態簽出至FileVault或Subversion；以取得安全性或進一步的更新。
* 可儲存在套件中，以便在設定其他執行個體時使用。
* 可讓您使用指令碼執行設定轉出，以傳播設定詳細資訊。

>[!NOTE]
>
>某些重要設定的詳細資料列在[OSGi組態設定下。](/help/sites-deploying/osgi-configuration-settings.md)

## 使用Web主控台進行OSGi設定 {#osgi-configuration-with-the-web-console}

AEM中的[Web主控台](/help/sites-deploying/web-console.md)提供標準化介面來設定組合。 **Configuration**&#x200B;索引標籤是用來設定OSGi組合，因此是設定AEM系統引數的基礎機制。

所做的任何變更會立即套用至相關的OSGi設定，不需要重新啟動。

>[!NOTE]
>
>在Web主控台中所做的變更會以[組態檔](#osgi-configuration-with-configuration-files)的形式儲存在存放庫中。 這些檔案可包含在內容套件中，以供後續安裝重複使用。

>[!NOTE]
>
>在Web主控台上，提及預設設定的任何說明都與Sling預設值有關。
>
>Adobe Experience Manager有自己的預設值，因此設定的預設值可能與主控台上記錄的預設值不同。

若要使用Web主控台更新設定：

1. 存取Web Console的&#x200B;**組態**&#x200B;索引標籤，方法如下：

   * 正在從&#x200B;**工具>作業**&#x200B;功能表上的連結開啟Web主控台。 登入主控台後，您可以使用下拉式功能表：

     **OSGi >**

   * 直接URL；例如：

     `http://localhost:4502/system/console/configMgr`

   隨即顯示清單。

1. 選取您要透過下列任一方式設定的組合：

   * 按一下該套件組合的&#x200B;**編輯**&#x200B;圖示
   * 按一下組合的&#x200B;**名稱**

1. 對話方塊開啟。 您可以視需要在此編輯。 例如，將&#x200B;**記錄層級**&#x200B;設定為`INFO`：

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新會以[組態檔](#osgi-configuration-with-configuration-files)的形式儲存在存放庫中。 若要在之後找到這些檔案，以包含在內容套件中，以供其他執行個體使用，例如，記下永久性身分識別( `PID`)。

1. 按一下「**儲存**」。

   您的變更會立即套用至執行中系統的相關OSGi設定，不需要重新啟動。

   >[!NOTE]
   >
   >您現在可以找到相關的[組態檔](#osgi-configuration-with-configuration-files)。 例如，將包含在內容套件中以供在其他執行個體上使用。

## 使用組態檔的OSGi組態 {#osgi-configuration-with-configuration-files}

使用Web主控台進行的組態變更會作為組態檔( `.config`)保留在儲存庫中，位於：

`/apps`

這些檔案可包含在內容套件中，並可在其他執行個體上重複使用。

>[!NOTE]
>
>設定檔案的格式是特定的 — 請參閱Sling Apache檔案以瞭解：
>* [Apache Sling布建模型和Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)的完整詳細資料。
>* [在Sling](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html)中取得資源與屬性的教學課程與範例。
>
>因此，建議您在Web主控台中進行實際變更，以建立和維護設定檔案。

Web主控台不會顯示存放庫中儲存變更的位置，但可以輕鬆找到變更：

1. 透過[在Web主控台](#osgi-configuration-with-the-web-console)中進行初始變更來建立組態檔。
1. 開啟 CRXDE Lite。
1. 在&#x200B;**工具**&#x200B;功能表中，選取&#x200B;**查詢……** 。
1. 若要搜尋您已更新的組態PID，請提交&#x200B;**型別** `SQL`的查詢。

   例如，**Apache Felix OSGi管理主控台**&#x200B;的永久性身分(PID)為：

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此，SQL查詢可能是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 隨即顯示組態檔節點。

   對於上述範例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以開啟此檔案來檢視您的變更，但為了避免輸入錯誤，建議使用主控台進行實際的變更。

1. 您現在可以建立包含此節點的內容套件，並視需要在其他執行個體上使用。

## 存放庫中的OSGi設定 {#osgi-configuration-in-the-repository}

除了使用Web主控台，您也可以在存放庫中定義設定詳細資訊。 如此可讓您輕鬆設定不同的執行模式。

這些設定是透過在存放庫中建立`sling:OsgiConfig`節點以供系統參考來進行。 這些節點會反映OSGi設定，並在其中形成使用者介面。 若要更新設定資料，請更新節點屬性。

如果您修改存放庫中的設定資料，變更會立即套用至相關的OSGi設定。 就好像變更是使用Web主控台所進行，並透過適當的驗證和一致性檢查。 此工作流程也適用於將設定從`/libs/`複製到`/apps/`的動作。

由於相同的組態引數位於數個位置，因此系統：

* 搜尋型別`sling:OsgiConfig`的所有節點
* 根據服務名稱篩選
* 根據執行模式篩選

>[!NOTE]
>
>另請閱讀[如何定義特定執行個體的存放庫型設定](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=zh-Hant)。

### 新增設定至存放庫 {#adding-a-new-configuration-to-the-repository}

#### 您需要瞭解的事項 {#what-you-need-to-know}

若要將設定新增到存放庫，您必須知道以下內容：

1. 服務的&#x200B;**持續性身分** (PID)。

   參考Web主控台中的&#x200B;**組態**&#x200B;欄位。 此名稱會顯示在組合名稱后的方括弧中（或顯示在頁面底部的&#x200B;**組態資訊**&#x200B;中）。

   例如，建立節點`com.day.cq.wcm.core.impl.VersionManagerImpl.`以設定&#x200B;**AEM WCM版本管理員**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是否需要特定的[執行模式](/help/sites-deploying/configure-runmodes.md)？ 建立資料夾：

   * `config` — 適用於所有執行模式
   * `config.author` — 適用於作者環境
   * `config.publish` — 用於發佈環境
   * `config.<run-mode>` — 視情況而定

1. 需要&#x200B;**組態**&#x200B;或&#x200B;**工廠組態**&#x200B;嗎？
1. 要設定的個別引數，包括必須重新建立的任何現有引數定義。

   參考Web主控台中的個別引數欄位。 名稱會以方括弧顯示於每個引數。

   例如，建立屬性
   `versionmanager.createVersionOnActivation`設定&#x200B;**啟動時建立版本**。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs`中是否有組態？ 若要列出執行個體中的所有組態，請使用CRXDE Lite中的&#x200B;**查詢**&#x200B;工具來提交下列SQL查詢：

   `select * from sling:OsgiConfig`

   若是如此，此設定可以複製到` /apps/<yourProject>/`，然後在新的位置自訂。

#### 在存放庫中建立組態 {#creating-the-configuration-in-the-repository}

若要將新設定實際新增至存放庫：

1. 使用CRXDE Lite來導覽至：

   ` /apps/<yourProject>`

1. 如果不存在，請建立`config`資料夾( `sling:Folder`)：

   * `config` — 適用於所有執行模式
   * `config.<run-mode>` — 特定執行模式專用

1. 在此資料夾下，建立節點：

   * 類型：`sling:OsgiConfig`
   * 名稱：永續性身分(PID)；

     例如，AEM WCM版本管理員使用`com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >進行Factory組態時，將`-<identifier>`附加至名稱。
   >
   >原樣： `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >其中`<identifier>`由您（必須）輸入以識別執行個體的任意文字取代（您無法忽略此資訊）；例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 針對您要設定的每個引數，在此節點上建立一個屬性：

   * 名稱：引數名稱，如Web主控台中所示；名稱會顯示在欄位說明結尾的方括弧中。 例如，`Create Version on Activation`使用`versionmanager.createVersionOnActivation`
   * 型別：視情況而定。
   * 值：視需要。

   您只能為您要設定的引數建立屬性，其他使用者仍會採用AEM設定的預設值。

1. 儲存所有變更。

   透過重新啟動服務來更新節點時，會套用變更（如同Web主控台中所做的變更）。

>[!CAUTION]
>
>請勿變更`/libs`路徑中的任何專案。

>[!CAUTION]
>
>設定的完整路徑必須正確，才能在啟動時讀取。

## 設定詳細資料 {#configuration-details}

### 啟動時的解決順序 {#resolution-order-at-startup}

使用的優先順序如下：

1. `/apps/*/config...`下的存放庫節點。具有型別`sling:OsgiConfig`或屬性檔案。

1. `/libs/*/config...`下型別為`sling:OsgiConfig`的存放庫節點。 （現成定義）。

1. 來自`<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`的任何`.config`檔案。 在本機檔案系統上。

`/libs`中的一般組態可以被`/apps`中的專案特定組態遮罩。

### 執行階段的解決順序 {#resolution-order-at-runtime}

系統執行時進行的設定變更會觸發使用修改後的設定重新載入。

然後套用下列優先順序：

1. 在Web主控台中修改組態會立即生效，因為它在執行階段具有優先權。
1. 在`/apps`中修改組態會立即生效。
1. 在`/libs`中修改組態會立即生效，除非它被`/apps`中的組態遮罩。

### 多重執行模式的解析度 {#resolution-of-multiple-run-modes}

對於執行模式特定的配置，可以組合多個執行模式。 例如，您可以以下列樣式建立組態資料夾：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有執行模式都符合啟動時定義的執行模式，則會套用此類資料夾中的設定。

例如，如果執行個體是以執行模式`author,dev,emea`啟動，則套用`/apps/*/config.emea`、`/apps/*/config.author.dev/`和`/apps/*/config.author.emea.dev/`中的設定節點，而不套用`/apps/*/config.author.asean/`和`/config/author.dev.emea.noldap/`中的設定節點。

如果同一PID適用多個設定，則會套用符合執行模式數量最多的設定。

例如，如果執行個體是以執行模式`author,dev,emea`啟動，而`/apps/*/config.author/`和`/apps/*/config.emea.author/`都定義了設定
`com.day.cq.wcm.core.impl.VersionManagerImpl`，已套用`/apps/*/config.emea.author/`中的組態。

此規則的詳細程度位於PID層級。
您無法在`/apps/*/config.author/`中為同一個PID定義某些屬性，也無法在`/apps/*/config.emea.author/`中為同一個PID定義更具體的屬性。
符合執行模式數量最多的設定對整個PID有效。

### 標準設定 {#standard-configurations}

下列清單顯示存放庫中（在標準安裝中）提供的一小部分設定：

* 作者 — AEM WCM篩選器：

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publish - AEM WCM篩選器：

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publish - AEM WCM頁面統計資料：

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>由於這些設定位於`/libs`，因此不可直接編輯它們，但在自訂之前必須先複製到您的應用程式區域( `/apps`)。

若要列出執行個體中的所有設定節點，請使用CRXDE Lite中的&#x200B;**查詢**&#x200B;功能來提交下列SQL查詢：

`select * from sling:OsgiConfig`

### 設定持續性 {#configuration-persistence}

* 如果您透過Web主控台變更設定，則通常會將該設定寫入存放庫：

  `/apps/{somewhere}`

   * 根據預設，`{somewhere}`為`system/config`，因此組態會寫入

     `/apps/system/config`

   * 不過，如果您要編輯的組態最初來自存放庫中的其他位置，例如：

     /libs/foo/config/someconfig

     然後，更新的設定會寫入原始位置下；例如：

     `/apps/foo/config/someconfig`

* 由`admin`變更的設定儲存在`*.config`個檔案中：

  ```
     /crx-quickstart/launchpad/config
  ```

   * 此區域是OSGi設定管理員的私人資料，並保留`admin`所指定的所有設定詳細資料，無論他們如何進入系統。
   * 此區域是實作詳細資料，您絕不可直接編輯此目錄。
   * 不過，瞭解這些組態檔的位置會很有用，這樣就可以擷取復本進行備份、進行多重安裝，或同時進行兩者：

      * Apache Felix OSGi管理主控台

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling使用者端存放庫

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>切勿編輯下列資料夾或檔案：
>
>`/crx-quickstart/launchpad/config`
