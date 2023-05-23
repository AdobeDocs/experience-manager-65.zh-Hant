---
title: AEM Forms應用
seo-title: AEM Forms app
description: AEM Forms應用讓現場工作人員可以在他們的移動設備上使用自適應表格。
seo-description: AEM Forms app enables your field workers to use adaptive forms on their mobile devices.
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
exl-id: 171754a2-1ba5-42dc-b6d2-3d730807cc31
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 1%

---

# AEM Forms應用簡介 {#aem-forms-app}

## 概觀 {#overview}

AEM Forms應用支援根據您的伺服器在移動設備上同步自適應表單、移動表單和表單。 您可以定義 [FormsOSGi上以工作流為中心](/help/forms/using/aem-forms-workflow.md) 或Forms的JEE工作流。 例如，您運營一家銀行公司，並使用AEM Forms管理客戶應用程式和通信。 您的客戶填寫表格並提交以供驗證。 如果在移動設備上啟用表單，您的客戶可以在AEM Forms應用中填寫表單。 您還可以通過在移動設備上啟用驗證表單來管理驗證工作流。 您的現場工作人員可以將移動設備運送給客戶、驗證詳細資訊並提交表單。 AEM Forms應用與AEM Forms伺服器同步，並讀取為移動設備啟用的表單。 如果應用處於離線狀態，則它將資料儲存在本地。

