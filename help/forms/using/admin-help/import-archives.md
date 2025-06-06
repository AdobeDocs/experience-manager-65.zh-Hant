---
title: 匯入及管理封存
description: 瞭解如何匯入及管理封存。 封存匯入並管理在Workbench中建立的LCA。 您可以匯入、設定、使用和刪除封存。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/importing_and_managing_applications_and_archives
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0c15677a-ee17-425e-a261-fb3ae8688eb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '1450'
ht-degree: 0%

---

# 匯入及管理封存 {#import-and-manage-archives}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

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
   * 若要新增「工作管理員」端點，請按一下「新增工作管理員」。 如需有關工作管理員設定的詳細資訊，請參閱[設定工作管理員端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 若要加入Watched資料夾端點，請按一下[加入WatchedFolder]。 如需Watched資料夾設定的詳細資訊，請參閱[Watched資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 若要新增電子郵件端點，請按一下[新增電子郵件]。 如需電子郵件設定的詳細資訊，請參閱[電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 若要新增EJB端點，請按一下新增EJB並指定端點的名稱和描述。
   * 若要新增SOAP端點，請按一下「新增SOAP」並指定端點的名稱和說明。
   * 若要新增遠端端點，請按一下[新增遠端]。 如需有關遠端設定的詳細資訊，請參閱[遠端端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 若要新增REST端點，請按一下新增REST並指定端點的名稱和描述。 請注意「新增REST端點」頁面上顯示的REST引動URL。
   * 若要移除端點，請選取其旁邊的核取方塊，然後按一下「移除」。

1. 按一下「下一步」。
1. 如果LCA中的處理作業或服務有組態引數，就會顯示「設定引數」頁面，您可以在此設定服務引數，然後按下一步。
1. 在「設定安全性設定檔」頁面上，進行您需要的變更：

   * **需要來電者驗證：**&#x200B;此設定表示是否可以使用或不使用認證來叫用服務。

     如果顯示&#x200B;*呼叫者目前必須驗證*，則必須驗證服務的呼叫者，而且必須授權該呼叫者的使用者主體以叫用服務；否則，將會拒絕叫用嘗試。 若要移除驗證的必要性，請按一下[允許未驗證的來電者]。

     如果顯示&#x200B;*來電者不需要驗證*，則不需要驗證服務的來電者。 因為沒有授權檢查，所以服務的呼叫一律會成功。 若要要求驗證，請按一下[要求來電者驗證]。

   * **執行身分：**&#x200B;指定服務在叫用後所使用的執行階段識別身分。 若要變更此選項，請按一下[變更]。 從下列選項中選擇：

     **未指定：**&#x200B;使用預設行為。

     **叫用者：**&#x200B;使用與叫用服務之使用者相同的身分。

     **系統：**&#x200B;以完整許可權執行服務。 這是長期處理程式的預設設定。

     **具名使用者：**&#x200B;可讓您以特定使用者的身分執行服務。 這是短期程式的預設設定。 選取此選項時，按一下「選取使用者」以顯示「選取主參與者」頁面，您可以在此頁面搜尋和選取使用者。

   * 若要將主參與者加入安全性設定檔，請按一下「加入主參與者」，然後選取使用者或群組以加入為主參與者。 按[下一步]，然後選取要指派給此主體的許可權：

     **INVOKE_PERM：**&#x200B;若要叫用服務上的所有作業

     **MODIFY_CONFIG_PERM：**&#x200B;若要修改服務的設定

     **SUPERVISOR_PERM：**&#x200B;若要檢視從處理序建立之服務的處理序執行個體資料

     **START_STOP_PERM：**&#x200B;若要啟動和停止服務

     **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;若要新增、移除及修改服務的端點

     **CREATE_VERSION_PERM：**&#x200B;若要建立服務的版本

     **DELETE_版本_PERM：**&#x200B;若要刪除服務的版本

     **MODIFY_VERSION_PERM：**&#x200B;若要修改服務的版本

     **READ_PERM：**&#x200B;檢視服務

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
   * 若要新增「工作管理員」端點，請按一下「新增工作管理員」。 如需有關工作管理員設定的詳細資訊，請參閱[設定工作管理員端點](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)。
   * 若要加入Watched資料夾端點，請按一下[加入WatchedFolder]。 如需Watched資料夾設定的詳細資訊，請參閱[Watched資料夾端點設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)。
   * 若要新增電子郵件端點，請按一下[新增電子郵件]。 如需電子郵件設定的詳細資訊，請參閱[電子郵件端點設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)。
   * 若要新增EJB端點，請按一下新增EJB並指定端點的名稱和描述。
   * 若要新增SOAP端點，請按一下「新增SOAP」並指定端點的名稱和說明。
   * 若要新增遠端端點，請按一下[新增遠端]。 如需有關遠端設定的詳細資訊，請參閱[遠端端點設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)。
   * 若要新增REST端點，請按一下新增REST並指定端點的名稱和描述。 請注意「新增REST端點」頁面上顯示的REST引動URL。
   * 若要移除端點，請選取其旁邊的核取方塊，然後按一下「移除」。

1. 按一下「下一步」。
1. 如果LCA中的處理作業或服務有組態引數，就會顯示「設定引數」頁面，您可以在此設定服務引數，然後按下一步。
1. 在「設定安全性設定檔」頁面上，您可以進行任何需要的變更：

   * **需要來電者驗證：**&#x200B;此設定表示是否可以使用或不使用認證來叫用服務。

     如果顯示&#x200B;*呼叫者目前必須驗證*，則必須驗證服務的呼叫者，而且必須授權該呼叫者的使用者主體以叫用服務；否則，將會拒絕叫用嘗試。 若要移除驗證的必要性，請按一下[允許未驗證的來電者]。

     如果顯示&#x200B;*來電者不需要驗證*，則服務的來電者可能會驗證，也可能不驗證。 因為沒有授權檢查，所以服務的呼叫一律會成功。 若要要求驗證，請按一下[要求來電者驗證]。

   * **執行身分：**&#x200B;指定服務在叫用後所使用的執行階段識別身分。 若要變更此選項，請按一下[變更]。 從下列選項中選擇：

     **未指定：**&#x200B;使用預設行為。

     **叫用者：**&#x200B;使用與叫用服務之使用者相同的身分。

     **系統：**&#x200B;以完整許可權執行服務。 這是長期處理程式的預設設定。

     **具名使用者：**&#x200B;可讓您以特定使用者的身分執行服務。 這是短期程式的預設設定。 選取此選項時，按一下「選取使用者」以顯示「選取主參與者」頁面，您可以在此頁面搜尋和選取使用者。

   * 若要將主參與者加入安全性設定檔，請按一下「加入主參與者」，然後選取使用者或群組以加入為主參與者。 按[下一步]，然後選取要指派給此主體的許可權：

     **INVOKE_PERM：**&#x200B;若要叫用服務上的所有作業

     **MODIFY_CONFIG_PERM：**&#x200B;若要修改服務的設定

     **SUPERVISOR_PERM：**&#x200B;若要檢視從處理序建立之服務的處理序執行個體資料

     **START_STOP_PERM：**&#x200B;若要啟動和停止服務

     **ADD_REMOVE_ENDPOINTS_PERM：**&#x200B;若要新增、移除及修改服務的端點

     **CREATE_VERSION_PERM：**&#x200B;若要建立服務的版本

     **DELETE_版本_PERM：**&#x200B;若要刪除服務的版本

     **MODIFY_VERSION_PERM：**&#x200B;若要修改服務的版本

     **READ_PERM：**&#x200B;檢視服務

     按一下[完成]將主體加入安全性設定檔。

## 移除封存 {#remove-an-archive}

>[!NOTE]
>
>若要移除包含儲存在協力廠商存放庫(EMC Documentum Content Server、IBM FileNet Content Manager或IBM Content Manager)中的資產的封存，您也必須使用Workbench從存放庫中刪除資產檔案。

1. 在Administration Console中，按一下「服務>應用程式和服務>封存管理」。
1. 在「歸檔管理」頁面上，選取要移除的歸檔核取方塊，然後按一下移除。
