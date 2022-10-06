---
title: 移轉 AEM Forms 資產和文件
seo-title: Migrate AEM Forms assets and documents
description: 移轉公用程式可讓您將AEM Forms資產和檔案從AEM 6.3 Forms或舊版移轉至AEM 6.4 Forms。
seo-description: The Migration utility allows you to Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
uuid: a3fdf940-7fc2-441c-91c8-ad66ba47e5f2
content-type: reference
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-strategy: max-2018
discoiquuid: 39dfef85-d047-4b6d-a0f5-92bd77df103b
docset: aem65
role: Admin
exl-id: 0f9aab7d-8e41-449a-804b-7e1bfa90befd
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 1%

---

# 移轉 AEM Forms 資產和文件{#migrate-aem-forms-assets-and-documents}

移轉公用程式會轉換 [適用性Forms資產](../../forms/using/introduction-forms-authoring.md), [雲配置](/help/sites-developing/extending-cloud-config.md)，和 [通信管理資產](/help/forms/using/cm-overview.md) 從舊版中使用的格式轉換為AEM 6.5 Forms中使用的格式。 當您執行移轉公用程式時，會移轉下列項目：

* 最適化表單的自訂元件
* 適用性表單和通信管理範本
* 雲配置
* 通信管理和最適化表單資產

>[!NOTE]
>
>如果升級不當，若是通信管理資產，您可以在每次匯入資產時執行移轉。 若是通信管理移轉，您必須安裝Forms相容性套件。

## 遷移方法 {#approach-to-migration}

您可以 [升級](../../forms/using/upgrade.md) 從AEM Forms 6.4、6.3或6.2升級至AEM Forms 6.5的最新版本，或執行全新安裝。 根據您是升級了以前的安裝還是執行了最新安裝，您需要執行以下操作之一：

**就地升級**

