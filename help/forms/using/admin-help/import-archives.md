---
title: 匯入和管理封存
seo-title: Import and manage archives
description: 了解如何匯入和管理封存檔。
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

# 匯入和管理封存 {#import-and-manage-archives}

使用存檔頁簽導入和管理在Workbench中建立的LCA。

## 匯入封存 {#import-an-archive}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」，然後按一下「存檔」頁簽。
1. 按一下「匯入」。
1. 按一下「瀏覽」以找到要匯入的封存，然後按一下「預覽」。
1. 查看將隨歸檔檔案一起安裝的資源和對象的清單。 確保與現有資源、對象和服務配置之間沒有衝突，因為沒有可用的撤消功能。

   如果選擇導入服務配置，AEM Forms將導入LCA中進程使用的所有進程配置檔案（端點、安全配置檔案和服務配置參數）。

1. 按一下「匯入」。
1. 查看導入結果，然後按一下「跳過配置」以完成導入過程，或按一下「配置」以配置存檔。

   >[!NOTE]
   >
   >如果按一下「略過配置」，則可以稍後配置歸檔。

1. 如果按一下配置，將出現「配置端點」頁，您可以在其中進行任何需要的更改：

   * 要更名終結點或編輯其說明，請按一下它。
   * 要添加任務管理器終結點，請按一下添加任務管理器。 有關「任務管理器」設定的詳細資訊，請參閱 [配置Task Manager端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * 若要新增「監看資料夾」端點，請按一下「新增WatchedFolder」。 如需「已觀看資料夾」設定的詳細資訊，請參閱 [已監看資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * 若要新增電子郵件端點，請按一下新增電子郵件。 如需「電子郵件」設定的詳細資訊，請參閱 [電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * 要添加EJB端點，請按一下「添加EJB」，並指定端點的名稱和說明。
   * 要添加SOAP端點，請按一下「添加SOAP」並指定端點的名稱和說明。
   * 要添加Remoting端點，請按一下Add Remoting。 如需Remoting設定的詳細資訊，請參閱 [遠程處理端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * 要添加REST端點，請按一下「添加REST」並指定端點的名稱和說明。 請注意「添加REST端點」頁上顯示的REST調用URL。
   * 要刪除終結點，請選中該終結點旁邊的複選框，然後按一下「刪除」。

1. 按一下下一步。
1. 如果LCA中的進程或服務具有配置參數，則會出現「配置參數」頁，您可在此配置服務參數，然後按一下下一步。
1. 在「配置安全配置檔案」頁上，進行您需要的任何更改：

   * **要求呼叫者進行身份驗證：** 此設定指示是否可以使用憑據調用該服務。

      若 *當前需要呼叫者進行身份驗證* 顯示，必須驗證服務的調用方，並且必須授權該調用方的用戶主體調用服務；否則，將拒絕調用嘗試。 要刪除驗證的需要，請按一下允許未驗證的呼叫者。

      若 *呼叫者不需要進行驗證* 顯示，則不需要驗證服務的呼叫者。 由於沒有授權檢查，服務調用將始終成功。 要要求驗證，請按一下要求呼叫者進行驗證。

   * **運行方式：** 指定調用服務後所使用的運行時標識。 要更改此選項，請按一下「更改」。 從下列選項中選擇：

      **未指定：** 使用預設行為。

      **發票人：** 使用與叫用服務的使用者相同的身分。

      **系統：** 以完全權限運行服務。 這是長期進程的預設設定。

      **指名用戶：** 可讓您以特定使用者身分執行服務。 這是短期進程的預設設定。 選擇此選項時，按一下「選擇用戶」(Select User)以顯示「選擇承擔者」(Select Principal)頁，在該頁中可以搜索並選擇用戶。

   * 要向安全配置檔案添加主體，請按一下「添加主體」(Add Principal)，然後選擇要作為主體添加的用戶或組。 按一下「下一步」 ，然後選擇要分配給此主體的權限：

      **INVOKE_PERM:** 調用服務上的所有操作

      **MODIFY_CONFIG_PERM:** 修改服務的配置

      **SUPERVISOR_PERM:** 查看從進程建立的服務的進程實例資料

      **START_STOP_PERM:** 啟動和停止服務

      **ADD_REMOVE_ENDPOINTS_PERM:** 添加、刪除和修改服務的端點

      **CREATE_VERSION_PERM:** 建立新版本的服務

      **DELETE_版本_權限：** 刪除服務版本的方式

      **MODIFY_VERSION_PERM:** 修改服務版本的方式

      **READ_PERM:** 查看服務

      按一下「完成」(Finished)將主體添加到安全配置檔案中。

1. 按一下「完成」以完成設定。

## 設定歸檔檔案中的AEM表單 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」，然後按一下「存檔」頁簽。
1. 在「存檔管理」頁上，選擇要配置的存檔檔案。
1. 在「查看存檔」頁上，選擇突出顯示的存檔資源。
1. 配置導入的進程存檔檔案。

## 使用配置嚮導配置歸檔檔案中的AEM表單 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「應用程式管理」，然後按一下「存檔」頁簽。
1. 按一下要配置的存檔檔案旁的配置。
1. 此時將出現「配置端點」頁，您可以在其中進行任何需要的更改：

   * 要更名終結點或編輯其說明，請按一下它。
   * 要添加任務管理器終結點，請按一下添加任務管理器。 有關「任務管理器」設定的詳細資訊，請參閱 [配置Task Manager端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * 若要新增「監看資料夾」端點，請按一下「新增WatchedFolder」。 如需「已觀看資料夾」設定的詳細資訊，請參閱 [已監看資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * 若要新增電子郵件端點，請按一下新增電子郵件。 如需「電子郵件」設定的詳細資訊，請參閱 [電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * 要添加EJB端點，請按一下「添加EJB」，並指定端點的名稱和說明。
   * 要添加SOAP端點，請按一下「添加SOAP」並指定端點的名稱和說明。
   * 要添加Remoting端點，請按一下Add Remoting。 如需Remoting設定的詳細資訊，請參閱 [遠程處理端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * 要添加REST端點，請按一下「添加REST」並指定端點的名稱和說明。 請注意「添加REST端點」頁上顯示的REST調用URL。
   * 要刪除終結點，請選中該終結點旁邊的複選框，然後按一下「刪除」。

1. 按一下下一步。
1. 如果LCA中的進程或服務具有配置參數，則會出現「配置參數」頁，您可在此配置服務參數，然後按一下下一步。
1. 在「配置安全配置檔案」頁上，您可以進行任何需要的更改：

   * **要求呼叫者進行身份驗證：** 此設定指示是否可以使用憑據調用該服務。

      若 *當前需要呼叫者進行身份驗證* 顯示，必須驗證服務的調用方，並且必須授權該調用方的用戶主體調用服務；否則，將拒絕調用嘗試。 要刪除驗證的需要，請按一下允許未驗證的呼叫者。

      若 *呼叫者不需要進行驗證* 顯示，服務的呼叫者可能或可能不被驗證。 由於沒有授權檢查，服務調用將始終成功。 要要求驗證，請按一下要求呼叫者進行驗證。

   * **運行方式：** 指定調用服務後所使用的運行時標識。 要更改此選項，請按一下「更改」。 從下列選項中選擇：

      **未指定：** 使用預設行為。

      **發票人：** 使用與叫用服務的使用者相同的身分。

      **系統：** 以完全權限運行服務。 這是長期進程的預設設定。

      **指名用戶：** 可讓您以特定使用者身分執行服務。 這是短期進程的預設設定。 選擇此選項時，按一下「選擇用戶」(Select User)以顯示「選擇承擔者」(Select Principal)頁，在該頁中可以搜索並選擇用戶。

   * 要向安全配置檔案添加主體，請按一下「添加主體」(Add Principal)，然後選擇要作為主體添加的用戶或組。 按一下「下一步」 ，然後選擇要分配給此主體的權限：

      **INVOKE_PERM:** 調用服務上的所有操作

      **MODIFY_CONFIG_PERM:** 修改服務的配置

      **SUPERVISOR_PERM:** 查看從進程建立的服務的進程實例資料

      **START_STOP_PERM:** 啟動和停止服務

      **ADD_REMOVE_ENDPOINTS_PERM:** 添加、刪除和修改服務的端點

      **CREATE_VERSION_PERM:** 建立新版本的服務

      **DELETE_版本_權限：** 刪除服務版本的方式

      **MODIFY_VERSION_PERM:** 修改服務版本的方式

      **READ_PERM:** 查看服務

      按一下「完成」(Finished)將主體添加到安全配置檔案中。

## 移除封存 {#remove-an-archive}

>[!NOTE]
>
>要刪除包含儲存在第三方儲存庫(EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager)中的資產的存檔，您還必須使用Workbench從儲存庫中刪除資產檔案。

1. 在管理控制台中，按一下「服務」>「應用程式和服務」>「存檔管理」。
1. 在「存檔管理」頁上，選擇要刪除的存檔的複選框，然後按一下「刪除」。
