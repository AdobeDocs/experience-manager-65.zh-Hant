---
title: 儲存資源提供者概觀
description: 瞭解社群內容(稱為使用者產生的內容(UGC))如何儲存在儲存資源提供者(SRP)提供的簡單通用存放區中。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 0%

---

# 儲存資源提供者概觀 {#storage-resource-provider-overview}

## 簡介 {#introduction}

截至Adobe Experience Manager (AEM) Communities 6.1，社群內容(通常稱為使用者產生的內容(UGC))儲存在[儲存資源提供者](working-with-srp.md) (SRP)提供的單一共用存放區中。

有數個SRP選項，所有選項都可透過新的AEM Communities介面[SocialResourceProvider API](srp-and-ugc.md) (SRP API)存取UGC，該API包括所有建立、讀取、更新和刪除(CRUD)作業。

所有SCF元件都是使用SRP API實作，允許程式碼不需要知道[基礎拓撲](topologies.md)或UGC位置即可開發。

***SocialResourceProvider API僅適用於AEM Communities的授權客戶。***

>[!NOTE]
>
>**自訂元件**：對於AEM Communities的授權客戶，自訂元件的開發人員可以使用SRP API來存取UGC，而不考慮基礎拓撲。 請參閱[SRP和UGC Essentials](srp-and-ugc.md)。

另請參閱：

* [SRP與UGC Essentials](srp-and-ugc.md) - SRP公用程式方法與範例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md) — 編碼准則。
* [SocialUtils重構](socialutils.md) — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。

## 關於存放庫 {#about-the-repository}

若要瞭解SRP，瞭解AEM社群網站中AEM存放庫(Oak)的角色會很有幫助。

**Java™內容存放庫(JCR)**
此標準定義了內容存放庫的資料模型和應用程式設計介面([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))。 它結合了傳統檔案系統與關聯式資料庫的特性，並新增了內容應用程式經常需要的幾項額外功能。

JCR的一個實作是AEM存放庫Oak。

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md)是JCR 2.0的實作，這是專為以內容為中心的應用程式而設計的資料儲存系統。 這是一種階層式資料庫，專為非結構化和半結構化資料而設計。 存放庫不僅儲存面向使用者的內容，也儲存應用程式使用的所有程式碼、範本和內部資料。 用於存取內容的UI是[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。

JCR和Oak通常用於表示AEM存放庫。

在私人製作環境中開發網站內容後，必須將其複製到公開發佈環境。 這項作業通常透過名為&#x200B;*[復寫](deploy-communities.md#replication-agents-on-author)*&#x200B;的作業來完成。 這會發生在作者/開發人員/管理員的控制下。

若為UGC，內容由公開發佈環境中的註冊網站訪客（社群成員）輸入。 這是隨機發生的。

為了管理和報告，從私人製作環境存取UGC會很有用。 使用SRP時，由於不需要從Publish反向復寫至作者，因此從「作者」存取UGC會更加一致且效能更高。

## 關於SRP {#about-srp}

UGC儲存至共用儲存空間時，在大部分部署中，成員內容的單一例項可同時從製作和發佈環境存取。 無論SRP選擇為何(MSRP、ASRP、JSRP)，所有必須透過SRP API以程式設計方式存取。

>[!NOTE]
>
>如需範常式式碼和其他詳細資訊，請參閱[SRP和UGC Essentials](srp-and-ugc.md)。
>
>請參閱[使用SRP](accessing-ugc-with-srp.md)存取UGC，以瞭解編碼時的最佳作法。

### ASRP {#asrp}

如果有ASRP，UGC就不會儲存在JCR中，而是儲存在由Adobe託管和管理的雲端服務中。 ASRP中儲存的UGC不可使用CRXDE Lite檢視或使用JCR API存取。

請參閱[ASRP -Adobe儲存資源提供者](asrp.md)。

開發人員無法直接存取UGC。

ASRP使用Adobe雲端進行查詢。

### MSRP {#msrp}

如果有，MSRP、UGC就不會儲存在JCR中，而是儲存在MongoDB中。 儲存在MSRP中的UGC不可以CRXDE Lite檢視或使用JCR API存取。

請參閱[MSRP - MongoDB儲存資源提供者](msrp.md)。

雖然MSRP可與ASRP相提並論，因為所有AEM伺服器執行個體都存取相同的UGC，所以您可以使用通用工具直接存取儲存在MongoDB中的UGC。

MSRP使用Solr進行查詢。

### JSRP {#jsrp}

JSRP為存取單一AEM執行個體上所有UGC的預設提供者。 它可讓您快速體驗AEM Communities 6.1，而不需要設定MSRP或ASRP。

請參閱[JSRP - JCR儲存資源提供者](jsrp.md)。

如果UGC儲存在JCR時存在JSRP，並且可在CRXDE Lite和JCR API中存取，Adobe建議您永遠不要使用JCR API來存取。 如果您這麼做，未來的變更可能會影響自訂程式碼。

此外，不會共用作者和Publish環境的存放庫。 雖然發佈執行個體的叢集會產生共用發佈存放庫，但在Publish中輸入的UGC在Author上不可見，因此無法管理Author的UGC。 UGC只會保留在輸入其所在例項的AEM存放庫(JCR)中。

JSRP會使用Oak索引進行查詢。

## 關於JCR中的陰影節點 {#about-shadow-nodes-in-jcr}

模擬指向UGC的路徑的陰影節點存在於本機存放庫中，以實現兩個目的：

1. [存取控制(ACL)](#for-access-control-acls)
1. [非現有資源(NER)](#for-non-existing-resources-ners)

不論SRP實作為何，實際UGC在與陰影節點相同的位置上是&#x200B;*not*。

### 針對存取控制(ACL) {#for-access-control-acls}

有些SRP實作（例如ASRP和MSRP）會將社群內容儲存在未提供ACL驗證的資料庫中。 陰影節點會提供本機存放庫中ACL可套用的位置。

使用SRP API時，所有SRP選項都會在所有CRUD作業之前，對陰影位置執行相同的檢查。

ACL檢查會使用公用程式方法，傳回適合檢查套用至資源UGC之許可權的路徑。

如需範常式式碼，請參閱[SRP和UGC Essentials](srp-and-ugc.md)。

### 針對非現有資源(NER) {#for-non-existing-resources-ners}

部分Communities元件不可包含在指令碼中，因此需要Sling可定址節點來支援Communities功能。 [包含的元件](scf.md#add-or-include-a-communities-component)稱為非現有資源(NER)。

陰影節點會在存放庫中提供Sling可定址位置。

>[!CAUTION]
>
>由於陰影節點有多重使用，陰影節點的存在&#x200B;*不*&#x200B;表示該元件是NER。

### 儲存位置 {#storage-location}

以下是陰影節點的範例，使用[社群元件指南](components-guide.md)中的[註解元件](http://localhost:4502/content/community-components/en/comments.html)：

* 元件存在於本機存放庫中：

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 對應的陰影節點存在於本機存放庫中：

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

在陰影節點下找不到UGC。

預設行為是在參考相關子樹狀結構以進行讀取或寫入時，在發佈執行個體上設定陰影節點。

例如，假設部署是具有TarMK發佈伺服器陣列的[MSRP](msrp.md)。

當[成員](users.md)在pub1上發佈UGC （儲存在MongoDB中）時，陰影節點會在pub1上的JCR中建立。

在pub2上第一次讀取UGC時，如果未設定任何專案，預設行為是建立陰影節點。

如果需要預設行為以外的其他行為，則必須在製作執行個體上設定該行為，並將其轉存到所有發佈執行個體，這通常是手動流程。
