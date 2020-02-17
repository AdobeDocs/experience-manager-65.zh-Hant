---
title: SRP和UGC Essentials
seo-title: SRP和UGC Essentials
description: 儲存資源提供商和用戶生成的內容概述
seo-description: 儲存資源提供商和用戶生成的內容概述
uuid: a4ee8725-f554-4fcf-ac1e-34878d6c02f8
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0763f236-5648-49e9-8a24-dbc8f4c77ee3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# SRP和UGC Essentials {#srp-and-ugc-essentials}

## 簡介 {#introduction}

如果不熟悉儲存資源提供商(SRP)及其與用戶生成內容(UGC)的關係，請訪問 [社區內容儲存](working-with-srp.md)[和儲存資源提供商概述](srp.md)。

本文檔的這一部分提供了有關SRP和UGC的一些基本資訊。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)是各種Sling Resource Provider API的擴充功能。 它包含分頁和原子增量支援（對計分和計分很有用）。

SCF元件需要查詢，因為需要按日期、幫助、票數等進行排序。 所有SRP選項都具有不依賴分組的靈活查詢機制。

SRP儲存位置併入了元件路徑。 SRP API應一律用於存取UGC，因為根路徑取決於所選SRP選項，例如ASRP、MSRP或JSRP。

SRP API不是抽象類，它是介面。 自訂實作不應輕易進行，因為升級至新版本時，將來對內部實作的改善會錯失良機。

使用SRP API的方式是透過提供的公用程式，例如SocialResourceUtilities套件中的公用程式。

從AEM 6.0或更舊版本升級時，必須移轉所有SRP的UGC，而Open Source工具可供使用。 請參 [閱「升級至AEM Communities 6.3」](upgrade.md)。

>[!NOTE]
>
>過去，SocialUtils套件中會找到用於存取UGC的公用程式，而SocialUtils套件已不再存在。
>
>如需取代公用程式，請參 [閱SocialUtils重構](socialutils.md)。

## 訪問UGC的實用方法 {#utility-method-to-access-ugc}

若要存取UGC，請使用SocialResourceUtilities套件中的方法，傳回適合從SRP存取UGC的路徑，並取代SocialUtils套件中找到的已過時方法。

以下是在servlet中使用resourceToUGCStoragePath()方法的最小示例：

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

如需其他SocialUtils替代項目，請參 [閱SocialUtils重構](socialutils.md)。

如需編碼准則，請造 [訪使用SRP存取UGC](accessing-ugc-with-srp.md)。

>[!CAUTION]
>
>傳回的路徑resourceToUGCStoragePath()是*not *不適合 [ACL檢查](srp.md#for-access-control-acls)。

## 訪問ACL的實用方法 {#utility-method-to-access-acls}

某些SRP實施（如ASRP和MSRP）將社區內容儲存在不提供ACL驗證的資料庫中。 卷影節點在本地儲存庫中提供可應用ACL的位置。

使用SRP API，所有SRP選項在所有CRUD操作之前對陰影位置執行相同的檢查。

要檢查ACL，請使用返回適合於檢查應用於資源UGC的權限的路徑的方法。

以下是在servlet中使用resourceToACLPath()方法的簡單示例：

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
>resourceToACLPath()傳回的路徑是*not *不適 [合存取UGC](#utility-method-to-access-acls) 。

## 與UGC相關的儲存位置 {#ugc-related-storage-locations}

以下儲存位置說明在使用JSRP或MSRP進行開發時可能會有幫助。 目前沒有UI可存取儲存在ASRP中的UGC，因為JSRP([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))和MSRP（MongoDB工具）。

**元件位置**

當成員在發佈環境中輸入UGC時，他們會與AEM網站的元件互動。

此類元件的示例是存在 [於「社群元件指南](http://localhost:4502/content/community-components/en/comments.html) 」站點 [中的注釋元件](components-guide.md) 。 本地儲存庫中注釋節點的路徑為：

* 元件路徑= */content/community-components/en/comments/jcr:content/content/include/comments*

**陰影節點位置**

建立UGC還會建立 [一個影子節點](srp.md#about-shadow-nodes-in-jcr) ，以便應用必要的ACL。 到本地儲存庫中相應卷影節點的路徑是在元件路徑中預先放置卷影節點根路徑的結果：

* 根路徑= /content/usergenerated
* 注釋陰影節點= /content/usergenerated/content/community-components/en/comments/jcr:content/content/include/comments

**UGC位置**

UGC不是在這兩個位置中建立的，且僅應使用叫用SRP API的 [公用程式方法](#utility-method-to-access-ugc) 來存取。

* 根路徑= /content/usergenerated/asi/srp-choice
* JSRP的UGC節點= /content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_

*請注意*，對於JSRP,UGC節點將只 *會出現* （作者或發佈）在輸入AEM例項上。 如果在發佈例項上輸入，則無法從作者的協調控制台進行協調。

## 相關資訊 {#related-information}

* [儲存資源提供方概述](srp.md) -簡介和儲存庫使用概述
* [使用SRP存取UGC](accessing-ugc-with-srp.md) —— 編碼准則
* [SocialUtils重構](socialutils.md) -將不建議使用的公用程式方法對應至目前的SRP公用程式方法

