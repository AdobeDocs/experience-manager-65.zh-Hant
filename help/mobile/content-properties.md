---
title: 內容屬性和節點
seo-title: Content Properties and Nodes
description: 請詳閱本頁面，了解內容屬性和節點。
seo-description: Follow this page to learn about content properties and nodes.
uuid: 2dad52c8-5b6c-4b90-8498-62217a9a27fc
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: f5721ddc-df5c-496c-be61-38d1cab63ad4
exl-id: 05c8c846-69cc-4075-9149-33890b3d1e08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 21%

---

# 內容屬性和節點 {#content-properties-and-nodes}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

文章、橫幅和集合在AEM中會以cq:Pages來呈現。

除了下方顯示的數個其他屬性外，這些屬性也共用任何cq:Page中找到的相同共同屬性，這些屬性代表Adobe Experience Manager(AEM)Mobile On-Demand Services中繼資料和整合支援屬性。

下表說明內容屬性和節點。

## 常見整合屬性 {#common-integration-properties}

| **屬性名稱** | **類型** | **預設值或預期值** | **說明** |
|---|---|---|---|
| dps-id | 字串 |  | 由AEM Mobile指派，並由AEM儲存後上傳至AEM Mobile或從AEM Mobile匯入 |
| dps-resourceType | 字串 | dps:Article | dps:Banner | dps:Collection | 實體類型屬性 |
| dps-version | 字串 |  | AEM Mobile實體版本（也包含在完整aem-id中） |
| dps-lastSynced | 日期 |  | 上次同步/從AEM Mobile匯入AEM的日期 |
| dps-lastUploaded | 日期 |  | 上次從AEM上傳至AEM Mobile的日期 |
| dps-lastUpploadedBy | String:userid |  | 從AEM執行上次上傳請求至AEM Mobile的id使用者 |

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
| dps-internalKeywords | 字串[] |  |
| dps-imperience | 字串[] | 重要性來自{&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;} |

### 文章 {#articles}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps-author | 字串 |  |
| dps-authorURL | 字串 |  |
| dps-hideFromBrowsePage | 布林值 |  |
| dps-access | 字串 | ProtectedAccess來自{&quot;protected&quot;、&quot;metered&quot;、&quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | 字串 |  |
| dps-articleText | 字串 |  |
| dps-url | 字串 |  |

### 橫幅 {#banners}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps-tapAction |  | 從{webLink}點選Action |
| dps-tapActionUrl |  |  |

### 集合 {#collections}

| 屬性名稱 | 類型 | 預設值或預期值 |
|--- |--- |--- |
| dps-productId | 字串 |  |
| dps-readingPosition | 字串 | 從{&quot;reset&quot;,&quot;retain&quot;} |
| dps-horizontalSwipe | 布林值 |  |
| dps-allowDownload | 布林值 |  |
| dps-openDefault | 字串 | 從{&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps配置 | 字串 |  |

## 內容節點 {#content-nodes}

### 公用節點 {#common-nodes}

| 節點名稱 | 類型 | 預設值或預期值 | 說明 |
|--- |--- |--- |--- |
| 影像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |

### 實體 {#entities}

#### 文章 {#articles-1}

| 節點名稱 | 類型 | 預設值 | 說明 |
|--- |--- |--- |--- |
| social-share-image |  | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |

#### 橫幅 {#banners-1}

| 節點名稱 | 類型 | 預設值 | 說明 |
|---|---|---|---|
| 不適用 |  |  |  |

#### 集合 {#collections-1}

| 節點名稱 | 類型 | 預設值 | 說明 |
|--- |--- |--- |--- |
| 背景 — 影像 | jcr:primaryType=nt:unstructured <br> sling:resourceType=foundation/components/image |  |  |
