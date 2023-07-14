---
title: AEM 6.5中的Forms存放庫重組
description: 瞭解如何進行必要的變更，以移轉至Forms的AEM 6.5中的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# AEM 6.5中的Forms存放庫重組{#forms-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級至AEM 6.5的客戶應使用此頁面評估與影響AEM Forms解決方案的存放庫變更相關的工作量。 有些變更需要在AEM 6.5升級過程中投入精力，而其他變更則可能延遲到未來升級。

**6.5版升級**

* [其他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**在日後升級之前**

* [EchosignCloud Service設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [RecaptchaCloud Service設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [其他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5版升級 {#with-upgrade}

### 其他 {#misc}

| **上一個位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重組指引** | 自訂程式碼中任何對舊版位置的明確參照都必須更新至新位置。 |
| **附註** | 不應編輯或擴充這些使用者端程式庫。 |

| **上一個位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重組指引** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重組指引** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重組指引** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指引** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指引** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重組指引** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重組指引** | 我們從未建議或支援變更這些clientlibs。 如果已對這些clientlibs進行修改，則應將其復原以使用AEM提供的程式碼。 |
| **附註** | N/A |

| **上一個位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重組指引** | 我們從未建議或支援變更這些clientlibs。 如果已對這些clientlibs進行修改，則應將其復原以使用AEM提供的程式碼。 |
| **附註** | N/A |

## 在日後升級之前 {#prior-to-upgrade}

### EchosignCloud Service設定 {#echosign-cloud-service-configuration}

| **上一個位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重組指引** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 從Forms移轉UI觸發的公用程式。 |
| **附註** | N/A |

### RecaptchaCloud Service設定 {#recaptcha-cloud-service-configurations}

| **上一個位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重組指引** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 從Forms移轉UI觸發的公用程式。 |
| **附註** | N/A |

### TypekitCloud Service設定 {#typekit-cloud-service-configurations}

| **上一個位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重組指引** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 從Forms移轉UI觸發的公用程式。 |
| **附註** | N/A |

### 其他 {#misc-1}

| **上一個位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重組指引** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 從Forms移轉UI觸發的公用程式。 |
| **附註** | N/A |

| **上一個位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重組指引** | 更新對/etc範本的任何參考以指向其 `/libs` 對應專案。 |
| **附註** | N/A |
