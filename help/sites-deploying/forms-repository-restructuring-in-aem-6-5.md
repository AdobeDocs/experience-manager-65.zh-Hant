---
title: Forms6.AEM5版資料庫重組
seo-title: Forms6.AEM5版資料庫重組
description: 瞭解如何進行必要的更改，以便遷移到針對Forms的AEM6.5中的新儲存庫結構。
seo-description: 瞭解如何進行必要的更改，以便遷移到針對Forms的AEM6.5中的新儲存庫結構。
uuid: e60830d4-23ca-4be9-941a-ee4abe4786a6
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: repo_restructuring
discoiquuid: 1ce9a622-5968-407f-a74b-d325a2bff669
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 7%

---


# Forms6.AEM5{#forms-repository-restructuring-in-aem}中的儲存庫重組

如[父6.5](/help/sites-deploying/repository-restructuring.md)頁中的「資料庫重組」頁中所述，升級至AEM6.5的客戶應使用此頁評估與影響AEM Forms解決方案的資料庫更改相關的工作成果。 有些變更需要在6.5升級程AEM序中努力工作，而有些則會延遲至日後升級。

**使用6.5升級**

* [其他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

**未來升級前**

* [EchosignCloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#echosign-cloud-service-configuration)
* [重新捕獲Cloud Service配置](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#recaptcha-cloud-service-configurations)
* [TypekitCloud Service組態](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#typekit-cloud-service-configurations)
* [其他](/help/sites-deploying/forms-repository-restructuring-in-aem-6-5.md#misc)

## 使用6.5升級{#with-upgrade}

### Misc {#misc}

| **上一個位置** | `/etc/clientlibs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp/components` |
| **重組指導** | 自訂程式碼中對「舊版」位置的任何明確參照都必須更新至「新增」位置。 |
| **附註** | 不應修改或擴展這些客戶端庫。 |

| **上一個位置** | `/etc/clientlibs/fd/rte` |
|---|---|
| **新位置** | `/libs/fd/rte` |
| **重組指導** | 對於客戶機庫中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | N/A |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/authoring/clientlibs` |
| **重組指導** | 對於客戶機庫中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/clientlibs/fd/xfaforms` |
|---|---|
| **新位置** | `/libs/fd/xfaforms/clientlibs/` |
| **重組指導** | 對於客戶機庫中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指導** | 對於客戶機庫中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/clientlibs/fd/af` |
|---|---|
| **新位置** | `/libs/fd/af/runtime/clientlibs` |
| **重組指導** | 對於客戶機庫中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/clientlibs/fd/expeditor` |
|---|---|
| **新位置** | `/libs/fd/expeditor/clientlibs` |
| **重組指導** | 對於客戶機庫中可以通過絕對路徑引用的資源，您需要在新資產中使用較新的路徑。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/clientlibs/fd/fmaddon` |
|---|---|
| **新位置** | `/libs/fd/fmaddon` |
| **重組指導** | 不建議或支援變更這些clientlibs。 如果對這些clientlibs進行了修改，則應回滾以使用AEM提供的代碼。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/aep` |
|---|---|
| **新位置** | `/var/fd/content/annotations` |
| **重組指導** | 不建議或支援變更這些clientlibs。 如果對這些clientlibs進行了修改，則應回滾以使用AEM提供的代碼。 |
| **附註** | 不適用 |

## 未來升級前{#prior-to-upgrade}

### EchosignCloud Service配置{#echosign-cloud-service-configuration}

| **上一個位置** | `/etc/cloudservices/echosign` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/echosign` |
| **重組指導** | 要從Forms遷移UI觸發的[延遲內容遷移](/help/sites-deploying/lazy-content-migration.md)實用程式。 |
| **附註** | 不適用 |

### 重新捕獲Cloud Service配置{#recaptcha-cloud-service-configurations}

| **上一個位置** | `/etc/cloudservices/recaptcha` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/recaptcha` |
| **重組指導** | 要從Forms遷移UI觸發的[延遲內容遷移](/help/sites-deploying/lazy-content-migration.md)實用程式。 |
| **附註** | 不適用 |

### TypekitCloud Service配置{#typekit-cloud-service-configurations}

| **上一個位置** | `/etc/cloudservices/typekit` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/typekit` |
| **重組指導** | 要從Forms遷移UI觸發的[延遲內容遷移](/help/sites-deploying/lazy-content-migration.md)實用程式。 |
| **附註** | 不適用 |

### Misc {#misc-1}

| **上一個位置** | `/etc/cloudservices/fdm` |
|---|---|
| **新位置** | `/conf/<tenant>/settings/cloudconfigs/fdm` |
| **重組指導** | 要從Forms遷移UI觸發的[延遲內容遷移](/help/sites-deploying/lazy-content-migration.md)實用程式。 |
| **附註** | 不適用 |

| **上一個位置** | `/etc/designs/fd/fp` |
|---|---|
| **新位置** | `/libs/fd/fp` |
| **重組指導** | 對/etc模板的任何引用最終應更新為指向其`/libs`對應項。 |
| **附註** | 不適用 |

