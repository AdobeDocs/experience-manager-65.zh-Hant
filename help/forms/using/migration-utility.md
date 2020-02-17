---
title: 移轉AEM Forms資產和檔案
seo-title: 移轉AEM Forms資產和檔案
description: 移轉公用程式可讓您將AEM Forms資產和檔案從AEM 6.3 Forms或舊版移轉至AEM 6.4 Forms。
seo-description: 移轉公用程式可讓您將AEM Forms資產和檔案從AEM 6.3 Forms或舊版移轉至AEM 6.4 Forms。
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
translation-type: tm+mt
source-git-commit: 3226edb575de3d9f8bff53f5ca81e2957f37c544

---


# 移轉AEM Forms資產和檔案{#migrate-aem-forms-assets-and-documents}

移轉公用程式會將 [Adaptive Forms資產](../../forms/using/introduction-forms-authoring.md)、 [雲端設定和](/help/sites-developing/extending-cloud-config.md)[](/help/forms/using/cm-overview.md) Correponsent Management資產從舊版中使用的格式轉換為AEM 6.5 Forms中使用的格式。 運行遷移實用程式時，將遷移以下內容：

* 最適化表單的自訂元件
* 最適化表單與對應管理範本
* 雲端組態
* Commenting Management和調適性表單資產

>[!NOTE]
>
>如果升級不到位，對於Correponsement Management資產，您可以在每次導入資產時運行遷移。 對於通信管理遷移，您需要安裝Forms Compatibility Package。

## 移轉方法 {#approach-to-migration}

您可 [以從](../../forms/using/upgrade.md) AEM Forms 6.4、6.3或6.2升級至最新版的AEM Forms 6.5，或執行全新的安裝。 根據您是否升級了先前的安裝或執行了新安裝，您需要執行下列操作之一：

**就地升級**

