---
title: 配置OSGi
seo-title: 配置OSGi
description: OSGi是Adobe Experience Manager()技術層的一個基AEM本要素。 它用於控制複合束及其AEM配置。 本文詳細說明如何管理此類套件的組態設定。
seo-description: OSGi是Adobe Experience Manager()技術層的一個基AEM本要素。 它用於控制複合束及其AEM配置。 本文詳細說明如何管理此類套件的組態設定。
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: 設定
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---


# 配置OSGi{#configuring-osgi}

[](https://www.osgi.org/) OSG是Adobe Experience Manager(M)技術層面的一個基AEM本要素。它用於控制複合束及其AEM配置。

OSGi &quot;*提供標準化的基元，可讓應用程式由小型、可重複使用和協作的元件來建立。 這些元件可以組成到應用程式並部署*&quot;。

這樣可以輕鬆管理捆綁包，因為它們可以單獨停止、安裝和啟動。 互依關係會自動處理。 每個OSGi元件（請參見[OSGi規範](https://www.osgi.org/Specifications/HomePage)）都包含在各種束之一中。

您可以透過以下任一方式管理此類組合的組態設定：

* 使用[Adobe CQWeb控制台](#osgi-configuration-with-the-web-console)
* 使用[配置檔案](#osgi-configuration-with-configuration-files)
* 在儲存庫](#osgi-configuration-in-the-repository)中配置[content-nodes(`sling:OsgiConfig`)

兩種方法都可使用，但主要與[運行模式](/help/sites-deploying/configure-runmodes.md)有關：

* [Adobe CQ網路主控台](#osgi-configuration-with-the-web-console)

   * Web控制台是OSGi配置的標準介面。 它提供編輯各種屬性的UI，可從預先定義的清單中選擇可能的值。

      因此，它是最簡單的使用方法。

   * 使用Web控制台進行的任何配置都會立即應用並適用於當前實例，而不考慮當前運行模式或對運行模式的任何後續更改。

* [配置檔案](#osgi-configuration-with-configuration-files)

   * 包含Web主控台中定義的設定。
   * 可包含在內容套件中，以用於其他例項。

* [content-nodes(sling:osgiConfig) in the repository](#osgi-configuration-in-the-repository)

   * 這需要使用CRXDE Lite進行手動配置。
   * 由於`sling:OsgiConfig`節點的命名慣例，您可以將配置關聯到特定的[運行模式](/help/sites-deploying/configure-runmodes.md)。 您甚至可以在同一儲存庫中保存多個運行模式的配置。
   * 任何適當的組態都會立即套用（視執行模式而定）。

無論您使用哪種方法，所有這些配置方法：

* 確保複製或複製儲存庫內容會重新建立相同的配置。
* 允許您將配置檢出到FileVault或Subversion;安全性或更新。
* 可保存在包中，以便在設定其他實例時使用。
* 允許您使用指令碼來傳播配置詳細資訊，以執行配置推展。

>[!NOTE]
>
>某些重要設定的詳細資訊列在[OSGi配置設定下。](/help/sites-deploying/osgi-configuration-settings.md)

## 使用Web控制台{#osgi-configuration-with-the-web-console}進行OSGi配置

中的[Web控制台](/help/sites-deploying/web-console.md)提供了用於AEM配置捆綁的標準化介面。 **Configuration**&#x200B;頁籤用於配置OSGi捆綁，因此是配置系統參數的基AEM礎機制。

所做的任何更改都會立即應用於相關的OSGi配置，無需重新啟動。

>[!NOTE]
>
>在Web控制台中所做的更改將保存在儲存庫中為[配置檔案](#osgi-configuration-with-configuration-files)。 這些內容可包含在內容套件中，以便在進一步安裝中重複使用。

>[!NOTE]
>
>在Web主控台上，任何提及預設設定的說明都與Sling預設值相關。
>
>Adobe Experience Manager有自己的預設值，因此預設集可能與主控台記載的不同。

要使用Web控制台更新配置，請執行以下操作：

1. 通過以下任一方法訪問Web控制台的&#x200B;**Configuration**&#x200B;頁籤：

   * 從&#x200B;**工具->操作**&#x200B;菜單上的連結開啟Web控制台。 登入主控台後，您可使用下列功能表：

      **OSGi >**

   * 直接網址；例如：

      `http://localhost:4502/system/console/configMgr`
   將會顯示清單。

1. 選擇要通過以下任一方法配置的包：

   * 按一下該包的&#x200B;**編輯**&#x200B;表徵圖
   * 按一下包的&#x200B;**名稱**

1. 對話方塊將會開啟。 您可在此視需要編輯；例如，將&#x200B;**Log Level**&#x200B;設為`INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >更新將保存在儲存庫中為[配置檔案](#osgi-configuration-with-configuration-files)。 若要在之後找到這些識別碼（例如，要包含在內容套件中以便用於另一個實例），您應記下永久性識別碼(`PID`)。

1. 按一下「**儲存**」。

   您的更改會立即應用於正在運行的系統的相關OSGi配置，無需重新啟動。

   >[!NOTE]
   >
   >您現在可以找到相關的[配置檔案](#osgi-configuration-with-configuration-files);例如，要包含在內容套件中，以便用於另一個例項。

## OSGi配置配置配置檔案{#osgi-configuration-with-configuration-files}

使用Web控制台所做的配置更改將作為配置檔案(`.config`)保存在儲存庫中，位於：

`/apps`

這些內容可包含在內容封裝中，並可在其他例項上重複使用。

>[!NOTE]
>
>設定檔的格式非常特定——如需完整詳細資訊，請參閱[Sling Apache檔案](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format)。
>
>因此，建議在Web控制台中進行實際更改，以建立和維護配置檔案。

Web Console不顯示已保存更改的儲存庫中的位置，但可以輕鬆找到這些更改：

1. 通過[在Web控制台中進行初始更改來建立配置檔案。](#osgi-configuration-with-the-web-console)
1. 開啟CRXDE Lite。
1. 在&#x200B;**工具**&#x200B;菜單中，選擇&#x200B;**查詢……**。
1. 提交&#x200B;**Type** `SQL`的查詢，以搜索已更新的配置的PID。

   例如，**Apache Felix OSGi Management Console**&#x200B;具有以下的持久身份(PID):

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   因此SQL查詢可以是：

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. 將顯示配置檔案節點。

   對於上述範例：

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >您可以開啟此檔案以檢視您所做的變更，但為避免輸入錯誤，建議您使用主控台進行實際變更。

1. 您現在可以建立包含此節點的內容套件，並視需要在其他執行個體上使用。

## 資料庫{#osgi-configuration-in-the-repository}中的OSGi配置

除了使用Web控制台外，您還可以在儲存庫中定義配置詳細資訊。 這可讓您輕鬆設定不同的執行模式。

這些配置是通過在儲存庫中建立`sling:OsgiConfig`節點來進行的，以供系統參考。 這些節點將鏡像OSGi配置，並對其形成用戶介面。 要更新配置資料，請更新節點屬性。

如果修改儲存庫中的配置資料，則更改將立即應用到相關的OSGi配置，就像更改是使用Web控制台進行的一樣，並執行相應的驗證和一致性檢查。 這也適用於將配置從`/libs/`複製到`/apps/`的操作。

由於相同的配置參數可以位於多個位置，因此系統：

* 搜索類型`sling:OsgiConfig`的所有節點
* 根據服務名稱進行篩選
* 根據運行模式進行篩選

>[!NOTE]
>
>另請閱讀[如何為特定實例定義基於儲存庫的配置](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html)。

### 向儲存庫{#adding-a-new-configuration-to-the-repository}添加新配置

#### 您需要知道的{#what-you-need-to-know}

要向儲存庫添加新配置，您需要瞭解以下內容：

1. 服務的&#x200B;**持久身份**(PID)。

   參考Web控制台中的&#x200B;**Configurations**&#x200B;欄位。 名稱在包名稱后面的括弧中顯示（或在頁面底部的&#x200B;**配置資訊**&#x200B;中）。

   例如，建立節點`com.day.cq.wcm.core.impl.VersionManagerImpl.`以配置&#x200B;**AEM WCM Version Manager**。

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. 是否需要特定的[運行模式](/help/sites-deploying/configure-runmodes.md)。 建立資料夾：

   * `config` -所有運行模式
   * `config.author` -適用於作者環境
   * `config.publish` -適用於發佈環境
   * `config.<run-mode>` -適當

1. 是否需要&#x200B;**配置**&#x200B;或&#x200B;**工廠配置**。
1. 要配置的單個參數；包括需要重新建立的任何現有參數定義。

   參考Web控制台中的個別參數欄位。 每個參數的名稱以方括弧顯示。

   例如，建立屬性
   `versionmanager.createVersionOnActivation` 在啟動 **時設定Create Version**。

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. `/libs`中是否已存在配置？ 要列出實例中的所有配置，請使用CRXDE Lite中的&#x200B;**Query**&#x200B;工具提交以下SQL查詢：

   `select * from sling:OsgiConfig`

   如果是，此配置可以複製到` /apps/<yourProject>/`，然後在新位置中自定義。

#### 在儲存庫{#creating-the-configuration-in-the-repository}中建立配置

要將新配置實際添加到儲存庫，請執行以下操作：

1. 使用CRXDE Lite導航至：

   ` /apps/<yourProject>`

1. 如果尚未存在，請建立`config`資料夾(`sling:Folder`):

   * `config` -適用於所有運行模式
   * `config.<run-mode>` -特定於特定運行模式

1. 在此資料夾下建立一個節點：

   * 類型: `sling:OsgiConfig`
   * 名稱：持久性身份(PID);

      例如，AEMWCM版本管理器使用`com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >在進行工廠配置時，將`-<identifier>`附加到名稱。
   >
   >如：`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >其中`<identifier>`由您（必須）輸入以識別實例的自由文本替換（您不能忽略此資訊）;例如：
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. 對於要配置的每個參數，請在此節點上建立一個屬性：

   * 名稱：參數名稱，如Web控制台所示；名稱會在欄位說明結尾的方括弧中顯示。 例如，對於`Create Version on Activation`，請使用`versionmanager.createVersionOnActivation`
   * 類型：視情況而定。
   * 值：視需要。

   您只需要為要設定的參數建立屬性，其他參數仍會採用預設值，如AEM所設定。

1. 儲存所有變更。

   當節點更新時，會立即重新啟動服務（如Web控制台中所做的變更）。

>[!CAUTION]
>
>您不得變更`/libs`路徑中的任何項目。

>[!CAUTION]
>
>配置的完整路徑必須正確，才能在啟動時讀取。

## 配置詳細資訊{#configuration-details}

### 啟動時的解析順序{#resolution-order-at-startup}

使用下列優先順序：

1. `/apps/*/config...`.either type `sling:OsgiConfig`或property files下的儲存庫節點。

1. 在`/libs/*/config...`下鍵入`sling:OsgiConfig`的儲存庫節點。 （現成可用的定義）。

1. 來自`<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`的任何`.config`檔案。 在本機檔案系統上。

這表示`/libs`中的一般配置可由`/apps`中的項目特定配置遮罩。

### 執行時期的解析順序{#resolution-order-at-runtime}

在系統運行時所做的配置更改會觸發重新載入並使用修改的配置。

接著，應按下列優先順序：

1. 在Web控制台中修改配置將立即生效，因為它在運行時優先。
1. 在`/apps`中修改配置將立即生效。
1. 修改`/libs`中的配置將立即生效，除非它被`/apps`中的配置遮住。

### 多種運行模式的解析度{#resolution-of-multiple-run-modes}

對於運行模式特定的配置，可以組合多種運行模式。 例如，您可以建立以下樣式的配置資料夾：

`/apps/*/config.<runmode1>.<runmode2>/`

如果所有運行模式都與啟動時定義的運行模式匹配，則將應用這些資料夾中的配置。

例如，如果以運行模式`author,dev,emea`啟動實例，則`/apps/*/config.emea`、`/apps/*/config.author.dev/`和`/apps/*/config.author.emea.dev/`中的配置節點將被應用，而`/apps/*/config.author.asean/`和`/config/author.dev.emea.noldap/`中的配置節點將不被應用。

如果同一PID的多個配置適用，則應用具有最多匹配運行模式的配置。

例如，如果實例是以運行模式`author,dev,emea`啟動的，並且`/apps/*/config.author/`和`/apps/*/config.emea.author/`都定義了
`com.day.cq.wcm.core.impl.VersionManagerImpl`，將應用`/apps/*/config.emea.author/`中的配置。

此規則的詳細程度為PID層級。
不能為`/apps/*/config.author/`中的相同PID定義某些屬性，也不能為相同PID在`/apps/*/config.emea.author/`中定義更多特定屬性。
對於整個PID，具有最大匹配運行模式的配置是有效的。

### 標準配置{#standard-configurations}

以下清單顯示了儲存庫中可用配置的一小部分（在標準安裝中）:

* 作者- AEM WCM篩選：

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* 發佈- AEM WCM篩選器：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* 發佈- AEM WCM頁面統計資料：

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>由於這些配置位於`/libs`中，因此不能直接編輯它們，而是在自定義之前複製到您的應用程式區域(`/apps`)。

要列出實例中的所有配置節點，請使用CRXDE Lite中的&#x200B;**Query**&#x200B;功能提交以下SQL查詢：

`select * from sling:OsgiConfig`

### 配置持久性{#configuration-persistence}

* 如果通過Web控制台更改配置，則配置（通常）會寫入儲存庫，位於：

   `/apps/{somewhere}`

   * 預設情況下，`{somewhere}`為`system/config` ，因此配置將寫入

      `/apps/system/config`

   * 但是，如果您正在編輯最初來自儲存庫中其他位置的配置：例如：

      /libs/foo/config/someconfig

      然後將更新後的配置寫入原始位置；例如：

      `/apps/foo/config/someconfig`

* 由`admin`變更的設定會儲存在`*.config`檔案中，位於：

   ```
      /crx-quickstart/launchpad/config
   ```

   * 這是OSGi配置管理員的專用資料區，並保存`admin`指定的所有配置詳細資訊，而不管它們如何進入系統。
   * 這是實作詳細資料，您絕不能直接編輯此目錄。
   * 但是，瞭解這些配置檔案的位置是很有用的，以便備份和／或多個安裝可以進行拷貝：

      * Apache Felix OSGi Management Console

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * CRX Sling Client Repository

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>您必須&#x200B;***never***&#x200B;編輯以下資料夾或檔案：
>
>`/crx-quickstart/launchpad/config`

