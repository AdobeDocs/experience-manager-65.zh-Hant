---
title: 標籤啟用資源
seo-title: Tagging Enablement Resources
description: 啟用資源的標籤允許在成員瀏覽目錄時篩選資源和學習路徑
seo-description: Tagging of enablement resources allows for filtering of resources and learning paths as members browse catalogs
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
role: Admin
exl-id: ce58c8e9-8b4a-43fb-a108-ed2ac40268c7
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 標籤啟用資源 {#tagging-enablement-resources}

## 總覽 {#overview}

啟用資源的標籤可讓成員瀏覽時篩選資源和學習路徑 [目錄](functions.md#catalog-function).

基本上：

* [建立標籤命名空間](../../help/sites-administering/tags.md#creating-a-namespace) 每個目錄

   * [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)
   * 僅適用於社群成員（封閉社群）

      * 允許的讀取存取 [社群網站的成員組](users.md#publish-group-roles)
   * 針對任何網站訪客，無論是登入或匿名（開放社群）

      * 允許的讀取存取 `Everyone` 群組
   * [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)



* [定義社群網站的標籤範圍](sites-console.md#tagging)

   * [配置站點結構中存在的目錄](functions.md#catalog-function)

      * 可以新增標籤至目錄例項，以控制UI篩選器中呈現的標籤清單。
      * 可新增 [預先篩選](catalog-developer-essentials.md#pre-filters)，以限制目錄的已包含資源。

* [發佈社群網站](sites-console.md#publishing-the-site)
* [套用標籤至啟用資源](resources.md#create-a-resource) 因此，它們可能被斷斷續續地過濾
* [發佈啟用資源](resources.md#publish)

## 社群網站標籤 {#community-site-tags}

建立或編輯社群網站時， [標籤設定](sites-console.md#tagging) 通過選擇現有標籤命名空間的子集來設定網站功能可用的標籤範圍。

雖然標籤可隨時建立並新增至社群網站，但建議您事先設計分類法，類似於設計資料庫。 請參閱 [使用標籤](../../help/sites-authoring/tags.md).

稍後將標籤新增至現有社群網站時，必須先儲存編輯，才能將新標籤新增至網站結構中的目錄函式。

對於社群網站，發佈網站和發佈標籤後，必須啟用對社群成員的讀取存取。 請參閱 [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions).

管理員將讀取權限套用至時，CRXDE中的顯示方式如下 `/etc/tags/ski-catalog` 組 `Community Enable Members`.

![網站標籤](assets/site-tags.png)

## 目錄標籤命名空間 {#catalog-tag-namespaces}

目錄功能使用標籤來定義本身。 在社群網站中設定目錄函式時，要選擇的標籤命名空間集由社群網站設定的標籤命名空間範圍定義。

「目錄」函式包含標籤設定，定義目錄的篩選器UI中所列的標籤。 「所有命名空間」設定是指為社群網站選取的標籤命名空間範圍。

![目錄命名空間](assets/catalog-namespace.png)

## 將標籤套用至啟用資源 {#applying-tags-to-enablement-resources}

當 `Show in Catalog` 已勾選。 將標籤新增至資源和學習路徑可允許預先篩選至特定目錄，以及在目錄UI中進行篩選。

借由建立 [預先篩選](catalog-developer-essentials.md#pre-filters).

目錄UI可讓訪客將標籤篩選套用至該目錄中顯示的資源和學習路徑清單。

將標籤套用至啟用資源的管理員必須知道與目錄相關聯的標籤命名空間以及分類法，才能選取子標籤，以便更精細地分類。

例如，若 `ski-catalog` 在名為的目錄中建立和設定命名空間 `Ski Catalog`，可能有兩個子標籤： `lesson-1` 和 `lesson-2`.

因此，任何以下列其中一項標籤的啟用資源：

* ski-catalog:lession-1
* ski-catalog:lession-2

將顯示在 `Ski Catalog` 啟用資源發佈後。

![基本資訊](assets/applytags-basicinfo.png)

## 在發佈時檢視目錄 {#viewing-catalog-on-publish}

從製作環境設定完所有內容並發佈後，就能在發佈環境中體驗使用目錄尋找啟用資源的體驗。

如果下拉式清單中未顯示任何標籤命名空間，請確定權限已在發佈環境中正確設定。

如果已新增標籤命名空間且遺失，請確定標籤和網站已重新發佈。

如果在檢視目錄時選取標籤後未顯示啟用資源，請確定有來自目錄命名空間的標籤套用至啟用資源。

![view-catalog](assets/viewcatalog.png)
