---
title: SocialUtils重構
seo-title: SocialUtils重構
description: 在AEM 6.1中不建議使用套件com.adobe.cq.sosical.ugcbase.SocialUtils
seo-description: 在AEM 6.1中不建議使用套件com.adobe.cq.sosical.ugcbase.SocialUtils
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---


# SocialUtils重構{#socialutils-refactoring}

## SocialUtils套件已過時{#socialutils-package-deprecated}

AEM 6.1中不建議使用套件`com.adobe.cq.social.ugcbase.SocialUtils`。

下表列出了用來取代`SocialUtils`方法的方法。

## SocialResourceUtilities軟體包{#socialresourceutilities-package}

| com.adobe.cq.sosical.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| Boolean checkPermission（ResourceResolver解析器、字串路徑、字串操作） |  |
| SocialResourceProvider getSocialResourceProvider（資源資源） |  |
| SocialResourceConfiguration getStorageConfig（資源資源） |  |
| 資源getUGCResource（資源userResource） |  |
| 資源getUGCResource(Resource userResource、ResourceResolverFactory rrf) | 新 |
| 資源getUGCResource(Resource userResource、ResourceResolverFactory rrf、String resourceTypeHint) | 新 |
| 資源getUGCResource(Resource userResource, String resourceTypeHint) |  |
| 布林值hasModeraPermissions（資源資源） |  |
| 字串資源ToACLPath（資源資源） |  |
| 字串資源ToUGCStoragePath（資源資源） | 替換字串resourceToUGCPath（資源資源） |
| 字串UGCToResourcePath（資源資源） |  |
| 字串UGCToResourcePath（字串ugcPath） | 更改簽名 |
| 字串UGCToResourcePath（字串ugcPath，資源解析器） | 新 |

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities中的方法 |
|---|
| SocialResourceProvider getSocialResourceProvider（資源資源） | 取代SocialResourceProvider getConfiguredProvider（資源資源） |

## SCFUtilities軟體包{#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilites中的方法 |
|---|
| 字串getAvatar(UserProperties userProperties) |
| 字串getAvatar(UserProperties userProperties, int size) |
| 字串getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| 字串getAvatar（UserProperties userProperties、String absoluteDefaultAvatar、SocialUtils.AVATAR_SIZE大小） |
| Page getContainingPage（資源資源） |
| 字串getSocialProfileURL（字串使用者名稱、資源解析程式、頁面頁面） |
| UserProperties getUserProperties(ResourceResolver、String userId) |

## 僅供內部使用{#for-internal-use-only}

| 布林canAddNode（作業階段，字串路徑） |
|---|
| 字串createUniqueNameHint（字串訊息） |
| 字串createUniqueNameHint（字串訊息， int numRandomChars） |
| 字串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage（字串路徑，資源解析程式） |
| 字串getPagePath（資源資源） |
| 字串getPagePath（字串路徑） |
| 字串getResourceTypeForIncludedResource（資源元件，字串defaultResourceType，字串designPropertyName） |
| 字串getResourceTypeFromDesign（資源， String styleProperty, String defaultValue） |
| 布爾型isResourceOwner（資源資源） |
| 字串映射UGCPath（資源資源） |
| String mapUGCPath(String ugcPath, ResourceResolver)解析器 |
| 布爾型mayPost（資源解析器、資源資源） |
| 字串prepareUserGeneratedContent(ResourceResolver, String path) |

## 方法不再可用{#methods-no-longer-available}

| Node createNode（ResourceResolver解析器、字串路徑、字串nodeType） |
|---|
| 資源getResourceAtPath（資源解析器，字串路徑） |
| 資源getResourceAtPath（資源解析器、字串路徑、字串resourceType） |
| 配置getStorageCloudServiceConfig（資源資源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布爾型mayAccessUGC(ResourceResolver) |

