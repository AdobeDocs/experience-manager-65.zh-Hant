---
title: srp和UGC Essentials
description: 儲存資源提供者和使用者產生的內容概觀
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8279684f-23dd-4234-bf01-fd2ce74bcb4e
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# srp和UGC Essentials {#srp-and-ugc-essentials}

## 簡介 {#introduction}

如果不熟悉儲存資源提供者(SRP)及其和使用者產生內容(UGC)的關係，請造訪 [社群內容儲存](working-with-srp.md) 和 [儲存資源提供者概觀](srp.md).

本檔案的這個區段提供有關SRP和UGC的一些基本資訊。

## StorageResourceProvider API {#storageresourceprovider-api}

SocialResourceProvider API (SRP API)是各種Sling資源提供者API的擴充功能。 其中包括對分頁和原子增量的支援（適用於計分和評分）。

SCF元件需要查詢，因為需要依日期、實用性、票數等排序。 所有SRP選項都有彈性的查詢機制，不依賴分組。

SRP儲存位置整合了元件路徑。 SRP API應一律用於存取UGC，因為根路徑取決於所選的SRP選項，例如ASRP、MSRP或JSRP。

SRP API不是抽象類別，而是介面。 自訂實施不應輕易進行，因為升級到新版本時，會錯過未來內部實施改善的好處。

使用SRP API的方法是透過提供的公用程式，例如SocialResourceUtilities套件中的公用程式。

從AEM 6.0或更舊版本升級時，必須移轉所有SRP （有開放原始碼工具可用）的UGC。 另請參閱 [升級至AEM Communities 6.3](upgrade.md).

>[!NOTE]
>
>過去，用於存取UGC的公用程式已存在於SocialUtils套件中，該套件已不存在。
>
>有關替代公用程式，請參閱 [SocialUtils重構](socialutils.md).

## 存取UGC的公用程式方法 {#utility-method-to-access-ugc}

若要存取UGC，請使用SocialResourceUtilities套件中的方法，該方法會傳回適合從SRP存取UGC的路徑，並取代SocialUtils套件中找到的已棄用方法。

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

如需其他SocialUtils取代專案，請參閱 [SocialUtils重構](socialutils.md).

如需程式碼指南，請造訪 [使用SRP存取UGC](accessing-ugc-with-srp.md).

>[!CAUTION]
>
>resourceToUGCStoragePath()傳回的路徑為 *非* 適合 [ACL檢查](srp.md#for-access-control-acls).

## 存取ACL的公用程式方法 {#utility-method-to-access-acls}

有些SRP實作（例如ASRP和MSRP）會將社群內容儲存在未提供ACL驗證的資料庫中。 陰影節點會提供本機存放庫中ACL可套用的位置。

使用SRP API時，所有SRP選項都會在所有CRUD作業之前，對陰影位置執行相同的檢查。

若要檢查ACL，請使用傳回適合檢查套用至資源UGC之許可權的路徑的方法。

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
>resourceToACLPath()傳回的路徑為 *非* 適合 [存取UGC](#utility-method-to-access-acls) 本身。

## UGC相關的儲存位置 {#ugc-related-storage-locations}

以下儲存位置的說明在使用JSRP或是MSRP進行開發時可能會有所幫助。 目前沒有UI可存取ASRP中儲存的UGC，因為JSRP有([CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md))和MSRP （MongoDB工具）。

**元件位置**

當成員在發佈環境中進入UGC時，他們與AEM網站中的元件互動。

以下是這類元件的範例： [comments元件](http://localhost:4502/content/community-components/en/comments.html) 中存在於 [社群元件指南](components-guide.md) 網站。 本機存放庫中註解節點的路徑為：

* 元件路徑= `/content/community-components/en/comments/jcr:content/content/includable/comments`

**陰影節點位置**

建立UGC也會建立 [陰影節點](srp.md#about-shadow-nodes-in-jcr) 將必要的ACL套用到其中。 本機存放庫中對應陰影節點的路徑是在元件路徑前加上陰影節點根路徑的結果：

* 根路徑= `/content/usergenerated`
* 註解陰影節點= `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

**UGC位置**

UGC不會在這兩個位置中建立，且僅能使用 [公用程式方法](#utility-method-to-access-ugc) 會叫用SRP API。

* 根路徑= `/content/usergenerated/asi/srp-choice`
* JSRP的UGC節點= `/content/usergenerated/asi/jcr/content/community-components/en/comments/jcr:content/content/includable/comments/srzd-let_it_be_`

*注意*，針對JSRP，UGC節點將 *僅限* 出現在輸入它的AEM例項（製作或發佈）上。 如果在發佈執行個體上輸入，就無法在作者上的稽核控制檯中進行稽核。

## 相關資訊 {#related-information}

* [儲存資源提供者概觀](srp.md)  — 簡介和存放庫使用概述。
* [使用SRP存取UGC](accessing-ugc-with-srp.md)  — 程式碼指南。
* [SocialUtils重構](socialutils.md)  — 將已棄用的公用程式方法對應到目前的SRP公用程式方法。
