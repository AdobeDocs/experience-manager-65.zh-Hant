---
title: 內容屬性和節點
seo-title: Content Properties and Nodes
description: 按照本頁瞭解內容屬性和節點。
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
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

文章、條幅和集合在中以cq:Pages表示AEM。

除了下面顯示的其他幾個屬性外，它們還共用任何cq:Page中的相同公共屬性，這些屬性代表Adobe Experience Manager(AEM)移動按需服務元資料和整合支援屬性。

下表描述了內容屬性和節點。

## 通用整合屬性 {#common-integration-properties}

| **屬性名稱** | **類型** | **預設值或預期值** | **說明** |
|---|---|---|---|
| dps-id | 字串 |  | 由AEM Mobile分配，一AEM次上傳至AEM Mobile或從AEM Mobile進口 |
| dps-resourceType | 字串 | dps:Article | dps:Banner | dps:Collection | 實體類型屬性 |
| dps版本 | 字串 |  | AEM Mobile實體的版本（也包含在完整aemm-id中） |
| dps — 上次同步 | 日期 |  | 上次同步/從AEM Mobile導入日AEM期 |
| dps — 上次上載 | 日期 |  | 上次從上載到AEMAEM Mobile的日期 |
| dps-lastUploadedBy | 字串：用戶ID |  | 從AEM Mobile執行上次上載請求的AEMid用戶 |

## 核心元資料屬性 {#core-metadata-properties}

| 屬性名稱 | 類型 | 預設值或預期值 |
|--- |--- |--- |
| dps標題 | 字串 |  |
| dps-shortTitle | 字串 |  |
| dps抽象 | 字串 |  |
| dps-short抽象 | 字串 |  |
| DPS部門 | 字串 |  |
| dps類別 | 字串 |  |
| dps關鍵字 | 字串[] |  |
| dps-internal關鍵字 | 字串[] |  |
| dps重要性 | 字串[] | 重要性來自{&quot;low&quot;、&quot;normal&quot;、&quot;high&quot;} |

### 文章 {#articles}

| **屬性名稱** | **類型** | **預設值或預期值** |
|---|---|---|
| dps作者 | 字串 |  |
| dps-authorURL | 字串 |  |
| dps-hideFromBrowsePage | 布林值 |  |
| dps訪問 | 字串 | ProtectedAccess來自{&quot;protected&quot;、&quot;metered&quot;、&quot;free&quot;} |
| **Social** |  |  |
| dps-socialShareURL | 字串 |  |
| dps-article文本 | 字串 |  |
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
| dps-readingPosition | 字串 | 從「重置」，「保留」 |
| dps — 水準輕掃 | 布林值 |  |
| dps-allowDownload | 布林值 |  |
| dps-openDefault | 字串 | 從{&quot;browsePage&quot;,&quot;contentView&quot;} |
| dps佈局 | 字串 |  |

## 內容節點 {#content-nodes}

### 公共節點 {#common-nodes}

| 節點名稱 | 類型 | 預設值或預期值 | 說明 |
|--- |--- |--- |--- |
| 影像 | jcr:primaryType=nt：非結構化 <br> sling:resourceType=foundation/components/image |  |  |

### 實體 {#entities}

#### 文章 {#articles-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|--- |--- |--- |--- |
| 社會共用形象 |  | jcr:primaryType=nt：非結構化 <br> sling:resourceType=foundation/components/image |  |

#### 橫幅 {#banners-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|---|---|---|---|
| 不適用 |  |  |  |

#### 集合 {#collections-1}

| 節點名稱 | 類型 | 預期值的預設值 | 說明 |
|--- |--- |--- |--- |
| 背景影像 | jcr:primaryType=nt：非結構化 <br> sling:resourceType=foundation/components/image |  |  |
