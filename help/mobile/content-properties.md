---
title: 內容屬性和節點
seo-title: 內容屬性和節點
description: 請依照本頁瞭解內容屬性和節點。
seo-description: 請依照本頁瞭解內容屬性和節點。
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 內容屬性和節點 {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

文章、橫幅和系列會在AEM中呈現為cq:Pages。

除了下列顯示的其他數個屬性外，這些屬性還共用與任何cq:Page中相同的常用屬性，這些屬性代表Adobe Experience Manager(AEM)Mobile On-Demand Services中繼資料和整合支援屬性。

下表說明內容屬性和節點。

## 通用整合屬性 {#common-integration-properties}

| **屬性名稱** | **類型** | **預設值或預期值** | **說明** |
|---|---|---|---|
| dps-id | 字串 |  | 指派給AEM mobile且AEM儲存的AEM在上傳至AEM mobile或從AEM mobile匯入後 |
| dps-resourceType | 字串 | dps:Article | dps:Banner | dps:Collection | 實體類型屬性 |
| dps-version | 字串 |  | AEM mobile實體的版本（也包含在完整的aemm-id中） |
| dps-lastSynced | 日期 |  | 上次同步／從AEM mobile匯入至AEM的日期 |
| dps-lastUploaded | 日期 |  | 上次從AEM上傳至AEM mobile的日期 |
| dps-lastUploadedBy | 字串：userid |  | ID使用者，此使用者已執行從AEM到AEM mobile的上傳請求 |

## 核心中繼資料屬性 {#core-metadata-properties}

| 屬性名稱 | 類型 | 預設值或預期值 |
|--- |--- |--- |
| dps-title | 字串 |  |
| dps-shortTitle | 字串 |  |
| dps-abstract | 字串 |  |
| dps-shortAbstract | 字串 |  |
| dps-department | 字串 |  |
| dps-category | 字串 |  |
| dps-keywords | String[] |  |
| dps-internalKeywords | String[] |  |
| dps-importance | String[] | 重要性來自{&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;} |

### 文章 {#articles}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps-author | 字串 |  |
| dps-authorURL | 字串 |  |
| dps-hideFromBrowsePage | 布林值 (Boolean) |  |
| dps-access | 字串 | ProtectedAccess from {&quot;protected&quot;, &quot;metered&quot;, &quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | 字串 |  |
| dps-articleText | 字串 |  |
| dps-url | 字串 |  |

### 橫幅 {#banners}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps-tapAction |  | 來自{webLink}的TapAction |
| dps-tapActinUrl |  |  |

### 集合 {#collections}

| 屬性名稱 | 類型 | 預設值或預期值 |
|--- |--- |--- |
| dps-productId | 字串 |  |
| dps-readingPosition | 字串 | 來自{&quot;reset&quot;,&quot;retain&quot;} |
| dps-horizontalSwipe | 布林值 (Boolean) |  |
| dps-allow下載 | 布林值 (Boolean) |  |
| dps-openDefault | 字串 | 來自{&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps-layout | 字串 |  |

## 內容節點 {#content-nodes}

### 公共節點 {#common-nodes}

| 節點名稱 | 類型 | 預設值或預期值 | 說明 |
--- |--- |--- |--- |
| 影像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### 實體 {#entities}

#### 文章 {#articles-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### 橫幅 {#banners-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|---|---|---|---|
| 不適用 |  |  |  |

#### 集合 {#collections-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|--- |--- |--- |--- |
| 背景影像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
