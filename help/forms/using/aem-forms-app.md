---
title: AEM Forms應用程式
seo-title: AEM Forms應用程式
description: AEM Forms應用程式可讓現場工作人員在行動裝置上使用調適性表單。
seo-description: AEM Forms應用程式可讓現場工作人員在行動裝置上使用調適性表單。
uuid: fac976c8-b713-4492-b153-f567e7a11ceb
contentOwner: sashanka
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: e18aa345-034c-473b-b4c2-01678bb10616
translation-type: tm+mt
source-git-commit: 94472fad34fe97740e4711d2cb35beb884db52ce

---


# Introduction to AEM Forms app {#aem-forms-app}

## 概覽 {#overview}

AEM Forms應用程式可讓您根據伺服器，在行動裝置上同步最適化表單、行動表單和表單。 您可以定義以OSGi或JEE的 [Forms工作流程為中心的](/help/forms/using/aem-forms-workflow.md)[工作流程](/help/forms/using/finance-reference-site-walkthrough.md#approving-the-application)。 例如，您經營一家銀行，並使用AEM Forms來管理客戶應用程式和通訊。 您的客戶填寫表格並送出以進行驗證。 如果您在行動裝置上啟用表單，您的客戶可以在AEM Forms應用程式中填寫表單。 您也可以在行動裝置上啟用驗證表單，以管理驗證工作流程。 您的現場工作人員可以攜帶行動裝置給客戶、驗證詳細資訊並提交表單。 AEM Forms應用程式會與AEM Forms伺服器同步，並擷取針對行動裝置啟用的表單。 如果應用程式已離線，它會將資料儲存在本機。

AEM Forms應用程式的原始碼可透過套件共用方式提供給客戶。 包共用中的原始碼包可用於： `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

iOS、Android和Windows裝置支援AEM Forms應用程式。 您可以從Google Play、App Store的iOS和Windows市集的Windows，安裝適用於Android的AEM Forms應用程式。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

若要在iOS、Android或Windows裝置上安裝、自訂和散發應用程式，請參閱「自訂、建 [立和散發AEM Forms應用程式」](#customize-build-distribute)。

## 必備條件 {#prerequisites}

AEM Forms應用程式需要AEM Forms伺服器。 使用者可以在AEM Formsserver中演算您建立的表單、填寫表單、另存為草稿，然後送出。 應用程式會連線至伺服器，並從中擷取已啟用的表格。 AEM Forms應用程式會與伺服器同步，當表單載入應用程式時，使用者就可以離線工作。 如果應用程式已離線，資料會儲存在裝置上，當應用程式連線時，資料會與伺服器同步。

### AEM Forms應用程式與使用AEM Forms workflow的伺服器 {#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms Workflow伺服器，則可以在AEM Forms應用程式中將表單轉譯為工作。 例如，您經營一家銀行，客戶會填寫應用程式來使用您的服務。 此應用程式是可接受客戶資訊的調適性表單，並將其儲存為提交供審核。 管理員會檢閱應用程式，並將驗證要求轉送給現場工作者。 轉發的應用程式會在現場工作人員的應用程式中啟用驗證表單作為任務。 您的現場工作人員將行動裝置帶給客戶，並驗證詳細資訊。

### AEM Forms應用程式與伺服器搭配使用OSGi上以表單為中心的工作流程 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

如果您有AEM Forms伺服器，則可將最適化表單轉譯為AEM Inbox應用程式，以及AEM Forms應用程式中的工作。 例如，您經營一家銀行，客戶會填寫應用程式來使用您的服務。 此應用程式與可接受客戶資訊的最適化表單相關聯，並將其儲存為提交以供審核。 管理員會審查任務，並批准向現場工作者發出的驗證請求。 您的現場工作人員將行動裝置帶給客戶，並驗證詳細資訊。

### 獨立表單或AEM Forms應用程式與伺服器搭配使用，不含AEM Forms Workflow {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms workflow的AEM Forms伺服器是OSGi上的AEM Forms，或是獨立行動表單或最適化表單。 AEM Forms應用程式可與您在 [OSGi上的AEM Forms實作搭](/help/sites-deploying/configuring-osgi.md)配使用。 您為AEM Forms應用程式啟用和發佈的表單，都可在您的應用程式中使用。

表單會下載到您的應用程式中，並可離線使用。 例如，您經營的是一家銀行，而客戶填寫了您網站上的應用程式。 應用程式是可接受客戶資訊並儲存以供審核的調適性表單。 管理員會檢閱表單，並在AEM作者例項中建立驗證表單。 管理員可啟用表單與AEM Forms應用程式的同步，並發佈它。 如果驗證表單可在AEM Forms應用程式中使用，您的現場代理可以使用行動裝置來驗證客戶的詳細資訊。 行動裝置與伺服器同步，驗證表單會載入應用程式中。 您的現場工程師可以造訪客戶、驗證詳細資訊、將資料儲存為草稿，或提交驗證表單。 每當應用程式連線時，表單就會與伺服器同步。

若要在AEM Forms應用程式中同步您的表格：

1. 在作者實例中，選擇一個表單，然後按一下「查 **[!UICONTROL 看屬性」]**。

1. 在屬性頁面中，按一下「進 **[!UICONTROL 階」]**。
1. 在「進階」下方，啟用選項：與 **[!UICONTROL AEM Forms應用程式同步]** ，然後點選「 **[!UICONTROL 儲存」]**。

發佈表單時，應用程式會與伺服器同步並擷取表單。 若要同步多個表單，請在作者例項中，在表單管理員中選取多個表單，然後點選「與AEM Forms應 **[!UICONTROL 用程式同步」]**。

## 行動裝置支援 {#mobile-device-support}

請參 [閱AEM Forms應用程式（先前稱為Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms應用程式的主要功能 {#key-features-of-aem-forms-app}

### AEM Forms應用程式與AEM Forms伺服器 {#aem-forms-app-with-aem-forms-servers}

您可以將應用程式與AEM Forms伺服器同步，並可在行動裝置上使用表格。

有了AEM Forms Workflow伺服器，表單就可以與工作台程式和AEM Inbox應用程式中的起點建立關聯。 AEM Inbox應用程式可以有與其關聯的最適化表單。 起點可以具有與其關聯的最適化表單、HTML5表單或表單集。 起始點可以作為任務提交，或者任務可以另存為草稿。 如需AEM Inbox應用程式與起點之間差異的詳細資訊，請參閱「OSGi和AEM Forms JEE工作流程上以表單為中心的 [AEM工作流程的動作與功能」](/help/forms/using/capabilities-osgi-jee-workflows.md)。

在沒有AEM Forms工作流程的AEM Forms伺服器中，AEM Forms應用程式會轉譯可在應用程式中同步的表單。 表單可在應用程式的「表單」索引標籤中使用、可提交或儲存為草稿。 應用程式支援最適化表單和行動表單。

1. **將任務或表單另存為草稿**

   另存為草稿選項保存任務或表單的快照以及已填充的資料和在關聯表單中附加的檔案。 草稿會儲存到行動裝置，並與AEM Forms伺服器同步，以供日後擷取。

   請參 [閱將任務或表單另存為草稿](/help/forms/using/save-as-draft.md)。

1. **將表單另存為範本**

   有時，當使用者填寫表格時，輸入到幾個欄位的內容會維持不變。 對於這些例項，您可以在每個例項中填寫需要相同值的欄位，並將表單或草稿儲存為範本。 現在，每次您建立範本的例項時，指定的欄位都已填入範本中指定的值。 它可協助您節省填寫表單所需的時間和精力。

   請參 [閱將表單另存為範本](/help/forms/using/save-forms-and-start-points-as-templates.md)。

### 使用工作和表單 {#working-with-tasks-and-forms}

您可以將應用程式與AEM Forms Workflow伺服器同步，並可在行動裝置上處理工作和表單。

行動裝置上的工作包含最適化表單、HTML5表單或表單集，也可包含附件和摘 [要URL](/help/forms/using/getting-task-variables-summary-url.md)。 預設情況下，分配給您的任務將放在「任務」 **[!UICONTROL 資料夾]** 中。 在處理工作時，您可以變更工作，並在AEM Forms伺服器上儲存工作草稿副本。

行動裝置上的表單可以是最適化表單或行動表單。 在表單應用程式中啟用同步的表單，可從「表單」檔案夾取用。 您可以同步在AEM Forms伺服器中啟用的表單，而不需AEM Forms工作流程（OSGi上的AEM Forms）。

請參閱：

* [開啟任務](/help/forms/using/open-task.md)
* [使用表單](/help/forms/using/working-with-form.md)

### 離線工作 {#working-offline}

您可以在離線模式下在行動裝置上工作。 即使沒有網路連線，您也可以登入應用程式，而且可以處理上次連線時與裝置同步的所有表單。 如需如何同步表單的詳細資訊，請參閱「同 [步應用程式」](/help/forms/using/sync-app.md)。 如果您選擇同步與表單關聯的附件，也可以在離線模式下開啟附件。 您可以在離線模式中編輯表單、新增註解，以及提交或儲存表單。 下次您連線時，表單會與AEM Forms伺服器同步。

如需詳細資訊，請 [參閱「在離線模式中工作](/help/forms/using/work-offline-mode.md)」。

### 添加註釋 {#adding-annotations}

您可以將下列附件新增至行動裝置上的表單

* **Notes**—— 您可以使用「附註」功能，在表單中新增手繪文字或文字附註。 如需詳細資訊，請 [參閱新增附註](/help/forms/using/add-attachments.md#adding-a-note)。

* **圖片**- AEM Forms應用程式包含使用相機功能或行動裝置圖庫的功能。 使用照片附件，可以添加具有關聯表單的照片。 如需詳細資訊，請 [參閱新增像片](/help/forms/using/add-attachments.md#adding-a-photograph)。

### 自動儲存 {#autosave}

當使用者在AEM Forms應用程式中輸入資料時，自動儲存功能會定期儲存資料。 AEM Forms應用程式中的自動儲存功能可協助您避免因電池電量不足等狀況而關閉應用程式時遺失資料。

請參 [閱「在AEM Forms應用程式中使用自動儲存」](/help/forms/using/autosave-data-app.md)。

## AEM Inbox和AEM Forms應用程式功能的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動「表單導向」工作流程的兩種主要方式是使用 [AEM Inbox](/help/forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 不過，AEM Inbox和AEM Forms應用程式的功能不同。 AEM Inbox只能與 [Forms導向的工作流程搭配使用](/help/forms/using/aem-forms-workflow.md) ，而AEM Forms應用程式則可與Forms導向的工作流程以及流程管理搭配使用。 如需AEM Inbox和AEM Forms應用程式功能之間差異的詳細資訊，請參閱「OSGi和AEM Forms JEE工作流程中以表單為中心的AEM工作流程的動作與功能」 [](/help/forms/using/capabilities-osgi-jee-workflows.md)。

## 支援的表單 {#supported-forms}

AEM Forms應用程式中支援的表格類型：

### 調適性表單 {#adaptive-form}

AEM Forms應用程式支援動態適應使用者輸入的最適化表單。 也支援延遲載入的最適化表單。

### 行動表單 {#mobile-form}

您可以在AEM Forms中建立行動裝置的表格。 行動表單會在行動裝置中轉譯為HTML表單，以根據顯示裝置進行調整。

### 表單集 {#formset}

使用表單集，可以將與服務或流程相關的多個表單分組，以自動化業務流程並呈現給最終用戶。 在這種情況下，使用者可以將整組表格一併填寫，而不需要歸檔、提交及追蹤個別表格或程式。

>[!NOTE]
>
>需要AEM Forms Workflow(AEM Forms on JEE)。

## AEM Forms應用程式的運作方式 {#how-aem-forms-app-works}

AEM Forms應用程式提供行動解決方案，讓現場工作人員處理指派給他們的表單。 應用程式會從伺服器快取完整資料，並借由將所有工作儲存在本機，提供有效率的使用者體驗。 磁碟中的資料通過及時同步更新發送到伺服器。

AEM Forms應用程式是以PhoneGap 5.0為基礎的應用程式，Backbone模型可有效率地用來透過檢視呈現模型中儲存的資料。 所有原生作業都是透過PhoneGap外掛程式執行。

## 自訂、建立和散發AEM Forms應用程式 {#customize-build-distribute}

>[!NOTE]
>
>僅適用於您使用AEM Forms應用程式原始碼來建立應用程式時。

AEM Forms應用程式可輕鬆自訂，以符合組織特定需求。 應用程式的原始碼隨附AEM Forms。 您可以變更原始碼，並建立自己的行動職場解決方案。 您也可以使用自己的企業金鑰簽署應用程式。

### 自訂 {#customize}

您可以自訂您的應用程式：

**品牌**:在AEM Forms應用程式中變更應用程式圖示、應用程式名稱、啟動影像和頁面。 您也可以變更文字，將應用程式當地語系化至特定地區。 如需AEM Forms應用程式品牌化的詳細資訊，請參閱「品牌 [化自訂」](/help/forms/using/branding-customization.md)。

**主題**:在AEM Forms應用程式使用者介面中變更顏色、字型和間距等樣式。 如需詳細資訊，請參閱 [主題自訂](/help/forms/using/theme-customization.md)。

**手勢**:在AEM Forms應用程式使用者介面中變更手勢，例如向右滑動和向左滑動。 如需詳細資訊，請參閱「手 [勢自訂」](/help/forms/using/gesture-customization.md)。

如需設定AEM Forms應用程式專案以進行自訂的詳細資訊，請參閱：

* [設定AEM Forms應用程式的環境](/help/forms/using/setup-environment-mobile-workspace.md)
* [設定Visual studio專案並建立Windows應用程式](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [設定Xcode專案並建立iOS應用程式](/help/forms/using/setup-xcode-project-build-installer.md)
* [設定Eclipse專案並建立Android應用程式](/help/forms/using/setup-eclipse-project-build-installer.md)

### 建立和散發 {#build-and-distribute}

AEM Forms應用程式的原始碼可從adobe-lc-mobileworkspace-src.zip解壓縮，此軟體是AEM Forms應用程式來源套件中封裝共用的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 導覽至封裝共用

   URL: `https://<server>:<port>/crx/packageshare`.

1. 下載來源套件。 當您下載套件時，它會新增至您的AEM Forms套件管理員。
1. 下載後，導覽至：和 `https://<server>:<port>/crx/packmgr/index.jsp`安裝 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 若要下載套件，請在您的 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 瀏覽器中開啟。

   來源套件會下載在您的裝置上。

**針對iOS**:

如需如何建立iOS應用程式(.ipa)的詳細資訊，請參 [閱「設定Xcode專案並建立iOS應用程式」](/help/forms/using/setup-xcode-project-build-installer.md)。

如需如何使用您的布建設定檔簽署AEM Forms應用程式的詳細資訊，請參閱 [iOS程式碼簽署設定、程式和疑難排解](https://developer.apple.com/support/code-signing/)。

**針對Android**:

如需如何建立Android應用程式(.apk)的詳細資訊，請參 [閱「設定Eclipse專案並建立Android應用程式」](/help/forms/using/setup-eclipse-project-build-installer.md)。

如需如何簽署AEM Forms應用程式的詳細資訊，請參閱「簽署 [您的應用程式」](https://developer.android.com/tools/publishing/app-signing.html)。

**針對Windows**:

如需如何建立Windows應用程式(.appx)的詳細資訊，請參 [閱「設定Visual studio專案並建立Windows應用程式」](/help/forms/using/setup-visual-studio-project-build-installer.md)。

如需如何透過MDM散發應用程式的詳細資訊，請參閱「 [散發AEM Forms應用程式」](/help/forms/using/distribute-mobile-workspace-app.md)。 透過MDM散發應用程式僅適用於iOS和Android。

## 將Mobile Workspace升級至AEM Forms應用程式的建議 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升級至最新版的AEM Forms應用程式，請確定您已閱讀以下幾點：

* **如果您是從Android上的Play商店安裝舊版應用程式**，您可以直接從Play商店升級應用程式。

* **如果應用程式的舊版是使用原始碼建立和安裝的（適用於iOS和Android）**:

   在安裝新應用程式之前，請先將所有資料與AEM Forms伺服器同步。 同步資料後，請解除安裝舊版應用程式，然後安裝新的應用程式。

