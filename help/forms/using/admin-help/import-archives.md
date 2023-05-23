---
title: 導入和管理存檔
seo-title: Import and manage archives
description: 瞭解如何導入和管理存檔。
seo-description: Learn how to import and manage archives.
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# 導入和管理存檔 {#import-and-manage-archives}

使用「存檔」標籤可導入和管理在工作台中建立的LCA。

## 導入存檔 {#import-an-archive}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」，然後按一下「存檔」頁籤。
1. 按一下「導入」。
1. 按一下「瀏覽」查找要導入的存檔，然後按一下「預覽」。
1. 查看將隨存檔一起安裝的資源和對象的清單。 確保與現有資源、對象和服務配置沒有衝突，因為沒有可用的撤消功能。

   如果選擇導入服務配置，AEM則表單將導入LCA中進程使用的所有進程配置檔案（端點、安全配置檔案和服務配置參數）。

1. 按一下「導入」。
1. 查看導入結果，然後按一下跳過配置以完成導入過程，或按一下配置以配置存檔。

   >[!NOTE]
   >
   >如果按一下「跳過配置」，則可以稍後配置存檔。

1. 如果按一下配置，將顯示「配置端點」頁，在該頁中可以進行任何需要的更改：

   * 要更名終結點或編輯其說明，請按一下它。
   * 要添加任務管理器終結點，請按一下添加任務管理器。 有關「任務管理器」設定的詳細資訊，請參閱 [配置Task Manager終結點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 要添加「監視資料夾」終結點，請按一下「添加監視資料夾」。 有關「監視資料夾」設定的詳細資訊，請參閱 [已監視資料夾終結點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 要添加電子郵件終結點，請按一下「添加電子郵件」。 有關電子郵件設定的詳細資訊，請參閱 [電子郵件終結點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB終結點，請按一下「添加EJB」，然後指定終結點的名稱和說明。
   * 要添加SOAP終結點，請按一下「添加SOAP」並指定終結點的名稱和說明。
   * 要添加遠程處理終結點，請按一下添加遠程處理。 有關遠程處理設定的詳細資訊，請參閱 [遠程處理終結點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端點，請按一下「添加REST」(Add REST)，並指定端點的名稱和說明。 請注意「添加REST端點」頁上顯示的REST調用URL。
   * 要刪除端點，請選中端點旁邊的複選框，然後按一下「刪除」。

1. 按一下下一步。
1. 如果LCA中的進程或服務具有配置參數，則會顯示「配置參數」頁，在該頁中配置服務參數並按一下下一步。
1. 在「配置安全性配置檔案」頁上，進行任何需要的更改：

   * **要求呼叫者驗證：** 此設定指示是否可以使用或不使用憑據調用服務。

      如果 *當前需要呼叫者進行身份驗證* 服務的調用方必須經過驗證，並且該調用方的用戶主體必須被授權調用該服務；否則，調用嘗試將被拒絕。 要刪除驗證的需要，請按一下允許未驗證的呼叫者。

      如果 *不需要呼叫者進行身份驗證* 顯示，無需驗證服務的調用方。 由於沒有授權檢查，因此服務調用將始終成功。 要要求驗證，請按一下要求呼叫者驗證。

   * **運行方式：** 指定在調用服務後由服務使用的運行時標識。 要更改此選項，請按一下「更改」。 從以下選項中選擇：

      **未指定：** 使用預設行為。

      **調用程式：** 使用與調用服務的用戶相同的標識。

      **系統：** 以完全權限運行服務。 這是長期進程的預設設定。

      **命名用戶：** 允許您以特定用戶身份運行服務。 這是短時間進程的預設設定。 選擇此選項後，按一下選擇用戶以顯示「選擇承擔者」頁，在該頁中可以搜索和選擇用戶。

   * 要將承擔者添加到安全配置檔案，請按一下「添加承擔者」(Add Principal)，然後選擇要作為承擔者添加的用戶或組。 按一下「下一步」，然後選擇要分配給此承擔者的權限：

      **INVOKE_PERM:** 調用服務上的所有操作：

      **MODIFY_CONFIG_PERM:** 修改服務的配置

      **SUPERVISOR_PERM:** 查看從進程建立的服務的進程實例資料

      **START_STOP_PERM:** 啟動和停止服務

      **ADD_REMOVE_ENDPOINTS_PERM:** 添加、刪除和修改服務的端點

      **CREATE_VERSION_PERM:** 建立服務的新版本

      **DELETE_版本_PERM:** 刪除服務版本

      **MODIFY_VERSION_PERM:** 修改服務版本

      **讀取(_P):** 查看服務

      按一下「完成」(Finished)將承擔者添加到安全配置檔案。

1. 按一下「完成」(Finished)完成配置。

## 配置AEM作為存檔檔案一部分的表單 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」，然後按一下「存檔」頁籤。
1. 在「存檔管理」頁上，選擇要配置的存檔檔案。
1. 在「查看存檔」頁上，選擇突出顯示的存檔資源。
1. 配置導入的進程存檔檔案。

## 使用配置嚮導配置AEM作為存檔檔案一部分的表單 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」，然後按一下「存檔」頁籤。
1. 按一下要配置的存檔檔案旁的「配置」。
1. 此時將顯示「配置端點」頁，在該頁中可以進行任何需要的更改：

   * 要更名終結點或編輯其說明，請按一下它。
   * 要添加任務管理器終結點，請按一下添加任務管理器。 有關「任務管理器」設定的詳細資訊，請參閱 [配置Task Manager終結點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 要添加「監視資料夾」終結點，請按一下「添加監視資料夾」。 有關「監視資料夾」設定的詳細資訊，請參閱 [已監視資料夾終結點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 要添加電子郵件終結點，請按一下「添加電子郵件」。 有關電子郵件設定的詳細資訊，請參閱 [電子郵件終結點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB終結點，請按一下「添加EJB」，然後指定終結點的名稱和說明。
   * 要添加SOAP終結點，請按一下「添加SOAP」並指定終結點的名稱和說明。
   * 要添加遠程處理終結點，請按一下添加遠程處理。 有關遠程處理設定的詳細資訊，請參閱 [遠程處理終結點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端點，請按一下「添加REST」(Add REST)，並指定端點的名稱和說明。 請注意「添加REST端點」頁上顯示的REST調用URL。
   * 要刪除端點，請選中端點旁邊的複選框，然後按一下「刪除」。

1. 按一下下一步。
1. 如果LCA中的進程或服務具有配置參數，則會顯示「配置參數」頁，在該頁中配置服務參數並按一下下一步。
1. 在「配置安全性配置檔案」頁上，您可以進行任何需要的更改：

   * **要求呼叫者驗證：** 此設定指示是否可以使用或不使用憑據調用服務。

      如果 *當前需要呼叫者進行身份驗證* 服務的調用方必須經過驗證，並且該調用方的用戶主體必須被授權調用該服務；否則，調用嘗試將被拒絕。 要刪除驗證的需要，請按一下允許未驗證的呼叫者。

      如果 *不需要呼叫者進行身份驗證* 顯示，服務的呼叫者可以或不可以被認證。 由於沒有授權檢查，因此服務調用將始終成功。 要要求驗證，請按一下要求呼叫者驗證。

   * **運行方式：** 指定在調用服務後由服務使用的運行時標識。 要更改此選項，請按一下「更改」。 從以下選項中選擇：

      **未指定：** 使用預設行為。

      **調用程式：** 使用與調用服務的用戶相同的標識。

      **系統：** 以完全權限運行服務。 這是長期進程的預設設定。

      **命名用戶：** 允許您以特定用戶身份運行服務。 這是短時間進程的預設設定。 選擇此選項後，按一下選擇用戶以顯示「選擇承擔者」頁，在該頁中可以搜索和選擇用戶。

   * 要將承擔者添加到安全配置檔案，請按一下「添加承擔者」(Add Principal)，然後選擇要作為承擔者添加的用戶或組。 按一下「下一步」，然後選擇要分配給此承擔者的權限：

      **INVOKE_PERM:** 調用服務上的所有操作：

      **MODIFY_CONFIG_PERM:** 修改服務的配置

      **SUPERVISOR_PERM:** 查看從進程建立的服務的進程實例資料

      **START_STOP_PERM:** 啟動和停止服務

      **ADD_REMOVE_ENDPOINTS_PERM:** 添加、刪除和修改服務的端點

      **CREATE_VERSION_PERM:** 建立服務的新版本

      **DELETE_版本_PERM:** 刪除服務版本

      **MODIFY_VERSION_PERM:** 修改服務版本

      **讀取(_P):** 查看服務

      按一下「完成」(Finished)將承擔者添加到安全配置檔案。

## 刪除存檔 {#remove-an-archive}

>[!NOTE]
>
>要刪除包含儲存在第三方儲存庫(EMC Documentum Content Server 、IBM FileNet Content Manager或IBMContent Manager)中的資產的存檔，還必須使用Workbench從儲存庫中刪除資產檔案。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「存檔管理」。
1. 在「存檔管理」頁上，選中要刪除的存檔的複選框，然後按一下刪除。
