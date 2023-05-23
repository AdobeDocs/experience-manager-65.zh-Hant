---
title: 基本配置概念
seo-title: Basic Configuration Concepts
description: 瞭解如何配AEM置。
seo-description: Learn how to configure AEM.
uuid: edcdd4bd-5917-417e-8913-40d488383ea9
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 2673ea92-1651-4b1b-9aac-f4ba8b36782e
feature: Configuring
exl-id: 3777a1ba-cc4e-41b9-9098-236f8141925f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 1%

---

# 基本配置概念{#basic-configuration-concepts}

Adobe Experience Manager(AEM)安裝時，所有參數的預設設定允許其「開箱即用」。 但是，您可以根據AEM自己的特定要求進行配置。

可以配置的AEM方面有很多：

* 有些 [通常為每個項目安裝配置](#primary-configuration-considerations) 並且必須進行審閱以確認它們是否適用於您的項目。
* [其他配置](#further-configuration-considerations) 可能是常見的，但並非勢在必行；與功能或系統效能和穩定性有關。
* 其他功能僅需要某些可選功AEM能（這些功能與相應功能一起記錄）。

根據特定配置，可以使用以下任一方法進行這些更改：

* **Adobe CQWeb控制台**

   這是配置OSGi捆綁包和服務的標準位置。

   請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 詳細資訊和建議的操作。

* **存放庫**

   OSGi配置的子集在儲存庫中可用。 這可確保複製或複製儲存庫內容重新建立相同的配置。 您還可以根據運行模式將自己的配置添加到儲存庫中。

   請參閱 [儲存庫中的OSGi配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) 特別是 [將新配置添加到儲存庫](/help/sites-deploying/configuring-osgi.md#adding-a-new-configuration-to-the-repository) 的上界。

* **檔案系統**

   檔案系統中有幾個配置檔案。

* **AEMWCM**

   在WCM本身中可以配置AEM各種方面，許多方面使用 [工具](/help/sites-administering/tools-consoles.md) 控制台；例如，複製代理。

>[!NOTE]
>
>在與Adobe Experience Manager合作時，有幾種方法管理OSGi服務（控制台或儲存庫節點）的配置設定。
>
>請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。

>[!NOTE]
>
>配AEM置很簡單，但必須知道：
>
>某些更改可能會對應用程式產生重大影響。 因此，在開始配置之前，請確保您擁有必要的經驗和知識AEM，並只進行您知道需要的更改。 通過OSGi控制台所做的任何更改 **立即** 應用到正在運行的系統（不需要重新啟動）。

## 主要配置注意事項 {#primary-configuration-considerations}

此清單詳細列出了為每個新項目通常配置的主要區域。 並非所有項目都需要，但必須閱讀並審查清單，以查看哪些項目適用。

該清單簡要概述了每個配置方面，以及指向提供完整詳細資訊的頁面的連結。

### 安全核對表 {#security-checklist}

中列出了幾個關鍵配置問題 [安全核對表](/help/sites-administering/security-checklist.md)。 請確保您閱讀此內容並採取安裝所需的任何操作。

### 配置預設UI — 觸控優化或經典 {#configuring-the-default-ui-touch-optimized-or-classic}

有兩個UI可供使用AEM:

* 觸控優化的UI
* 經典UI

可以配置所需的UI [根映射](/help/sites-deploying/osgi-configuration-settings.md)。

>[!NOTE]
>
>有關選擇UI的詳細資訊，請參閱 [選擇UI](/help/sites-authoring/select-ui.md)。

### IPv4和IPv6 {#ipv-and-ipv}

IPv4和IPv6網AEM絡中都可以安裝所有元素（如儲存庫、調度程式等）。

操作是無縫的，因為不需要特殊配置，在需要時，您只需使用適合您網路類型的格式指定IP地址即可。

這意味著，當需要指定IP地址時，您可以從以下位置（根據需要）選擇：

* IPv6地址

   例如 `https://[ab12::34c5:6d7:8e90:1234]:4502`

* IPv4地址

   例如 `https://123.1.1.4:4502`

* 伺服器名稱

   比如說， `https://www.yourserver.com:4502`

* 預設大小寫 `localhost` 將解釋為IPv4和IPv6網路安裝

   比如說， `http://localhost:4502`

### 版本清除 {#version-purging}

在標準安AEM裝中，無論何時激活頁面（更新內容後），都會建立頁面或節點的新版本。您還可以使用 **版本控制** 擊中了。 所有這些版本都儲存在儲存庫中，如果需要，可以恢復。

這些版本從不被清除，因此儲存庫大小會隨著時間的推移而增長，因此需要進行管理。

請參閱 [版本清除](/help/sites-deploying/version-purging.md) 詳細資訊，尤其是 [版本管理器](/help/sites-deploying/version-purging.md#version-manager) 有關如何配置以AEM在建立新版本時清除舊版本的詳細資訊。

### 記錄 {#logging}

提AEM供了配置：

* 中央日誌記錄服務的全局參數
* 請求資料記錄；請求資訊的專用日誌記錄配置
* 具體設定；例如，日誌消息的單個日誌檔案和格式

請參閱 [記錄](/help/sites-deploying/configure-logging.md) 的雙曲餘切值。

### 執行模式 {#run-modes}

運行模式允許您針對AEM特定目的調整實例；例如，作者或發佈、test、開發或內部網等。

這可以通過為每個運行模式定義配置參數的集合來完成。 所有運行模式都應用了一組基本的配置參數，然後您可以根據特定環境的目的調整其它設定。 然後根據需要應用這些。

所有配置設定都儲存在一個儲存庫中，並通過設定 **運行模式**。

請參閱 [運行模式](/help/sites-deploying/configure-runmodes.md) 的雙曲餘切值。

### 單一登錄 {#single-sign-on}

單一登錄(SSO)允許用戶在提供一次身份驗證憑據（如用戶名和密碼）後訪問多個系統。 單獨的系統（稱為受信任驗證器）執行該驗證並提供與用戶憑據的Experience Manager。 Experience Manager檢查並強制用戶的訪問權限（即確定允許用戶訪問哪些資源）。

請參閱 [單一登錄](/help/sites-deploying/single-sign-on.md) 的上界。

### 資源對應 {#resource-mapping}

資源映射用於定義重定向、虛擬URL和虛擬主AEM機。

例如，可以使用這些映射：

* 將所有請求前置詞為 `/content` 這樣內部結構就不會被訪問您網站的人看到。
* 定義重定向，以便向 `/content/en/gateway` 將網站的頁面重定向到 `https://gbiv.com/`。

請參閱 [資源映射](/help/sites-deploying/resource-mapping.md) 的上界。

### 複製、反向複製和複製代理 {#replication-reverse-replication-and-replication-agents}

複製代理作為用AEM於以下操作的機制的中心：

* [發佈（激活）](/help/sites-authoring/publishing-pages.md) 從作者到發佈環境的內容。
* 顯式刷新Dispatcher快取中的內容。
* 將用戶輸入（例如，表單輸入）從發佈環境返回給作者環境（在作者環境的控制下）。

有關詳細資訊，請參閱 [複製](/help/sites-deploying/replication.md)。

### OSGi配置設定 {#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) 是技術層面的一個基本要AEM素。 它用於控制複合束及其AEM結構。

請參閱 [OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md) 列出與項目實施相關的各種捆綁包（根據捆綁包列出）。 並非所有列出的設定都需要調整，有些設定可幫助您瞭解操作AEM方式。

使用時，AEM有幾種方法管理此類服務的配置設定；見 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的子菜單。

### 配置LDAP {#configuring-ldap}

對儲存在（中央）LDAP目錄（如Active Directory）中的用戶進行身份驗證需要LDAP身份驗證。 這有助於減少管理用戶帳戶所需的工作。

LDAP身份驗證在儲存庫級別進行，因此由儲存庫直接處理。 有關詳細資訊，請參閱 [使用配置LDAPAEM](/help/sites-administering/ldap-config.md)。

有關內的用戶管AEM理（包括訪問權限的分配），請參閱 [用戶管理和安全](/help/sites-administering/security.md)。

### 配置Dispatcher {#configuring-the-dispatcher}

Dispatcher 是 Adobe Experience Manager 的快取及/或負載平衡工具，可搭配企業級網頁伺服器使用。

請參閱 [調度程式](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) 詳細資訊，尤其是 [配置Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html) 的子菜單。

### 配置AEMLiveCycle連接器 {#configuring-aem-livecycle-connector}

隨著文檔服務和AEM文檔安全AEM性的發佈，我們現在能夠調用LiveCycle文檔服務來呈現XFA表單、將文檔轉換為PDF並策略保護文檔。 請閱讀 [AEMLiveCycle](https://helpx.adobe.com/livecycle/help/aem/aem-livecycle-connector.html) 的子菜單。

### 作業卸載和拓撲管理 {#job-offloading-and-topology-administration}

[卸載](/help/sites-deploying/offloading.md) 在拓撲中分配處理任務量Experience Manager實例。 在卸載時，可以使用特定的Experience Manager實例來執行特定類型的處理。 專用處理使您能夠最大限度地利用可用的伺服器資源。

拓撲是鬆散耦合的Experience Manager群集，參與卸載。 群集由一個或多個Experience Manager伺服器實例（單個實例被視為群集）組成。

有關如何查看或修改拓撲成員身份的詳細資訊，請參閱 [管理拓撲](/help/sites-deploying/offloading.md#administering-topologies) 的子菜單。

### 配置歡迎控制台 {#configuring-the-welcome-console}

經典UI的「歡迎」控制台提供指向中各種控制台和功能的鏈AEM接。

可以配置可見的連結，請參見 [配置歡迎控制台](/help/sites-developing/customizing-the-welcome-console.md) 的上界。

### 配置效能 {#configuring-for-performance}

[效能](/help/sites-deploying/configuring-performance.md) 是你項目的關鍵。 可以配置AEM（和/或基礎儲存庫）的某些方面以優化效能。

請參閱 [配置效能](/help/sites-deploying/configuring-performance.md#configuring-for-performance) 的上界。

<!--delete ### Scaling {#scaling}

Scaling a CQ installation correctly depends greatly on the details of your particular use case. A detailed discussion of solution patterns for various situations can be found in [Scaling CQ](/help/sites-deploying/scaling.md).-->

### 共用資料儲存 {#shared-data-store}

儲存庫資料儲存用於將大型二進位檔案的儲存從儲存庫卸載到適當的單獨區域，從而儲存庫樹內相同二進位檔案（例如影像）的多個實例只儲存一次。

此「儲存一次、引用多次」功能可擴展為不僅服務於單個儲存庫樹，而且服務於完全獨立的儲存庫，方法是將每個儲存庫的資料儲存配置為引用同一共用檔案系統位置。

這樣的資料儲存可以在同一群集中的不同節點、同一安裝中的不同發佈和/或作者實例之間共用，甚至可以在不同安裝中完全獨立的實例之間共用。

有關詳細資訊，請參見 [配置資料儲存和節點儲存](/help/sites-deploying/data-store-config.md)。

## 進一步配置注意事項 {#further-configuration-considerations}

### 啟用HTTP over SSL {#enabling-http-over-ssl}

您可以啟用HTTP over SSL，以使用更安全的連接連接到伺服器。

請參閱 [啟用HTTP over SSL](/help/sites-administering/ssl-by-default.md) 的上界。

### 門AEM戶和Portlet {#aem-portals-and-portlets}

門戶是一個Web應用程式，它提供個性化、單一登錄、來自不同來源的內容整合，並承載資訊系統的呈現層。 Portlet元件還允許您將Portlet嵌入到頁面中。 為了訪問CQ5 WCM提供的內容，門戶伺服器可以配置CQ5門戶Director門戶Portlet。 可以通過安裝、配置和將portlet添加到門戶頁面來完成此操作。

請參閱 [門戶和Portlet](/help/sites-administering/aem-as-portal.md) 的上界。

### 靜態對象的到期 {#expiration-of-static-objects}

靜態對象（例如，表徵圖）不會更改。 因此，應配置系統，使其不會過期（在合理的時間段內），從而減少不必要的通信量。

請參閱 [靜態對象的到期](/help/sites-deploying/expiration-static-objects.md) 的上界。

### 在Java進程中開啟FIle {#open-files-in-the-java-process}

每個java進程都可以訪問檔案 — 這需要系統資源。 因此，對允許每個進程同時訪問的檔案數定義了上限。 如果超出此範圍，則可能出現異常錯誤。

如果進AEM程超過此最大值，則消息&#39;&#39; `too many open files`將在 `error.log`。

要避免此類例外，您需要：

1. 檢查進程正在使AEM用的開啟檔案數。

   如何進行此檢查將取決於實例運行的平台。 可以使用lsof(Unix)或Process Explorer(Windows)等實用程式。

   在開發和測試期間應監控此值，以：

   * 確認檔案正在根據需要關閉
   * 確定所需的最大值（在各種情況下）

1. 設定允許的最大值。

   新值應同時滿足當前需求和未來任何峰值，因此建議將當前需求增加一倍。

   預設情況下， `serverctl` 配置 `CQ_MAX_OPEN_FILES` 至 `8192`;這應該足以應對大多數情況。

### 配置富格文本編輯器 {#configuring-the-rich-text-editor}

的 **富格文本編輯器** (**RTE**)為作者提供了 [功能](/help/sites-authoring/rich-text-editor.md) 編輯文字內容；為他們提供表徵圖、選擇框和菜單，以獲得WYSIWYG體驗。

請參閱 [配置富格文本編輯器](/help/sites-administering/rich-text-editor.md) 的上界。

### 為頁面編輯配置撤消 {#configuring-undo-for-page-editing}

有幾個屬性可控制用於編輯頁面的撤消和重做命令的行為。 可以配置這些，請參見 [為頁面編輯配置撤消](/help/sites-administering/config-undo.md) 的上界。

### 配置視頻元件 {#configuring-the-video-component}

的 [視頻元件](/help/sites-authoring/default-components-foundation.md#video) 允許您將預定義的現成視頻元素放置在頁面上。

要進行正確的轉碼，您的管理員必須 [安裝FFmpeg](/help/sites-administering/config-video.md#install-ffmpeg) 單獨進行。 他們也 [配置視頻配置檔案](/help/sites-administering/config-video.md#configure-video-profiles) 用於html5元素。

### 配置和自定義報告 {#configuring-and-customizing-reports}

為幫助您監視和分析實例的狀態，CQ提供了選擇的預設報告，這些報告可根據您的個別要求進行配置：

查看 [報表自定義基礎](/help/sites-administering/reporting.md#the-basics-of-report-customization) 的上界。

### 配置電子郵件通知 {#configuring-email-notification}

CQ向以下用戶發送電子郵件通知：

* 已訂閱頁事件，例如修改或複製。
* 已訂閱論壇活動。
* 必須在工作流中執行步驟。

請參閱 [配置電子郵件通知](/help/sites-administering/notification.md) 的上界。

### 啟用頁面印象 {#enabling-page-impressions}

頁面印象顯示在 **印象** 經典UI siteadmin控制台的列。 要啟用頁面印象的捕獲，您需要配置：

* 在發佈實例上：

   * [第CQ WCM天頁統計資訊](/help/sites-deploying/osgi-configuration-settings.md)

* 在作者案例中：

   * [Adobe頁面印象跟蹤](/help/sites-deploying/osgi-configuration-settings.md)

>[!CAUTION]
>
>在作者環境上配置Adobe頁印象跟蹤器將允許對跟蹤服務進行匿名請求。
