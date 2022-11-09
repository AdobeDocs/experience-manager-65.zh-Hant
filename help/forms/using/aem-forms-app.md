---
title: AEM Forms應用程式
seo-title: AEM Forms app
description: AEM Forms應用程式可讓您的現場工作人員在行動裝置上使用最適化表單。
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

# AEM Forms應用程式簡介 {#aem-forms-app}

## 總覽 {#overview}

AEM Forms應用程式可讓您根據伺服器，在行動裝置上同步適用性表單、行動表單和表單。 您可以定義 [Forms OSGi工作流程](/help/forms/using/aem-forms-workflow.md) 或JEE上的Forms工作流程。 例如，您經營一家銀行，並使用AEM Forms管理客戶應用程式和通信。 您的客戶填寫表格並提交以進行驗證。 如果您在行動裝置上啟用表單，您的客戶就可以在AEM Forms應用程式中填寫表單。 您也可以在行動裝置上啟用驗證表單，以管理驗證工作流程。 您的現場工作人員可以將移動設備帶給客戶、驗證詳細資訊並提交表單。 AEM Forms應用程式會與AEM Forms伺服器同步，並擷取為行動裝置啟用的表單。 如果應用程式離線，會將資料儲存在本機。

AEM Forms應用程式的原始碼可透過Software Distribution提供給客戶使用。 Software Distribution中的原始碼套件提供如下： `adobe-aemfd-forms-app-src-pkg-<version>.zip`.