如果您執行就地升級，升級的實例已具有資產和文檔。 不過，在使用資產和文檔之前，您需要安裝 [AEMFD相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括通信管理相容性包）

然後，您需要運行遷移實用程式來更新 [資產和文檔](#runningmigrationutility)。

**在安裝不當時**

如果安裝不當（新鮮），則您必須安裝 [AEMFD相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括通信管理相容性包），才能使用資產和文檔。

然後，您需要在新的設定中匯入資產套件（zip或cmp），然後執行移轉公用程式來更新 [資產和檔案](#runningmigrationutility)。 Adobe建議在新設定上建立新資產，但必須在執行移轉公用程式之後。

由於向後 [相容性相關的更改](/help/sites-deploying/backward-compatibility.md) ,crx-repository中幾個資料夾的位置將發生更改。 從先前的設定手動匯出和匯入相依性（自訂資料庫和資產）至新鮮環境。

## 繼續移轉前先閱讀 {#prerequisites}

對於通信管理資產：

* 對於從先前平台匯入的資產，會新增屬性： **fd:version=1.0**。
* 自從AEM 6.1 Forms起，便無法立即使用注釋。 先前新增的注釋可在資產中使用，但不會自動在介面上顯示。 您必須自訂AEM Forms使用者介面中的extendedProperties屬性，才能讓注釋可見。
* 在舊版（例如LiveCycle ES4）中，文字是使用Flex RichTextEditor編輯，但是由於使用AEM 6.1 Forms，所以會使用HTML編輯器。 由於此轉換和外觀的字型、字型大小和字型邊界可能與「作者」使用者介面的舊版不同。 但是，在轉譯時，字母看起來是相同的。
* 文字模組中的清單已改善，現在呈現的方式也不同。 可能會有視覺上的差異。 建議您演算並查看文字模組中使用清單的字母。
* 由於影像內容模組會轉換為DAM資產，而且在移轉期間會將版面和片段新增至表單，因此這些模組的「更新者」屬性會變更為管理員。
* 資產的版本記錄不會移轉，且移轉後無法使用。 後續版本歷史記錄在移轉後會維持。
* 自從AEM 6.1 Forms起，「準備發佈」狀態即已停用，因此「準備發佈」狀態中的所有資產都會變更為「已修改」狀態。
* 由於使用者介面已在AEM Forms 6.3中更新，因此執行自訂的步驟也不同。 如果您要從6.3之前的版本移轉，則需要重做自訂。
* 版面片段從/content/apps/cm/layouts/fragmentlayouts/1001移至/content/apps/cm/modules/fragmentlayouts。 資產中的資料字典參考會顯示資料字典的路徑，而非其名稱。
* 任何用於文本模組中對齊的制表符空格都需要重新調整。 如需詳細資訊，請參 [閱「對應管理——使用索引標籤間距來排列文字](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)」。
* 資產編排器組態變更為「對應管理」組態。
* 資產會移至檔案夾下，並加上「現有文字」和「現有清單」等名稱。

## 使用遷移實用程式 {#using-the-migration-utility}

### 運行遷移實用程式 {#runningmigrationutility}

在對資產進行任何更改或建立資產之前，運行遷移實用程式。 建議您在進行任何變更或建立資產後，不要執行公用程式。 請確定在移轉程式執行時，「對應管理」或「最適化表單資產」使用者介面未開啟。

首次運行遷移實用程式時，將建立具有以下路徑和名稱的日誌：\cq-quickstart\logs\aem-forms-migration.log。 此日誌會不斷更新「對應管理」和「最適化表單」移轉資訊，例如移動資產。

>[!NOTE]
>
>運行遷移實用程式之前，請確保您已備份了crx儲存庫。

1. 在瀏覽器工作階段中，以管理員身分登入AEM作者例項。

1. 在瀏覽器中開啟下列URL:

   https://[*hostname*]:[*port*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   瀏覽器會顯示4個選項：

   * AEM Forms 資產移轉
   * 最適化表單自訂元件移轉
   * 最適化表單範本移轉
   * AEM 表單雲端組態移轉

1. 執行下列操作以執行遷移：

   * 若要移 **轉資產**，請點選「AEM Forms Assets Migration」，然後在下一個畫面中，點選「 **開始移轉」**。 以下是移轉的項目：

      * 最適化表單
      * 檔案片段
      * 主題
      * 字母
      * 資料字典
   >[!NOTE]
   >
   >在資產移轉期間，您會發現警告訊息，例如「找到衝突……」。 這些消息表示無法遷移自適應表單中某些元件的規則。 例如，如果元件有同時具有規則和指令碼的事件，則規則在任何指令碼之後發生，則不會遷移元件的規則。 不過，這些規則可透過在最適化表單製作中開啟規則編輯器來移轉。
   >
   >
   >這些元件可在「最適化表單」編輯器的「規則編輯器」中開啟，以進行移轉。
   >
   >
   >
   >    * 若要在自訂元件中移轉規則和指令碼（若從6.3升級則不需要），請點選「最適化表單自訂元件移轉」，然後在下一個畫面中點選「開始移轉」。 以下是移轉的項目：   >
      >
      >
      >        

      * 使用規則編輯器（6.1 FP1和更新版本）建立的規則和指令碼
      >        * 使用6.1及舊版UI中的「指令碼」標籤建立的指令碼
   >
   >
   >    * 若要移轉範本（從6.3和6.4升級時不需要），請點選「最適化表單範本移轉」，然後在下一個畫面中點選「開始移轉」。 以下是移轉的項目：
      >
      >
      >
      >        


      * 舊範本——使用AEM 6.1 Forms或更早版本在/apps下建立的最適化表單範本。 這包括在模板元件中定義的指令碼。
      >        * 新範本——使用/conf下範本編輯器建立的最適化表單範本。 這包括移轉使用規則編輯器建立的規則和指令碼。


   * 若要移轉最適化表單自訂元件，請點選 **「最適化表單自訂元件移轉** 」，然後在「自訂元件移轉」頁面中，點選「 **開始移轉」**。 以下是移轉的項目：

      * 為Adaptive Forms編寫的自定義元件
      * 元件覆蓋（如果有）。
   * 若要移轉最適化表單範本，請點選「 **最適化表單範本移轉** 」，然後在「自訂元件移轉」頁面中點選「 **開始移轉」**。 以下是移轉的項目：

      * 使用AEM範本編輯器在/apps或/conf下建立的最適化表單範本。
   * 移轉AEM Forms cloud設定服務，以運用全新的內容感應雲端服務範例，其中包含觸控功能UI（在/conf下）。 當您移轉AEM Forms Cloud Configuration服務時，/etc中的雲端服務會移至/conf。 如果您沒有任何雲端服務自訂，這些自訂會依賴舊式路徑(/etc)，建議您在升級至6.5後立即執行移轉公用程式，並使用雲端設定Touch UI進行任何進一步的工作。 如果您有任何現有的雲端服務自訂，請在升級的設定上繼續使用傳統UI，直到自訂內容更新為與已移轉的路徑(/conf)一致，然後執行移轉公用程式。
   若要移轉 **AEM Forms雲端服務**（包括下列服務），請點選「AEM Forms雲端設定移轉」（雲端設定移轉獨立於AEMFD相容套件），點選「AEM Forms雲端設定移轉」，然後在「設定移轉」頁面上，點選「 **開始移轉」**:

   * 表單資料模型雲端服務

      * 源路徑：/etc/cloudservices/fdm
      * 目標路徑：/conf/global/settings/cloudconfigs/fdm
   * Recaptcha

      * 源路徑：/etc/cloudservices/recaptcha
      * 目標路徑：/conf/global/settings/cloudconfigs/recaptcha
   * Adobe Sign

      * 源路徑：/etc/cloudservices/echosign
      * 目標路徑：/conf/global/settings/cloudconfigs/echosign
   * Typekit雲端服務

      * 源路徑：/etc/cloudservices/typekit
      * 目標路徑：/conf/global/settings/cloudconfigs/typekit
   移轉程式進行時，瀏覽器視窗會顯示下列內容：

   * 更新資產時：資產已成功更新。
   * 移轉完成後：完成資產移轉。
   執行時，遷移實用程式執行以下操作：

   * **新增標籤至資產**:新增標籤「Correponsements Management:移轉資產」/「最適化表單：移轉資產」。 移轉資產，讓使用者能夠識別移轉的資產。 運行遷移實用程式時，系統中的所有現有資產都標籤為「已遷移」。
   * **產生標籤**:先前系統中出現的類別和子類別會建立為標籤，然後這些標籤會與AEM中的相關「對應管理」資產產生關聯。 例如，字母模板的類別（索賠）和子類別（索賠）將生成為標籤。

















1. 在遷移實用程式完成運行後，繼續執行內部 [任務](#housekeepingtasks)。

### 運行遷移實用程式後的內部管理任務 {#housekeepingtasks}

運行遷移實用程式後，請處理以下內部管理任務： [](../../forms/using/import-export-forms-templates.md)

1. 請確定XFA版本的版面和片段版面是3.3或更新版本。 如果您使用舊版的版面和片段版面，則在轉譯字母時可能會發生問題。 若要將舊版XFA更新為最新版本，請完成下列步驟：

   1. [從Forms使用者介面下載XFA](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) ，以zip檔案的形式。
   1. 解壓縮檔案。
   1. 在最新的設計工具中開啟XFA檔案並儲存它。 XFA的版本會更新為最新的版本。
   1. 在Forms使用者介面中上傳XFA。

1. 在移轉前發佈在先前系統中的所有資產。 移轉公用程式只會更新作者例項上的資產，並更新發佈例項上發佈資產時所需的資產。
1. 在AEM Forms 6.4和6.5中，部分表格使用者群組的權限會變更。 如果您希望任何使用者能夠上傳包含指令碼的XDP和Adaptive Forms，或使用程式碼編輯器，您需要將它們新增至Forms-power-users群組。 同樣地，範本作者也無法再使用規則編輯器中的程式碼編輯器。 為使用者能夠使用程式碼編輯器，請將它們新增至af-template-script-writer群組。 如需將使用者新增至群組的指示，請參 [閱管理使用者和使用者群組](/help/communities/users.md)。

