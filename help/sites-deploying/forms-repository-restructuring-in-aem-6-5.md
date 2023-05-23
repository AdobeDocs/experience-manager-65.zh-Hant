---
title: Forms6AEM.5版
seo-title: Forms Repository Restructuring in AEM 6.5
description: 瞭解如何進行必要的更改，以便遷移到6.5版的AEMForms新儲存庫結構。
seo-description: Learn how to make the necessary changes in order to migrate to the new repository structure in AEM 6.5 for Forms.
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 7%

---

# Forms6AEM.5版{#forms-repository-restructuring-in-aem}

如父代中所述 [6.5中的AEM儲存庫重組](/help/sites-deploying/repository-restructuring.md) 頁面，升級到AEM6.5的客戶應使用此頁面評估與影響AEM Forms解決方案的儲存庫更改相關的工作量。 某些更改需要在6.5升AEM級過程中進行工作，而其他更改則可以推遲到以後升級。

**使用6.5升級**

* [雜項](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**未來升級前**

* [回聲Cloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [重新捕獲Cloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [雜項](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 使用6.5升級 {#with-upgrade}

### 雜項 {#misc}

| **上一個位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重組指導** | 自定義代碼中對舊位置的任何顯式引用都必須更新到新位置。 |
| **附註** | 不應修改或擴展這些客戶端庫。 |

| **上一個位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重組指導** | 對於客戶端清單中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重組指導** | 對於客戶端清單中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重組指導** | 對於客戶端清單中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指導** | 對於客戶端清單中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指導** | 對於客戶端清單中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重組指導** | 對於客戶端清單中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重組指導** | 從不建議或支援更改這些客戶端。 如果對這些客戶端進行了修改，則應回滾這些客戶端以使AEM用提供的代碼。 |
| **附註** | N/A |

| **上一個位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重組指導** | 從不建議或支援更改這些客戶端。 如果對這些客戶端進行了修改，則應回滾這些客戶端以使AEM用提供的代碼。 |
| **附註** | N/A |

## 未來升級前 {#prior-to-upgrade}

### 回聲Cloud Service配置 {#echosign-cloud-service-configuration}

| **上一個位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重組指導** | 的 [懶惰內容遷移](/help/sites-deploying/lazy-content-migration.md) 從Forms遷移UI觸發的實用程式。 |
| **附註** | N/A |

### 重新捕獲Cloud Service配置 {#recaptcha-cloud-service-configurations}

| **上一個位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重組指導** | 的 [懶惰內容遷移](/help/sites-deploying/lazy-content-migration.md) 從Forms遷移UI觸發的實用程式。 |
| **附註** | N/A |

### TypekitCloud Service配置 {#typekit-cloud-service-configurations}

| **上一個位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重組指導** | 的 [懶惰內容遷移](/help/sites-deploying/lazy-content-migration.md) 從Forms遷移UI觸發的實用程式。 |
| **附註** | N/A |

### 雜項 {#misc-1}

| **上一個位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重組指導** | 的 [懶惰內容遷移](/help/sites-deploying/lazy-content-migration.md) 從Forms遷移UI觸發的實用程式。 |
| **附註** | N/A |

| **上一個位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重組指導** | 對/etc模板的任何引用最終應更新為指向其 `/libs` 同行。 |
| **附註** | N/A |
