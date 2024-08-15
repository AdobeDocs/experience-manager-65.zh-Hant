---
title: 建議的部署
description: 本文說明AEM的建議拓撲。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 0%

---

# 建議的部署{#recommended-deployments}

>[!NOTE]
>
>本頁介紹AEM的建議拓撲。 如需叢集功能以及如何設定它們的詳細資訊，請參閱[Apache Sling Discovery API檔案](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html)。

從AEM 6.2開始，MicroKernels會充當持續性管理員。選擇符合您需求的部署型別，取決於執行個體的用途以及您考慮的部署型別。

以下範例旨在指出最常見的AEM設定中，建議使用哪些功能。

## 部署案例 {#deployment-scenarios}

### 單一TarMK執行個體 {#single-tarmk-instance}

在此案例中，單一TarMK執行個體在單一伺服器上執行。

**這是作者執行個體的預設部署。**

![chlimage_1-15](assets/chlimage_1-15.png)

優點：

* 簡單
* 輕鬆維護
* 效能優異

缺點：

* 無法擴充到超出伺服器容量的限制
* 沒有容錯移轉容量

### TarMK冷待命 {#tarmk-cold-standby}

一個TarMK執行個體作為主要執行個體。 主要存放庫會複製到待命容錯移轉系統。

冷待命機制也可用作備份，因為完整存放庫會持續複製到容錯移轉伺服器。 容錯移轉伺服器正在冷待命模式下執行，這表示只有執行個體的HttpReceiver在執行。

![chlimage_1-16](assets/chlimage_1-16.png)

優點：

* 簡單性
* 可維護性
* 效能
* 容錯移轉

缺點：

* 無法擴充至超出伺服器容量的限制
* 一部伺服器大部分時間處於閒置狀態
* 容錯移轉不是自動的。 必須先在外部偵測到它，容錯移轉系統才能開始處理要求。

>[!NOTE]
>
>如需有關如何設定AEM與TarMK冷待命的詳細資訊，請參閱[此](/help/sites-deploying/tarmk-cold-standby.md)文章。

