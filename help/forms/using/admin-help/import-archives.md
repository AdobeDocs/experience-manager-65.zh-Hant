---
title: 匯入及管理封存
description: 瞭解如何匯入及管理封存。 封存匯入並管理在Workbench中建立的LCA。 您可以匯入、設定、使用和刪除封存。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# 匯入及管理封存 {#import-and-manage-archives}

使用「封存」標籤來匯入及管理在Workbench中建立的LCA。

## 匯入封存 {#import-an-archive}

1. 在Administration Console中，按一下「服務」>「應用程式與服務」>「應用程式管理」，然後按一下「封存」標籤。
1. 按一下「匯入」。
1. 按一下「瀏覽」以找出要匯入的封存，然後按一下「預覽」。
1. 檢閱將隨歸檔一起安裝的資源和物件清單。 確保與現有資源、物件和服務組態沒有衝突，因為沒有可用的復原功能。

   如果您選取匯入服務組態，AEM表單會匯入LCA中處理程式使用的所有處理程式組態檔（端點、安全性設定檔及服務組態引數）。

1. 按一下「匯入」。
1. 檢閱匯入結果，然後按一下「略過組態」完成匯入程式，或按一下「組態」設定歸檔。

   >[!NOTE]
   >
   >如果按一下「略過組態」，您可以稍後再設定封存。

