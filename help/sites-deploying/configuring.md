---
title: 基本設定概念
description: 瞭解如何針對您自己的特定需求設定Adobe Experience Manager。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 8f638eb384bdca59fb6f4f8990643e64f34622ce
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 0%

---

# 基本設定概念{#basic-configuration-concepts}

Adobe Experience Manager (AEM)已安裝所有引數的預設設定，允許其「立即可用」。 不過，您可以根據自己的特定需求設定AEM。

AEM有許多方面可供設定：

* 某些是每個專案安裝通常都設定的[&#128279;](#primary-configuration-considerations)，必須檢閱以確認它們是否適用於您的專案。
* [其他組態](#further-configuration-considerations)可能為通用組態，但不是必要組態；與功能或系統效能與穩定性相關。
* 只有AEM的特定選用功能才需要其他功能（這些功能會與適當的功能一併記錄）。

視特定設定而定，您可以使用下列任一專案來進行這些變更：

* **Adobe CQ Web Console**

  這是設定OSGi套件組合和服務的標準位置。

  請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)，以取得詳細資訊和建議的作法。

* **存放庫**

  存放庫中提供OSGi設定的子集。 這可確保複製或複製存放庫內容可重新建立相同的設定。 您也可以將自己的設定（取決於執行模式）新增到存放庫。

  請參閱存放庫中的[OSGi組態](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，特別是[新增組態至存放庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)以取得更多詳細資料。

* **檔案系統**

  檔案系統內有一些組態檔。

* **AEM WCM**

  您可以在AEM WCM本身中設定各種層面，許多方面都是使用[工具](/help/sites-administering/tools-consoles.md)主控台；例如，復寫代理程式。

>[!NOTE]
>
>使用Adobe Experience Manager時，有數種方法可管理OSGi服務的組態設定（主控台或存放庫節點）。
>
>如需完整詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>AEM的設定簡單明瞭。 不過，某些變更可能會對應用程式產生重大影響。 因此，在開始設定AEM之前，請確定您具備必要的經驗和知識，並只進行您知道必要的變更。 透過OSGi主控台所做的任何變更會&#x200B;**立即**&#x200B;套用至執行中的系統（不需要重新啟動）。

## 主要設定考量事項 {#primary-configuration-considerations}

此清單詳細說明每個新專案通常設定的主要區域。 並非所有專案都需要，但必須閱讀並檢閱清單，以檢視哪些專案適用於您的專案。

清單提供每個設定層面的簡短概觀，以及提供完整詳細資訊的頁面連結。

### 安全性檢查清單 {#security-checklist}

[安全性檢查清單](/help/sites-administering/security-checklist.md)中列出了幾個主要設定問題。 請務必閱讀本文，並採取安裝所需的任何動作。

### 設定預設UI — 觸控最佳化或Classic {#configuring-the-default-ui-touch-optimized-or-classic}

在AEM中有兩個UI可供使用：

* 觸控最佳化的UI
* 傳統UI

您可以使用[根對應](/help/sites-deploying/osgi-configuration-settings.md)來設定所需的UI。

>[!NOTE]
>
>在[選取您的UI](/help/sites-authoring/select-ui.md)下可取得有關選取UI的更多資訊。

### IPv4和IPv6 {#ipv-and-ipv}

AEM的所有元素(例如存放庫和Dispatcher)都可以安裝在IPv4和IPv6網路中。

操作是順暢的，因為不需要特殊設定，當需要時，您只需使用適合您網路型別的格式來指定IP位址。

這表示當必須指定IP位址時，您可以（視需要）從以下選取：

* IPv6位址

  例如，`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4位址

  例如，`https://123.1.1.4:4502`

* 伺服器名稱

  例如，`https://www.yourserver.com:4502`

* 將為IPv4和IPv6網路安裝解譯`localhost`的預設案例

  例如，`http://localhost:4502`

### 版本清除 {#version-purging}

在標準安裝中，每當啟動頁面（更新內容後）時，AEM都會建立頁面或節點的版本。 您也可以使用sidekick的&#x200B;**版本設定**&#x200B;索引標籤，依要求建立其他版本。 所有這些版本都儲存在存放庫中，並可在必要時還原。

這些版本永遠不會清除，因此存放庫大小會隨著時間增長，因此必須加以管理。

請參閱[版本清除](/help/sites-deploying/version-purging.md)以取得完整詳細資訊，特別是[版本管理員](/help/sites-deploying/version-purging.md#version-manager)，以取得如何設定AEM在建立新版本時清除舊版本的詳細資訊。

### 記錄 {#logging}

AEM可讓您設定：

* 中央記錄服務的全域引數
* 請求資料記錄；請求資訊的專用記錄設定
* 個別服務的特定設定；例如，個別記錄檔和記錄訊息的格式

如需完整詳細資訊，請參閱[記錄](/help/sites-deploying/configure-logging.md)。

### 執行模式 {#run-modes}

執行模式可讓您針對特定目的調整AEM執行個體。 例如，作者或發佈、測試、開發或內部網路等。

若要這麼做，請為每個執行模式定義設定引數集合。 所有執行模式都會套用一組基本組態引數，然後您就可以根據特定環境的目的調整其他組。 然後視需要套用這些引數。

所有組態設定都儲存在單一存放庫中，並透過設定&#x200B;**執行模式**&#x200B;來啟動。

如需完整詳細資訊，請參閱[執行模式](/help/sites-deploying/configure-runmodes.md)。

### 單一登入 {#single-sign-on}

單一登入(SSO)可讓使用者在提供一次驗證認證（例如使用者名稱和密碼）之後存取多個系統。 另一個系統（稱為信任的驗證者）會執行驗證並向Experience Manager提供使用者認證。 Experience Manager會檢查並強制使用者的存取許可權（即決定允許使用者存取哪些資源）。

如需詳細資訊，請參閱[單一登入](/help/sites-deploying/single-sign-on.md)。

### 資源對應 {#resource-mapping}

資源對應可用來定義AEM的重新導向、虛名URL和虛擬主機。

例如，您可以使用這些對應來：

* 請在所有要求加上前置詞`/content`，使您的網站訪客無法看見內部結構。
* 定義重新導向，將網站`/content/en/gateway`頁面的所有要求重新導向至`https://gbiv.com/`。

如需詳細資訊，請參閱[資源對應](/help/sites-deploying/resource-mapping.md)。

### 復寫、反向復寫和復寫代理程式 {#replication-reverse-replication-and-replication-agents}

復寫代理程式是AEM的核心，因為此機制可用於：

* 從作者[發佈（啟動）](/help/sites-authoring/publishing-pages.md)內容至發佈環境。
* 明確從Dispatcher快取排清內容。
* 將使用者輸入（例如表單輸入）從發佈環境傳回至作者環境（在作者環境的控制下）。

如需詳細資訊，請參閱[復寫](/help/sites-deploying/replication.md)。

### OSGi組態設定 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/)是AEM技術棧疊中的基本元素。 它可用來控制AEM的複合套件組合及其設定。

請參閱[OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md)，以取得與專案實作相關的各種組合清單（依組合列出）。 並非列出的所有設定都需要調整，有些是為了協助您瞭解AEM的運作方式。

使用AEM時，有數種方法可管理此類服務的組態設定；請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)以取得詳細資訊和建議的作法。

### 設定LDAP {#configuring-ldap}

需要LDAP驗證，才能驗證儲存在（中央） LDAP目錄（例如Active Directory）中的使用者。 這有助於減少管理使用者帳戶所需的工作。

LDAP驗證會在存放庫層級進行，因此會直接由存放庫處理。 如需詳細資訊，請參閱[使用AEM設定LDAP](/help/sites-administering/ldap-config.md)。

如需AEM中的使用者管理（包括存取許可權指派），請參閱[使用者管理與安全性](/help/sites-administering/security.md)。

### 設定 Dispatcher {#configuring-the-dispatcher}

Dispatcher是Adobe Experience Manager的快取或/及負載平衡工具。 它可以搭配企業級網頁伺服器使用。

如需完整詳細資訊，請參閱[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)，特別是[設定Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=zh-Hant)以取得進一步的設定詳細資料。

### 設定AEM LiveCycle Connector {#configuring-aem-livecycle-connector}

隨著AEM Doc Services和AEM Doc Security的發行，AEM現在能夠叫用LiveCycle檔案服務來轉譯XFA表單、將檔案轉換為PDF以及原則保護檔案。

### 工作解除安裝與拓撲管理 {#job-offloading-and-topology-administration}

[解除安裝](/help/sites-deploying/offloading.md)會將處理工作分散到拓撲中的Experience Manager執行個體。 透過解除安裝，您可以使用特定的Experience Manager執行個體來執行特定型別的處理。 專業化的處理可讓您最大限度地使用可用的伺服器資源。

拓撲是鬆散耦合的Experience Manager叢集，參與解除安裝。 叢集包含一或多個Experience Manager伺服器執行個體（單一執行個體視為叢集）。

如需如何檢視或修改拓撲成員資格的詳細資訊，請參閱[管理拓撲](/help/sites-deploying/offloading.md#administering-topologies)區段。

### 設定歡迎主控台 {#configuring-the-welcome-console}

傳統UI的「歡迎」主控台提供AEM中各種主控台和功能的連結清單。

可以設定可見的連結，請參閱[設定歡迎主控台](/help/sites-developing/customizing-the-welcome-console.md)以取得更多詳細資料。

### 設定效能 {#configuring-for-performance}

[效能](/help/sites-deploying/configuring-performance.md)是專案的關鍵。 AEM的某些層面（和/或基礎存放庫）可設定為最佳化效能。

如需詳細資訊，請參閱[設定效能](/help/sites-deploying/configuring-performance.md#configuring-for-performance)。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共用的資料存放區 {#shared-data-store}

儲存區域資料存放區可用來將大型二進位檔的儲存空間從儲存區域解除安裝至個別區域，因此儲存區域樹狀結構中同一個二進位檔（例如影像）的多個執行個體只會儲存一次。

此「一次儲存、多次參照」功能可進一步擴展，不僅提供單一存放庫樹狀結構，也提供完全不同的存放庫，方法是將每個存放庫的資料存放區設定為參照相同的共用檔案系統位置。

這類資料存放區可在相同叢集中的不同節點、相同安裝中的不同發佈和/或製作執行個體或甚至不同安裝中的完全不同執行個體之間共用。

如需詳細資訊，請參閱[設定資料存放區和節點存放區](/help/sites-deploying/data-store-config.md)。

## 其他設定考量事項 {#further-configuration-considerations}

### 啟用HTTP over SSL {#enabling-http-over-ssl}

您可以啟用透過SSL的HTTP，以採用與伺服器的更安全連線。

如需詳細資訊，請參閱[啟用HTTP over SSL](/help/sites-administering/ssl-by-default.md)。

### AEM入口網站和Portlet {#aem-portals-and-portlets}

入口網站是一種網頁應用程式，可提供個人化、單一登入、不同來源的內容整合，並代管資訊系統的展示層。 Portlet元件也可讓您在頁面上嵌入Portlet。 若要存取CQ5 WCM提供的內容，入口網站伺服器可配備CQ5 Portal Director Portlet。 您可以安裝、設定Portlet並將其新增至入口網站頁面，以執行此操作。

如需詳細資訊，請參閱[入口網站和Portlet](/help/sites-administering/aem-as-portal.md)。

### 靜態物件的到期日 {#expiration-of-static-objects}

靜態物件（例如圖示）不會變更。 因此，系統應設定為不會過期（在合理的時間範圍內），並減少不必要的流量。

如需詳細資訊，請參閱[靜態物件到期](/help/sites-deploying/expiration-static-objects.md)。

### 在Java™處理序中開啟檔案 {#open-files-in-the-java-process}

每個Java™程式都可以存取檔案 — 這需要系統資源。 因此，上限被定義為每個程式可同時存取多少檔案。 如果超過此限制，可能會發生例外狀況錯誤。

如果AEM處理序超過此最大值，則在`error.log`中會看到訊息「`too many open files`」。

若要避免此類例外，請執行下列動作：

1. 檢查您的AEM程式正在使用多少開啟的檔案。

   此檢查取決於執行個體的平台。 您可以使用lsof (UNIX®)或Process Explorer (Windows)等公用程式。

   在開發和測試期間應監控此值，以：

   * 確認檔案已視需要關閉
   * 以決定所需的最大值（在各種情況下）

1. 設定允許的最大值。

   新值應同時符合目前的需求和任何未來的尖峰，因此建議將目前的需求加倍。

   依預設，`serverctl`會將`CQ_MAX_OPEN_FILES`設定為`8192`；這應該足以應付大多數的情況。

### 設定RTF編輯器 {#configuring-the-rich-text-editor}

**RTF編輯器** (**RTE**)為作者提供各種[功能](/help/sites-authoring/rich-text-editor.md)，用於編輯其文字內容；為作者提供圖示、選取方塊和功能表，以提供WYSIWYG體驗。

如需詳細資訊，請參閱[設定RTF編輯器](/help/sites-administering/rich-text-editor.md)。

### 設定頁面編輯的復原 {#configuring-undo-for-page-editing}

有數個屬性可控制編輯頁面的還原和重做命令的行為。 這些可設定，如需詳細資訊，請參閱[設定頁面編輯的復原](/help/sites-administering/config-undo.md)。

### 設定視訊元件 {#configuring-the-video-component}

[視訊元件](/help/sites-authoring/default-components-foundation.md#video)可讓您在頁面上放置預先定義的現成視訊元素。

若要進行適當的轉碼，您的管理員必須分別[安裝FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg)。 他們也可以[設定您的視訊設定檔](/help/sites-administering/config-video.md#configure-video-profiles)以搭配html5元素使用。

### 設定和自訂報表 {#configuring-and-customizing-reports}

為協助您監控及分析執行個體的狀態，CQ提供了一組預設報表，您可依個別需求加以設定：

如需詳細資訊，請參閱[報表自訂基本概念](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

### 設定電子郵件通知 {#configuring-email-notification}

CQ傳送電子郵件通知給使用者，符合以下條件：

* 已訂閱頁面事件，例如，修改或復寫。
* 已訂閱論壇活動。
* 必須在工作流程中執行步驟。

如需詳細資訊，請參閱[設定電子郵件通知](/help/sites-administering/notification.md)。

### 啟用頁面印象 {#enabling-page-impressions}

頁面曝光數會顯示在傳統UI Siteadmin Console的&#x200B;**曝光數**&#x200B;欄中。 若要啟用頁面印象的擷取，請設定下列專案：

* 在發佈執行個體上：

   * [Day CQ WCM頁面統計資料](/help/sites-deploying/osgi-configuration-settings.md)

* 在作者執行個體上：

   * [Adobe頁面印象追蹤器](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>作者環境上的Adobe頁面曝光數追蹤器設定允許向追蹤服務提出匿名請求。
