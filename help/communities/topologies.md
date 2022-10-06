---
title: 適用於社群的建議拓撲
seo-title: Recommended Topologies for Communities
description: 如何處理使用者產生的內容(UGC)
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 適用於社群的建議拓撲 {#recommended-topologies-for-communities}

自AEM Communities 6.1起，已採用獨特的方法來處理網站訪客（成員）從發佈環境提交的使用者產生內容(UGC)。

此方法與AEM平台處理一般從製作環境管理之網站內容的方式有根本不同。

AEM平台使用節點存放區，將網站內容從作者複製到發佈，而AEM Communities則使用單一、通用存放區，用於從未複製過的UGC。

對於通用UGC存放區，必須選擇 [儲存資源提供程式(SRP)](working-with-srp.md). 建議的選擇包括：

* [DSRP — 關係資料庫儲存資源提供程式](dsrp.md)
* [MSRP - MongoDB儲存資源提供程式](msrp.md)
* [ASRP -Adobe儲存資源提供程式](asrp.md)

另一個SRP選項， [JSRP - JCR儲存資源提供商](jsrp.md)，不支援製作和發佈環境兩者皆存取的通用UGC存放區。

需要通用商店會產生以下建議的拓撲。

>[!NOTE]
>
>對於AEM Communities, [UGC從未複製](working-with-srp.md#ugc-never-replicated).
>
>當部署不包括 [公用商店](working-with-srp.md),UGC只會顯示在輸入UGC的AEM發佈或製作例項上。

>[!NOTE]
>
>如需AEM平台的詳細資訊，請參閱 [建議的部署](../../help/sites-deploying/recommended-deploys.md) 和 [AEM Platform簡介](../../help/sites-deploying/data-store-config.md).

## 生產 {#for-production}

為UGC建立公共儲存庫是必不可少的，因此基礎部署取決於其支援公共儲存庫的能力。

兩個範例：

1. 如果UGC的預期容量很高，並且可能有本地MongoDB實例，則選擇 [MSRP](msrp.md).

1. 為獲得最佳的頁面內容效能，請選取 [發佈農場](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) 和 [ASRP](asrp.md) 將提供相對簡單的操作來優化UGC的擴展。

對於這兩者，部署皆可以根據任何OAK微內核。

若要選擇適當的公用存放區，請仔細考慮 [特徵](working-with-srp.md#characteristics-of-srp-options) 每個的。

如需Oak microkernals的詳細資訊，請造訪 [建議的部署](../../help/sites-deploying/recommended-deploys.md).

### TarMK發佈伺服器陣列 {#tarmk-publish-farm}

當拓撲為發佈場時，相關重要主題為：

* [使用者同步](sync.md)
* [管理使用者和使用者群組](users.md)

### 建議：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 網站內容存放庫 | 用戶生成的CONTENTREPOSITORY | 儲存資源提供程式 | 公用商店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | MongoDB | MSRP | 是 |
| 任何 | JCR | Adobeon-demandstorage | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 網站內容存放庫 | 用戶生成的CONTENTREPOSITORY | 儲存資源提供程式 | 公用商店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK伺服器陣列（預設） | JCR | JCR | JSRP | 否 |
| Oak Cluster | JCR | JCR | JSRP | 僅發佈環境的選擇 |

## 開發 {#for-development}

針對非生產環境， [JSRP](jsrp.md) 使用一個製作例項和一個發佈例項來設定開發環境，簡單易用。

如果選擇 [ASRP](asrp.md), [DSRP](dsrp.md) 或 [MSRP](msrp.md) 在生產環境中，也可以使用Adobe按需儲存或MongoDB設定類似的開發環境。 如需範例，請參閱 [如何設定演示的MongoDB](demo-mongo.md).

## 引用 {#references}

* [使用者同步](sync.md)

   討論發佈伺服器陣列例項間使用者資料的同步化。

* [管理使用者和使用者群組](users.md)

   討論使用者和使用者群組在製作和發佈環境中的角色。

* UGC [公用商店](working-with-srp.md)

   說明社群內容與網站內容分開的儲存方式。

* [節點儲存和資料儲存](../../help/sites-deploying/data-store-config.md)

   基本上，網站內容儲存在節點儲存區中。 若為資產，可將資料存放區設定為儲存二進位資料。 針對Communities，必須設定共用商店以選取SRP。

* [儲存元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   描述兩個節點儲存實施：Tar和MongoDB。
