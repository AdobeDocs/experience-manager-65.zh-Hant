---
title: 儲存資源提供方概述
seo-title: 儲存資源提供方概述
description: 社群的通用儲存空間
seo-description: 社群的通用儲存空間
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 儲存資源提供方概述 {#storage-resource-provider-overview}

## 簡介 {#introduction}

自AEM Communities 6.1起，社群內容(通常稱為使用者產生的內容(UGC))會儲存在儲存資源提供者 [](working-with-srp.md) (SRP)提供的單一共用商店中。

有數個SRP選項，所有選項都可透過新的AEM Communities介面 [SocialResourceProvider API](srp-and-ugc.md) (SRP API)存取UGC，其中包含所有建立、讀取、更新和刪除(CRUD)作業。

所有SCF元件都使用SRP API實現，允許在不瞭解UGC的底層拓撲或 [位置](topologies.md) 的情況下開發代碼。

***SocialResourceProvider API僅適用於AEM Communities的授權客戶。***

>[!NOTE]
>
>**自訂元件**:對於AEM Communities的授權客戶，SRP API可供自訂元件的開發人員使用，以便存取UGC，而不考慮基礎的拓撲。 請參 [閱SRP和UGC Essentials](srp-and-ugc.md)。

另請參閱:

* [SRP和UGC Essentials](srp-and-ugc.md) - SRP實用程式方法和示例
* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 編碼准則
* [SocialUtils重構](socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法

## 關於儲存庫 {#about-the-repository}

若要瞭解SRP，請務必瞭解AEM社群網站中AEM存放庫(OAK)的角色。

**Java Content Repository(JCR)此標**&#x200B;準為內容儲存庫定義資料模型和應用程[式設計介面(JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))。 它結合了傳統檔案系統和關係資料庫的特性，並添加了內容應用程式經常需要的一些附加功能。

JCR的一個實作是AEM存放庫OAK。

**Apache Jackrabbit Oak(OAK)**[OAK](../../help/sites-deploying/platform.md) 是JCR 2.0的實作，此資料儲存系統是專為內容導向應用程式而設計的。 它是一種面向非結構化和半結構化資料的分層資料庫。 儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。 存取內容的UI是 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。

JCR和OAK通常都用來參照AEM存放庫。

在私人作者環境中開發網站內容後，必須複製至公開發佈環境。 這通常通過稱為複製的操作 *[完成](deploy-communities.md#replication-agents-on-author)*。 這會在作者／開發人員／管理員的控制下發生。

對於UGC，內容是由註冊網站訪客（社群成員）在公開發佈環境中輸入的。 這是隨機發生的。

為了管理和報告，從私人作者環境存取UGC非常實用。 使用SRP，作者對UGC的存取更加一致，而且不需要執行從發佈到作者的反向複製。

## 關於SRP {#about-srp}

將UGC儲存至共用儲存時，會有單一成員內容例項，在大部分的部署中，這些例項可同時從作者和發佈環境存取。 不論SRP選擇(MSRP、ASRP、JSRP)為何，都必須使用SRP API以程式方式存取。

>[!NOTE]
>
>如需 [范常式式碼和其他詳細資訊，請參閱SRP](srp-and-ugc.md) 和UGC Essentials。
>
>請參 [閱使用SRP存取UGC](accessing-ugc-with-srp.md) ，以取得編碼時的最佳實務。

### ASRP {#asrp}

如果是ASRP,UGC不會儲存在JCR中，而會儲存在Adobe代管和管理的雲端服務中。 儲存在ASRP中的UGC不得使用CRXDE Lite檢視，也不得使用JCR API存取。

請參 [閱ASRP - Adobe儲存資源提供者](asrp.md)。

開發人員無法直接存取UGC。

ASRP使用Adobe雲端進行查詢。

### MSRP {#msrp}

在MSRP中，UGC不儲存在JCR中，它儲存在MongoDB中。 儲存在MSRP中的UGC不得使用CRXDE Lite檢視，也不得使用JCR API存取。

請參 [閱MSRP - MongoDB儲存資源提供程式](msrp.md)。

雖然MSRP可與ASRP相比，但是由於所有AEM伺服器例項都在存取相同的UGC，因此可使用常用工具直接存取儲存在MongoDB中的UGC。

MSRP使用Solr進行查詢。

### JSRP {#jsrp}

JSRP是用來存取單一AEM例項上所有UGC的預設提供者。 它提供快速體驗AEM Communities 6.1的功能，而不需設定MSRP或ASRP。

請參 [閱JSRP - JCR儲存資源提供程式](jsrp.md)。

在JSRP的情況下，雖然UGC儲存在JCR中，並可透過CRXDE Lite和JCR API存取，但強烈建議不要使用JCR API，否則未來的變更可能會影響自訂程式碼。

此外，作者和發佈環境的儲存庫不共用。 雖然發佈例項叢集會產生共用發佈儲存庫，但發佈時輸入的UGC在作者上不可見，因此無法從作者管理UGC。 UGC僅會持續存在於輸入UGC的例項的AEM儲存庫(JCR)中。

JSRP使用Oak索引查詢。

## 關於JCR中的陰影節點 {#about-shadow-nodes-in-jcr}

模仿UGC路徑的卷影節點存在於本地儲存庫中，以提供兩種用途：

1. [訪問控制(ACL](#for-access-control-acls))
1. [非現有資源(NER)](#for-non-existing-resources-ners)

無論SRP實作如何，實際的UGC將*not *在與陰影節點相同的位置顯示。

### 針對訪問控制(ACL) {#for-access-control-acls}

某些SRP實施（如ASRP和MSRP）將社區內容儲存在不提供ACL驗證的資料庫中。 卷影節點在本地儲存庫中提供可應用ACL的位置。

使用SRP API，所有SRP選項在所有CRUD操作之前對陰影位置執行相同的檢查。

ACL檢查使用一種實用程式方法，該方法返回適合於檢查應用於資源UGC的權限的路徑。

如需 [范常式式碼，請參閱SRP](srp-and-ugc.md) 和UGC Essentials。

### 針對非現有資源(NER) {#for-non-existing-resources-ners}

有些Communities元件可包含在指令碼中，因此需要Sling可定址節點來支援Communities功能。 [包含的元件](scf.md#add-or-include-a-communities-component) ，稱為非現有資源(NER)。

卷影節點在儲存庫中提供Sling可定址位置。

>[!CAUTION]
>
>由於陰影節點有多種用途，因此存在陰影節 *點並不* 表示元件是NER。

### 儲存位置 {#storage-location}

以下是使用「社區元件指南」中的「注 [釋](http://localhost:4502/content/community-components/en/comments.html) 」元件 [的陰影節點示例](components-guide.md):

* 元件存在於本地儲存庫中：

   /content/community-components/tw/comments/jcr:content/content/include/comments

* 相應的卷影節點存在於本地儲存庫中，位於：

   /content/usergenerated/content/community-components/tw/comments/jcr:content/content/include/comments

在陰影節點下找不到UGC。

預設行為是在讀或寫引用相關子樹時，在發佈實例上設定卷影節點。

例如，假設部署是 [MSRP](msrp.md) ，並有TarMK發佈場。

當成 [員在pub1上](users.md) （儲存在MongoDB中）發佈UGC時，會在pub1的JCR中建立陰影節點。

第一次在pub2上讀取UGC時，如果未設定任何內容，預設行為是建立陰影節點。

如果需要除預設行為以外的其他行為，則必須在作者例項上設定，並轉存至所有發佈例項，這通常是手動程式。