>[!NOTE]
>
>這個TarMK範例中的「冷待命」部署要求主要執行個體和待命執行個體必須分別授權，因為容錯移轉伺服器會持續進行復寫。 如需有關授權的詳細資訊，請參閱[Adobe一般授權條款](https://www.adobe.com/legal/terms/enterprise-licensing.html)。

### TarMK陣列 {#tarmk-farm}

多個Oak執行個體使用一個TarMK執行個體來執行。 TarMK存放庫是獨立的，需要保持同步。

由於製作伺服器會向每個伺服器陣列成員發佈相同的內容，因此可以保持存放庫同步。 如需詳細資訊，請參閱[復寫](/help/sites-deploying/replication.md)。

對於AEM Communities，絕不會復寫使用者產生的內容(UGC)。 如需在TarMK伺服器陣列上支援UGC，請參閱AEM Communities的[考量事項](#considerations-for-aem-communities)。

**這是發佈環境的預設部署。**

![chlimage_1-17](assets/chlimage_1-17.png)

優點：

* 效能
* 讀取存取的擴充性
* 容錯移轉

### Oak叢集搭配MongoMK容錯移轉，可在單一資料中心提供高可用性 {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

此方法表示多個Oak執行個體存取單一資料中心內的MongoDB復本集，實際上就是為AEM製作環境建立主動 — 主動叢集。 MongoDB中的復本集可用於在硬體或網路故障時提供高可用性和備援。

![chlimage_1-18](assets/chlimage_1-18.png)

優點：

* 能夠使用新的AEM編寫執行個體水平縮放
* 資料層的高可用性、備援，以及自動容錯移轉

缺點：

* 在某些情況下，效能可能會低於使用TarMK

### 在多個資料中心間執行MongoMK容錯移轉的Oak叢集 {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

此方法表示多個Oak執行個體可跨多個資料中心存取MongoDB復本集，實際為AEM製作環境建立主動 — 主動叢集。 MongoDB復寫功能擁有多個資料中心，可提供相同的高可用性和備援能力，但現已具備處理資料中心中斷的能力。

![oakclustermongofailover2資料中心](assets/oakclustermongofailover2datacenters.png)

優點：

* 能夠使用新的AEM編寫執行個體水平縮放
* 資料層的高可用性、備援，以及自動容錯移轉（包括資料中心中斷）

>[!NOTE]
>
>在上圖中，假設資料中心2的AEM伺服器與資料中心1的MongoDB主要節點之間的網路延遲，高於[具有MongoDB — 檢查清單](/help/sites-deploying/aem-with-mongodb.md#checklists)的Adobe Experience Manager下記錄的要求，AEM Server 3和AEM Server 4會顯示非使用中狀態。 如果最大延遲與需求相容（例如透過使用可用性區域），則資料中心2中的AEM伺服器也可以作用中，以建立跨多個資料中心作用中的AEM叢集。

>[!NOTE]
>
>如需本節中說明的MongoDB架構概念的其他資訊，請參閱[MongoDB復寫](https://docs.mongodb.org/manual/replication/)。

## 微核心：要使用哪一個 {#microkernels-which-one-to-use}

在兩個可用的微核心之間進行選擇時，需要考慮的基本規則是，TarMK是針對效能而設計，而MongoMK則是針對擴充能力而設計。

您可以使用這些決策矩陣來建立適合您需求的最佳部署型別。

Adobe強烈建議TarMK作為客戶在所有部署案例(AEM Author和Publish例項除外)中使用的預設持續性技術。

### 在製作執行個體上選擇AEM MongoMK而非TarMK的例外情況 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

選擇MongoMK持續性後端而非TarMK的主要原因是要水平縮放執行個體。 這表示需隨時執行兩個或多個作用中的製作執行個體，並使用MongoDB作為持續性儲存系統。 通常需要執行多個製作執行個體，是因為單一伺服器的CPU和記憶體容量（支援所有並行製作活動）已無法持續。

預測新網站上線後的確切並行模式幾乎是不可能的。 因此，Adobe建議您在評估是否使用MongoMK和兩個或更多作者活動節點時，考慮以下標準：

1. 一天內連線的已命名使用者數：以千或以上為單位。
1. 同時使用者人數：以數百或以上的數量計算。
1. 每日資產擷取量：數十萬或以上。
1. 每日頁面編輯量：數十萬或更多（例如透過多網站管理員或新聞摘要擷取進行的自動更新）。
1. 每天的搜尋量：以萬或更多。

>[!NOTE]
>
>[嚴苛日](/help/sites-developing/tough-day.md)可用來評估客戶應用程式在已部署硬體組態內容中的效能。

使用MongoDB的最低部署通常涉及以下拓撲：

* MongoDB復本集包含一個主要節點、兩個次要節點，每個MongoDB執行個體都在可用性區域中執行，每個節點的延遲時間不到15毫秒；
* 一個製作執行個體叢集，具有一個導線節點、一個非導線節點且兩者皆隨時啟動，每個製作執行個體都在每個資料中心中執行，其中主要和次要執行個體都在執行。

此外，強烈建議您在共用檔案系統或Amazon S3上設定資料存放區，好讓資產或二進位檔不會儲存在MongoDB中。 這將確保部署內的最佳效能。

部署具有兩個或多個製作執行個體叢集的MongoDB復本集的額外優點之一，就是如果製作執行個體、MongoDB復本或資料中心完全失敗，便能以最小的停機時間自動復原案例。 儘管如此，選擇MongoMK而非TarMK不應完全由復原需求所驅動，因為TarMK也可以提供具備受控容錯移轉機制的最小停機時間解決方案。

如果在部署的前18個月中不符合上述標準，建議先使用TarMK部署AEM，稍後當上述標準適用時，再重新評估您的設定，最後決定是否留在TarMK上或移轉至MongoMK。

### 在Publish執行個體上選擇AEM MongoMK而非TarMK的例外情況 {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

不建議為發佈執行個體部署MongoMK。 部署的發佈層級幾乎總是部署為執行TarMK的完全獨立發佈執行個體的陣列，透過從製作執行個體複製內容來保持同步。 這種「不共用」的架構適用於發佈執行個體，可讓發佈層的部署以線性方式水準擴展。 陣列拓撲還提供以滾動方式套用任何更新或升級至發佈執行個體的優點，因此對發佈層級的任何變更不需要任何停機時間。

當有多個發佈者時，這不適用於在發佈層上使用叢集的AEM Communities。 若選擇JSRP （請參閱[社群內容儲存體](/help/communities/working-with-srp.md)），則MongoMK叢集會很合適，不論選擇哪個MK （例如MongoDB或RDB），任何發佈端叢集都一樣。

### 使用MongoMK部署AEM時的先決條件和Recommendations {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

如果您考慮使用AEM的MongoMK部署，有一組必要條件和建議可供使用：

**MongoDB部署的必要先決條件：**

1. 在熟悉AEM的Adobe Consulting或MongoDB架構師的協助下，MongoDB部署架構和規模調整必須是專案實作的一部分；
1. 合作夥伴或客戶團隊必須具備MongoDB專業知識，才能有信心維持及維護現有或新的MongoDB環境；
1. 您可以選擇部署商業或開放原始碼版本的MongoDB (AEM同時支援兩者)，但必須直接從MongoDB Inc購買MongoDB維護和支援合約；
1. 整體AEM和MongoDB架構和基礎架構應由AdobeAEM架構師妥善定義和驗證；
1. 檢閱包含MongoDB的AEM部署的支援模型。

**MongoDB部署的Strong建議：**

* 請參閱Adobe Experience Manager的[MongoDB部署檢閱](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)；
* 檢閱[MongoDB作業檢查清單](https://docs.mongodb.org/manual/administration/production-checklist/)；
* 參加MongoDB上的[認證課程 — 可在](https://university.mongodb.com/)線上取得。

>[!NOTE]
>
>如需這些准則、先決條件和建議的所有其他問題，請連絡[Adobe客戶服務](https://helpx.adobe.com/tw/marketing-cloud/contact-support.html)。

### AEM Communities的考量事項 {#considerations-for-aem-communities}

針對計畫部署[AEM Communities](/help/communities/overview.md)的網站，建議[選擇針對處理社群成員從發佈環境張貼的UGC而最佳化的部署](/help/communities/working-with-srp.md#characteristicsofstorageoptions)。

使用[通用存放區](/help/communities/working-with-srp.md)，就不需要在作者與其他發佈執行個體之間復寫UGC，即可取得UGC的一致檢視。

以下是一組決策矩陣，可協助您為部署選擇最佳型別的持續性：

#### 選擇作者執行個體的部署型別 {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### 選擇發佈執行個體的部署型別 {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB是協力廠商軟體，不包含在AEM授權套件中。 如需詳細資訊，請參閱[MongoDB授權原則](https://www.mongodb.org/about/licensing/)頁面。
>
>為了充分利用AEM部署，Adobe建議授權MongoDB企業版，以享受專業支援。
>
>此授權包含標準復本集，該標準復本集由一個主要和兩個次要執行個體組成，可用於製作或發佈部署。
>
>如果您想要在MongoDB上同時執行author和publish，則需要購買兩個不同的授權。
>
>如需詳細資訊，請參閱[適用於Adobe Experience Manager的MongoDB頁面](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)。
