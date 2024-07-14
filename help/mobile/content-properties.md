---
title: 內容屬性和節點
description: 請依照此頁面瞭解內容屬性和節點。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 18%

---

# 內容屬性和節點 {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

在AEM中，文章、橫幅和集合以cq：Pages表示。

除了下面顯示的幾個其他屬性外，它們共用在任何cq：Page中找到的相同常見屬性，這些屬性代表Adobe Experience Manager (AEM) Mobile On-Demand Services中繼資料和整合支援屬性。

下表說明內容屬性和節點。

## 通用整合屬性 {#common-integration-properties}

| **屬性名稱** | **類型** | **預設值或預期值** | **說明** |
|---|---|---|---|
| dps-id | 字串 |  | 上傳至AEM Mobile或從AEM Mobile匯入後，由AEM Mobile指派並由AEM儲存 |
| dps-resourceType | 字串 | dps:Article | dps:Banner | dps:Collection | 實體型別屬性 |
| dps-version | 字串 |  | AEM Mobile實體版本（也包含在完整aemm-id中） |
| dps-lastSynced | 日期 |  | 上次從AEM Mobile同步/匯入至AEM的日期 |
| dps-lastUploaded | 日期 |  | 上次從AEM上傳至AEM Mobile的日期 |
| dps-lastUploadedBy | 字串：userid |  | 執行了上次從AEM到AEM Mobile上傳請求的id使用者 |

## 核心中繼資料屬性 {#core-metadata-properties}

| 屬性名稱 | 類型 | 預設值或預期值 |
|--- |--- |--- |
| dps-title | 字串 |  |
| dps-shortTitle | 字串 |  |
| dps-abstract | 字串 |  |
| dps-shortAbstract | 字串 |  |
| dps-department | 字串 |  |
| dps-category | 字串 |  |
| dps-keywords | 字串[] |  |
| dps-internalKeywords | 字串[] |  |
| dps-importance | 字串[] | 重要性來自{&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;} |

### 文章 {#articles}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps-author | 字串 |  |
| dps-authorURL | 字串 |  |
| dps-hideFromBrowsePage | 布林值 |  |
| dps-access | 字串 | ProtectedAccess來自{&quot;protected&quot;， &quot;metered&quot;， &quot;free&quot;} |
| **社交** |  |  |
| dps-socialShareURL | 字串 |  |
| dps-articleText | 字串 |  |
| dps-url | 字串 |  |

### 橫幅 {#banners}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps-tapAction |  | 來自{webLink}的TapAction |
| dps-tapActionUrl |  |  |

### 集合 {#collections}

| 屬性名稱 | 類型 | 預設值或預期值 |
|--- |--- |--- |
| dps-productId | 字串 |  |
| dps-readingPosition | 字串 | 從{&quot;reset&quot;，&quot;retain&quot;} |
| dps-horizontalSwipe | 布林值 |  |
| dps-allowDownload | 布林值 |  |
| dps-openDefault | 字串 | 從{&quot;browsePage&quot;，&quot;contentView&quot;} |
| dps-layout | 字串 |  |

## 內容節點 {#content-nodes}

### 通用節點 {#common-nodes}

| 節點名稱 | 類型 | 預設值或預期值 | 說明 |
|--- |--- |--- |--- |
| 影像 | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |  |

### 實體 {#entities}

#### 文章 {#articles-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|--- |--- |--- |--- |
| social-share-image |  | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |

#### 橫幅 {#banners-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|---|---|---|---|
| 不適用 |  |  |  |

#### 集合 {#collections-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|--- |--- |--- |--- |
| background-image | jcr：primaryType=nt：unstructured <br> sling：resourceType=foundation/components/image |  |  |
