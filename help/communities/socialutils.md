---
title: SocialUtils重構
description: AEM 6.1已棄用套件com.adobe.cq.social.ugcbase.SocialUtils
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 1%

---

# SocialUtils重構 {#socialutils-refactoring}

## 已棄用SocialUtils套件 {#socialutils-package-deprecated}

套件 `com.adobe.cq.social.ugcbase.SocialUtils` 在AEM 6.1中已過時。

下表列出用來取代的方法 `SocialUtils` 方法。

## SocialResourceUtilities套件  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| 布林值checkPermission(ResourceResolver resolver， String path， String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource) |  |
| 資源getUGCResource(Resource userResource) |  |
| 資源getUGCResource(Resource userResource， ResourceResolverFactory rrf) | 新 |
| 資源getUGCResource(Resource userResource， ResourceResolverFactory rrf， String resourceTypeHint) | 新 |
| 資源getUGCResource(Resource userResource， String resourceTypeHint) |  |
| 布林值hasModeratePermissions(Resource) |  |
| 字串resourceToACLPath(Resource) |  |
| 字串resourceToUGCStoragePath(Resource) | 取代String resourceToUGCPath(Resource) |
| 字串UGCToResourcePath(Resource) |  |
| 字串UGCToResourcePath（字串ugcPath） | 方法簽章已變更 |
| 字串UGCToResourcePath（字串ugcPath， ResourceResolver resolver） | 新 |

| 中的方法 `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | 取代SocialResourceProvider getConfiguredProvider(Resource) |

## SCFUtilities套件 {#scfutilities-package}

| 中的方法 `com.adobe.cq.social.`utilities.scf.api.SCFUtitles |
|---|
| 字串getAvatar(UserProperties userProperties) |
| 字串getAvatar(UserProperties userProperties， int size) |
| 字串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar) |
| 字串getAvatar(UserProperties userProperties， String absoluteDefaultAvatar， SocialUtils.AVATAR_SIZE) |
| 頁面getContainingPage（資源） |
| 字串getSocialProfileURL（字串使用者名稱，ResourceResolver解析器，頁面） |
| UserProperties getUserProperties(ResourceResolver resolver， String userId) |

## 僅供內部使用 {#for-internal-use-only}

| 布林值canAddNode（工作階段，字串路徑） |
|---|
| 字串createUniqueNameHint（字串訊息） |
| 字串createUniqueNameHint(String message， int numRandomChars) |
| 字串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| 頁面getPage（字串路徑， ResourceResolver resolver） |
| 字串getPagePath（資源） |
| 字串getPagePath（字串路徑） |
| 字串getResourceTypeForIncludedResource（資源元件，字串defaultResourceType，字串designPropertyName） |
| 字串getResourceTypeFromDesign（資源，字串styleProperty，字串defaultValue） |
| 布林值isResourceOwner(Resource) |
| 字串mapUGCPath（資源） |
| 字串mapUGCPath（字串ugcPath， ResourceResolver resolver） |
| 布林值mayPost(ResourceResolver resolver， Resource) |
| 字串prepareUserGeneratedContent（ResourceResolver resolver，字串路徑） |

## 方法已無法使用 {#methods-no-longer-available}

| 節點createNode(ResourceResolver resolver， String path， String nodeType) |
|---|
| 資源getResourceAtPath（ResourceResolver resolver，字串路徑） |
| 資源getResourceAtPath(ResourceResolver resolver， String path， String resourceType) |
| 設定getStorageCloudServiceConfig（資源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布林值mayAccessUGC(ResourceResolver resolver) |
