---
title: 匯入和管理封存
seo-title: 匯入和管理封存
description: 瞭解如何匯入和管理封存。
seo-description: 瞭解如何匯入和管理封存。
uuid: aa1613dd-6350-49a7-9643-44365e2acdcc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b6f6463a-2ae4-43d2-8d16-cc20a954e50e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 匯入和管理封存 {#import-and-manage-archives}

使用封存標籤來匯入和管理在工作台中建立的LCA。

## 匯入封存 {#import-an-archive}

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」，然後按一下封存標籤。
1. 按一下「匯入」。
1. 按一下「瀏覽」以找出要匯入的封存，然後按一下「預覽」。
1. 查看將隨歸檔檔案一起安裝的資源和對象的清單。 確保與現有資源、對象和服務配置沒有衝突，因為沒有可用的還原功能。

   如果您選擇匯入服務設定，AEM表單會匯入LCA中流程所使用的所有流程設定檔案（端點、安全性設定檔和服務設定參數）。

1. 按一下「匯入」。
1. 檢視匯入結果，然後按一下「略過設定」以完成匯入程式，或按一下「設定」以設定封存檔。

   >[!NOTE]
   >
   >如果按一下「跳過配置」，則可以稍後配置存檔。

1. 如果按一下「配置」，將顯示「配置端點」頁，您可以在其中進行任何需要的更改：

   * 要更名端點或編輯其說明，請按一下該端點。
   * 要添加任務管理器端點，請按一下添加任務管理器。 有關Task Manager設定的詳細資訊，請參 [閱Configuring Task Manager端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 若要新增「監看資料夾」端點，請按一下「新增WatchedFolder」。 如需「Watched資料夾」設定的詳細資訊，請參閱「 [Watched資料夾端點設定」](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 若要新增電子郵件端點，請按一下「新增電子郵件」。 如需「電子郵件」設定的詳細資訊，請參閱「電 [子郵件端點設定」](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB端點，請按一下「添加EJB」並指定端點的名稱和說明。
   * 要添加SOAP端點，請按一下「添加SOAP」並指定端點的名稱和說明。
   * 要添加遠程端點，請按一下「添加遠程」。 如需「移除」設定的詳細資訊，請參閱「 [移除端點設定」](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端點，請按一下「添加REST」(Add REST)，並指定端點的名稱和說明。 請注意「添加REST端點」頁上顯示的REST調用URL。
   * 要刪除端點，請選中端點旁的複選框，然後按一下「刪除」。

1. 按一下「下一步」。
1. 如果LCA中的進程或服務具有配置參數，將顯示「配置參數」頁，在該頁中配置服務參數並按一下「下一步」。
1. 在「配置安全性配置檔案」頁上，進行任何需要的更改：

   * **** 要求呼叫者驗證：此設定指示是否可以使用或不使用憑據調用服務。

      如果 *顯示當前需要呼叫者進行驗證* ，則服務呼叫者必須經過驗證，並且該呼叫者的用戶主體必須獲得調用該服務的授權；否則，將拒絕調用。 若要移除驗證的需要，請按一下「允許未驗證的呼叫者」。

      如果 *不需要呼叫者來驗證* ，則無需驗證服務的呼叫者。 由於沒有授權檢查，因此服務的調用始終會成功。 要要求驗證，請按一下要求呼叫者驗證。

   * **** 執行方式：指定服務在被調用後所使用的運行時標識。 若要變更此選項，請按一下「變更」。 從下列選項中選擇：

      **** 未指定：使用預設行為。

      **** 調用程式：使用與呼叫服務的使用者相同的身分。

      **** 系統：以完全權限運行服務。 這是長壽命進程的預設設定。

      **** 指名用戶：可讓您以特定使用者身分執行服務。 這是短時間進程的預設設定。 選擇此選項後，按一下選擇用戶以顯示「選擇承擔者」頁，您可以在其中搜索和選擇用戶。

   * 要將承擔者添加到安全配置檔案中，請按一下「添加承擔者」(Add Principal)，然後選擇要添加為承擔者的用戶或組。 按一下「下一步」(Next)，然後選擇要分配給此承擔者的權限：

      **** INVOKE_PERM:調用服務上的所有操作

      **** MODIFY_CONFIG_PERM:修改服務的配置

      **** SUPERVISOR_PERM:要查看從流程建立的服務的流程實例資料

      **** START_STOP_PERM:啟動和停止服務

      **** ADD_REMOVE_ENDIPTS_PERM:添加、刪除和修改服務的端點

      **** CREATE_VERSION_PERM:建立服務的新版本

      **** DELETE_VERSION_PERM:刪除服務版本

      **** MODIFY_VERSION_PERM:修改服務版本

      **** READ_PERM:若要檢視服務

      按一下「完成」(Finished)將承擔者添加到安全配置檔案中。

1. 按一下「完成」以完成設定。

## 設定屬於封存檔案一部分的AEM表單 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」，然後按一下封存標籤。
1. 在「存檔管理」頁上，選擇要配置的存檔檔案。
1. 在「查看存檔」頁上，選擇突出顯示的存檔資源。
1. 配置導入的進程存檔檔案。

## 使用設定精靈來設定屬於封存檔案一部分的AEM表單 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在管理控制台中，按一下「服務>應用程式與服務>應用程式管理」，然後按一下封存標籤。
1. 按一下要配置的存檔檔案旁邊的配置。
1. 此時將顯示「配置端點」頁，您可以在其中進行任何需要的更改：

   * 要更名端點或編輯其說明，請按一下該端點。
   * 要添加任務管理器端點，請按一下添加任務管理器。 有關Task Manager設定的詳細資訊，請參 [閱Configuring Task Manager端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 若要新增「監看資料夾」端點，請按一下「新增WatchedFolder」。 如需「Watched資料夾」設定的詳細資訊，請參閱「 [Watched資料夾端點設定」](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 若要新增電子郵件端點，請按一下「新增電子郵件」。 如需「電子郵件」設定的詳細資訊，請參閱「電 [子郵件端點設定」](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 要添加EJB端點，請按一下「添加EJB」並指定端點的名稱和說明。
   * 要添加SOAP端點，請按一下「添加SOAP」並指定端點的名稱和說明。
   * 要添加遠程端點，請按一下「添加遠程」。 如需「移除」設定的詳細資訊，請參閱「 [移除端點設定」](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 要添加REST端點，請按一下「添加REST」(Add REST)，並指定端點的名稱和說明。 請注意「添加REST端點」頁上顯示的REST調用URL。
   * 要刪除端點，請選中該端點旁的複選框，然後按一下「刪除」。

1. 按一下「下一步」。
1. 如果LCA中的進程或服務具有配置參數，將顯示「配置參數」頁，在該頁中配置服務參數並按一下「下一步」。
1. 在「配置安全性配置檔案」頁上，您可以進行任何需要的更改：

   * **** 要求呼叫者驗證：此設定指示是否可以使用或不使用憑據調用服務。

      如果 *顯示當前需要呼叫者進行驗證* ，則服務呼叫者必須經過驗證，並且該呼叫者的用戶主體必須獲得調用該服務的授權；否則，將拒絕調用。 若要移除驗證的需要，請按一下「允許未驗證的呼叫者」。

      如果 *不需要呼叫者來驗證* ，則服務呼叫者可能會被驗證，也可能不被驗證。 由於沒有授權檢查，因此服務的調用始終會成功。 要要求驗證，請按一下要求呼叫者驗證。

   * **** 執行方式：指定服務在被調用後所使用的運行時標識。 若要變更此選項，請按一下「變更」。 從下列選項中選擇：

      **** 未指定：使用預設行為。

      **** 調用程式：使用與呼叫服務的使用者相同的身分。

      **** 系統：以完全權限運行服務。 這是長壽命進程的預設設定。

      **** 指名用戶：可讓您以特定使用者身分執行服務。 這是短時間進程的預設設定。 選擇此選項後，按一下選擇用戶以顯示「選擇承擔者」頁，您可以在其中搜索和選擇用戶。

   * 要將承擔者添加到安全配置檔案中，請按一下「添加承擔者」(Add Principal)，然後選擇要添加為承擔者的用戶或組。 按一下「下一步」(Next)，然後選擇要分配給此承擔者的權限：

      **** INVOKE_PERM:調用服務上的所有操作

      **** MODIFY_CONFIG_PERM:修改服務的配置

      **** SUPERVISOR_PERM:要查看從流程建立的服務的流程實例資料

      **** START_STOP_PERM:啟動和停止服務

      **** ADD_REMOVE_ENDIPTS_PERM:添加、刪除和修改服務的端點

      **** CREATE_VERSION_PERM:建立服務的新版本

      **** DELETE_VERSION_PERM:刪除服務版本

      **** MODIFY_VERSION_PERM:修改服務版本

      **** READ_PERM:若要檢視服務

      按一下「完成」(Finished)將承擔者添加到安全配置檔案中。

## 移除封存 {#remove-an-archive}

>[!NOTE]
>
>要刪除包含儲存在第三方儲存庫（EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager）中的資產的存檔，您還必須使用Workbench從儲存庫中刪除資產檔案。

1. 在管理控制台中，按一下「服務>應用程式與服務>封存管理」。
1. 在「存檔管理」頁面上，選中要刪除的存檔的複選框，然後按一下刪除。

