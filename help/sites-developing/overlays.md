---
title: 覆蓋
seo-title: 覆蓋
description: AEM使用覆蓋的原則，讓您擴充並自訂控制台和其他功能
seo-description: AEM使用覆蓋的原則，讓您擴充並自訂控制台和其他功能
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# 覆蓋{#overlays}

AEM（以及在此之前，CQ）長期以來都採用覆蓋原則，讓您擴充和自訂[控制台](/help/sites-developing/customizing-consoles-touch.md)和其他功能（例如，[頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md)）。

Overlay是可在許多內容中使用的詞語。 在此內容（擴充AEM）中，覆蓋表示您會取用預先定義的功能，並將您自己的定義加入該功能（以自訂標準功能）。

在標準例項中，預先定義的功能保存在`/libs`下，建議您在`/apps`分支下定義覆蓋（自訂）。 AEM使用搜尋路徑來尋找資源，先搜尋`/apps`分支，再搜尋`/libs`分支（[搜尋路徑可設定](#configuring-the-search-paths)）。 此機制表示您的覆蓋（及其中定義的自訂）將具有優先順序。

自AEM 6.0起，已變更覆蓋的實作與使用方式：

* AEM 6.0以上版本——適用於[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相關覆蓋（即觸控式UI）

   * 方法

      * 在`/apps`下重建適當的`/libs`結構。

         這不需要1:1復本，[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)會用來交叉參考所需的原始定義。 Sling Resource Merger提供服務，透過差異(differencing)機制存取和合併資源。

      * 在`/apps`下進行任何更改。
   * 優勢

      * 對`/libs`下的變更更更穩健。
      * 只重新定義實際需要的內容。


* AEM 6.0之前的非花崗石覆蓋和覆蓋

   * 方法

      * 將內容從`/libs`複製到`/apps`

         您需要複製整個子分支，包括屬性。

      * 在`/apps`下進行任何更改。
   * 缺點

      * 雖然您的變更不會在`/libs`下方發生變更時遺失，但您可能必須重新建立在`/apps`下方覆蓋中發生的特定變更。


>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)和相關方法只能與[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)一起使用。 這表示建立具有骨架結構的覆蓋僅適用於標準的觸控式使用者介面。
>
>其他區域（包括傳統UI）的覆蓋包括複製適當的節點和整個子結構，然後進行所需的變更。

Overlays是許多變更的建議方法，例如在側面板[（用於製作頁面）中，設定控制台[或](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)建立選擇類別至資產瀏覽器。 ](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)它們的要求如下：

* ***不得*&#x200B;在`/libs`分支&#x200B;**中進行變更
您所做的任何變更都可能會遺失，因為此分支在您執行下列動作時都會面臨變更：

   * 升級至您的實例
   * 套用修補程式
   * 安裝功能套件

* 他們將您的變更集中在一個位置；讓您更輕鬆地追蹤、移轉、備份和／或除錯變更。

## 配置搜索路徑{#configuring-the-search-paths}

對於覆蓋，所傳送的資源是所檢索的資源和屬性的匯總，具體取決於可定義的搜索路徑：

* 資源&#x200B;**解析器搜索路徑**，如[OSGi configuration](/help/sites-deploying/configuring-osgi.md)中為&#x200B;**Apache Sling資源解析器工廠**&#x200B;定義的。

   * 搜索路徑的自頂向下順序指示其各自的優先順序。
   * 在標準安裝中，主要預設值為`/apps`、`/libs` —— 因此`/apps`的內容具有比`/libs`高的優先順序（即&#x200B;*覆蓋*）。

* 兩個服務用戶需要對指令碼儲存位置的JCR：讀取訪問。 這些使用者包括：components-search-service(由com.day.cq.wcm.coreto存取／快取元件使用)和sling-scripting（由org.apache.sling.servlets.resolver用來尋找servlet）。
* 還必鬚根據指令碼的放置位置配置以下配置（在此示例中，位於/etc、/libs或/apps下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後，還必須配置Servlet解析程式（在本示例中，還要添加/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用範例{#example-of-usage}

以下是一些範例：

* [自定義控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md)