AEM Forms應用的原始碼可通過軟體分發提供給客戶。 軟體分發中的原始碼包的可用形式為： `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

AEM Forms應用在iOS、安卓和Windows設備上受支援。 你可以安裝AEM Forms的Android應用，Google Play的Android應用，App Store的iOS的Android應用，Windows應用商店的Windows應用。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms
    
    [ ][app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8
    
    [ ][microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt

要在iOS、Android或Windows設備上安裝、自定義和分發應用，請參閱 [自定義、構建和分發AEM Forms應用](#customize-build-distribute)。

## 必備條件 {#prerequisites}

AEM Forms應用需要AEM Forms伺服器。 用戶可以呈現您在AEM Forms伺服器中建立的表單、填寫表單、另存為草稿並提交表單。 應用程式連接到伺服器並從中提取已啟用的表單。 AEM Forms應用與伺服器同步，一旦在應用中載入了表單，用戶就可以離線工作。 如果應用處於離線狀態，則資料將保存在設備上，當應用處於聯機狀態時，資料將與伺服器同步。

### AEM Forms應用，帶伺服器使用AEM Forms工作流 {#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms工作流伺服器，則可以在AEM Forms應用中將表單渲染為任務。 例如，您運行一家銀行公司，客戶填寫應用程式以使用您的服務。 該應用程式是一種自適應表單，它接受客戶提供的資訊，並將其儲存為提交以供審閱。 管理員審閱應用程式並將驗證請求轉發給現場工作人員。 轉發的應用程式會將現場工作人員的應用程式中的驗證表單作為任務啟用。 您的現場工作人員將移動設備運送給客戶並驗證詳細資訊。

### AEM Forms應用，在OSGi上使用以Forms為中心的工作流 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

如果您有AEM Forms伺服器，則可以將自適應表單作為收件箱應AEM用程式和AEM Forms應用程式中的任務進行呈現。 例如，您運行一家銀行公司，客戶填寫應用程式以使用您的服務。 該應用程式與一個自適應表單相關聯，該表單接受來自您客戶的資訊並將其儲存為提交以供審閱。 管理員審閱該任務並將驗證請求批准給現場工作人員。 您的現場工作人員將移動設備運送給客戶並驗證詳細資訊。

### 獨立表單或AEM Forms應用程式，帶有沒有AEM Forms工作流的伺服器 {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms工作流的AEM Forms伺服器是OSGi上的AEM Forms，或獨立的移動表單或自適應表單。 AEM Forms應用與您的AEM Forms實施協作 [OSGi](/help/sites-deploying/configuring-osgi.md)。 Forms，您的應用中提供了AEM Forms應用的啟用和發佈。

表單將下載到您的應用上，並可離線使用。 例如，您正在運行一家銀行公司，而客戶在您的站點上填寫應用程式。 該應用程式是一種自適應表單，可接受客戶提供的資訊並儲存它以供審閱。 管理員審閱表單，並在作者實例中建立AEM驗證表單。 管理員啟用表單與AEM Forms應用同步並發佈它。 如果驗證表單在AEM Forms應用中可用，則您的現場代理可以使用移動設備驗證客戶的詳細資訊。 移動設備與伺服器同步，驗證表單載入到應用中。 您的現場工程師可以訪問客戶、驗證詳細資訊、將資料另存為草稿或提交驗證表。 無論應用程式處於聯機狀態，表單都會與伺服器同步。

要在AEM Forms應用中同步窗體：

1. 在作者實例中，選擇一個表單，然後按一下 **[!UICONTROL 查看屬性]**。

1. 在屬性頁中，按一下 **[!UICONTROL 高級]**。
1. 在「高級」下，啟用選項： **[!UICONTROL 與AEM Forms應用同步]** 點擊 **[!UICONTROL 保存]**。

發佈表單時，應用程式與伺服器同步並提取表單。 要同步多個表單，請在作者實例中，在表單管理器中選擇多個表單，然後點擊 **[!UICONTROL 與AEM Forms應用同步]**。

## 移動設備支援 {#mobile-device-support}

請參閱 [AEM Forms應用（以前稱為Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms應用的關鍵功能 {#key-features-of-aem-forms-app}

### AEM Forms應用與AEM Forms伺服器 {#aem-forms-app-with-aem-forms-servers}

你可以將你的應用與AEM Forms伺服器同步，並可以在你的移動設備上使用表單。

使用AEM Forms工作流伺服器，表單可以與工作台流程和收件箱應用程式中的起始AEM點關聯。 收件AEM箱應用程式可以具有與其關聯的自適應表單。 起始點可以具有與其關聯的自適應表單、HTML5表單或表單集。 起始點可以作為任務提交，也可以將任務另存為草稿。 有關收件箱應用程式與起始點之AEM間差異的詳細資訊，請參閱 [OSGi和AEM FormsJEE工作流中以AEM表單為中心的工作流的操作和功能](capabilities-osgi-jee-workflows.md)。

如果AEM Forms伺服器沒有AEM Forms工作流，則在AEM Forms應用中呈現一個表單，該表單啟用了應用程式中的同步。 Forms可在應用的「Forms」頁籤中找到，可以提交或保存為草稿。 應用程式支援自適應表單和移動表單。

1. **將任務或表單另存為草稿**

   另存為草稿選項保存任務或表單的快照以及關聯表單中填寫的資料和附加的檔案。 這些草稿將保存到移動設備，並與AEM Forms伺服器同步，以供以後檢索。

   請參閱 [將任務或表單另存為草稿](/help/forms/using/save-as-draft.md)。

1. **將表單另存為模板**

   有時，當用戶填寫表單時，對幾個欄位的輸入保持不變。 對於此類實例，您可以填寫每個實例中需要相同值的欄位，並將表單或草稿另存為模板。 現在，每次建立模板實例時，指定的欄位都已填充在模板中指定的值。 它有助於您節省填表所需的時間和精力。

   請參閱 [將表單另存為模板](/help/forms/using/save-forms-and-start-points-as-templates.md)。

### 處理任務和表單 {#working-with-tasks-and-forms}

你可以將你的應用與AEM Forms工作流伺服器同步，並可以在你的移動設備上處理任務和表單。

移動設備上的任務包含自適應表單、HTML5表單或表單集，還可包含附件和 [摘要URL](/help/forms/using/getting-task-variables-summary-url.md)。 預設情況下，分配給您的任務將放在 **[!UICONTROL 任務]** 的子菜單。 處理任務時，可以更改任務並在AEM Forms伺服器上保存任務的草稿副本。

移動設備上的表格可以是自適應格式或移動格式。 Forms在表單應用中啟用同步功能，可在Forms資料夾中找到。 您可以同步在AEM Forms伺服器中啟用的表單，而無需AEM Forms工作流(OSGi上的AEM Forms)。

請參閱：

* [開啟任務](/help/forms/using/open-task.md)
* [使用表單](/help/forms/using/working-with-form.md)

### 離線工作 {#working-offline}

您可以在離線模式下在移動設備上工作。 即使沒有網路連接，您也可以登錄到應用程式，並且可以處理上次聯機時與設備同步的所有表單。 有關如何同步表單的詳細資訊，請參閱 [正在同步應用](/help/forms/using/sync-app.md)。 如果選擇同步與表單關聯的附件，您也可以在離線模式下開啟附件。 您可以編輯表單、添加註釋，以及在離線模式下提交或保存表單。 下次聯機時，表單將與AEM Forms伺服器同步。

有關詳細資訊，請參閱 [在離線模式下工作](/help/forms/using/work-offline-mode.md)。

### 添加註釋 {#adding-annotations}

您可以將以下附件添加到移動設備上的表單

* **注釋** — 可以使用「注釋」功能在窗體中添加手繪文字或文本注釋。 有關詳細資訊，請參閱 [添加附註](/help/forms/using/add-attachments.md#adding-a-note)。

* **圖片**-AEM Forms應用包含使用照相機功能或移動設備庫的功能。 使用照片附件，可以添加具有關聯表單的照片。 有關詳細資訊，請參閱 [添加照片](/help/forms/using/add-attachments.md#adding-a-photograph)。

### 自動保存 {#autosave}

當用戶在AEM Forms應用中輸入資料時，自動保存功能會定期保存資料。 AEM Forms應用中的自動保存功能可幫助您避免因電池電量不足等情況而關閉應用時的資料丟失。

請參閱 [在AEM Forms應用中使用自動保存](/help/forms/using/autosave-data-app.md)。

## 收件箱AEM和AEM Forms應用功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流的兩種主要方式都在使用 [收件箱AEM](/help/forms/using/manage-applications-inbox.md) 和AEM Forms應用。 但是，Inbox和AEMAEM Forms應用的功能不同。 收AEM件箱僅與 [以Forms為中心的工作流](/help/forms/using/aem-forms-workflow.md) 同時，AEM Forms應用可以與以Forms為中心的工作流程和流程管理配合使用。 有關收件箱和AEM Forms應用功AEM能之間差異的詳細資訊，請參見 [OSGi和AEM FormsJEE工作流中以AEM表單為中心的工作流的操作和功能](capabilities-osgi-jee-workflows.md)。

## 支援的表單 {#supported-forms}

AEM Forms應用中支援的表單類型：

### 調適性表單 {#adaptive-form}

AEM Forms應用支援動態適應用戶輸入的自適應表單。 還支援延遲載入的自適應表單。

### 移動表單 {#mobile-form}

您可以在AEM Forms為移動設備建立表單。 在根據顯示設備適應的移動設備中，將移動表單呈現為HTML表單。

### 表單集 {#formset}

使用表單集，可以將與服務或流程相關的多個表單分組以自動執行業務流程並呈現給最終用戶。 在這種情況下，用戶可以將整個集合一併填充，而不需要歸檔、提交和跟蹤各個表單或進程。

>[!NOTE]
>
>需要AEM Forms工作流(JEE上的AEM Forms)。

## AEM Forms應用的工作原理 {#how-aem-forms-app-works}

AEM Formsapp為現場工作人員提供移動解決方案，讓他們處理分配給他們的表單。 應用程式從伺服器快取完整資料，並通過本地保存所有工作提供高效的用戶體驗。 通過及時同步更新將來自磁碟的資料發送到伺服器。

AEM Forms應用是一個基於PhoneGap 5.0的應用程式，其中Backbone模型被有效地用於通過視圖呈現儲存在模型中的資料。 所有本機操作都通過PhoneGap插件執行。

## 自定義、構建和分發AEM Forms應用 {#customize-build-distribute}

>[!NOTE]
>
>僅當您使用AEM Forms應用原始碼來構建應用時才適用。

AEM Forms應用可輕鬆定制以滿足特定組織的需求。 應用程式的原始碼與AEM Forms一起提供。 您可以更改原始碼並構建自己的移動工作人員解決方案。 您也可以使用自己的企業密鑰對應用進行簽名。

### 自訂 {#customize}

您可以為以下對象自定義應用：

**品牌**:更改應用表徵圖、應用名稱、啟動影像和AEM Forms應用中的頁面。 您還可以更改文本，以便為特定區域本地化應用程式。 有關AEM Forms應用品牌的詳細資訊，請參閱 [品牌定制](/help/forms/using/branding-customization.md)。

**主題**:更改AEM Forms應用用戶介面中的顏色、字型和間距等樣式。 有關詳細資訊，請參見 [主題自定義](/help/forms/using/theme-customization.md)。

**手勢**:在AEM Forms應用用戶介面中更改手勢，如向右輕掃和向左輕掃。 有關詳細資訊，請參見 [手勢自定義](/help/forms/using/gesture-customization.md)。

有關設定AEM Forms應用程式項目以進行自定義的詳細資訊，請參閱：

* [為AEM Forms應用設定環境](/help/forms/using/setup-environment-mobile-workspace.md)
* [設定Visual Studio項目並生成Windows應用](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [設定Xcode項目並生成iOS應用](/help/forms/using/setup-xcode-project-build-installer.md)
* [設定Eclipse項目並構建Android應用](/help/forms/using/setup-eclipse-project-build-installer.md)

### 構建和分發 {#build-and-distribute}

可以從以下位置提取AEM Forms應用的原始碼： `adobe-lc-mobileworkspace-src.zip` 作為AEM Forms軟體分發應用程式源包的一部分提供。

要獲取AEM Forms應用程式源，請執行以下步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

**為iOS**:

有關如何建立iOS應用(.ipa)的詳細資訊，請參閱 [設定Xcode項目並生成iOS應用](/help/forms/using/setup-xcode-project-build-installer.md)。

有關如何使用您的設定配置檔案對AEM Forms應用進行簽名的詳細資訊，請參閱 [iOS代碼簽名設定、處理和故障排除](https://developer.apple.com/support/code-signing/)。

**對於Android**:

有關如何建立Android應用(.apk)的詳細資訊，請參閱 [設定Eclipse項目並構建Android應用](/help/forms/using/setup-eclipse-project-build-installer.md)。

有關如何簽署AEM Forms應用的詳細資訊，請參閱 [簽名應用程式](https://developer.android.com/tools/publishing/app-signing.html)。

**對於Windows**:

有關如何建立Windows應用(.appx)的詳細資訊，請參閱 [設定Visual Studio項目並生成Windows應用](/help/forms/using/setup-visual-studio-project-build-installer.md)。

有關如何通過MDM分發應用程式的詳細資訊，請參見 [分發AEM Forms應用](/help/forms/using/distribute-mobile-workspace-app.md)。 通過MDM發佈的應用程式僅適用於iOS和Android。

## Recommendations將Mobile Workspace升級到AEM Forms應用 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果要升級到最新版的AEM Forms應用，請確保閱讀以下內容：

* **如果您從Android上的播放商店安裝了早期版本的應用**
你可以直接從播放商店升級應用。

* **如果應用的早期版本是使用原始碼構建和安裝的(適用於iOS和Android)**:

   安裝新應用之前，請將所有資料與AEM Forms伺服器同步。 同步資料後，卸載該應用的早期版本，然後安裝新應用。
