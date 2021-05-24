---
title: 覆蓋
seo-title: 覆蓋
description: AEM使用覆蓋原則，可讓您擴充及自訂主控台和其他功能
seo-description: AEM使用覆蓋原則，可讓您擴充及自訂主控台和其他功能
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---

# 覆蓋{#overlays}

AEM（在此之前，CQ）長期以來都採用覆蓋原則，可讓您擴充及自訂[console](/help/sites-developing/customizing-consoles-touch.md)和其他功能（例如[頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md)）。

覆蓋是可在許多內容中使用的詞語。 在此內容中(擴充AEM)，覆蓋表示需取用預先定義的功能，並將您自己的定義加以保留（以自訂標準功能）。

在標準例項中，預先定義的功能保存在`/libs`下，建議您在`/apps`分支下定義覆蓋（自訂）。 AEM使用搜尋路徑來尋找資源，先搜尋`/apps`分支，再搜尋`/libs`分支（[搜尋路徑可以設定](#configuring-the-search-paths)）。 此機制表示您的覆蓋（以及那裡定義的自訂）將具有優先順序。

自AEM 6.0起，已變更覆蓋的實作和使用方式：

* AEM 6.0以上 — 適用於[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)相關覆蓋（即觸控式UI）

   * 方法

      * 在`/apps`下重建相應的`/libs`結構。

         這不需要1:1副本，[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)會用來交叉參考所需的原始定義。 Sling Resource Merger通過差異（差異）機制提供存取和合併資源的服務。

      * 在`/apps`下進行任何更改。
   * 優勢

      * 對`/libs`下的變更更穩健。
      * 只重新定義實際需要的。


* AEM 6.0之前的非Granite覆蓋圖和覆蓋圖

   * 方法

      * 將內容從`/libs`複製到`/apps`

         您需要複製整個子分支，包括屬性。

      * 在`/apps`下進行任何更改。
   * 缺點

      * 雖然在`/libs`下有所變更時，您的變更不會遺失，但您可能必須重新建立在`/apps`下覆蓋中發生的特定變更。


>[!CAUTION]
>
>[Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)及相關方法只能搭配[Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)使用。 這表示以骨架結構建立覆蓋圖僅適用於標準觸控式UI。
>
>其他區域（包括傳統UI）的覆蓋涉及複製適當的節點和整個子結構，然後進行必要的變更。

覆蓋是許多變更的建議方法，例如[設定主控台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console)或[在側面板](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser)的資產瀏覽器中建立您的選取類別（用於製作頁面）。 這些參數為：

* 您&#x200B;***不得*&#x200B;在`/libs`分支&#x200B;**中進行變更
您所做的任何變更都可能會遺失，因為只要您符合以下條件，此分支就會發生變更：

   * 在您的執行個體上升級
   * 套用hotfix
   * 安裝功能套件

* 他們將你的變更集中在一個位置；讓您更輕鬆地視需要追蹤、移轉、備份和/或除錯變更。

## 配置搜索路徑{#configuring-the-search-paths}

對於覆蓋，傳送的資源是所擷取資源和屬性的匯總，視可定義的搜尋路徑而定：

* **Apache Sling Resource Resolver Factory**&#x200B;的[OSGi設定](/help/sites-deploying/configuring-osgi.md)中定義的資源&#x200B;**解析器搜尋路徑**。

   * 搜尋路徑的由上而下順序會指出其各自的優先順序。
   * 在標準安裝中，主預設值為`/apps`, `/libs` — 因此`/apps`的內容具有比`/libs`更高的優先順序（即&#x200B;*覆蓋*）。

* 兩個服務用戶需要JCR：讀取對指令碼儲存位置的訪問。 這些使用者包括：components-search-service(由com.day.cq.wcm.coreto存取/快取元件使用)和sling-scripting（由org.apache.sling.servlets.resolver用來尋找servlet）。
* 還必鬚根據您放置指令碼的位置配置以下配置（在本示例中，位於/etc、/libs或/apps下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後，還必須設定Servlet解析器（在此範例中，也需新增/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用範例{#example-of-usage}

下列情形會提供一些範例：

* [自訂主控台](/help/sites-developing/customizing-consoles-touch.md)
* [自訂頁面編寫](/help/sites-developing/customizing-page-authoring-touch.md)
