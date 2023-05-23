---
title: 儲存資源提供程式概述
seo-title: Storage Resource Provider Overview
description: 社區的通用儲存
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

自AEM Communities6.1起，社區內容（通常稱為用戶生成內容）儲存在由 [儲存資源提供程式](working-with-srp.md) (SRP)。

有幾個SRP選項，所有選項都通過新的AEM Communities介面訪問UGC。 [SocialResourceProvider API](srp-and-ugc.md) (SRP API)，包括所有建立、讀取、更新和刪除(CRUD)操作。

所有SCF元件都使用SRP API實現，允許在不瞭解以下任一元件的情況下開發代碼 [基礎拓撲](topologies.md) 或UGC的位置。

***SocialResourceProvider API僅適用於AEM Communities的授權客戶。***

>[!NOTE]
>
>**自定義元件**:對於AEM Communities的許可客戶，SRP API可供定制元件的開發人員使用，以便訪問UGC而不考慮底層拓撲。 請參閱 [SRP和UGC軟體包](srp-and-ugc.md)。

另請參閱:

* [SRP和UGC軟體包](srp-and-ugc.md) - SRP實用程式方法和示例。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法。

## 關於儲存庫 {#about-the-repository}

要瞭解SRP，瞭解社區站點中儲存AEM庫(OAK)的作用AEM很有幫助。

**Java內容儲存庫(JCR)**
此標準定義了資料模型和應用程式寫程式介面([JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html))。 它將傳統檔案系統的特性與關係資料庫的特性相結合，並添加了內容應用程式經常需要的一些附加功能。

JCR的一個實現是AEMOAK。

**Apache Jackrabbit橡樹**
[橡樹](../../help/sites-deploying/platform.md) 是JCR 2.0的實現，它是專門為以內容為中心的應用程式設計的資料儲存系統。 它是一種針對非結構化和半結構化資料設計的分層資料庫。 儲存庫不僅儲存面向用戶的內容，還儲存應用程式使用的所有代碼、模板和內部資料。 用於訪問內容的UI是 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)。

JCR和OAK通常都用於指代儲存AEM庫。

在專用作者環境中開發網站內容後，必須將其複製到公共發佈環境。 這通常通過名為 *[複製](deploy-communities.md#replication-agents-on-author)*。 這種情況在作者/開發者/管理員的控制下發生。

對於UGC，內容由註冊站點訪問者（社區成員）在公共發佈環境中輸入。 這是隨機發生的。

為了管理和報告的目的，從私人作者環境訪問UGC非常有用。 使用SRP，作者對UGC的訪問更加一致，並且不需要從發佈到作者的反向複製。

## 關於SRP {#about-srp}

將UGC保存到共用儲存時，會有一個成員內容的單個實例，在大多數部署中，這些實例可以從作者和發佈環境訪問。 無論SRP選項(MSRP、ASRP、JSRP)如何，都必須通過SRP API以寫程式方式訪問。

>[!NOTE]
>
>請參閱 [SRP和UGC軟體包](srp-and-ugc.md) 示例代碼和其他詳細資訊。
>
>請參閱 [使用SRP訪問UGC](accessing-ugc-with-srp.md) 最佳編碼方法。

### ASRP {#asrp}

在ASRP的情況下，UGC不儲存在JCR中，而儲存在由Adobe托管和管理的雲服務中。 ASRP中儲存的UGC不能使用CRXDE Lite查看，也不能使用JCR API訪問。

請參閱 [ASRP -Adobe儲存資源提供程式](asrp.md)。

開發人員無法直接訪問UGC。

ASRP使用Adobe雲進行查詢。

### MSRP {#msrp}

在MSRP的情況下，UGC不儲存在JCR中，它儲存在MongoDB中。 儲存在MSRP中的UGC不能使用CRXDE Lite查看，也不能使用JCR API訪問。

請參閱 [MSRP - MongoDB儲存資源提供程式](msrp.md)。

雖然MSRP與ASRP相當，但是AEM由於所有伺服器實例都在訪問相同的UGC，因此可以使用通用工具直接訪問儲存在MongoDB中的UGC。

MSRP使用Solr進行查詢。

### JSRP {#jsrp}

JSRP是訪問單個實例上所有UGC的預設提AEM供程式。 它提供了快速體驗AEM Communities6.1的能力，而不需要建立管理系統更新項目或ASRP。

請參閱 [JSRP - JCR儲存資源提供程式](jsrp.md)。

在JSRP的情況下，雖然UGC儲存在JCR中，並且可通過CRXDE Lite和JCR API訪問，但強烈建議不要使用JCR API，否則將來的更改可能會影響自定義代碼。

此外，作者和發佈環境的儲存庫不是共用的。 雖然發佈實例集群會導致共用發佈儲存庫，但發佈時輸入的UGC在作者中不可見，因此無法從作者中管理UGC。 UGC僅保留在AEM其輸入實例的儲存庫(JCR)中。

JSRP使用Oak索引進行查詢。

## 關於JCR中的陰影節點 {#about-shadow-nodes-in-jcr}

模擬UGC路徑的卷影節點存在於本地儲存庫中，用於以下兩個目的：

1. [訪問控制(ACL)](#for-access-control-acls)
1. [非現有資源(NER)](#for-non-existing-resources-ners)

無論SRP實施如何，實際UGC都將*不會在與卷影節點相同的位置顯示。

### 用於訪問控制(ACL) {#for-access-control-acls}

某些SRP實現（如ASRP和MSRP）將社區內容儲存在不提供ACL驗證的資料庫中。 卷影節點提供本地儲存庫中可應用ACL的位置。

使用SRP API，所有SRP選項在執行所有CRUD操作之前都對卷影位置執行相同的檢查。

ACL檢查使用一種實用方法，該方法返回一條路徑，該路徑適合於檢查應用於資源UGC的權限。

請參閱 [SRP和UGC軟體包](srp-and-ugc.md) 示例代碼。

### 對於非現有資源(NER) {#for-non-existing-resources-ners}

某些社區元件可包含在指令碼中，因此需要Sling可定址節點來支援社區功能。 [包括的元件](scf.md#add-or-include-a-communities-component) 稱為非現有資源。

卷影節點在儲存庫中提供Sling可定址位置。

>[!CAUTION]
>
>由於卷影節點具有多種用途，因此存在卷影節點確實 *不* 表示元件是NER。

### 儲存位置 {#storage-location}

下面是陰影節點的示例，使用 [注釋元件](http://localhost:4502/content/community-components/en/comments.html) 的 [社區元件指南](components-guide.md):

* 該元件位於以下位置的本地儲存庫中：

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 相應的卷影節點位於以下位置的本地儲存庫中：

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

在卷影節點下找不到UGC。

預設行為是在引用相關子樹進行讀或寫時，在發佈實例上設定卷影節點。

例如，假設部署為 [MSRP](msrp.md) 與TarMK發佈伺服器場。

當 [成員](users.md) 在pub1上發佈UGC（儲存在MongoDB中），在pub1上的JCR中建立陰影節點。

首次在pub2上讀取UGC時，如果未設定任何設定，則預設行為是建立陰影節點。

如果需要除預設行為之外的其他行為，則必須在作者實例上設定它，並將其滾動到所有發佈實例，這通常是手動過程。
