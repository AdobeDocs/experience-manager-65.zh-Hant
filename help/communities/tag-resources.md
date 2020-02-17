---
title: 標籤啟用資源
seo-title: 標籤啟用資源
description: 標籤啟用資源允許在成員瀏覽目錄時篩選資源和學習路徑
seo-description: 標籤啟用資源允許在成員瀏覽目錄時篩選資源和學習路徑
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 標籤啟用資源 {#tagging-enablement-resources}

## 概覽 {#overview}

標籤啟用資源可讓成員在瀏覽目錄時篩選資源和學習 [路徑](functions.md#catalog-function)。

基本上：

* [為每個目錄建立標籤命名空間](../../help/sites-administering/tags.md#creating-a-namespace) ,

   * [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)

      * 僅限社群成員（封閉社群）

         * 允許社群站點成 [員組的讀取訪問](users.md#publish-group-roles)
      * 對於任何網站訪客，不論登入或匿名（開放社群）

         * 允許群組的讀取存 `Everyone`取
   * [發佈標籤](../../help/sites-administering/tags.md#publishing-tags)



* [定義社群網站的標籤範圍](sites-console.md#tagging)

   * [設定網站結構中存在的目錄](functions.md#catalog-function)

      * 可新增標籤至目錄例項，以控制UI篩選器中顯示的標籤清單
      * 可新增 [預先篩選](catalog-developer-essentials.md#pre-filters)，以限制目錄所包含的資源

* [發佈社群網站](sites-console.md#publishing-the-site)
* [套用標籤至啟用資源](resources.md#create-a-resource) ，以便可斷斷續續地篩選
* [發佈啟用資源](resources.md#publish)

## 社群網站標籤 {#community-site-tags}

建立或編輯社群網站時，「標籤」 [設定會選取現有標籤名稱空間的子集](sites-console.md#tagging) ，以設定可用於網站功能的標籤範圍。

雖然可隨時建立標籤並新增至社群網站，但建議事先設計分類法，類似於設計資料庫。 請參 [閱使用標籤](../../help/sites-authoring/tags.md)。

稍後將標籤新增至現有社群網站時，必須先儲存編輯，才能將新標籤新增至網站結構中的目錄函式。

對於社群網站，發佈網站和發佈標籤後，必須啟用社群成員的讀取存取權。 請參閱 [設定標籤權限](../../help/sites-administering/tags.md#setting-tag-permissions)。

以下是當管理員將讀取權限套用至群組時，在CRXDE中 `/etc/tags/ski-catalog` 的顯示方式 `Community Enable Members`。

![chlimage_1-420](assets/chlimage_1-420.png)

## 目錄標籤名稱空間 {#catalog-tag-namespaces}

型錄功能使用標籤來定義自身。 在社群站點中配置目錄函式時，要選擇的標籤名稱空間集由社區站點的標籤命名空間集的範圍定義。

Catalog函式包含標籤設定，可定義目錄篩選器UI中所列的標籤。 設定「所有名稱空間」是指為社區站點選擇的標籤名稱空間的範圍。

![chlimage_1-421](assets/chlimage_1-421.png)

## 套用標籤至啟用資源 {#applying-tags-to-enablement-resources}

勾選後，啟用資源和學習路徑會顯示在所有 `Show in Catalog` 目錄中。 新增標籤至資源和學習路徑可讓您預先篩選至特定目錄，以及在目錄UI中篩選。

將啟用資源和學習路徑限制在特定型錄上是透過建立預 [先篩選來完成](catalog-developer-essentials.md#pre-filters)。

目錄UI可讓訪客將標籤篩選套用至該目錄中顯示的資源和學習路徑清單。

將標籤應用到啟用資源的管理員必須知道與目錄相關聯的標籤名稱空間以及分類，以便選擇子標籤以進行更精確的分類。

例如，如果在名為 `ski-catalog` 的目錄上建立並設定了命名空間 `Ski Catalog`，則可能有兩個子標籤： `lesson-1` 和 `lesson-2`。

因此，任何標有下列其中一項的啟用資源：

* ski-catalog:
* ski-catalog:leansion-1
* ski-catalog:leassion-2

將在啟用 `Ski Catalog` 資源發佈後顯示。

![chlimage_1-422](assets/chlimage_1-422.png)

## 在發佈時檢視目錄 {#viewing-catalog-on-publish}

一旦從作者環境設定並發佈所有內容後，就可以在發佈環境中體驗使用目錄尋找啟用資源的經驗。

如果下拉式清單中未顯示任何標籤名稱空間，請確定權限已在發佈環境中正確設定。

如果新增標籤名稱空間且遺失，請確定標籤和網站已重新發佈。

如果在檢視目錄時選取標籤後未顯示啟用資源，請確定目錄的命名空間中有標籤套用至啟用資源。

![chlimage_1-423](assets/chlimage_1-423.png)

