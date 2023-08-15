---
title: 移轉 AEM Forms 資產和文件
seo-title: Migrate AEM Forms assets and documents
description: 移轉公用程式可讓您將AEM Forms資產和檔案從AEM 6.3 Forms或舊版移轉至AEM 6.4 Forms。
seo-description: The Migration utility lets you Migrate AEM Forms assets and documents from AEM 6.3 Forms or prior versions to AEM 6.4 Forms.
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
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1742'
ht-degree: 1%

---

# 移轉 AEM Forms 資產和文件{#migrate-aem-forms-assets-and-documents}

移轉公用程式會將 [最適化Forms資產](../../forms/using/introduction-forms-authoring.md)， [雲端設定](/help/sites-developing/extending-cloud-config.md)、和 [通訊管理資產](/help/forms/using/cm-overview.md) 從舊版所使用的格式改成AEM 6.5 Forms中使用的格式。 當您執行移轉公用程式時，將會移轉下列專案：

* 調適型表單的自訂元件
* 最適化表單與通訊管理範本
* 雲端設定
* 通訊管理和調適型表單資產

>[!NOTE]
>
>如果升級不當而使用「通訊管理」資產，則可在每次匯入資產時執行移轉。 若要進行Correspondence Management移轉，您必須安裝Forms相容性套件。

## 移轉方法 {#approach-to-migration}

您可以 [升級](../../forms/using/upgrade.md) 更新至AEM Forms 6.4、6.3或6.2中的AEM Forms 6.5最新版本，或執行全新安裝。 根據您是升級先前的安裝還是執行全新安裝，您需要執行下列其中一項操作：

**就地升級時**

