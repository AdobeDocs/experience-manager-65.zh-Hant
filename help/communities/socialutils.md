---
title: SocialUtils重構
seo-title: SocialUtils Refactoring
description: AEM 6.1已棄用套件com.adobe.cq.social.ugcbase.SocialUtils
seo-description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
exl-id: 0f731ec6-a12e-4098-a1ec-ee4cd4dc1432
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# SocialUtils重構 {#socialutils-refactoring}

## 已棄用SocialUtils套件 {#socialutils-package-deprecated}

套件 `com.adobe.cq.social.ugcbase.SocialUtils` 已在AEM 6.1中淘汰。

下表列出要取代的方法 `SocialUtils` 方法。

## SocialResourceUtilities套件  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| 布林值checkPermission（ResourceResolver，字串路徑，字串動作） |  |
| SocialResourceProvider getSocialResourceProvider（資源） |  |
| SocialResourceConfiguration getStorageConfig（資源資源） |  |
| 資源getUGCResource(Resource userResource) |  |
| 資源getUGCResource(Resource userResource, ResourceResolverFactory rrf) | 新 |
| 資源getUGCResource（Resource userResource, ResourceResolverFactory rrf，字串resourceTypeHint） | 新 |
| 資源getUGCResource(Resource userResource, String resourceTypeHint) |  |
| 布林值hasModeratePermissions（資源） |  |
| 字串資源ToACLPath（資源資源） |  |
| 字串資源ToUGCStoragePath（資源資源） | 取代字串resourceToUGCPath（資源資源） |
| 字串UGCToResourcePath（資源資源） |  |
| 字串UGCToResourcePath（字串ugcPath） | 簽名更改 |
| 字串UGCToResourcePath（字串ugcPath, ResourceResolver） | 新 |

| 中的方法 `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider（資源） | 取代SocialResourceProvider getConfiguredProvider(Resource) |

## SCFUtilities包 {#scfutilities-package}

| 中的方法 `com.adobe.cq.social.`實用程式.scf.api.SCFUtilites |
|---|
| 字串getAvatar(UserProperties userProperties) |
| 字串getAvatar(UserProperties userProperties, int size) |
| 字串getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| 字串getAvatar（UserProperties userProperties，字串absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE大小） |
| Page getContainingPage（資源） |
| 字串getSocialProfileURL（字串使用者名稱、 ResourceResolver、Page頁面） |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## 僅供內部使用 {#for-internal-use-only}

| 布林值canAddNode（工作階段，字串路徑） |
|---|
| 字串createUniqueNameHint（字串消息） |
| 字串createUniqueNameHint（字串消息， int numRandomChars） |
| 字串generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage（字串路徑， ResourceResolver） |
| 字串getPagePath（資源） |
| 字串getPagePath（字串路徑） |
| 字串getResourceTypeForIncludedResource（Resource元件，字串defaultResourceType，字串designPropertyName） |
| 字串getResourceTypeFromDesign(Resource, String styleProperty, String defaultValue) |
| 布林值isResourceOwner（資源） |
| 字串mapUGCPath（資源） |
| 字串mapUGCPath(String ugcPath, ResourceResolver) |
| 布林值mayPost（ResourceResolver，資源） |
| 字串prepareUserGeneratedContent（ResourceResolver，字串路徑） |

## 不再提供方法 {#methods-no-longer-available}

| Node createNode（ResourceResolver，字串路徑，字串nodeType） |
|---|
| 資源getResourceAtPath（ResourceResolver，字串路徑） |
| 資源getResourceAtPath（ResourceResolver，字串路徑，字串resourceType） |
| 配置getStorageCloudServiceConfig（資源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布林值mayAccessUGC(ResourceResolver) |
