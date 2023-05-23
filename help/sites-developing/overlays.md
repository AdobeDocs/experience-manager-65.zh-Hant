---
title: 覆蓋
seo-title: Overlays
description: 使AEM用疊加原則，可擴展和定制控制台和其他功能
seo-description: AEM uses the principle of overlays to allow you to extend and customize the consoles and other functionality
uuid: d14c08fe-04c0-4925-8c99-c6644357919d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0470b74c-2c34-4327-afed-b95eefb1d521
exl-id: e57a6971-6a6f-427b-a8cd-a2f2e8cdf9e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# 覆蓋{#overlays}

AEM（在此之前， CQ）一直使用覆蓋原則來擴展和定制 [控制台](/help/sites-developing/customizing-consoles-touch.md) 和其他功能(例如， [頁面創作](/help/sites-developing/customizing-page-authoring-touch.md))。

Overlay是可在許多上下文中使用的術語。 在此上下文(擴展AEM)中，疊加意味著採用預定義的功能並將您自己的定義強加到該功能之上（以自定義標準功能）。

在標準實例中，預定義功能保留在 `/libs` 建議在以下位置定義覆蓋（自定義） `/apps` 分支。 使AEM用搜索路徑查找資源，首先搜索 `/apps` 分支，然後 `/libs` 分支( [可以配置搜索路徑](#configuring-the-search-paths))。 此機制意味著您的覆蓋（以及在其中定義的自定義）將具有優先順序。

自AEM6.0以來，已對如何實施和使用重疊做了更改：

* AEM6.0以上 [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) — 相關覆蓋（即啟用觸摸的UI）

   * 方法

      * 重建適當的 `/libs` 結構 `/apps`。

         這不需要1:1的拷貝， [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 用於交叉引用所需的原始定義。 Sling資源合併通過差異（差異）機制提供訪問和合併資源的服務。

      * 在下進行任何更改 `/apps`。
   * 優點

      * 對以下項的更改更加穩健 `/libs`。
      * 只重新定義實際需要的內容。


* 6.0之前的非花崗岩覆AEM蓋和覆蓋

   * 方法

      * 從 `/libs` 至 `/apps`

         您需要複製整個子分支，包括屬性。

      * 在下進行任何更改 `/apps`。
   * 缺點

      * 雖然您的更改不會在以下情況下發生更改時丟失 `/libs`，您可能必須重新建立覆蓋下發生的某些更改 `/apps`。


>[!CAUTION]
>
>的 [Sling資源合併](/help/sites-developing/sling-resource-merger.md) 相關方法只能與 [花崗岩](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)。 這意味著建立具有骨架結構的覆蓋僅適用於標準的啟用觸摸的UI。
>
>覆蓋其他區域（包括經典UI）涉及複製相應的節點和整個子結構，然後進行所需的更改。

對於許多更改，建議使用疊加方法，如 [配置控制台](/help/sites-developing/customizing-consoles-touch.md#create-a-custom-console) 或 [在側面板中將選擇類別建立到資產瀏覽器](/help/sites-developing/customizing-page-authoring-touch.md#add-new-selection-category-to-asset-browser) （在創作頁面時使用）。 它們要求為：

* 你 ***不能* 在 `/libs` 分支&#x200B;**您所做的任何更改都可能丟失，因為在以下情況下，此分支可能會發生更改：

   * 升級實例
   * 應用修補程式
   * 安裝功能包

* 他們把你的改變集中在一個地方；使您能夠根據需要更輕鬆地跟蹤、遷移、備份和/或調試更改。

## 配置搜索路徑 {#configuring-the-search-paths}

對於覆蓋交付的資源是檢索到的資源和屬性的集合，具體取決於可以定義的搜索路徑：

* 資源 **解析程式搜索路徑** 定義 [OSGi配置](/help/sites-deploying/configuring-osgi.md) 為 **Apache Sling資源解析器工廠**。

   * 搜索路徑的自頂向下順序指示它們各自的優先順序。
   * 在標準安裝中，主要預設值為 `/apps`。 `/libs`  — 因此， `/apps` 優先順序高於 `/libs` (即 *重疊* )。

* 兩個服務用戶需要對儲存指令碼的位置進行JCR:READ訪問。 這些用戶是：components-search-service(由com.day.cq.wcm.coreto訪問/快取元件使用)和sling-scripting（由org.apache.sling.servlets.resolver用於查找servlet）。
* 還必鬚根據指令碼的放置位置配置以下配置（在本示例中，位於/etc、/libs或/apps下）。

   ```
   PID = org.apache.sling.jcr.resource.internal.JcrResourceResolverFactoryImpl
   resource.resolver.searchpath=["/etc","/apps","/libs"]
   resource.resolver.vanitypath.whitelist=["/etc/","/apps/","/libs/","/content/"]
   ```

* 最後還必須配置Servlet解析程式（在本示例中，還要添加/etc）

   ```
   PID = org.apache.sling.servlets.resolver.SlingServletResolver
   servletresolver.paths=["/bin/","/libs/","/apps/","/etc/","/system/","/index.servlet","/login.servlet","/services/"]
   ```

## 使用示例 {#example-of-usage}

在以下情況下，將介紹一些示例：

* [自定義控制台](/help/sites-developing/customizing-consoles-touch.md)
* [自定義頁面創作](/help/sites-developing/customizing-page-authoring-touch.md)