1. 如果按一下設定，便會顯示「設定端點」頁面，您可以在此頁面進行任何需要的變更：

   * 若要重新命名端點或編輯其說明，請按一下它。
   * 若要新增「工作管理員」端點，請按一下「新增工作管理員」。 有關「工作管理員」設定的詳細資訊，請參閱 [設定任務管理員端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * 若要加入Watched資料夾端點，請按一下[加入WatchedFolder]。 如需Watched資料夾設定的詳細資訊，請參閱 [Watched資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * 若要新增電子郵件端點，請按一下[新增電子郵件]。 如需電子郵件設定的詳細資訊，請參閱 [電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * 若要新增EJB端點，請按一下新增EJB並指定端點的名稱和描述。
   * 若要新增SOAP端點，請按一下新增SOAP並指定端點的名稱和描述。
   * 若要新增遠端端點，請按一下[新增遠端]。 如需有關遠端設定的詳細資訊，請參閱 [遠端端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * 若要新增REST端點，請按一下新增REST並指定端點的名稱和描述。 請注意「新增REST端點」頁面上顯示的REST引動URL。
   * 若要移除端點，請選取其旁邊的核取方塊，然後按一下「移除」。

1. 按一下「下一步」。
1. 如果LCA中的處理作業或服務有組態引數，就會顯示「設定引數」頁面，您可以在此設定服務引數，然後按下一步。
1. 在「設定安全性設定檔」頁面上，進行您需要的變更：

   * **要求來電者進行驗證：** 此設定會指出是否可使用或不使用認證來叫用服務。

     如果 *目前需要來電者才能進行驗證* 顯示，服務的呼叫者必須經過驗證，而且該呼叫者的使用者主體必須獲得授權才能叫用服務；否則，將會拒絕叫用嘗試。 若要移除驗證的必要性，請按一下[允許未驗證的來電者]。

     如果 *來電者不需要進行驗證* 顯示，服務的呼叫者不需要驗證。 因為沒有授權檢查，所以服務的呼叫一律會成功。 若要要求驗證，請按一下[要求來電者驗證]。

   * **執行身分：** 指定服務在叫用後所使用的執行階段識別。 若要變更此選項，請按一下[變更]。 從下列選項中選擇：

     **未指定：** 系統會使用預設行為。

     **叫用者：** 使用與叫用服務之使用者相同的身分。

     **系統：** 以完整許可權執行服務。 這是長期處理程式的預設設定。

     **已命名的使用者：** 可讓您以特定使用者的身分執行服務。 這是短期程式的預設設定。 選取此選項時，按一下「選取使用者」以顯示「選取主參與者」頁面，您可以在此頁面搜尋和選取使用者。

   * 若要將主參與者加入安全性設定檔，請按一下「加入主參與者」，然後選取使用者或群組以加入為主參與者。 按[下一步]，然後選取要指派給此主體的許可權：

     **INVOKE_PERM：** 啟動服務上的所有作業

     **修改_組態_永久性：** 修改服務的組態

     **監督員_PERM：** 若要檢視從處理建立之服務的處理序執行處理資料，請執行下列步驟：

     **START_STOP_PERM：** 啟動和停止服務的方式

     **ADD_REMOVE_ENDPOINTS_PERM：** 新增、移除和修改服務的端點

     **CREATE_VERSION_PERM：** 建立服務的版本

     **DELETE_版本_PERM：** 若要刪除服務的版本

     **MODIFY_VERSION_PERM：** 修改服務的版本

     **讀取_PERM：** 若要檢視服務

     按一下[完成]將主體加入安全性設定檔。

1. 按一下「完成」以完成設定。

## 設定屬於封存檔案一部分的AEM表單 {#configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在Administration Console中，按一下「服務」>「應用程式與服務」>「應用程式管理」，然後按一下「封存」標籤。
1. 在「歸檔管理」頁面上，選取要設定的歸檔檔案。
1. 在「檢視封存」頁面上，選取醒目提示的封存資源。
1. 設定匯入的程式封存檔案。

## 使用設定精靈來設定屬於封存檔案一部分的AEM表單 {#use-the-configuration-wizard-to-configure-the-aem-forms-that-are-part-of-an-archive-file}

1. 在Administration Console中，按一下「服務」>「應用程式與服務」>「應用程式管理」，然後按一下「封存」標籤。
1. 按一下要設定的封存檔案旁的設定。
1. 便會顯示「設定端點」頁面，您可以在此頁面進行任何需要的變更：

   * 若要重新命名端點或編輯其說明，請按一下它。
   * 若要新增「工作管理員」端點，請按一下「新增工作管理員」。 有關「工作管理員」設定的詳細資訊，請參閱 [設定任務管理員端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints).
   * 若要加入Watched資料夾端點，請按一下[加入WatchedFolder]。 如需Watched資料夾設定的詳細資訊，請參閱 [Watched資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings).
   * 若要新增電子郵件端點，請按一下[新增電子郵件]。 如需電子郵件設定的詳細資訊，請參閱 [電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings).
   * 若要新增EJB端點，請按一下新增EJB並指定端點的名稱和描述。
   * 若要新增SOAP端點，請按一下新增SOAP並指定端點的名稱和描述。
   * 若要新增遠端端點，請按一下[新增遠端]。 如需有關遠端設定的詳細資訊，請參閱 [遠端端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings).
   * 若要新增REST端點，請按一下新增REST並指定端點的名稱和描述。 請注意「新增REST端點」頁面上顯示的REST引動URL。
   * 若要移除端點，請選取其旁邊的核取方塊，然後按一下「移除」。

1. 按一下「下一步」。
1. 如果LCA中的處理作業或服務有組態引數，就會顯示「設定引數」頁面，您可以在此設定服務引數，然後按下一步。
1. 在「設定安全性設定檔」頁面上，您可以進行任何需要的變更：

   * **要求來電者進行驗證：** 此設定會指出是否可使用或不使用認證來叫用服務。

     如果 *目前需要來電者才能進行驗證* 顯示，服務的呼叫者必須經過驗證，而且該呼叫者的使用者主體必須獲得授權才能叫用服務；否則，將會拒絕叫用嘗試。 若要移除驗證的必要性，請按一下[允許未驗證的來電者]。

     如果 *來電者不需要進行驗證* 顯示時，服務的呼叫者可能會驗證，也可能不會驗證。 因為沒有授權檢查，所以服務的呼叫一律會成功。 若要要求驗證，請按一下[要求來電者驗證]。

   * **執行身分：** 指定服務在叫用後所使用的執行階段識別。 若要變更此選項，請按一下[變更]。 從下列選項中選擇：

     **未指定：** 系統會使用預設行為。

     **叫用者：** 使用與叫用服務之使用者相同的身分。

     **系統：** 以完整許可權執行服務。 這是長期處理程式的預設設定。

     **已命名的使用者：** 可讓您以特定使用者的身分執行服務。 這是短期程式的預設設定。 選取此選項時，按一下「選取使用者」以顯示「選取主參與者」頁面，您可以在此頁面搜尋和選取使用者。

   * 若要將主參與者加入安全性設定檔，請按一下「加入主參與者」，然後選取使用者或群組以加入為主參與者。 按[下一步]，然後選取要指派給此主體的許可權：

     **INVOKE_PERM：** 啟動服務上的所有作業

     **修改_組態_永久性：** 修改服務的組態

     **監督員_PERM：** 若要檢視從處理建立之服務的處理序執行處理資料，請執行下列步驟：

     **START_STOP_PERM：** 啟動和停止服務的方式

     **ADD_REMOVE_ENDPOINTS_PERM：** 新增、移除和修改服務的端點

     **CREATE_VERSION_PERM：** 建立服務的版本

     **DELETE_版本_PERM：** 若要刪除服務的版本

     **MODIFY_VERSION_PERM：** 修改服務的版本

     **讀取_PERM：** 若要檢視服務

     按一下[完成]將主體加入安全性設定檔。

## 移除封存 {#remove-an-archive}

>[!NOTE]
>
>若要移除包含儲存在協力廠商存放庫(EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager)中的資產的封存，您也必須使用Workbench從存放庫中刪除資產檔案。

1. 在Administration Console中，按一下「服務>應用程式和服務>封存管理」。
1. 在「歸檔管理」頁面上，選取要移除的歸檔核取方塊，然後按一下移除。