如果您執行就地升級，升級的執行個體已擁有資產和檔案。 不過，您必須先安裝資產和檔案，才能使用 [AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括通信管理相容性包）

接著，您需要更新資產和檔案，依 [運行遷移實用程式](#runningmigrationutility).

**如果安裝不到位**

如果安裝過程不當（最新），則您必須先安裝，才能使用資產和檔案 [AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括通信管理相容性套件）。

然後，您需要在新的設定上匯入資產套件（zip或cmp），然後依以下方式更新資產和檔案： [運行遷移實用程式](#runningmigrationutility). Adobe建議僅在執行移轉公用程式後，才在新設定上建立新資產。

因 [向後相容性相關](/help/sites-deploying/backward-compatibility.md) 變更，crx-repository中一些資料夾的位置會變更。 手動從先前的設定將相依性（自訂程式庫和資產）匯出並匯入至全新環境。

## 請先閱讀，再繼續移轉 {#prerequisites}

對於通信管理資產：

* 針對從上一個平台匯入的資產，會新增屬性： **fd:version=1.0**.
* 自AEM 6.1 Forms起，無法立即使用註解。 先前新增的註解可在資產中使用，但不會自動顯示在介面上。 您需要自訂AEM Forms使用者介面中的extendedProperties屬性，才能顯示註解。
* 在部分舊版(例如LiveCycleES4)中，文字是使用Flex RichTextEditor編輯，但自AEM 6.1 Forms起，使用HTML編輯器。 由於字型的呈現和外觀，字型大小和字型邊距可能與「作者」使用者介面中的舊版不同。 不過，轉譯後的字母看起來一樣。
* 文字模組中的清單已有所改善，現在呈現的方式也有所不同。 可能有視覺上的差異。 建議您呈現並查看文字模組中使用清單的信函。
* 由於影像內容模組會轉換為DAM資產，且配置和片段會在移轉期間新增至表單，因此這些模組的「更新者」屬性會變更為管理員。
* 資產的版本記錄不會移轉，且在移轉後無法使用。 移轉後會維護後續的版本記錄。
* 自AEM 6.1 Forms以來，「準備發佈」狀態已遭取代，因此「準備發佈」狀態中的所有資產都會變更為「已修改」狀態。
* 由於使用者介面已在AEM Forms 6.3中更新，因此執行自訂的步驟也不同。 如果您要從6.3之前的版本移轉，則需要重做自訂。
* 版面片段從/content/apps/cm/layouts/fragmentlayouts/1001移至/content/apps/cm/modules/fragmentlayouts。 資產中的資料字典參考會顯示資料字典的路徑，而非其名稱。
* 需要重新調整文本模組中用於對齊的任何tab空格。 如需詳細資訊，請參閱 [通信管理 — 使用頁簽間距排列文本](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* 資產撰寫器設定對通信管理設定的變更。
* 資產會移至資料夾下，且名稱如「現有文字」和「現有清單」。

## 使用移轉公用程式 {#using-the-migration-utility}

### 運行遷移實用程式 {#runningmigrationutility}

在對資產進行任何變更或建立資產之前，請執行移轉公用程式。 建議您在進行任何變更或建立資產後，不要執行公用程式。 請確定在移轉程式執行期間，通信管理或適用性Forms Assets使用者介面未開啟。

當您首次運行遷移實用程式時，將使用以下路徑和名稱建立日誌： `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. 此記錄會持續更新通信管理和適用性Forms移轉資訊，例如資產移動。

>[!NOTE]
>
>執行移轉公用程式之前，請確定您已備份crx存放庫。

1. 在瀏覽器工作階段中，以管理員身分登入AEM製作例項。

1. 在瀏覽器中開啟下列URL:

   https://[*主機名*]:[*埠*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   瀏覽器顯示四個選項：

   * AEM Forms 資產移轉
   * 適用性Forms自訂元件移轉
   * 適用性Forms範本移轉
   * AEM 表單雲端組態移轉

1. 執行下列操作以執行遷移：

   * 移轉 **資產**，點選「 AEM Forms Assets Migration 」，然後在下一個畫面中點選 **開始移轉**. 下列項目會移轉：

      * 調適型表單
      * 檔案片段
      * 主題
      * 字母
      * 資料字典

   >[!NOTE]
   >
   >在資產移轉期間，您可能會發現警告訊息，例如「為……找到衝突」。 這些訊息表示無法移轉適用性表單中某些元件的規則。 例如，如果元件的事件同時具有規則和指令碼，如果規則發生在任何指令碼之後，則不會遷移元件的任何規則。 您可以 [開啟規則編輯器以移轉此類規則](#migrate-rules) 最適化表單製作。

   * 若要移轉最適化表單自訂元件，請點選 **適用性Forms自訂元件移轉** 和在「自訂元件移轉」頁面中，點選 **開始移轉**. 下列項目會移轉：

      * 為適用性Forms撰寫的自訂元件
      * 元件覆蓋（如果有）。
   * 若要移轉最適化表單範本，請點選 **適用性Forms範本移轉** 和在「自訂元件移轉」頁面中，點選 **開始移轉**. 下列項目會移轉：

      * 在下建立的最適化表單範本 `/apps` 或 `/conf` 使用AEM範本編輯器。
   * 移轉AEM Forms雲端設定服務，以運用新的內容感知雲端服務範例，包括觸控式啟用的UI(位於 `/conf`)。 移轉AEM Forms雲端設定服務時，雲端服務位於 `/etc` 已移至 `/conf`. 如果您沒有任何依賴舊版路徑的雲端服務自訂項目(`/etc`)，建議您在升級至6.5後立即執行移轉公用程式，並使用雲端設定觸控式UI進行任何後續工作。 如果您有任何現有雲端服務自訂項目，請在升級的設定中繼續使用傳統UI，直到自訂項目更新為與已移轉的路徑一致(`/conf`)，然後執行移轉公用程式。

   移轉 **AEM Forms雲端服務**，請點選「 AEM Forms雲端設定移轉」（雲端設定移轉獨立於AEMFD相容性套件）、點選「 AEM Forms雲端設定移轉」，然後在「設定移轉」頁面上，點選 **開始移轉**:

   * 表單資料模型雲端服務

      * 源路徑： `/etc/cloudservices/fdm`
      * 目標路徑： `/conf/global/settings/cloudconfigs/fdm`
   * Recaptcha

      * 源路徑： `/etc/cloudservices/recaptcha`
      * 目標路徑： `/conf/global/settings/cloudconfigs/recaptcha`
   * Adobe Sign

      * 源路徑： `/etc/cloudservices/echosign`
      * 目標路徑： `/conf/global/settings/cloudconfigs/echosign`
   * Typekit雲端服務

      * 源路徑： `/etc/cloudservices/typekit`
      * 目標路徑： `/conf/global/settings/cloudconfigs/typekit`

   移轉程式進行時，瀏覽器視窗會顯示下列項目：

   * 更新資產時：已成功更新資產。
   * 移轉完成後：已完成資產的移轉。

   執行時，移轉公用程式會執行下列動作：

   * **將標籤新增至資產**:新增「通信管理：移轉資產」/「適用性Forms :移轉的資產」。 移轉的資產，讓使用者能識別移轉的資產。 當您執行移轉公用程式時，系統中的所有現有資產都會標示為已移轉。
   * **產生標籤**:先前系統中顯示的類別和子類別會建立為標籤，然後這些標籤會與AEM中的相關通信管理資產建立關聯。 例如，信函模板的「類別」（「索賠」）和「子類別」（「索賠」）將生成為標籤。










1. 移轉公用程式完成執行後，請繼續執行 [家務處理任務](#housekeepingtasks).

#### 使用規則編輯器移轉規則 {#migrate-rules}

這些元件可在適用性Forms編輯器的規則編輯器中開啟，以便移轉。

* 若要在自訂元件中移轉規則和指令碼（若從6.3升級則非必要），請點選「適用性Forms自訂元件移轉」，在下一個畫面中，點選「開始移轉」。 下列項目會移轉：

   * 使用規則編輯器（6.1 FP1和更新版本）建立的規則和指令碼

   * 在6.1及舊版UI中使用「指令碼」索引標籤建立的指令碼

* 若要移轉範本（若從6.3和6.4升級則不需要），請點選「適用性Forms範本移轉」，然後在下一個畫面中點選「開始移轉」。 下列項目會移轉：

   * 舊範本 — 使用AEM 6.1 Forms或更舊版本，在/apps下建立的最適化表單範本。 這包括範本元件中定義的指令碼。

   * 新範本 — 使用/conf底下的範本編輯器建立的最適化表單範本。 這包括移轉使用規則編輯器建立的規則和指令碼。

### 運行遷移實用程式後的內部管理任務 {#housekeepingtasks}

運行遷移實用程式後，請處理以下內部管理任務：

1. 請確定XFA版本的配置和片段配置是3.3或更新版本。 如果您使用舊版的版面和片段版面，則轉譯信函時可能會發生問題。 若要將舊版XFA更新至最新版本，請完成下列步驟：

   1. [將XFA下載為zip檔案](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) 從Forms使用者介面。
   1. 解壓縮檔案。
   1. 在最新的Designer中開啟XFA檔案並儲存。 XFA的版本會更新為最新版本。
   1. 在Forms使用者介面中上傳XFA。

1. 移轉前先發佈於先前系統的所有資產。 移轉公用程式只會更新製作執行個體上的資產，以及更新發佈執行個體上需要發佈資產的資產。

1. 在AEM Forms 6.4和6.5中，表單使用者群組的某些權限已變更。 如果您希望任何使用者能夠上傳包含指令碼的XDP和適用性Forms，或使用程式碼編輯器，則需將其新增至表單功能使用者群組。 同樣地，範本作者無法再使用規則編輯器中的程式碼編輯器。 為使用者能夠使用程式碼編輯器，請將其新增至af-template-script-writers群組。 有關向組添加用戶的說明，請參閱 [管理使用者和使用者群組](/help/communities/users.md).
