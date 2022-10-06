---
title: 儲存資源提供程式概述
seo-title: Storage Resource Provider Overview
description: Communities的通用儲存
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 0%

---

# 儲存資源提供程式概述 {#storage-resource-provider-overview}

## 簡介 {#introduction}

自AEM Communities 6.1起，社群內容(通常稱為使用者產生的內容(UGC))儲存在 [儲存資源提供程式](working-with-srp.md) (SRP)。

有數個SRP選項，所有選項都透過新的AEM Communities介面(即 [SocialResourceProvider API](srp-and-ugc.md) (SRP API)，包含所有建立、讀取、更新和刪除(CRUD)操作。

所有SCF元件均使用SRP API來實作，因此可在不了解 [基礎拓撲](topologies.md) 或UGC的位置。

***SocialResourceProvider API僅適用於AEM Communities的授權客戶。***

>[!NOTE]
>
>**自訂元件**:對於AEM Communities的授權客戶，自訂元件的開發人員可使用SRP API，以便不考慮基礎拓撲而存取UGC。 請參閱 [SRP和UGC要點](srp-and-ugc.md).

另請參閱:

* [SRP和UGC要點](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將棄用的公用程式方法對應至目前的SRP公用程式方法。

## 關於存放庫 {#about-the-repository}

若要了解SRP，了解AEM存放庫(OAK)在AEM社群網站中的角色會很有幫助。

**Java內容存放庫(JCR)**
此標準定義了資料模型和應用程式寫程式介面([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))（適用於內容存放庫）。 它將傳統檔案系統的特性與關係資料庫的特性相結合，並添加了內容應用程式經常需要的一些附加特性。

JCR的實作之一是AEM存放庫OAK。

**Apache Jackrabbit Oak(OAK)**
[OAK](../../help/sites-deploying/platform.md) 是JCR 2.0的實作，這是專門為以內容為中心的應用程式而設計的資料儲存系統。 它是一種針對非結構化和半結構化資料而設計的分層資料庫。 儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。 用於存取內容的UI為 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR和OAK通常用來指稱AEM存放庫。

在私人製作環境中開發網站內容後，必須複製到公開發佈環境。 這通常是透過 *[複製](deploy-communities.md#replication-agents-on-author)*. 這會在作者/開發人員/管理員控制下發生。

若為UGC，內容是由已註冊的網站訪客（社群成員）在公開發佈環境中輸入。 這是隨機發生的。

為了管理和報告之目的，從私人製作環境存取UGC很實用。 透過SRP，從作者存取UGC的方式更為一致，且效能也因為從發佈到作者的反向復寫並非必要。

## 關於SRP {#about-srp}

將UGC儲存至共用儲存時，會有單一成員內容例項，在大部分部署中，可從製作和發佈環境存取。 無論採用何種SRP(MSRP、ASRP、JSRP)，都必須採用SRP API以寫程式方式訪問。

>[!NOTE]
>
>請參閱 [SRP和UGC要點](srp-and-ugc.md) 以取得范常式式碼和其他詳細資訊。
>
>請參閱 [使用SRP存取UGC](accessing-ugc-with-srp.md) 以了解編碼時的最佳實務。

### ASRP {#asrp}

在ASRP的情況下，UGC不儲存在JCR中，它儲存在由Adobe托管和管理的雲服務中。 儲存在ASRP中的UGC不得以CRXDE Lite檢視，也不得使用JCR API存取。

請參閱 [ASRP -Adobe儲存資源提供程式](asrp.md).

開發人員無法直接存取UGC。

ASRP使用Adobe雲進行查詢。

### MSRP {#msrp}

若是MSRP,UGC不會儲存在JCR中，而會儲存在MongoDB中。 儲存在MSRP中的UGC不得以CRXDE Lite檢視，也不得使用JCR API存取。

請參閱 [MSRP - MongoDB儲存資源提供程式](msrp.md).

雖然MSRP可與ASRP比較，但由於所有AEM伺服器執行個體都在存取相同的UGC，因此可以使用通用工具直接存取儲存在MongoDB中的UGC。

MSRP使用Solr查詢。

### JSRP {#jsrp}

JSRP是存取單一AEM例項上所有UGC的預設提供者。 它提供快速體驗AEM Communities 6.1的功能，而無需設定MSRP或ASRP。

請參閱 [JSRP - JCR儲存資源提供商](jsrp.md).

若是JSRP，雖然UGC會儲存在JCR中，且可透過CRXDE Lite和JCR API存取，但強烈建議不要使用JCR API來存取，否則日後的變更可能會影響自訂程式碼。

此外，作者和發佈環境的存放庫也不會共用。 雖然發佈例項叢集會產生共用的發佈存放庫，但在發佈時輸入的UGC在作者上不會顯示，因此無法從作者管理UGC。 UGC只會保存在輸入執行個體的AEM存放庫(JCR)中。

JSRP會使用Oak索引進行查詢。

## 關於JCR中的陰影節點 {#about-shadow-nodes-in-jcr}

模擬UGC路徑的卷影節點存在於本機存放庫中，以提供兩種用途：

1. [訪問控制(ACL)](#for-access-control-acls)
1. [非現有資源(NER)](#for-non-existing-resources-ners)

無論是否實作SRP，實際UGC都*不會*顯示在與陰影節點相同的位置。

### 用於訪問控制(ACL) {#for-access-control-acls}

一些SRP實施，例如ASRP和MSRP，將社區內容儲存在不提供ACL驗證的資料庫中。 卷影節點在本地儲存庫中提供可應用ACL的位置。

所有SRP選項都使用SRP API，在所有CRUD操作之前對卷影位置執行相同的檢查。

ACL檢查使用實用程式方法，該方法返回適合於檢查應用於資源UGC的權限的路徑。

請參閱 [SRP和UGC要點](srp-and-ugc.md) 程式碼範例。

### 針對非現有資源 {#for-non-existing-resources-ners}

某些Communities元件可包含在指令碼中，因此需要Sling可定址節點來支援Communities功能。 [包含的元件](scf.md#add-or-include-a-communities-component) 稱為非現有資源。

卷影節點在存放庫中提供Sling可定址的位置。

>[!CAUTION]
>
>由於卷影節點具有多個用途，因此存在卷影節點就會 *not* 表示元件為NER。

### 儲存位置 {#storage-location}

以下是卷影節點的示例，使用 [註解元件](http://localhost:4502/content/community-components/en/comments.html) 在 [社群元件指南](components-guide.md):

* 元件存在於本機存放庫中：

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 相應的卷影節點存在於本地儲存庫中，位於：

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

在卷影節點下找不到UGC。

預設行為是每當讀取或寫入時參考相關子樹時，在發佈執行個體上設定卷影節點。

例如，假設部署為 [MSRP](msrp.md) 與TarMK發佈伺服器陣列。

當 [會員](users.md) 在pub1上發佈UGC（儲存在MongoDB中），在pub1上的JCR中建立影子節點。

第一次在pub2上讀取UGC時，如果未設定任何內容，預設行為是建立卷影節點。

如果需要預設行為以外的其他行為，則必須在製作例項上加以設定，並轉存至所有發佈例項，這通常是手動程式。
