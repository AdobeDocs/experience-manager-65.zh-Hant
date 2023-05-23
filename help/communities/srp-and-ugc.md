---
title: SRP和UGC軟體包
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

# SRP和UGC軟體包 {#srp-and-ugc-essentials}

## 簡介 {#introduction}

如果不熟悉儲存資源提供程式(SRP)及其與用戶生成內容(UGC)的關係，請訪問 [社區內容儲存](working-with-srp.md) 和 [儲存資源提供程式概述](srp.md)。

本文檔的這一部分提供了有關SRP和UGC的一些基本資訊。

## 儲存資源提供程式API {#storageresourceprovider-api}

SocialResourceProvider API(SRP API)是各種Sling資源提供程式API的擴展。 它包括對分頁和原子增量的支援（用於計數和計分）。

SCF元件需要查詢，因為需要按日期、幫助、投票次數等進行排序。 所有SRP選項都具有不依賴分段的靈活查詢機制。

SRP儲存位置合併了元件路徑。 SRP API應始終用於訪問UGC，因為根路徑取決於所選的SRP選項，如ASRP、MSRP或JSRP。

SRP API不是抽象類，它是介面。 不應輕率地執行自定義實施，因為升級到新版本時將忽略未來改進內部實施的好處。

使用SRP API的方法是通過提供的實用程式，如SocialResourceUtilities包中的實用程式。

從6.0或更AEM早版本升級時，需要遷移所有SRP的UGC，其中有開放原始碼工具。 請參閱 [升級到AEM Communities6.3](upgrade.md)。

>[!NOTE]
>
>以前，訪問UGC的實用程式在SocialUtils包中找到，該包已不存在。
>
>有關替換實用程式，請參見 [SocialUtils重構](socialutils.md)。

## 訪問UGC的實用方法 {#utility-method-to-access-ugc}

要訪問UGC，請使用SocialResourceUtilities包中的方法返回適合從SRP訪問UGC的路徑，並替換SocialUtils包中找到的已過時方法。

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

有關其他SocialUtils替代項，請參見 [SocialUtils重構](socialutils.md)。

有關編碼指南，請訪問 [使用SRP訪問UGC](accessing-ugc-with-srp.md)。

>[!CAUTION]
>
>返回的路徑resourceToUGCStoragePath()為 *不* 適合 [ACL檢查](srp.md#for-access-control-acls)。

## 訪問ACL的實用方法 {#utility-method-to-access-acls}

某些SRP實現（如ASRP和MSRP）將社區內容儲存在不提供ACL驗證的資料庫中。 卷影節點提供本地儲存庫中可應用ACL的位置。

使用SRP API，所有SRP選項在執行所有CRUD操作之前都對卷影位置執行相同的檢查。

要檢查ACL，請使用一種返回適合檢查應用到資源UGC的權限的路徑的方法。

下面是在servlet中使用resourceToACLPath()方法的一個簡單示例：

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
>resourceToACLPath()返回的路徑為 *不* 適合 [訪問UGC](#utility-method-to-access-acls) 本身。

## 與UGC相關的儲存位置 {#ugc-related-storage-locations}

以下對儲存位置的描述在使用JSRP或MSRP開發時可能會有所幫助。 當前沒有UI可訪問儲存在ASRP中的UGC，因為JSRP([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))和MSRP（MongoDB工具）。

**元件位置**

當成員在發佈環境中輸入UGC時，它們將作為站點的一部分與元件進AEM行交互。

此元件的示例是 [注釋元件](http://localhost:4502/content/community-components/en/comments.html) 存在於 [社區元件指南](components-guide.md) 的子菜單。 本地儲存庫中注釋節點的路徑是：

* 元件路徑= `/content/community-components/en/comments/jcr:content/content/includable/comments`

**卷影節點位置**

UGC的建立也會建立 [陰影節點](srp.md#about-shadow-nodes-in-jcr) 應用了必要ACL。 指向本地儲存庫中相應卷影節點的路徑是預掛起卷影節點根路徑到元件路徑的結果：

* 根路徑 = `/content/usergenerated`
* 注釋卷影節點= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC位置**

UGC在這兩個位置都不建立，只應使用 [實用方法](#utility-method-to-access-ugc) 調用SRP API。

* 根路徑 = `/content/usergenerated/asi/srp-choice`
* JSRP的UGC節點= `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意*，對於JSRP,UGC節點將 *僅* 在其上AEM輸入的實例（作者或發佈）上存在。 如果在發佈實例上輸入，則無法通過作者的審核控制台進行審核。

## 相關資訊 {#related-information}

* [儲存資源提供程式概述](srp.md)  — 簡介和儲存庫使用概述。
* [使用SRP訪問UGC](accessing-ugc-with-srp.md)  — 編碼准則。
* [SocialUtils重構](socialutils.md)  — 將過時的實用程式方法映射到當前SRP實用程式方法。