如果您執行就地升級，則升級的執行個體已有資產和檔案。 不過，您必須先安裝，才能使用資產和檔案 [AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包含Correspondence Management相容性套件）

然後，您需要透過以下方式更新資產和檔案 [執行移轉公用程式](#runningmigrationutility).

**安裝不當時**

如果是非適當（全新）安裝，您必須先安裝，才能使用資產和檔案 [AEMFD相容性套件](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包含通訊管理相容性套件）。

之後，您需要在新設定上匯入資產套件（zip或cmp），然後透過以下方式更新資產和檔案 [執行移轉公用程式](#runningmigrationutility). Adobe建議您必須先執行移轉公用程式，才能在新設定上建立新資產。

到期日 [與回溯相容性相關](/help/sites-deploying/backward-compatibility.md) 變更，crx-repository中一些資料夾的位置也會變更。 從先前的設定手動匯出並匯入相依性（自訂程式庫和資產）到全新的環境。

## 開始移轉前請先閱讀 {#prerequisites}

對於通訊管理資產：

* 對於從上一個平台匯入的資產，屬性會新增： **fd：version=1.0**.
* 自AEM 6.1 Forms起，無法立即使用註解。 先前新增的註解可在資產中使用，但不會自動顯示在介面中。 您必須在AEM Forms使用者介面中自訂extendedProperties屬性，才能看到註解。
* 在某些舊版(例如LiveCycle ES4)中，文字是使用Flex RichTextEditor進行編輯，但由於AEM 6.1 Forms，因此會使用HTML編輯器。 由於這種呈現方式以及字型的外觀，字型大小和字型邊界可能與作者使用者介面中先前的版本不同。 但是，字母在轉譯時看起來是相同的。
* 文字模組中的清單已改善，現在呈現方式也不同。 可能有視覺差異。 我們建議您轉譯並檢視您在文字模組中使用清單的字母。
* 由於影像內容模組已轉換為DAM資產，並在移轉期間將版面和片段新增到表單，這些模組的「更新者」屬性將變更為「管理員」。
* 資產的版本記錄未移轉，且在移轉後無法使用。 將會維護移轉後的後續版本記錄。
* 自AEM 6.1 Forms起，準備發佈狀態即已過時，因此所有處於準備發佈狀態的資產都會變更為已修改狀態。
* 由於使用者介面在AEM Forms 6.3中更新，執行自訂的步驟也不同。 如果您要從6.3之前的版本移轉，則需要重做自訂。
* 佈局片段從/content/apps/cm/layouts/fragmentlayouts/1001移至/content/apps/cm/modules/fragmentlayouts。 資產中的資料字典參考會顯示資料字典的路徑而非其名稱。
* 在文字模組中用於對齊的任何定位字元空格都需要重新調整。 如需詳細資訊，請參閱 [通訊管理 — 使用索引標籤間距來排列文字](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html).
* 「通訊管理」設定的資產撰寫器設定變更。
* 資產會移至名為「現有文字」和「現有清單」等名稱的資料夾下。

## 使用移轉公用程式 {#using-the-migration-utility}

### 執行移轉公用程式 {#runningmigrationutility}

在變更資產或建立資產之前，請先執行移轉公用程式。 建議您在變更或建立資產後不要執行公用程式。 請確定在移轉程式執行期間，通訊管理或最適化Forms資產使用者介面未開啟。

當您第一次執行Migration Utility時，會建立具有下列路徑和名稱的記錄檔： `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`. 此記錄會持續更新通訊管理和最適化Forms移轉資訊，例如資產移動。

>[!NOTE]
>
>在執行移轉公用程式之前，請確定您已備份crx存放庫。

1. 在瀏覽器工作階段中，以管理員身分登入AEM作者執行個體。

1. 在瀏覽器中開啟下列URL：

   https://[*主機名稱*]：[*連線埠*]/[*context_path*]/libs/fd/foundation/gui/content/migration.html

   瀏覽器會顯示四個選項：

   * AEM Forms 資產移轉
   * 最適化Forms自訂元件移轉
   * 最適化Forms範本移轉
   * AEM 表單雲端組態移轉

1. 請執行以下動作以執行移轉：

   * 若要移轉 **資產**，點選「 AEM Forms資產移轉」，然後在下一個畫面中，點選「 」 **開始移轉**. 下列專案已移轉：

      * 調適型表單
      * 檔案片段
      * 主題
      * 字母
      * 資料字典

   >[!NOTE]
   >
   >在資產移轉期間，您可能會發現警告訊息，例如「發現衝突……」。 這類訊息表示無法移轉適用性表單中部分元件的規則。 例如，如果元件有一個同時具有規則和指令碼的事件，如果規則發生在任何指令碼之後，則不會移轉元件的任何規則。 您可以 [透過開啟規則編輯器來移轉這類規則](#migrate-rules) 在最適化表單製作中。

   * 若要移轉最適化表單自訂元件，請點選 **最適化Forms自訂元件移轉** 在「自訂元件移轉」頁面中，點選 **開始移轉**. 下列專案已移轉：

      * 為最適化Forms撰寫的自訂元件
      * 元件覆蓋（如果有的話）。

   * 若要移轉最適化表單範本，請點選 **最適化Forms範本移轉** 在「自訂元件移轉」頁面中，點選 **開始移轉**. 下列專案已移轉：

      * 最適化表單範本建立於 `/apps` 或 `/conf` 使用AEM範本編輯器。

   * 移轉AEM Forms雲端設定服務，以運用新的內容感知雲端服務範例，包括已啟用觸控的UI (位於 `/conf`)。 當您移轉AEM Forms雲端設定服務時，雲端服務位於 `/etc` 已移至 `/conf`. 如果您沒有任何相依於舊版路徑的雲端服務自訂(`/etc`)，建議您在升級至6.5後立即執行移轉公用程式，並使用雲端設定觸控式UI進行進一步的作業。 如果您有任何現有的雲端服務自訂專案，請在升級設定時繼續使用傳統UI，直到自訂專案更新以符合移轉的路徑(`/conf`)，然後執行移轉公用程式。

   若要移轉 **AEM Forms雲端服務**，包括下列，點選「 AEM Forms雲端設定移轉」 （雲端設定移轉獨立於AEMFD相容性套件），點選「 AEM Forms雲端設定移轉」 ，然後點選「 Configuration移轉」頁面上的 **開始移轉**：

   * 表單資料模型雲端服務

      * 來源路徑： `/etc/cloudservices/fdm`
      * 目標路徑： `/conf/global/settings/cloudconfigs/fdm`

   * Recaptcha

      * 來源路徑： `/etc/cloudservices/recaptcha`
      * 目標路徑： `/conf/global/settings/cloudconfigs/recaptcha`

   * Adobe Sign

      * 來源路徑： `/etc/cloudservices/echosign`
      * 目標路徑： `/conf/global/settings/cloudconfigs/echosign`

   * Typekit雲端服務

      * 來源路徑： `/etc/cloudservices/typekit`
      * 目標路徑： `/conf/global/settings/cloudconfigs/typekit`

   當移轉程式進行時，瀏覽器視窗會顯示下列內容：

   * 資產更新時：資產已成功更新。
   * 移轉一旦完成：資產完成移轉。

   執行時，移轉公用程式會執行下列動作：

   * **將標籤新增至資產**：新增「Correspondence Management ：Migrated Assets」/「Adaptive Forms ：Migrated Assets」標籤。 至已移轉的資產，讓使用者能識別已移轉的資產。 當您執行「移轉」公用程式時，系統中所有現有的資產都會標示為「已移轉」。
   * **產生標籤**：先前系統中存在的類別和子類別會建立為標籤，然後這些標籤會與AEM中的相關通訊管理資產相關聯。 例如，信函範本的類別（索賠）和子類別（索賠）會產生為標籤。

1. 移轉公用程式執行完畢後，請繼續前往 [內部管理任務](#housekeepingtasks).

#### 使用規則編輯器移轉規則 {#migrate-rules}

若要移轉這些元件，請在Adaptive Forms編輯器的規則編輯器中將其開啟。

* 若要移轉自訂元件中的規則和指令碼（如果從6.3升級，則不需要移轉），請點選「最適化Forms自訂元件移轉」，然後在下一個畫面中點選「開始移轉」。 下列專案已移轉：

   * 使用規則編輯器（6.1 FP1和更新版本）建立的規則和指令碼

   * 使用6.1和更舊版本UI中的指令碼索引標籤建立的指令碼

* 若要移轉範本（如果從6.3和6.4升級，則不需要），請點選「最適化Forms範本移轉」，然後在下一個畫面中，點選「開始移轉」。 下列專案已移轉：

   * 舊範本 — 在/apps下使用AEM 6.1 Forms或更舊版本建立的最適化表單範本。 這包括範本元件中定義的指令碼。

   * 新範本 — 使用/conf下的範本編輯器建立的最適化表單範本。 這包括移轉使用規則編輯器建立的規則和指令碼。

### 執行移轉公用程式後的內部管理工作 {#housekeepingtasks}

執行移轉公用程式後，請處理下列內部管理工作：

1. 請確定版面和片段版面的XFA版本為3.3或更新版本。 如果您使用較舊版本的版面和片段版面，則呈現信函時可能會出現問題。 若要將舊版XFA更新至最新版本，請完成以下步驟：

   1. [將XFA下載為zip檔](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) 從Forms使用者介面。
   1. 擷取檔案。
   1. 在最新的設計工具中開啟XFA檔案並儲存。 XFA的版本會更新至最新版本。
   1. 在Forms使用者介面中上傳XFA。

1. 發佈移轉前已在先前系統中發佈的所有資產。 移轉公用程式只會更新作者例項上的資產，而更新發佈資產所需發佈例項上的資產。

1. 在AEM Forms 6.4和6.5中，使用者群組的某些表單許可權已變更。 如果您希望您的任何使用者能夠上傳XDP和包含指令碼的最適化Forms，或使用程式碼編輯器，您需要將它們新增到表單超級使用者群組。 同樣地，範本作者無法在規則編輯器中再使用程式碼編輯器。 若要讓使用者能夠使用程式碼編輯器，請將他們新增至af-template-script-writers群組。 如需將使用者新增至群組的說明，請參閱 [管理使用者和使用者群組](/help/communities/users.md).
