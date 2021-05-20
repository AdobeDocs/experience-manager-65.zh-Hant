---
title: 配置高級系統屬性
seo-title: 配置高級系統屬性
description: 使用「配置高級系統屬性」頁可以修改配置檔案中的某些設定，而無需導出、編輯和導入檔案。
seo-description: 使用「配置高級系統屬性」頁可以修改配置檔案中的某些設定，而無需導出、編輯和導入檔案。
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---

# 配置高級系統屬性{#configure-advanced-system-attributes}

使用「配置高級系統屬性」頁可以修改配置檔案中的某些設定，而無需導出、編輯和導入檔案。 （請參閱[匯入和匯出設定檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。）

1. 在管理控制台中，按一下「**[!UICONTROL 設定>用戶管理>配置>配置高級系統屬性]**」。
1. （選用）變更下列任一工作階段屬性：

   **工作階段逾時限制（分鐘）:** 使用者自動登出系統之前的時間量（以分鐘為單位）。依預設，無論活動或閒置，AEM表單元件（例如Workbench）都會在兩小時後逾時，且使用者必須重新登入。 有效值為`1`至`1440`。 預設值為`120`（2小時）。 此設定會更新設定檔案中的`SAML/Producer/assertionValidityInMinutes`項目鍵。

   >[!NOTE]
   >
   >您不應將工作階段逾時限制設定在10分鐘以下，因為系統可能無法正確運作。 建議值為10-120（分鐘）。

   **斷言臨界值（秒）:** 因叢集中AEM表單應用程式伺服器之間的系統時間差異而抵消延遲的緩衝時間。AEM Forms會依此屬性中指定的時間量（以秒為單位）來回溯使用者的登入時間。 有效值為`0`至`3600`。 預設值為 `60`. 此設定會更新設定檔案中的`SAML/Producer/assertionThresholdInSeconds`項目鍵。

   **允許的斷言的最大續訂次數：** 不需要登入即可透明地續訂使用者工作階段的次數上限。有效值為`0`至`9999`。 值`0`表示聲明未更新。 預設值為 10。此設定會更新設定檔案中的`SAML/Producer/maxAssertionRenewalCount`項目鍵。

1. （可選）更改以下任一目錄同步屬性：

   **同步統計記錄：** 指定用戶管理是否在同步過程中記錄詳細統計資訊。（請參閱[在同步期間啟用或禁用詳細記錄](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization)。）

   **Synch Finisher Cron表達式：** 用戶管理重試失敗同步的間隔。（請參閱[配置目錄同步重試選項](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option)。）

   **叢集作業鎖定逾時（分鐘）:** 用於叢集環境。如果某個節點上的同步失敗且未釋放群集鎖，此值將指定另一個節點在強制獲取鎖定之前等待的分鐘數。 預設值為`15`分鐘。 有效值為`1`到`1440`分鐘。

1. （可選）更改以下屬性，然後按一下&#x200B;**[!UICONTROL OK]**:

   **用戶管理器事件審核：** 選擇此選項以啟用對目錄同步事件和身份驗證事件（如成功、失敗和鎖定）的審核。預設情況下，除非您安裝了需要審核的元件(如Rights Management)，否則不會選擇此選項。 此設定會更新設定檔案中的`APSAuditService`項目鍵。

   **自動建立動態群組：** 啟用根據電子郵件網域自動建立動態群組。（請參閱[建立動態群組](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group)。）

您也可以按一下「重新載入」，回復到原始的「使用者管理」設定。