AEM Forms應用程式在iOS、Android、Windows裝置上皆受支援。 您可以從Google Play、從App Store安裝iOS，以及從Windows市集安裝適用於Android的AEM Forms應用程式。

    [ ![google_play](assets/google_play.png)](https://play.google.com/store/apps/details?id=com.adobe.aem.forms)
    
    [ ![app_store](assets/app_store.png)](https://itunes.apple.com/us/app/adobe-experience-manager-forms/id1129625976?ls=1&amp;mt=8)
    
    [ ![microsoft-badge-icon](assets/microsoft-badge-icon.png)](https://www.microsoft.com/en-us/store/p/adobe-experience-manager-forms/9nd12rlxtgtt)

若要在iOS、Android或Windows裝置上安裝、自訂和發佈應用程式，請參閱 [自訂、建置和發佈AEM Forms應用程式](#customize-build-distribute).

## 必備條件 {#prerequisites}

AEM Forms應用程式需要AEM Forms伺服器。 使用者可在AEM Forms伺服器中轉譯您建立的表單、填寫表單、另存為草稿，然後提交表單。 應用程式會連線至伺服器並從中擷取啟用的表單。 AEM Forms應用程式會與伺服器同步，當表單載入應用程式中時，使用者就能離線工作。 如果應用程式離線，資料會儲存在裝置上，而資料會在應用程式上線時與伺服器同步。

### AEM Forms應用程式搭配使用AEM Forms工作流程的伺服器 {#aem-forms-app-with-servers-using-aem-forms-workflow}

如果您有AEM Forms工作流程伺服器，則可以在AEM Forms應用程式中將表單轉譯為任務。 例如，您運行了一家銀行，客戶填寫了應用程式以使用您的服務。 此應用程式是最適化表單，可接受客戶提供的資訊，並將其儲存為提交以供審核。 管理員審閱應用程式並將驗證請求轉發到現場工作人員。 轉發的應用程式會在您的現場工作人員應用程式中作為任務啟用驗證表單。 您的現場工作人員將移動設備帶給客戶並驗證詳細資訊。

### AEM Forms應用程式，在OSGi上使用以Forms為中心的工作流程 {#aem-forms-app-with-servers-using-forms-centric-workflow-on-osgi}

如果您有AEM Forms伺服器，則可將適用性表單轉譯為AEM收件匣應用程式，以及AEM Forms應用程式中的工作。 例如，您運行了一家銀行，客戶填寫了應用程式以使用您的服務。 此應用程式與適用性表單相關聯，該表單接受客戶提供的資訊，並將其儲存為提交以供審核。 管理員審核任務並批准向現場工作人員提出的驗證請求。 您的現場工作人員將移動設備帶給客戶並驗證詳細資訊。

### 獨立表單或AEM Forms應用程式，搭配伺服器而不使用AEM Forms Workflow {#standalone-forms-or-aem-forms-app-with-servers-without-aem-forms-workflow}

未使用AEM Forms工作流程的AEM Forms伺服器為OSGi上的AEM Forms，或獨立行動表單或最適化表單。 AEM Forms應用程式可搭配您的AEM Forms實作 [OSGi](/help/sites-deploying/configuring-osgi.md). Forms您為AEM Forms應用程式啟用和發佈的功能，可在您的應用程式中使用。

表單會下載到您的應用程式中，且可離線使用。 例如，您經營的是銀行，而客戶填寫了您網站上的應用程式。 此應用程式是最適化表單，可接受客戶提供的資訊並儲存以供審核。 管理員會檢閱表單，並在AEM製作例項中建立驗證表單。 管理員可啟用表單與AEM Forms應用程式的同步處理並發佈。 如果驗證表單可在AEM Forms應用程式中使用，您的現場代理可以使用行動裝置驗證客戶的詳細資訊。 行動裝置與伺服器同步，驗證表單會載入應用程式中。 您的現場代理可以訪問客戶、驗證詳細資訊、將資料另存為草稿或提交驗證表。 應用程式上線時，表單會與伺服器同步。

若要在AEM Forms應用程式中同步表單：

1. 在製作例項中，選取表單，然後按一下 **[!UICONTROL 檢視屬性]**.

1. 在屬性頁面中，按一下 **[!UICONTROL 進階]**.
1. 在「進階」下，啟用選項： **[!UICONTROL 與AEM Forms應用程式同步]** 點選 **[!UICONTROL 儲存]**.

表單發佈後，應用程式會與伺服器同步並擷取表單。 若要同步多個表單，請在製作執行個體中，在forms manager中選取多個表單，然後點選 **[!UICONTROL 與AEM Forms應用程式同步]**.

## 行動裝置支援 {#mobile-device-support}

請參閱 [AEM Forms應用程式（先前稱為Mobile Workspace）](/help/forms/using/aem-forms-jee-supported-platforms.md#aem-forms-workspace-app)

## AEM Forms應用程式的主要功能 {#key-features-of-aem-forms-app}

### AEM Forms應用程式搭配AEM Forms伺服器 {#aem-forms-app-with-aem-forms-servers}

您可以將應用程式與AEM Forms伺服器同步，並可在行動裝置上使用表單。

使用AEM Forms工作流程伺服器，表單可以與Workbench程式和AEM收件匣應用程式中的起始點相關聯。 AEM收件匣應用程式可以有與其相關聯的最適化表單。 起始點可以有最適化表單、HTML5表單或與其相關聯的表單集。 起始點可以作為任務提交，或者任務可以另存為草稿。 有關AEM收件匣應用程式與起始點之間差異的詳細資訊，請參閱 [OSGi和AEM Forms JEE工作流程上以表單為中心的AEM工作流程的動作和功能](capabilities-osgi-jee-workflows.md).

在沒有AEM Forms工作流程的AEM Forms伺服器中，AEM Forms應用程式中會轉譯可在應用程式中同步的表單。 Forms可在應用程式的「Forms」標籤中取得，且可以提交或儲存為草稿。 應用程式支援最適化表單和行動表單。

1. **將任務或表單另存為草稿**

   另存為草稿選項可保存任務或表單的快照，以及已填充的資料和以關聯表單附加的檔案。 草稿會儲存至行動裝置並與AEM Forms伺服器同步，以供稍後擷取。

   請參閱 [將任務或表單另存為草稿](/help/forms/using/save-as-draft.md).

1. **將表單另存為範本**

   有時，當使用者填寫表單時，對幾個欄位的輸入會維持不變。 對於這類情況，您可以填寫每個實例中要求相同值的欄位，並將表單或草稿另存為模板。 現在，每次您建立範本的例項時，指定的欄位已填入範本中指定的值。 它可協助您節省填寫表格所需的時間和精力。

   請參閱 [將表單另存為範本](/help/forms/using/save-forms-and-start-points-as-templates.md).

### 使用任務和表單 {#working-with-tasks-and-forms}

您可以將應用程式與AEM Forms工作流程伺服器同步，並可在行動裝置上處理工作和表單。

行動裝置上的任務包含最適化表單、HTML5表單或表單集，也可包含附件和 [摘要URL](/help/forms/using/getting-task-variables-summary-url.md). 依預設，指派給您的任務會放在 **[!UICONTROL 工作]** 檔案夾。 處理任務時，您可以變更任務，並將任務草稿副本儲存在AEM Forms伺服器上。

行動裝置上的表單可以是最適化表單或行動表單。 Forms可在Forms資料夾中取得。 您可以在AEM Forms伺服器中啟用表單，而不需要AEM Forms工作流程(OSGi上的AEM Forms)。

請參閱：

* [開啟任務](/help/forms/using/open-task.md)
* [使用表單](/help/forms/using/working-with-form.md)

### 離線工作 {#working-offline}

您可以在離線模式下使用行動裝置。 即使沒有網路連接，您也可以登錄應用程式，並且可以在上次聯機時與設備同步的所有表單上工作。 如需如何同步表單的詳細資訊，請參閱 [同步應用程式](/help/forms/using/sync-app.md). 如果您選擇同步與表單關聯的附件，也可以以離線模式開啟附件。 您可以在離線模式中編輯表單、新增註解，以及提交或儲存表單。 表單會在您下次上線時與AEM Forms伺服器同步。

如需詳細資訊，請參閱 [在離線模式下工作](/help/forms/using/work-offline-mode.md).

### 新增註解 {#adding-annotations}

您可以在行動裝置上的表單中新增下列附件

* **附註** — 您可以使用「附註」功能，在表單中添加手繪或文本附註。 如需詳細資訊，請參閱 [新增附註](/help/forms/using/add-attachments.md#adding-a-note).

* **圖片**- AEM Forms應用程式包含使用相機功能或行動裝置圖庫的功能。 使用照片附件，可以添加具有關聯形式的照片。 如需詳細資訊，請參閱 [添加照片](/help/forms/using/add-attachments.md#adding-a-photograph).

### 自動儲存 {#autosave}

使用者在AEM Forms應用程式中輸入資料時，自動儲存功能會定期儲存資料。 AEM Forms應用程式中的自動儲存功能可協助您避免因電池不足等情況而關閉應用程式時造成資料遺失。

請參閱 [在AEM Forms應用程式中使用自動儲存](/help/forms/using/autosave-data-app.md).

## AEM收件匣和AEM Forms應用程式功能之間的差異 {#differences-between-aem-inbox-and-aem-forms-app-features}

啟動以Forms為中心的工作流程的兩種主要方式為 [AEM收件匣](/help/forms/using/manage-applications-inbox.md) 和AEM Forms應用程式。 不過，AEM收件匣和AEM Forms應用程式的功能則有所不同。 AEM收件匣僅適用於 [Forms工作流程](/help/forms/using/aem-forms-workflow.md) 而AEM Forms應用程式可搭配以Forms為中心的工作流程和程式管理運作。 如需AEM收件匣和AEM Forms應用程式功能之間差異的詳細資訊，請參閱 [OSGi和AEM Forms JEE工作流程上以表單為中心的AEM工作流程的動作和功能](capabilities-osgi-jee-workflows.md).

## 支援的表單 {#supported-forms}

AEM Forms應用程式中支援的表單類型：

### 調適性表單 {#adaptive-form}

AEM Forms應用程式支援動態適應使用者輸入的最適化表單。 也支援延遲載入的適用性表單。

### 行動表單 {#mobile-form}

您可以在AEM Forms中建立行動裝置的表單。 行動表單在可根據顯示裝置進行調整的行動裝置中，會轉譯為HTML表單。

### 表單集 {#formset}

使用表單集，可以將與服務或流程相關的多個表單分組，以自動執行業務流程並向最終用戶呈現。 在這種情況下，使用者可以將整組表單填入為一，而且不需要檔案、提交及追蹤個別表單或程式。

>[!NOTE]
>
>需要AEM Forms工作流程(JEE上的AEM Forms)。

## AEM Forms應用程式如何運作 {#how-aem-forms-app-works}

AEM Forms應用程式提供行動解決方案，讓現場工作人員處理指派給他們的表單。 應用程式從伺服器快取完整資料，並將所有工作儲存在本機以提供有效的使用者體驗。 磁碟中的資料通過及時的同步更新發送到伺服器。

AEM Forms應用程式是以PhoneGap 5.0為基礎的應用程式，其中主幹模型可有效透過檢視呈現儲存在模型中的資料。 所有原生操作都透過PhoneGap外掛程式執行。

## 自訂、建置和發佈AEM Forms應用程式 {#customize-build-distribute}

>[!NOTE]
>
>僅適用於您使用AEM Forms應用程式原始碼來建置應用程式時。

AEM Forms應用程式可輕鬆根據組織特定需求進行自訂。 應用程式的原始碼會與AEM Forms一併提供。 您可以更改原始碼並構建您自己的移動員工解決方案。 您也可以使用自己的企業金鑰簽署應用程式。

### 自訂 {#customize}

您可以針對下列項目自訂您的應用程式：

**品牌推廣**:變更AEM Forms應用程式中的應用程式圖示、應用程式名稱、啟動影像和頁面。 您也可以變更文字，將應用程式當地化至特定地區。 如需品牌化AEM Forms應用程式的詳細資訊，請參閱 [品牌自訂](/help/forms/using/branding-customization.md).

**主題**:在AEM Forms應用程式使用者介面中變更顏色、字型和間距等樣式。 如需詳細資訊，請參閱 [主題自訂](/help/forms/using/theme-customization.md).

**手勢**:在AEM Forms應用程式使用者介面中，變更向右滑動和向左滑動等手勢。 如需詳細資訊，請參閱 [手勢自訂](/help/forms/using/gesture-customization.md).

如需設定AEM Forms應用程式專案以進行自訂的詳細資訊，請參閱：

* [設定AEM Forms應用程式的環境](/help/forms/using/setup-environment-mobile-workspace.md)
* [設定Visual Studio項目並構建Windows應用程式](/help/forms/using/setup-visual-studio-project-build-installer.md)
* [設定Xcode專案並建置iOS應用程式](/help/forms/using/setup-xcode-project-build-installer.md)
* [設定Eclipse專案並建置Android應用程式](/help/forms/using/setup-eclipse-project-build-installer.md)

### 建置和發佈 {#build-and-distribute}

AEM Forms應用程式的原始碼可從 `adobe-lc-mobileworkspace-src.zip` 此元件是Software Distribution上AEM Forms應用程式來源套件的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 小節：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和類型。 您也可以使用 **[!UICONTROL 搜尋下載]** 選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選取套件，然後按一下 **[!UICONTROL 安裝]**.

**針對iOS**:

如需如何建立iOS應用程式(.ipa)的詳細資訊，請參閱 [設定Xcode專案並建置iOS應用程式](/help/forms/using/setup-xcode-project-build-installer.md).

如需如何使用您的布建設定檔簽署AEM Forms應用程式的詳細資訊，請參閱 [iOS程式碼簽署設定、程式和疑難排解](https://developer.apple.com/support/code-signing/).

**適用於Android**:

如需如何建立Android應用程式(.apk)的詳細資訊，請參閱 [設定Eclipse專案並建置Android應用程式](/help/forms/using/setup-eclipse-project-build-installer.md).

如需如何簽署AEM Forms應用程式的詳細資訊，請參閱 [簽署您的應用程式](https://developer.android.com/tools/publishing/app-signing.html).

**Windows版**:

有關如何建立Windows應用程式(.appx)的詳細資訊，請參閱 [設定Visual Studio項目並構建Windows應用程式](/help/forms/using/setup-visual-studio-project-build-installer.md).

有關如何通過MDM分發應用程式的詳細資訊，請參見 [發佈AEM Forms應用程式](/help/forms/using/distribute-mobile-workspace-app.md). 透過MDM發佈應用程式的作業僅適用於iOS和Android。

## Recommendations將Mobile Workspace升級至AEM Forms應用程式 {#recommendations-to-upgrade-mobile-workspace-to-aem-forms-app}

如果您要升級至最新版AEM Forms應用程式，請務必詳閱以下幾點：

* **如果您從Android上的play store安裝舊版應用程式**
您可以直接從Play商店升級應用程式。

* **如果使用原始碼建置並安裝舊版應用程式(適用於iOS和Android)**:

   安裝新應用程式之前，請先將所有資料與AEM Forms伺服器同步。 同步資料後，請解除安裝舊版應用程式，然後安裝新應用程式。
