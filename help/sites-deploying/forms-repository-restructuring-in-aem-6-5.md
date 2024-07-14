---
title: AEM 6.5中的Forms存放庫重組
description: 瞭解如何進行必要的變更，以移轉至Forms的AEM 6.5中的新存放庫結構。
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
feature: Upgrading
exl-id: d555422e-dc97-4d45-9525-4299d22315e2
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 7%

---

# AEM 6.5中的Forms存放庫重組{#forms-repository-restructuring-in-aem}

如AEM 6.5](/help/sites-deploying/repository-restructuring.md)頁面的上層[存放庫重新調整中所述，升級至AEM 6.5的客戶應使用此頁面來評估與影響AEM Forms解決方案的存放庫變更相關的工作量。 在AEM 6.5升級程式期間，有些變更需要投入大量精力，而其他變更則可能延遲到未來升級。

**升級為6.5**

* [雜項](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**未來升級之前**

* [EchosignCloud Service設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [RecaptchaCloud Service設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service設定](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [雜項](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 6.5版升級 {#with-upgrade}

### 雜項 {#misc}

| **先前位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重新建構指南** | 自訂程式碼中針對舊版位置的任何明確參照都必須更新至新位置。 |
| **附註** | 這些使用者端程式庫不應編輯或擴充。 |

| **先前位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重新建構指南** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重新建構指南** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重新建構指南** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重新建構指南** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重新建構指南** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重新建構指南** | 對於可由絕對路徑參照的使用者端程式庫中的資源，您必須在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重新建構指南** | 我們從未建議或支援變更這些clientlibs。 如果已對這些clientlibs進行修改，則應將其復原以使用AEM提供的程式碼。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重新建構指南** | 我們從未建議或支援變更這些clientlibs。 如果已對這些clientlibs進行修改，則應將其復原以使用AEM提供的程式碼。 |
| **附註** | 不適用 |

## 在日後升級之前 {#prior-to-upgrade}

### EchosignCloud Service設定 {#echosign-cloud-service-configuration}

| **先前位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重新建構指南** | 將從Forms移轉UI觸發[延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)公用程式。 |
| **附註** | 不適用 |

### RecaptchaCloud Service設定 {#recaptcha-cloud-service-configurations}

| **先前位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重新建構指南** | 將從Forms移轉UI觸發[延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)公用程式。 |
| **附註** | 不適用 |

### TypekitCloud Service設定 {#typekit-cloud-service-configurations}

| **先前位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重新建構指南** | 將從Forms移轉UI觸發[延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)公用程式。 |
| **附註** | 不適用 |

### 雜項 {#misc-1}

| **先前位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重新建構指南** | 將從Forms移轉UI觸發[延遲內容移轉](/help/sites-deploying/lazy-content-migration.md)公用程式。 |
| **附註** | 不適用 |

| **先前位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重新建構指南** | 更新對/etc範本的任何參考，以指向其`/libs`對應專案。 |
| **附註** | 不適用 |
