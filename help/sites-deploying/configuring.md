---
title: 基本配置概念
seo-title: 基本配置概念
description: 瞭解如何設AEM定。
seo-description: 瞭解如何設AEM定。
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: 設定
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2133'
ht-degree: 0%

---


# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM)安裝時會針對所有參數設定預設值，讓它「立即」執行。 不過，您可以針對AEM自己的特定需求進行設定。

可配置的AEM方面有很多：

* 有些項目通常為每個項目安裝[配置，必須進行審查以確認它們是否適用於您的項目。](#primary-configuration-considerations)
* [進一步](#further-configuration-considerations) 配置可能是常見的，但並非必要；與功能或系統效能與穩定性相關。
* 其他則只是某些可選功能的AEM必要項（這些功能與適當功能一起記錄）。

根據特定配置，這些更改可以使用：

* **Adobe CQ網路主控台**

   這是配置OSGi捆綁包和服務的標準位置。

   如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

* **存放庫**

   儲存庫中提供OSGi配置的子集。 這可確保複製或複製儲存庫內容重新建立相同的配置。 您也可以根據運行模式將自己的配置添加到儲存庫。

   有關詳細資訊，請參閱儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中的[OSGi配置，特別是[向儲存庫添加新配置。](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository)

* **檔案系統**

   檔案系統中有一些配置檔案。

* **WCM**

   在WCM本身可以配置AEM各種方面，許多方面使用[工具](/help/sites-administering/tools-consoles.md)控制台；例如，複製代理。

>[!NOTE]
>
>使用Adobe Experience Manager時，有幾種方法可管理OSGi服務（控制台或儲存庫節點）的配置設定。
>
>如需詳細資訊，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

>[!NOTE]
>
>設AEM定簡單明瞭，但您必須注意：
>
>某些變更可能會對應用程式產生重大影響。 因此，請先確定您有必要的經驗和知識，再開始設AEM定，並只進行您知道需要的變更。 通過OSGi控制台所做的任何更改都應用於運行的系統（不需要重新啟動）。****

## 主要配置注意事項{#primary-configuration-considerations}

此清單詳細列出了每個新項目通常配置的主要區域。 並非所有項目都需要，但必須閱讀並審查清單，以查看哪些項目適用。

此清單提供每個設定方面的簡短概述，以及提供完整詳細資訊之頁面的連結。

### 安全檢查清單{#security-checklist}

[安全檢查清單](/help/sites-administering/security-checklist.md)中列出了幾個關鍵配置問題。 請確定您已閱讀本文，並採取安裝所需的任何動作。

### 設定預設UI —— 最佳化觸控或經典{#configuring-the-default-ui-touch-optimized-or-classic}

有兩個UI可用於AEM:

* 觸控最佳化UI
* Classic UI

您可以使用[根映射](/help/sites-deploying/osgi-configuration-settings.md)來設定所需的UI。

>[!NOTE]
>
>有關選擇UI的詳細資訊，請參閱[選擇UI](/help/sites-authoring/select-ui.md)。

### IPv4和IPv6 {#ipv-and-ipv}

IPv4和IPv6AEM網路中可以同時安裝所有元素（如儲存庫、Dispatcher等）。

由於無需特殊配置，因此操作是無縫的，如果需要，您只需使用適合您網路類型的格式來指定IP地址。

這表示當需要指定IP位址時，您可以（視需要）從以下位置選擇：

* IPv6地址

   例如`https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

   例如`https://123.1.1.4:4502`

* 伺服器名稱

   例如，`https://www.yourserver.com:4502`

* `localhost`的預設情況將解釋為IPv4和IPv6網路安裝

   例如，`http://localhost:4502`

### 版本清除{#version-purging}

在標準安裝AEM中，每當您啟動頁面（更新內容後）時，都會建立頁面或節點的新版本。您也可以使用側點的&#x200B;**版本控制**&#x200B;標籤，在要求時建立其他版本。 所有這些版本都儲存在儲存庫中，並可以根據需要進行還原。

這些版本不會清除，因此儲存庫大小會隨著時間而增長，因此需要進行管理。

請參閱[版本清除](/help/sites-deploying/version-purging.md)以取得完整詳細資訊，尤其是[版本管理員](/help/sites-deploying/version-purging.md#version-manager)，以取得如何設定在建立新版本AEM時清除舊版的詳細資訊。

### 記錄 {#logging}

AEM提供您設定：

* 中央記錄服務的全局參數
* 要求資料記錄；要求資訊的專用記錄設定
* 個別服務的特定設定；例如，日誌消息的單個日誌檔案和格式

如需詳細資訊，請參閱[記錄](/help/sites-deploying/configure-logging.md)。

### 執行模式 {#run-modes}

運行模式允許您根據特定目AEM的調整實例；例如作者或發佈、測試、開發或內部網路等。

這是透過為每個執行模式定義組態參數集合來完成的。 基本的配置參數集將應用於所有運行模式，然後您可以根據特定環境的目的調整其它配置參數集。 然後會視需要套用這些值。

所有配置設定都儲存在一個儲存庫中，並通過設定&#x200B;**運行模式**&#x200B;激活。

如需詳細資訊，請參閱[執行模式](/help/sites-deploying/configure-runmodes.md)。

### 單一登入{#single-sign-on}

單一登入(SSO)可讓使用者在提供驗證憑證（例如使用者名稱和密碼）一次後，存取多個系統。 單獨的系統（稱為受信驗證器）執行該驗證並提供與用戶證書的Experience Manager。 Experience Manager會檢查並強制使用者的存取權限（亦即決定允許使用者存取哪些資源）。

如需詳細資訊，請參閱[單一登入](/help/sites-deploying/single-sign-on.md)。

### 資源映射{#resource-mapping}

資源對應用於定義重導、虛名URL和虛擬主機AEM。

例如，您可以使用這些映射來：

* 將所有請求前置詞`/content`，如此內部結構就會隱藏於您網站的訪客之外。
* 定義重新導向，以便將您網站的`/content/en/gateway`頁面的所有要求重新導向至`https://gbiv.com/`。

有關詳細資訊，請參見[資源映射](/help/sites-deploying/resource-mapping.md)。

### 複製、反向複製和複製代理{#replication-reverse-replication-and-replication-agents}

複製代理作為用AEM於：

* [從作者發佈(](/help/sites-authoring/publishing-pages.md) 啟用)內容至發佈環境。
* 從Dispatcher快取明確清除內容。
* 將使用者輸入（例如，表格輸入）從發佈環境傳回作者環境（在作者環境的控制下）。

有關詳細資訊，請參見[Replication](/help/sites-deploying/replication.md)。

### OSGi配置設定{#osgi-configuration-settings}

[](https://www.osgi.org/) OSG是OSG技術中的一個基本元AEM素。它用於控制複合束及其AEM配置。

有關與項目實施相關的各種捆綁包的清單（根據捆綁包列出），請參見[OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md)。 並非所有列出的設定都需要調整，有些設定會提及以協助您瞭解運作AEM方式。

使用時，有AEM幾種管理此類服務配置設定的方法；如需詳細資訊和建議的實務，請參閱[設定OSGi](/help/sites-deploying/configuring-osgi.md)。

### 配置LDAP {#configuring-ldap}

需要LDAP驗證才能驗證儲存在（中央）LDAP目錄（如Active Directory）中的用戶。 這有助於減少管理使用者帳戶所需的工作。

LDAP身份驗證發生在儲存庫級別，因此由儲存庫直接處理。 有關詳細資訊，請參見[使用&lt;a1/AEM>配置LDAP。](/help/sites-administering/ldap-config.md)

有關內部的用AEM戶管理（包括訪問權限的分配），請參閱[用戶管理和安全](/help/sites-administering/security.md)。

### 配置Dispatcher {#configuring-the-dispatcher}

Dispatcher是Adobe Experience Manager的快取和／或負載平衡工具，可與企業級Web伺服器一起使用。

有關完整詳細資訊，請參見[Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)，特別是[ Configuring the Dispatcher](https://helpx.adobe.com/tw/experience-manager/dispatcher/using/dispatcher-configuration.html) ，以瞭解更多配置詳細資訊。

### 配置AEMLiveCycle連接器{#configuring-aem-livecycle-connector}

隨著「檔案服務」和AEM「檔案安全性」的發AEM行，我們現在可以叫用LiveCycle檔案服務來轉換XFA表單、將檔案轉換為PDF並保護檔案的原則。 請閱讀[AEMLiveCycle連接器](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html)以取得詳細資訊。

### 作業卸載和拓撲管理{#job-offloading-and-topology-administration}

[分](/help/sites-deploying/offloading.md) 配在拓撲中分配處理任務的Experience Manager實例。透過卸載，您可以使用特定的Experience Manager例項來執行特定類型的處理。 專業化的處理可讓您最大化可用伺服器資源的使用。

拓撲是鬆散耦合的Experience Manager群集，它們參與卸載。 群集由一個或多個Experience Manager伺服器實例（單個實例被視為群集）組成。

有關如何查看或修改拓撲成員資格的詳細資訊，請參閱[管理拓撲](/help/sites-deploying/offloading.md#administering-topologies)一節。

### 配置歡迎控制台{#configuring-the-welcome-console}

傳統UI的歡迎控制台提供了指向中各種控制台和功能的連結列AEM表。

您可以設定可見的連結，如需詳細資訊，請參閱[設定歡迎控制台](/help/sites-developing/customizing-the-welcome-console.md)。

### 為效能配置{#configuring-for-performance}

[效](/help/sites-deploying/configuring-performance.md) 能是專案的關鍵。可以配置AEM（和／或基礎儲存庫）的某些方面以優化效能。

有關詳細資訊，請參見[配置效能](/help/sites-deploying/configuring-performance.md#configuring-for-performance)。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共用資料儲存{#shared-data-store}

儲存庫資料儲存用於將大型二進位檔案的儲存從儲存庫卸載到單獨的區域，以便儲存庫樹內同一二進位檔案（例如映像）的多個實例只儲存一次。

此「儲存一次、多次引用」功能可以通過配置每個儲存庫的資料儲存以引用同一共用檔案系統位置來擴展，從而不僅為單個儲存庫樹提供服務，還為完全獨立的儲存庫提供服務。

這樣的資料儲存可以在同一群集中的不同節點之間共用，在同一安裝中不同的發佈和／或作者實例，甚至在不同安裝中完全不同的實例。

有關詳細資訊，請參閱[配置資料儲存和節點儲存](/help/sites-deploying/data-store-config.md)。

## 進一步配置注意事項{#further-configuration-considerations}

### 啟用HTTP over SSL {#enabling-http-over-ssl}

您可以啟用HTTP over SSL，以運用更安全的連線至您的伺服器。

如需詳細資訊，請參閱[啟用HTTP over SSL](/help/sites-administering/ssl-by-default.md)。

### AEM門戶和Portlet {#aem-portals-and-portlets}

入口網站是提供個人化、單一登入、不同來源的內容整合，以及托管資訊系統表現層的網頁應用程式。 portlet元件還允許您在頁上嵌入portlet。 為了訪問CQ5 WCM提供的內容，門戶伺服器可以與CQ5門戶Director門戶Portlet配合。 您可以通過安裝、配置和將Portlet添加到門戶頁面來執行此操作。

有關詳細資訊，請參見[Portal和Portlet](/help/sites-administering/aem-as-portal.md)。

### 靜態對象{#expiration-of-static-objects}的過期時間

靜態物件（例如圖示）不會變更。 因此，應將系統配置為不會過期（在合理的時間段內），從而減少不必要的通信。

如需詳細資訊，請參閱[靜態物件的過期](/help/sites-deploying/expiration-static-objects.md)。

### 在Java進程{#open-files-in-the-java-process}中開啟FIle

每個Java進程都可以訪問檔案——這需要系統資源。 因此，會定義一個上限，即每個進程可同時訪問的檔案數。 如果超出此限制，可能會發生異常錯誤。

如果AEM進程超過此最大值，則`error.log`中將顯示消息&quot; `too many open files`&quot;。

要避免此類例外，您需要：

1. 檢查您的流程使用AEM的開啟檔案數。

   如何進行此檢查將取決於實例運行的平台。 可以使用lsof(Unix)或Process Explorer(Windows)等實用程式。

   在開發和測試期間，應監控此值，以：

   * 確認檔案已視需要關閉
   * 確定所需的最大值（在各種情況下）

1. 設定允許的上限。

   新價值應同時滿足當前需求和未來任何峰值，因此最好將當前需求增加一倍。

   預設情況下， `serverctl`將`CQ_MAX_OPEN_FILES`配置為`8192`;這應該足以適用於大多數情況。

### 配置富格文本編輯器{#configuring-the-rich-text-editor}

**富格文本編輯器**(**RTE**)為作者提供廣泛的[功能](/help/sites-authoring/rich-text-editor.md)以編輯其文本內容；提供圖示、選擇方塊和選單，以提供所見即所得的體驗。

如需詳細資訊，請參閱[設定Rich Text Editor](/help/sites-administering/rich-text-editor.md)。

### 設定頁面編輯的還原{#configuring-undo-for-page-editing}

有幾個屬性可控制編輯頁面的還原和重做命令的行為。 您可以設定這些項目，如需詳細資訊，請參閱[設定頁面編輯的還原。](/help/sites-administering/config-undo.md)

### 配置視頻元件{#configuring-the-video-component}

[視訊元件](/help/sites-authoring/default-components-foundation.md#video)可讓您將預先定義的現成可用視訊元素置於頁面上。

要正確進行轉碼，您的管理員必須分別安裝Fmpeg](/help/sites-administering/config-video.md#install-ffmpeg)。 [您也可以[設定您的視訊描述檔](/help/sites-administering/config-video.md#configure-video-profiles)以搭配html5元素使用。

### 設定和自訂報表{#configuring-and-customizing-reports}

為協助您監控和分析執行個體的狀態，CQ提供了一組預設報表，可針對個別需求進行設定：

如需詳細資訊，請參閱[報表自訂基礎](/help/sites-administering/reporting.md#the-basics-of-report-customization)。

### 配置電子郵件通知{#configuring-email-notification}

CQ會傳送電子郵件通知給下列使用者：

* 已訂閱頁面事件，例如修改或複製。
* 已訂閱論壇活動。
* 必須在工作流程中執行步驟。

如需詳細資訊，請參閱[設定電子郵件通知](/help/sites-administering/notification.md)。

### 啟用頁面印象{#enabling-page-impressions}

頁面曝光數會顯示在傳統UI網站管理主控台的&#x200B;**曝光數**&#x200B;欄中。 若要啟用頁面曝光的擷取，您必須進行設定：

* 在發佈例項上：

   * [日CQ WCM頁面統計資料](/help/sites-deploying/osgi-configuration-settings.md)

* 作者實例：

   * [Adobe頁面印象追蹤](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>作者環境上的Adobe頁面印象追蹤器設定將允許追蹤服務的匿名要求。

