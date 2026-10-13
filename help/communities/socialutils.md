---
title: SocialUtils重構
description: AEM 6.1已棄用套件com.adobe.cq.social.ugcbase.SocialUtils
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 1%
---
# SocialUtils重構 {#socialutils-refactoring}

## 已棄用SocialUtils套件 {#socialutils-package-deprecated}

AEM 6.1已棄用套件`com.adobe.cq.social.ugcbase.SocialUtils`。

下表列出取代`SocialUtils`方法要使用的方法。

## SocialResourceUtilities套件  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 | 備註 |
|---|---|
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

| `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities中的方法 | 備註 |
|---|---|
| SocialResourceProvider getSocialResourceProvider(Resource) | 取代SocialResourceProvider getConfiguredProvider(Resource) |

## SCFUtilities套件 {#scfutilities-package}

| `com.adobe.cq.social.`utilities.scf.api.SCFUtilites中的方法 |
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
