---
title: 移轉 AEM Forms 資產和文件
seo-title: Migrate AEM Forms assets and documents
description: 遷移實用程式允許您將AEM Forms資產和文檔從AEM6.3Forms或早期版本遷AEM移到6.4Forms。
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

遷移實用程式將 [自適應Forms資產](../../forms/using/introduction-forms-authoring.md)。 [雲配置](/help/sites-developing/extending-cloud-config.md), [通信管理資產](/help/forms/using/cm-overview.md) 從早期版本中使用的格式到6.AEM5Forms中使用的格式。 運行遷移實用程式時，將遷移以下內容：

* 自適應表單的自定義元件
* 適應性表單和通信管理模板
* 雲配置
* 信件管理和適應性表格資產

>[!NOTE]
>
>如果升級不到位，對於Tergement Management資產，您可以在每次導入資產時運行遷移。 對於通信管理遷移，您需要安裝Forms相容性包。

## 移民方法 {#approach-to-migration}

你可以 [升級](../../forms/using/upgrade.md) 從AEM Forms6.4、6.3或6.2的最新版本到AEM Forms6.5，或執行全新安裝。 根據您是升級了以前的安裝還是執行了新安裝，您需要執行以下操作之一：

**在就地升級時**

如果執行就地升級，則升級實例已具有資產和文檔。 但是，在使用資產和文檔之前，您需要安裝 [AEMFD相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括Tergement Management相容性包）

然後，您需要更新資產和文檔 [運行遷移實用程式](#runningmigrationutility)。

**在安裝不到位時**

如果安裝過程（新鮮），則在您可以使用資產和文檔之前，您需要安裝 [AEMFD相容性包](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) （包括「通信管理相容性」包）。

然後，您需要在新設定中導入資產包（zip或cmp），然後通過 [運行遷移實用程式](#runningmigrationutility)。 Adobe建議僅在運行遷移實用程式後才在新設定上建立新資產。

原因 [向後相容性相關](/help/sites-deploying/backward-compatibility.md) 更改，crx-repository中幾個資料夾的位置將更改。 手動將先前設定中的依賴項（自定義庫和資產）導出並導入到新環境。

## 在繼續遷移之前閱讀 {#prerequisites}

對於Tergement Management資產：

* 對於從上一個平台導入的資產，將添加一個屬性： **fd：版本=1.0**。
* 自AEMForms6.1以來，沒有現成的注釋。 以前添加的注釋在資產中可用，但在介面上不會自動顯示。 您需要在AEM Forms用戶介面中自定義extendedProperties屬性，以使注釋可見。
* 在LiveCycleES4等早期版本中，文本是使用FlexRichTextEditor編輯的，但自AEM6.1Forms以來，HTML編輯器就被使用。 由於此渲染和字型外觀，字型大小和字型邊距可能與「作者」用戶介面中的早期版本不同。 但是，在呈現字母時，字母看起來是相同的。
* 文本模組中的清單得到改進，現在呈現方式也有所不同。 可能有視覺差異。 我們建議您渲染並查看文本模組中使用清單的字母。
* 由於映像內容模組已轉換為DAM資產，並且佈局和片段在遷移期間添加到表單中，因此這些模組的「更新者」屬性將更改為admin。
* 資產的版本歷史記錄不會遷移，在遷移後不可用。 維護遷移後的後續版本歷史記錄。
* 自Forms6.1以來，「準備發佈」AEM狀態已棄用，因此「準備發佈」狀態中的所有資產都更改為「已修改」狀態。
* 由於用戶介面在AEM Forms6.3中更新，因此執行自定義的步驟也不同。 如果要從6.3之前的版本遷移，則需要重做自定義。
* 佈局片段從/content/apps/cm/layouts/fragmentlayouts/1001移動到/content/apps/cm/modules/fragmentlayouts。 資產中的資料字典引用顯示資料字典的路徑，而不是其名稱。
* 需要調整文本模組中用於對齊的任何制表符空格。 有關詳細資訊，請參見 [對應管理 — 使用制表符間距排列文本](https://helpx.adobe.com/aem-forms/kb/cm-tab-spacing-limitations.html)。
* 資產合成器配置對通信管理配置的更改。
* 資產將移到具有「現有文本」和「現有清單」等名稱的資料夾下。

## 使用遷移實用程式 {#using-the-migration-utility}

### 運行遷移實用程式 {#runningmigrationutility}

在對資產進行任何更改或建立資產之前，請運行遷移實用程式。 建議您在進行任何更改或建立資產後不要運行該實用程式。 確保在遷移進程運行期間未開啟「通信管理」或「自適應Forms資產」用戶介面。

首次運行遷移實用程式時，將使用以下路徑和名稱建立日誌： `\[aem-installation-directory]\cq-quickstart\logs\aem-forms-migration.log`。 此日誌不斷使用Tergement Management和Adaptive Forms遷移資訊（如移動資產）進行更新。

>[!NOTE]
>
>在運行遷移實用程式之前，請確保已備份了crx儲存庫。

1. 在瀏覽器會話中，以管理員身AEM份登錄到作者實例。

1. 在瀏覽器中開啟以下URL:

   https://[*主機名*]:[*埠*]/[*上下文路徑*]/libs/fd/foundation/gui/content/migration.html

   瀏覽器顯示四個選項：

   * AEM Forms 資產移轉
   * 自適應Forms自定義元件遷移
   * 自適應Forms模板遷移
   * AEM 表單雲端組態移轉

1. 執行以下操作以執行遷移：

   * 遷移 **資產**，按一下「AEM Forms資產遷移」，然後在下一螢幕中按一下 **開始遷移**。 遷移以下內容：

      * 調適型表單
      * 文檔片段
      * 主題
      * 字母
      * 資料字典

   >[!NOTE]
   >
   >在資產遷移期間，您可能會發現警告消息，如「為……找到衝突」。 這些消息表示無法遷移自適應表單中某些元件的規則。 例如，如果元件有一個同時具有規則和指令碼的事件，則如果規則在任何指令碼之後發生，則不會遷移該元件的任何規則。 你可以 [通過開啟規則編輯器來遷移此類規則](#migrate-rules) 在自適應窗體創作中。

   * 要遷移自適應表單自定義元件，請點擊 **自適應Forms自定義元件遷移** 在「自定義元件遷移」頁中，按一下 **開始遷移**。 遷移以下內容：

      * 為Adaptive Forms編寫的自定義元件
      * 元件重疊（如果有）。
   * 要遷移自適應表單模板，請點擊 **自適應Forms模板遷移** 在「自定義元件遷移」頁中，按一下 **開始遷移**。 遷移以下內容：

      * 在下建立的自適應表單模板 `/apps` 或 `/conf` 使用模AEM板編輯器。
   * 遷移AEM Forms雲配置服務以利用新的上下文感知雲服務模式，該模式包括啟用觸摸的UI(在 `/conf`)。 遷移AEM Forms雲配置服務時， `/etc` 已移至 `/conf`。 如果您沒有任何依賴於舊路徑的雲服務定制(`/etc`)，建議在升級到6.5後立即運行遷移實用程式，並使用雲配置Touch UI進行任何進一步的工作。 如果您有任何現有的雲服務自定義項，請在升級的安裝程式上繼續使用經典UI，直到更新自定義項以與遷移的路徑(`/conf`)，然後運行遷移實用程式。

   遷移 **AEM Forms雲服務**&#x200B;點擊「AEM Forms雲配置遷移」（雲配置遷移獨立於AEMFD相容性包），點擊「AEM Forms雲配置遷移」，然後在「配置遷移」頁上，點擊 **開始遷移**:

   * 表單資料模型雲服務

      * 源路徑： `/etc/cloudservices/fdm`
      * 目標路徑： `/conf/global/settings/cloudconfigs/fdm`
   * 重新捕獲

      * 源路徑： `/etc/cloudservices/recaptcha`
      * 目標路徑： `/conf/global/settings/cloudconfigs/recaptcha`
   * Adobe Sign

      * 源路徑： `/etc/cloudservices/echosign`
      * 目標路徑： `/conf/global/settings/cloudconfigs/echosign`
   * Typekit雲服務

      * 源路徑： `/etc/cloudservices/typekit`
      * 目標路徑： `/conf/global/settings/cloudconfigs/typekit`

   在遷移過程進行時，瀏覽器窗口將顯示以下內容：

   * 更新資產時：資產已成功更新。
   * 遷移完成後：已完成資產遷移。

   執行時，遷移實用程式將執行以下操作：

   * **將標籤添加到資產**:添加標籤「Tergement Management :遷移資產」/「自適應Forms:遷移資產」。 對遷移的資產進行識別，使用戶能夠識別遷移的資產。 運行遷移實用程式時，系統中的所有現有資產都標籤為已遷移。
   * **生成標籤**:先前系統中存在的類別和子類別將建立為標籤，然後這些標籤與中的相關Tergement Management資產相關聯AEM。 例如，字母模板的類別（索賠）和子類別（索賠）將生成為標籤。










1. 遷移實用程式運行完畢後，繼續執行 [家政任務](#housekeepingtasks)。

#### 使用規則編輯器遷移規則 {#migrate-rules}

通過在自適應Forms編輯器的規則編輯器中開啟這些元件，可以遷移這些元件。

* 要遷移自定義元件中的規則和指令碼（從6.3升級時不需要），請點擊自適應Forms自定義元件遷移，然後在下一螢幕中點擊開始遷移。 遷移以下內容：

   * 使用規則編輯器（6.1 FP1及更高版本）建立的規則和指令碼

   * 使用6.1及更低版本UI中的「指令碼」頁籤建立的指令碼

* 要遷移模板（從6.3和6.4升級時不需要），請點擊「自適應Forms模板遷移」，然後在下一螢幕中點擊「開始遷移」。 遷移以下內容：

   * 舊模板 — 在/apps下使用6.1Forms或更早版本AEM建立的自適應表單模板。 這包括在模板元件中定義的指令碼。

   * 新模板 — 使用/conf下的模板編輯器建立的自適應表單模板。 這包括遷移使用規則編輯器建立的規則和指令碼。

### 運行遷移實用程式後的管理任務 {#housekeepingtasks}

運行遷移實用程式後，請處理以下內部處理任務：

1. 確保XFA版本的佈局和片段佈局為3.3或更高版本。 如果使用舊版本的佈局和片段佈局，則在呈現字母時可能會出現問題。 要將舊XFA的版本更新為最新版本，請完成以下步驟：

   1. [將XFA下載為zip檔案](../../forms/using/import-export-forms-templates.md#p-import-and-export-assets-in-correspondence-management-p) 從Forms用戶介面。
   1. 解壓檔案。
   1. 在最新的設計器中開啟XFA檔案並保存它。 XFA的版本將更新為最新版本。
   1. 在Forms用戶介面中上載XFA。

1. 發佈遷移前在上一個系統中發佈的所有資產。 遷移實用程式只更新作者實例上的資產，並更新發佈實例上需要發佈資產的資產。

1. 在AEM Forms6.4和6.5中，表單用戶組的某些權利被更改。 如果希望任何用戶能夠上載包含指令碼或使用代碼編輯器的XDP和AdaptiveForms，則需要將它們添加到表單超級用戶組。 同樣，模板作者無法再使用規則編輯器中的代碼編輯器。 為使用戶能夠使用代碼編輯器，請將它們添加到af-template-script-writers組。 有關向組添加用戶的說明，請參見 [管理用戶和用戶組](/help/communities/users.md)。
