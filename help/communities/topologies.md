---
title: 推薦的社區拓撲
seo-title: 推薦的社區拓撲
description: 如何處理使用者產生的內容(UGC)
seo-description: 如何處理使用者產生的內容(UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 推薦的社區拓撲 {#recommended-topologies-for-communities}

自AEM Communities 6.1起，已採用獨特的方式來處理網站訪客（成員）從發佈環境提交的使用者產生內容(UGC)。

此方法與AEM平台處理一般由作者環境管理的網站內容的方式有根本不同。

AEM平台使用節點儲存區，將網站內容從作者複製到發佈，而AEM Communities則會針對從未複製的UGC使用單一、通用的儲存區。

對於常用UGC儲存，必須選擇儲存資 [源提供程式(SRP)](working-with-srp.md)。 建議的選項包括：

* [DSRP —— 關係資料庫儲存資源提供程式](dsrp.md)
* [MSRP - MongoDB儲存資源提供程式](msrp.md)
* [ASRP - adobe儲存資源供應商](asrp.md)

另一個SRP選項 [JSRP - JCR儲存資源提供方](jsrp.md)，不支援作者的通用UGC儲存，也不支援將環境發佈到兩者訪問。

需要通用儲存將導致以下建議的拓撲。

>[!NOTE]
>
>對於AEM Communities, [UGC不會複製](working-with-srp.md#ugc-never-replicated)。
>
>當部署不包含公用 [商店](working-with-srp.md),UGC只會顯示在輸入AEM發佈或作者例項上。

>[!NOTE]
>
>如需AEM平台的詳細資訊，請參 [閱Recommended Deployments](../../help/sites-deploying/recommended-deploys.md) [and Introduction to the AEM Platform](../../help/sites-deploying/data-store-config.md)。

## 適用於生產 {#for-production}

為UGC建立公用商店是十分必要的，因此基礎部署取決於其支援公用商店的能力。

兩個範例：

1) 如果預期的UGC量很高，且可能有本機MongoDB例項，則選擇為 [MSRP](msrp.md)。

2) 為獲得頁面內容的最佳效能，選擇發佈群 [和](../../help/sites-deploying/recommended-deploys.md#tarmk-farm)[ASRP](asrp.md) ，可提供相對簡單的作業來最佳化UGC縮放。

對於這兩者，部署可能基於任何OAK微內核。

要選擇適當的公用商店，請仔細考慮每個商店 [的獨特](working-with-srp.md#characteristics-of-srp-options) 性。

如需Oak microkernals的詳細資訊，請造訪建 [議的部署](../../help/sites-deploying/recommended-deploys.md)。

### TarMK發佈群組 {#tarmk-publish-farm}

當拓撲為發佈場時，相關重要主題為

* [用戶同步](sync.md)
* [管理使用者和使用者群組](users.md)

### 建議：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 網站內容儲存庫 | 用戶生成的內容儲存庫 | 儲存資源提供方 | 通用商店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobe隨選儲存 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 網站內容儲存庫 | 用戶生成的內容儲存庫 | 儲存資源提供方 | 通用商店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK農場（預設） | JCR | JCR | JSRP | 否 |
| Oak Cluster | JCR | JCR | JSRP | 僅限發佈環境的選項 |

## 開發 {#for-development}

對於非生產環境， [JSRP](jsrp.md) 可簡化使用一個作者實例和一個發佈實例來設定開發環境的程式。

如果選 [擇ASRP](asrp.md)、 [DSRP](dsrp.md) 或 [](msrp.md) MSRP供生產使用，也可以使用Adobe隨選儲存或MongoDB來設定類似的開發環境。 如需範例，請參 [閱HowTo Setup MongoDB for Demo](demo-mongo.md)。

## 引用 {#references}

* [用戶同步](sync.md)

   討論發佈群例項間使用者資料的同步化。

* [管理使用者和使用者群組](users.md)

   討論使用者和使用者群組在作者和發佈環境中的角色。

* UGC通 [用商店](working-with-srp.md)

   說明將社群內容與網站內容分開的儲存方式

* [節點儲存和資料儲存](../../help/sites-deploying/data-store-config.md)

   基本上，網站內容會儲存在節點儲存區中。 對於資產，可將資料儲存區設定為儲存二進位資料。 對於Communities，必須配置公共儲存來選擇SRP。

* [AEM 6.3中的儲存元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   介紹兩個節點儲存實施：Tar和MongoDB。
