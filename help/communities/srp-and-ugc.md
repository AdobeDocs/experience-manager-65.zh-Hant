---
title: SRP和UGC要點
seo-title: SRP and UGC Essentials
description: 儲存資源提供程式和用戶生成的內容概述
seo-description: Storage resource provider and user-generated content overview
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# SRP和UGC要點 {#srp-and-ugc-essentials}

## 簡介 {#introduction}

若不熟悉儲存資源提供者(SRP)及其與使用者產生的內容(UGC)的關係，請造訪 [社群內容儲存](working-with-srp.md) 和 [儲存資源提供程式概述](srp.md).

本檔案的本節提供關於SRP和UGC的一些基本資訊。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)是各種Sling資源提供者API的擴充功能。 其中包括分頁和原子增量支援（對計分和計分很有用）。

SCF元件需要查詢，因為需要按日期、幫助性、投票數等進行排序。 所有SRP選項都具有不依賴分段的彈性查詢機制。

SRP儲存位置併入元件路徑。 SRP API應一律用於存取UGC，因為根路徑取決於所選SRP選項，例如ASRP、MSRP或JSRP。

SRP API不是抽象類，而是介面。 自訂實作不應輕率進行，因為升級至新版本時，將會遺漏未來改善內部實作的優點。

使用SRP API的方法是透過提供的公用程式，例如SocialResourceUtilities套件中的公用程式。

從AEM 6.0或更舊版本升級時，必須移轉所有可使用開放原始碼工具的SRP的UGC。 請參閱 [升級至AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>過去，用於存取UGC的公用程式會顯示在SocialUtils套件中，但該套件已不存在。
>
>有關替換實用程式，請參閱 [SocialUtils重構](socialutils.md).

## 訪問UGC的實用方法 {#utility-method-to-access-ugc}

若要存取UGC，請使用SocialResourceUtilities套件中的方法，此方法會傳回適合從SRP存取UGC的路徑，並取代SocialUtils套件中已棄用的方法。

以下是在servlet中使用resourceToUGCStoragePath()方法的最小範例：

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String ugcPath = socialResourceUtilities.resourceToUGCStoragePath(request.getResource());
  // rest of servlet
}
```

有關其他SocialUtils替換項，請參見 [SocialUtils重構](socialutils.md).

如需編碼准則，請造訪 [使用SRP存取UGC](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>返回的路徑resourceToUGCStoragePath()為 *not* 適合 [ACL檢查](srp.md#for-access-control-acls).

## 訪問ACL的實用方法 {#utility-method-to-access-acls}

一些SRP實施，例如ASRP和MSRP，將社區內容儲存在不提供ACL驗證的資料庫中。 卷影節點在本地儲存庫中提供可應用ACL的位置。

所有SRP選項都使用SRP API，在所有CRUD操作之前對卷影位置執行相同的檢查。

若要檢查ACL，請使用傳回適合檢查套用至資源UGC之權限的路徑的方法。

以下是在servlet中使用resourceToACLPath()方法的簡單範例：

```java
import com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities;

@Reference
private SocialResourceUtilities socialResourceUtilities;

@Override
protected void doGet(final SlingHttpServletRequest request, final SlingHttpServletResponse response) throws ServletException, IOException {
  String aclPath = socialResourceUtilities.resourceToACLPath(request.getResource());
  // rest of servlet
}
```

>[!CAUTION]
>
>resourceToACLPath()返回的路徑是 *not* 適合 [訪問UGC](#utility-method-to-access-acls) 本身。

## 與UGC相關的儲存位置 {#ugc-related-storage-locations}

使用JSRP或MSRP開發時，下列儲存位置說明可能有所幫助。 目前沒有UI可存取儲存在ASRP中的UGC，因為JSRP([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))和MSRP（MongoDB工具）。

**元件位置**

當成員在發佈環境中輸入UGC時，他們會與AEM網站中的元件互動。

此類元件的範例為 [註解元件](http://localhost:4502/content/community-components/en/comments.html) 存在於 [社群元件指南](components-guide.md) 頁簽。 本地儲存庫中注釋節點的路徑是：

* 元件路徑= `/content/community-components/en/comments/jcr:content/content/includable/comments`

**卷影節點位置**

UGC的建立也會建立 [陰影節點](srp.md#about-shadow-nodes-in-jcr) ACL的ACL。 指向本地儲存庫中相應卷影節點的路徑是將卷影節點根路徑前置到元件路徑的結果：

* 根路徑 = `/content/usergenerated`
* 注釋卷影節點= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC位置**

UGC不會在這些位置中建立，且只應使用 [公用方法](#utility-method-to-access-ugc) 調用SRP API。

* 根路徑 = `/content/usergenerated/asi/srp-choice`
* JSRP的UGC節點= `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意*，對於JSRP,UGC節點將 *僅限* 存在於輸入的AEM例項（製作或發佈）上。 如果在發佈例項上輸入，則無法從作者上的協調控制台進行協調。

## 相關資訊 {#related-information}

* [儲存資源提供程式概述](srp.md)  — 簡介和存放庫使用概觀。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將棄用的公用程式方法對應至目前的SRP公用程式方法。
