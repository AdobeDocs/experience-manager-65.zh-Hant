---
title: Forms 6.5中的存放庫重新調整架構
seo-title: Forms Repository Restructuring in AEM 6.5
description: 了解如何進行必要的變更，以移轉至AEM 6.5 for Forms中的新存放庫結構。
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

# Forms 6.5中的存放庫重新調整架構{#forms-repository-restructuring-in-aem}

如父項所述 [AEM 6.5中的存放庫重新調整架構](/help/sites-deploying/repository-restructuring.md) 頁面中，升級至AEM 6.5的客戶應使用此頁面評估與影響AEM Forms解決方案的存放庫變更相關的工作量。 有些變更需要AEM 6.5升級程式中的工作量，而有些變更可能會延遲至日後升級。

**使用6.5升級**

* [雜項](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**未來升級前**

* [EchosignCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [RecaptchaCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [雜項](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 使用6.5升級 {#with-upgrade}

### 雜項 {#misc}

| **上一位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重組指導** | 自訂程式碼中對舊版位置的任何明確參照都必須更新至新位置。 |
| **附註** | 不應修改或擴展這些客戶端庫。 |

| **上一位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重組指導** | 對於用戶端LIB中可以由絕對路徑參照的資源，您需要在新資產中使用較新路徑。 |
| **附註** | N/A |

| **上一位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重組指導** | 對於用戶端LIB中可以由絕對路徑參照的資源，您需要在新資產中使用較新路徑。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重組指導** | 對於用戶端LIB中可以由絕對路徑參照的資源，您需要在新資產中使用較新路徑。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指導** | 對於用戶端LIB中可以由絕對路徑參照的資源，您需要在新資產中使用較新路徑。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指導** | 對於用戶端LIB中可以由絕對路徑參照的資源，您需要在新資產中使用較新路徑。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重組指導** | 對於用戶端LIB中可以由絕對路徑參照的資源，您需要在新資產中使用較新路徑。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重組指導** | 我們從不建議或支援變更這些clientlib。 如果已對這些clientlib進行修改，則應復原以使用AEM提供的程式碼。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重組指導** | 我們從不建議或支援變更這些clientlib。 如果已對這些clientlib進行修改，則應復原以使用AEM提供的程式碼。 |
| **附註** | 不適用 |

## 未來升級前 {#prior-to-upgrade}

### EchosignCloud Service配置 {#echosign-cloud-service-configuration}

| **上一位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重組指導** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 公用程式從Forms移轉UI觸發。 |
| **附註** | 不適用 |

### RecaptchaCloud Service配置 {#recaptcha-cloud-service-configurations}

| **上一位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重組指導** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 公用程式從Forms移轉UI觸發。 |
| **附註** | 不適用 |

### TypekitCloud Service配置 {#typekit-cloud-service-configurations}

| **上一位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重組指導** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 公用程式從Forms移轉UI觸發。 |
| **附註** | 不適用 |

### 雜項 {#misc-1}

| **上一位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重組指導** | 此 [延遲內容移轉](/help/sites-deploying/lazy-content-migration.md) 公用程式從Forms移轉UI觸發。 |
| **附註** | 不適用 |

| **上一位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重組指導** | 對/etc範本的任何參照最終應更新為指向其 `/libs` 對應。 |
| **附註** | 不適用 |
