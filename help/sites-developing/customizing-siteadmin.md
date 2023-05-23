---
title: 自定義網站控制台(Classic UI)
seo-title: Customizing the Websites Console (Classic UI)
description: 可以擴展網站管理控制台以顯示自定義列
seo-description: The Websites Administration console can be extended to display custom columns
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 0%

---

# 自定義網站控制台(Classic UI){#customizing-the-websites-console-classic-ui}

## 將自定義列添加到網站(siteadmin)控制台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

可以擴展網站管理控制台以顯示自定義列。 該控制台基於JSON對象構建，可通過建立實現 `ListInfoProvider` 。 此類服務修改發送到客戶端以構建控制台的JSON對象。

本逐步教程介紹如何通過實施 `ListInfoProvider` 。 它由以下步驟組成：

1. [建立OSGI服務](#creating-the-osgi-service) 並將包含該包的包部署到服AEM務器。
1. （可選） [測試新服務](#testing-the-new-service) 通過發出JSON調用來請求用於構建控制台的JSON對象。
1. [顯示新列](#displaying-the-new-column) 擴展儲存庫中控制台的節點結構。

>[!NOTE]
>
>本教程還可用於擴展以下管理控制台：
>
>* 數字資產控制台
>* 社區控制台
>


### 建立OSGI服務 {#creating-the-osgi-service}

的 `ListInfoProvider` 介面定義了兩種方法：

* `updateListGlobalInfo`，以更新清單的全局屬性，
* `updateListItemInfo`，以更新單個清單項。

兩種方法的參數為：

* `request`，關聯的Sling HTTP請求對象，
* `info`，要更新的JSON對象，即分別是全局清單或當前清單項，
* `resource`,Sling資源。

以下示例實現：

* 添加 *星* 每個項的屬性， `true` 如果頁面名稱以 *如*, `false` 否則。

* 添加 *星號計數* 屬性，該屬性是清單的全局屬性，包含星號清單項的數目。

要建立OSGI服務，請執行以下操作：

1. 在CRXDE Lite, [建立束](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
1. 添加下面的示例代碼。
1. 生成捆綁包。

新服務已啟動並正在運行。

```java
package com.test;

import com.day.cq.commons.ListInfoProvider;
import com.day.cq.i18n.I18n;
import com.day.cq.wcm.api.Page;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

@Component(metatype = false)
@Service(value = ListInfoProvider.class)
public class StarredListInfoProvider implements ListInfoProvider {

    private int count = 0;

    public void updateListGlobalInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        info.put("starredCount", count);
        count = 0; // reset for next execution
    }

    public void updateListItemInfo(SlingHttpServletRequest request, JSONObject info, Resource resource) throws JSONException {
        Page page = resource.adaptTo(Page.class);
        if (page != null) {
            // Consider starred if page name starts with 'e'
            boolean starred = page.getName().startsWith("e");
            if (starred) {
                count++;
            }
            I18n i18n = new I18n(request);
            info.put("starred", starred ? i18n.get("Yes") : i18n.get("No"));
        }
    }

}
```

>[!CAUTION]
>
>* 您的實現應根據提供的請求和/或資源決定是否應將資訊添加到JSON對象。
>* 如果 `ListInfoProvider` 實現定義了響應對象中已存在的屬性，其值將被您提供的屬性覆蓋。
>
>  您可以使用 [服務排序](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 管理多個 `ListInfoProvider` 實現。

### 測試新服務 {#testing-the-new-service}

當您開啟「網站管理」控制台並瀏覽您的網站時，瀏覽器將發出ajax調用以獲取用於構建控制台的JSON對象。 例如，當您瀏覽到 `/content/geometrixx` 資料夾中，以下請求將發送AEM到伺服器以構建控制台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要確保新服務在部署包含該服務的捆綁包後正在運行：

1. 將瀏覽器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 響應應按如下方式顯示新屬性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 顯示新列 {#displaying-the-new-column}

最後一步是調整網站管理控制台的節點結構，以通過覆蓋顯示所有Geometrixx頁的新屬性 `/libs/wcm/core/content/siteadmin`。 按如下方式繼續：

1. 在CRXDE Lite中，建立節點結構 `/apps/wcm/core/content` 具有類型的節點 `sling:Folder` 以反映結構 `/libs/wcm/core/content`。

1. 複製節點 `/libs/wcm/core/content/siteadmin` 然後貼在下面 `/apps/wcm/core/content`。

1. 複製節點 `/apps/wcm/core/content/siteadmin/grid/assets` 至 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 並更改其屬性：

   * 刪除 **頁面文本**

   * 設定 **pathRegex** 至 `/content/geometrixx(/.*)?`
這將使網格配置對所有幾何網站處於活動狀態。

   * 設定 **storeProxySuffix** 至 `.pages.json`

   * 編輯 **storeReaderFields** 多值屬性並添加 `starred` 值。

   * 要激活MSM功能，請將以下MSM參數添加到multi-String屬性 **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBluinet**
      * **msm:isLiveCopy**

1. 添加 `starred` 節點（類型） **nt：非結構化**&#x200B;下面 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 具有以下屬性：

   * **資料索引**: `starred` 字串類型

   * **標題**: `Starred` 字串類型

   * **x類型**: `gridcolumn` 字串類型

1. （可選）刪除不想在中顯示的列 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是一條虛榮之路，預設情況下，它指向 `/libs/wcm/core/content/siteadmin`。
將此重定向到您的站點管理員版本 `/apps/wcm/core/content/siteadmin` 定義屬性 `sling:vanityOrder` 值要高於上定義的值 `/libs/wcm/core/content/siteadmin`。 預設值為300，因此任何更高的值都合適。

1. 轉至「網站管理」控制台並導航至Geometrixx站點：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx)。

1. 名為 **星** 按如下所示顯示自定義資訊：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多個網格配置與由 **pathRegex** 屬性，將使用第一個，而不是最具體的，這意味著配置的順序非常重要。

### 示例包 {#sample-package}

本教程的結果可在 [自定義網站管理控制台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 包共用。
