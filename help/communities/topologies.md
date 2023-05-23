---
title: 推薦的社區拓撲
seo-title: Recommended Topologies for Communities
description: 如何處理用戶生成內容
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

# 推薦的社區拓撲 {#recommended-topologies-for-communities}

自AEM Communities6.1以來，已採用一種獨特的方法來處理網站訪問者（成員）從發佈環境提交的用戶生成內容。

此方法與平台處理通常從作AEM者環境管理的站點內容的方式有根本不同。

該平AEM台使用節點儲存，將站點內容從作者複製到發佈，而AEM Communities則使用一個從未複製的UGC通用儲存。

對於普通UGC儲存，必須選擇 [儲存資源提供程式(SRP)](working-with-srp.md)。 建議的選項包括：

* [DSRP — 關係資料庫儲存資源提供程式](dsrp.md)
* [MSRP - MongoDB儲存資源提供程式](msrp.md)
* [ASRP -Adobe儲存資源提供程式](asrp.md)

另一個SRP選項， [JSRP - JCR儲存資源提供程式](jsrp.md)，不支援作者的通用UGC儲存，也不支援對兩個訪問都發佈環境。

要求通用儲存將導致以下建議的拓撲。

>[!NOTE]
>
>對於AEM Communities, [UGC從未複製](working-with-srp.md#ugc-never-replicated)。
>
>當部署不包括 [普通商店](working-with-srp.md),UGC將僅在其輸入AEM的發佈或作者實例上可見。

>[!NOTE]
>
>有關平台的詳細信AEM息，請參見 [建議的部署](../../help/sites-deploying/recommended-deploys.md) 和 [平台簡AEM介](../../help/sites-deploying/data-store-config.md)。

## 用於生產 {#for-production}

為UGC建立公共儲存庫是必不可少的，因此基礎部署取決於其支援公共儲存庫的能力。

兩個示例：

1. 如果UGC的預期卷高且可能有本地MongoDB實例，則選擇 [MSRP](msrp.md)。

1. 為了獲得最佳的頁面內容效能， [發佈場](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) 和 [ASRP](asrp.md) 通過相對簡單的操作提供UGC的最佳擴展。

對於這兩種情況，部署可能基於任何OAK微內核。

要選擇適當的公用商店，請仔細考慮 [特徵](working-with-srp.md#characteristics-of-srp-options) 每一個。

有關Oak微核的詳細資訊，請訪問 [建議的部署](../../help/sites-deploying/recommended-deploys.md)。

### TarMK發佈場 {#tarmk-publish-farm}

當拓撲為發佈場時，相關重要主題為：

* [用戶同步](sync.md)
* [管理用戶和用戶組](users.md)

### 建議：DSRP、MSRP或ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | 站點內容儲存庫 | 用戶生成的內容儲存庫 | 儲存資源提供程式 | 公用儲存 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任何 | JCR | MySQL | DSRP | 是 |
| 任何 | JCR | 蒙戈DB | MSRP | 是 |
| 任何 | JCR | Adobe按需儲存 | ASRP | 是 |

### JSRP {#jsrp}


| 部署 | 站點內容儲存庫 | 用戶生成的內容儲存庫 | 儲存資源提供程式 | 公用儲存 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK場（預設） | JCR | JCR | JSRP | 否 |
| 橡樹座 | JCR | JCR | JSRP | 僅用於發佈環境 |

## 發展 {#for-development}

對於非生產環境， [JSRP](jsrp.md) 為使用一個作者實例和一個發佈實例來設定開發環境提供了簡便性。

如果選擇 [ASRP](asrp.md)。 [DSRP](dsrp.md) 或 [MSRP](msrp.md) 對於生產，還可以使用Adobe按需儲存或MongoDB來設定類似的開發環境。 有關示例，請參見 [如何設定MongoDB以進行演示](demo-mongo.md)。

## 引用 {#references}

* [用戶同步](sync.md)

   討論發佈場實例之間用戶資料的同步。

* [管理用戶和用戶組](users.md)

   討論用戶和用戶組在作者和發佈環境中的角色。

* UGC [普通商店](working-with-srp.md)

   描述獨立於站點內容的社區內容的儲存。

* [節點儲存和資料儲存](../../help/sites-deploying/data-store-config.md)

   基本上，站點內容被儲存在節點儲存中。 對於資產，可以將資料儲存配置為儲存二進位資料。 對於社區，必須配置公用儲存以選擇SRP。

* [儲存元素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   介紹兩種節點儲存實現：Tar和MongoDB
