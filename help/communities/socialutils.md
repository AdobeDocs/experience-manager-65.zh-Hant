---
title: SocialUtils重構
seo-title: SocialUtils Refactoring
description: 在6.1中不建議使用包com.adobe.cq.social.ugcbaseAEM.SocialUtils
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

## 已棄用SocialUtils包 {#socialutils-package-deprecated}

包 `com.adobe.cq.social.ugcbase.SocialUtils` 6.1中AEM不建議使用。

下表列出了要替代的方法 `SocialUtils` 的雙曲餘切值。

## SocialResourceUtilities包  {#socialresourceutilities-package}

| com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities中的方法 |
|---|
| Boolean checkPermission（ResourceResolver解析器，字串路徑，字串操作） |  |
| SocialResourceProvider getSocialResourceProvider（資源資源） |  |
| SocialResourceConfiguration getStorageConfig（資源資源） |  |
| 資源getUGCResource（資源用戶資源） |  |
| 資源getUGCResource(Resource userResource、ResourceResolverFactory rrf) | 新 |
| 資源getUGCResource(Resource userResource、ResourceResolverFactory rf、String resourceTypeHint) | 新 |
| 資源getUGCResource(Resource userResource、String resourceTypeHint) |  |
| 布爾型hasMedeatePermissions（資源資源） |  |
| 字串resourceToACLPath（資源資源） |  |
| 字串resourceToUGCStoragePath（資源資源） | 替換字串resourceToUGCPath（Resource資源） |
| 字串UGCToResourcePath（資源資源） |  |
| 字串UGCToResourcePath（字串ugcPath） | 更改了簽名 |
| 字串UGCToResourcePath（字串ugcPath, ResourceResolver） | 新 |

| 中的方法 `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider（資源資源） | 替換SocialResourceProvider getConfiguredProvider（資源資源） |

## SCFUtilities包 {#scfutilities-package}

| 中的方法 `com.adobe.cq.social.`實用程式.scf.api.SCFUtilites |
|---|
| 字串getAvatar(UserProperties userProperties) |
| 字串getAvatar（UserProperties userProperties, int大小） |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar（UserProperties userProperties、String absoluteDefaultAvatar、SocialUtils.AVATAR_SIZE大小） |
| Page getContainingPage（資源資源） |
| String getSocialProfileURL(String username, ResourceResolver, Page) |
| UserProperties getUserProperties(ResourceResolver, String userId) |

## 僅供內部使用 {#for-internal-use-only}

| 布爾canAddNode（會話，字串路徑） |
|---|
| 字串createUniqueNameHint（字串消息） |
| 字串createUniqueNameHint（String消息， int numRandomChars） |
| 字串generateRandomString（int長度） |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage（字串路徑，資源解析器） |
| 字串getPagePath（資源資源） |
| 字串getPagePath（字串路徑） |
| 字串getResourceTypeForIncludedResource（資源元件，字串defaultResourceType，字串designPropertyName） |
| 字串getResourceTypeFromDesign（資源、字串styleProperty、字串defaultValue） |
| 布爾型isResourceOwner（資源資源） |
| 字串mapUGCPath（資源資源） |
| 字串mapUGCPath（字串ugcPath, ResourceResolver） |
| 布爾型mayPost（ResourceResolver、Resource資源） |
| 字串prepareUserGeneratedContent（ResourceResolver, String路徑） |

## 方法不再可用 {#methods-no-longer-available}

| Node createNode（ResourceResolver解析器， String path, String nodeType） |
|---|
| 資源getResourceAtPath（ResourceResolver, String路徑） |
| 資源getResourceAtPath(ResourceResolver, String path, String resourceType) |
| 配置getStorageCloudServiceConfig（資源資源） |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| 布爾型mayAccessUGC(ResourceResolver) |
