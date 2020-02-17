---
title: 基本配置概念
seo-title: 基本配置概念
description: 瞭解如何設定AEM。
seo-description: 瞭解如何設定AEM。
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM)會安裝所有參數的預設設定，讓它「立即可用」。 不過，您可以針對自己的特定需求設定AEM。

AEM有許多方面可以設定：

* 有些 [通常會針對每個專案安裝進行設定](#primary-configuration-considerations) ，而且必須進行審查，以確認這些設定是否適用於您的專案。
* [進一步的配置](#further-configuration-considerations) ，可能是常見的，但並非必要；與功能或系統效能與穩定性相關。
* 其他則僅是AEM的某些選用功能所需（這些功能會連同適當的功能一起記錄）。

根據特定配置，這些更改可以使用：

* **Adobe CQ Web Console**

   這是配置OSGi捆綁包和服務的標準位置。

   如需詳 [細資訊和建議的實務](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

* **存放庫**

   儲存庫中提供OSGi配置的子集。 這可確保複製或複製儲存庫內容重新建立相同的配置。 您也可以根據運行模式將自己的配置添加到儲存庫。

   有關詳 [細資訊，請參見Repository中的](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) OSGi Configuration（OSGi配置）, [特別是Adding a New Configuration to the Repository](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) （向儲存庫添加新配置）。

* **檔案系統**

   檔案系統中有一些配置檔案。

* **AEM WCM**

   AEM WCM本身可以設定各種方面，其中許多使用「工具」控 [制台](/help/sites-administering/tools-consoles.md) ;例如，複製代理。

>[!NOTE]
>
>使用Adobe Experience Manager時，有幾種方法可管理OSGi服務（控制台或儲存庫節點）的組態設定。
>
>如需 [完整詳細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

>[!NOTE]
>
>設定AEM很簡單，但您必須注意：
>
>某些變更可能會對應用程式產生重大影響。 因此，請先確定您有必要的經驗和知識，再開始設定AEM，並只進行您知道需要的變更。 通過OSGi控制台所做的任何更改 **都會立即應用** 到正在運行的系統（不需要重新啟動）。

## 主要配置注意事項 {#primary-configuration-considerations}

此清單詳細列出了每個新項目通常配置的主要區域。 並非所有項目都需要，但必須閱讀並審查清單，以查看哪些項目適用。

此清單提供每個設定方面的簡短概述，以及提供完整詳細資訊之頁面的連結。

### 安全性檢查清單 {#security-checklist}

安全檢查清單中列出了幾個關 [鍵配置問題](/help/sites-administering/security-checklist.md)。 請確定您已閱讀本文，並採取安裝所需的任何動作。

### 設定預設UI —— 最佳化觸控或傳統 {#configuring-the-default-ui-touch-optimized-or-classic}

AEM中有兩個可用的UI:

* 觸控最佳化UI
* Classic UI

您可以使用根對應來設定您所 [需的UI](/help/sites-deploying/osgi-configuration-settings.md)。

>[!NOTE]
>
>有關選擇UI的詳細資訊，請參閱「選 [擇您的UI](/help/sites-authoring/select-ui.md)」。

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素（例如儲存庫、Dispatcher等）都可安裝在IPv4和IPv6網路中。

由於無需特殊配置，因此操作是無縫的，如果需要，您只需使用適合您網路類型的格式來指定IP地址。

這表示當需要指定IP位址時，您可以（視需要）從以下位置選擇：

* IPv6地址

   例如 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

   例如 `https://123.1.1.4:4502`

* 伺服器名稱

   例如， `https://www.yourserver.com:4502`

* 對於IPv4和 `localhost` IPv6網路安裝，將解釋預設情況

   例如， `http://localhost:4502`

### 版本清除 {#version-purging}

在標準安裝中，每當您啟動頁面（更新內容後）時，AEM都會建立新版本的頁面或節點。您也可以使用側點的「版本控制」索引標籤，在要求時建立其他版本。 **** 所有這些版本都儲存在儲存庫中，並可以根據需要進行還原。

這些版本不會清除，因此儲存庫大小會隨著時間而增長，因此需要進行管理。

如需 [完整詳細資訊](/help/sites-deploying/version-purging.md) ，請參閱「版本清除」，尤其是 [Version Manager](/help/sites-deploying/version-purging.md#version-manager) ，以取得如何設定AEM在建立新版本時清除舊版的詳細資訊。

### 記錄 {#logging}

AEM提供您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定；例如，日誌消息的單個日誌檔案和格式

如需完 [整詳細資訊](/help/sites-deploying/configure-logging.md) ，請參閱記錄。

### 執行模式 {#run-modes}

執行模式可讓您針對特定用途調整AEM實例；例如作者或發佈、測試、開發或內部網路等。

這是透過為每個執行模式定義組態參數集合來完成的。 基本的配置參數集將應用於所有運行模式，然後您可以根據特定環境的目的調整其它配置參數集。 然後會視需要套用這些值。

所有配置設定都儲存在一個儲存庫中，並通過設定「運行模式」 **激活**。

如需完 [整詳細資訊](/help/sites-deploying/configure-runmodes.md) ，請參閱執行模式。

### 單一登入 {#single-sign-on}

單一登入(SSO)可讓使用者在提供驗證憑證（例如使用者名稱和密碼）一次後，存取多個系統。 另一個系統（稱為受信任驗證器）執行驗證，並為Experience manager提供用戶憑證。 Experience manager會檢查並強制使用者的存取權限（亦即決定允許使用者存取哪些資源）。

如需詳 [細資訊](/help/sites-deploying/single-sign-on.md) ，請參閱單一登入。

### 資源映射 {#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以使用這些映射來：

* 在所有請求前加 `/content` 上前置詞，如此內部結構就會對網站訪客隱藏。
* 定義重新導向，以便將網站頁 `/content/en/gateway` 面的所有請求重新導向至 `https://gbiv.com/`。

有關詳 [細資訊，請參閱資源映射](/help/sites-deploying/resource-mapping.md) 。

### 複製、反向複製和複製代理 {#replication-reverse-replication-and-replication-agents}

複製代理是AEM的中心，作為用於：

* [從作者發佈](/help/sites-authoring/publishing-pages.md) （啟用）內容至發佈環境。
* 從Dispatcher快取明確清除內容。
* 將使用者輸入（例如，表格輸入）從發佈環境傳回作者環境（在作者環境的控制下）。

有關詳細資訊，請參 [閱複製](/help/sites-deploying/replication.md)。

### OSGi配置設定 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 是AEM技術層的基本元素。 它用於控制AEM的組合束及其配置。

如需 [專案實作相關的各種叢集清單](/help/sites-deploying/osgi-configuration-settings.md) （依叢集列出），請參閱OSGi組態設定。 並非所有列出的設定都需要調整，有些設定會提及以協助您瞭解AEM的運作方式。

使用AEM時，有幾種方法可管理此類服務的組態設定；如需詳 [細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

### 配置LDAP {#configuring-ldap}

需要LDAP驗證才能驗證儲存在（中央）LDAP目錄（如Active Directory）中的用戶。 這有助於減少管理使用者帳戶所需的工作。

LDAP身份驗證發生在儲存庫級別，因此由儲存庫直接處理。 如需詳細資訊，請參 [閱「使用AEM設定LDAP](/help/sites-administering/ldap-config.md)」。

如需AEM中的使用者管理（包括存取權限的指派），請參閱「使用者 [管理與安全性」](/help/sites-administering/security.md)。

### 配置Dispatcher {#configuring-the-dispatcher}

Dispatcher是Adobe的快取和／或負載平衡工具。 使用Dispatcher也有助於保護您的AEM伺服器不受攻擊。 因此，您可以搭配使用 Dispatcher 與企業級 Web 伺服器，以提高 AEM 例項的安全性。

有關完整 [的詳細資訊](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) ，請參見Dispatcher [，特別是](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) Configuring the Dispatcher，以瞭解更多配置詳細資訊。

### 設定AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

隨著AEM檔案服務和AEM檔案安全性的發行，我們現在可以叫用LiveCycle檔案服務來轉換XFA表單、將檔案轉換為PDF，以及原則保護檔案。 請閱讀 [AEM liveCycle Connector](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) ，以取得詳細資訊。

### 作業卸載和拓撲管理 {#job-offloading-and-topology-administration}

[卸載](/help/sites-deploying/offloading.md) ，在拓撲中分發包含Experience manager實例的處理任務。 借由卸載，您可以使用特定的Experience manager實例來執行特定類型的處理。 專業化的處理可讓您最大化可用伺服器資源的使用。

拓撲是鬆散耦合的Experience manager群集，它們參與卸載。 群集由一個或多個Experience manager伺服器實例（單個實例被視為群集）組成。

有關如何查看或修改拓撲成員資格的詳細資訊，請參 [閱管理拓撲](/help/sites-deploying/offloading.md#administering-topologies) 。

### 配置歡迎控制台 {#configuring-the-welcome-console}

傳統UI的「歡迎使用」主控台提供AEM中各種主控台與功能的連結清單。

您可以設定可見的連結，如需詳細資訊，請 [參閱設定歡迎控制台](/help/sites-developing/customizing-the-welcome-console.md) 。

### 效能配置 {#configuring-for-performance}

[效能](/help/sites-deploying/configuring-performance.md) ，是專案的關鍵。 AEM（和／或基礎儲存庫）的某些方面可以設定為最佳化效能。

如需詳 [細資訊，請參閱](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 「設定效能」。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### Shared Data Store {#shared-data-store}

儲存庫資料儲存用於將大型二進位檔案的儲存從儲存庫卸載到單獨的區域，以便儲存庫樹內同一二進位檔案（例如映像）的多個實例只儲存一次。

此「儲存一次、多次引用」功能可以通過配置每個儲存庫的資料儲存以引用同一共用檔案系統位置來擴展，從而不僅為單個儲存庫樹提供服務，還為完全獨立的儲存庫提供服務。

這樣的資料儲存可以在同一群集中的不同節點之間共用，在同一安裝中不同的發佈和／或作者實例，甚至在不同安裝中完全不同的實例。

如需詳細資訊，請參 [閱設定資料儲存區和節點儲存區](/help/sites-deploying/data-store-config.md)。

## 進一步配置注意事項 {#further-configuration-considerations}

### 啟用HTTP over SSL {#enabling-http-over-ssl}

您可以啟用HTTP over SSL，以運用更安全的連線至您的伺服器。

如需詳 [細資訊，請參閱啟用HTTP over SSL](/help/sites-administering/ssl-by-default.md) 。

### AEM入口網站和Portlet {#aem-portals-and-portlets}

入口網站是提供個人化、單一登入、不同來源的內容整合，以及托管資訊系統表現層的網頁應用程式。 portlet元件還允許您在頁上嵌入portlet。 要訪問CQ5 WCM提供的內容，可以使用CQ5 Portal Director Portlet來安裝門戶伺服器。 您可以通過安裝、配置和將Portlet添加到門戶頁面來執行此操作。

有關詳 [細資訊，請參見Portal](/help/sites-administering/aem-as-portal.md) 和Portlet。

### 靜態對象的過期 {#expiration-of-static-objects}

靜態物件（例如圖示）不會變更。 因此，應將系統配置為不會過期（在合理的時間段內），從而減少不必要的通信。

如需詳 [細資訊，請參閱靜態物件](/help/sites-deploying/expiration-static-objects.md) 「過期」。

### 在Java程式中開啟FIle {#open-files-in-the-java-process}

每個Java進程都可以訪問檔案——這需要系統資源。 因此，會定義一個上限，即每個進程可同時訪問的檔案數。 如果超出此限制，可能會發生異常錯誤。

如果AEM程式超過此上限，則訊息「 `too many open files`」將會顯示於 `error.log`。

要避免此類例外，您需要：

1. 檢查您的AEM程式使用多少個開啟的檔案。

   如何進行此檢查將取決於實例運行的平台。 可以使用lsof(Unix)或Process Explorer(Windows)等實用程式。

   在開發和測試期間，應監控此值，以：

   * 確認檔案已視需要關閉
   * 確定所需的最大值（在各種情況下）

1. 設定允許的上限。

   新價值應同時滿足當前需求和未來任何峰值，因此最好將當前需求增加一倍。

   預設情況下， `serverctl` 配置 `CQ_MAX_OPEN_FILES` 為 `8192`;這應該足以適用於大多數情況。

### 設定Rich Text編輯器 {#configuring-the-rich-text-editor}

Rich **Text Editor** (**RTE**)為作者提供多種功能， [](/help/sites-authoring/rich-text-editor.md) 以編輯其文字內容；提供圖示、選擇方塊和選單，以提供所見即所得的體驗。

如需詳 [細資訊，請參閱設定Rich Text Editor](/help/sites-administering/rich-text-editor.md) 。

### 設定頁面編輯的還原 {#configuring-undo-for-page-editing}

有幾個屬性可控制編輯頁面的還原和重做命令的行為。 您可以設定這些項目，如需詳 [細資訊，請參閱設定頁面編輯的還原](/help/sites-administering/config-undo.md) 。

### 設定視訊元件 {#configuring-the-video-component}

視訊 [元件](/help/sites-authoring/default-components-foundation.md#video) ，可讓您將預先定義、現成可用的視訊元素置於頁面上。

若要正確進行轉碼，您的管理員必須 [個別安裝FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) 。 您也可以 [設定您的視訊描述檔](/help/sites-administering/config-video.md#configure-video-profiles) ，以便搭配html5元素使用。

### 設定和自訂報表 {#configuring-and-customizing-reports}

為協助您監控和分析執行個體的狀態，CQ提供了一組預設報表，可針對個別需求進行設定：

如需詳細 [資訊，請參閱報表自訂基本](/help/sites-administering/reporting.md#the-basics-of-report-customization) 。

### 設定電子郵件通知 {#configuring-email-notification}

CQ會傳送電子郵件通知給下列使用者：

* 已訂閱頁面事件，例如修改或複製。
* 已訂閱論壇活動。
* 必須在工作流程中執行步驟。

如需詳 [細資訊，請參閱設定電子郵件](/help/sites-administering/notification.md) 通知。

### 啟用頁面印象 {#enabling-page-impressions}

頁面印象會顯示在傳統 **UI網站** 「管理控制台」的「印象」欄中。 若要啟用頁面曝光的擷取，您必須進行設定：

* 在發佈例項上：

   * [日CQ WCM頁面統計資料](/help/sites-deploying/osgi-configuration-settings.md)

* 作者實例：

   * [Adobe頁面印象追蹤](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>在作者環境中設定Adobe頁面印象追蹤器可允許追蹤服務的匿名要求。

