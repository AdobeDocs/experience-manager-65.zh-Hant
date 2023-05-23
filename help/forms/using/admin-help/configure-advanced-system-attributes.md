---
title: 配置高級系統屬性
seo-title: Configure advanced system attributes
description: 使用「配置高級系統屬性」頁可以修改配置檔案中的某些設定，而無需導出、編輯和導入檔案。
seo-description: Use the Configure Advanced System Attributes page to modify certain settings in the configuration file without the need to export, edit, and import the file.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 1%

---

# 配置高級系統屬性 {#configure-advanced-system-attributes}

使用「配置高級系統屬性」頁可以修改配置檔案中的某些設定，而無需導出、編輯和導入檔案。 (請參閱 [導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。)

1. 在管理控制台中，按一下 **[!UICONTROL 設定>用戶管理>配置>配置高級系統屬性]**。
1. （可選）更改以下任一會話屬性：

   **會話超時限制（分鐘）:** 用戶自動從系統註銷之前的時間（以分鐘為單位）。 預設情況下，AEM表單元件（如Workbench）在兩小時後超時，而不管活動或不活動狀態如何，用戶必須重新登錄。 有效值為 `1` 至 `1440`。 預設值為 `120` （2小時）。 此設定將更新 `SAML/Producer/assertionValidityInMinutes` 的子菜單。

   >[!NOTE]
   >
   >您不應將會話超時限制設定在10分鐘以下，因為系統可能不能正常運行。 建議的值為10-120（分鐘）。

   **斷言閾值（秒）:** 用於補償由於群集中表單應用程式伺服器之間的系統時AEM間差而引起的延遲的緩衝時間。 表AEM單按此屬性中指定的時間（秒）將用戶的登錄時間進行回溯。 有效值為 `0` 至 `3600`。 預設值為 `60`。此設定將更新 `SAML/Producer/assertionThresholdInSeconds` 的子菜單。

   **斷言的允許最大續訂數：** 無需登錄即可透明地續訂用戶會話的最大次數。 有效值為 `0` 至 `9999`。 值 `0` 意味著不會更新斷言。 預設值為 10。此設定將更新 `SAML/Producer/maxAssertionRenewalCount` 的子菜單。

1. （可選）更改下列任一目錄同步屬性：

   **同步統計記錄：** 指定用戶管理是否在同步過程中記錄詳細統計資訊。 (請參閱 [在同步期間啟用或禁用詳細記錄](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)。)

   **同步分頁裝訂器Cron表達式：** 用戶管理重試失敗同步的間隔。 (請參閱 [配置目錄同步重試選項](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)。)

   **群集作業鎖定超時（分鐘）:** 用於群集環境。 如果一個節點上的同步失敗且未釋放群集鎖，則此值指定另一個節點在強制獲取鎖之前等待的分鐘數。 預設值為 `15` 分鐘。 有效值為 `1` 至 `1440` 分鐘。

1. （可選）更改以下屬性，然後按一下 **[!UICONTROL 確定]**:

   **用戶管理器事件審核：** 選擇此選項可啟用對目錄同步事件和驗證事件（如成功、失敗和鎖定）的審核。 預設情況下，除非您安裝了需要審核的元件(如Rights Management)，否則不會選擇此選項。 此設定將更新 `APSAuditService` 的子菜單。

   **自動建立動態組：** 啟用基於電子郵件域的動態組的自動建立。 (請參閱 [建立動態組](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)。)

也可以通過按一下「重新載入」(Reload)恢復到原始的「用戶管理」(User Management)設定。
