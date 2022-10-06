---
title: 自訂網站主控台（傳統UI）
seo-title: Customizing the Websites Console (Classic UI)
description: 網站管理控制台可延伸，以顯示自訂欄
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

# 自訂網站主控台（傳統UI）{#customizing-the-websites-console-classic-ui}

## 新增自訂欄至網站（網站管理員）主控台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

網站管理控制台可延伸，以顯示自訂欄。 主控台是根據JSON物件建置，可透過建立實作的OSGI服務來擴充 `ListInfoProvider` 介面。 此類服務會修改傳送至用戶端的JSON物件，以建置主控台。

本逐步教學課程說明如何透過實作 `ListInfoProvider` 介面。 它包含下列步驟：

1. [建立OSGI服務](#creating-the-osgi-service) 並將包含該套件的套件組合部署至AEM伺服器。
1. （可選） [測試新服務](#testing-the-new-service) 發出JSON呼叫以要求用來建置主控台的JSON物件。
1. [顯示新列](#displaying-the-new-column) 擴充存放庫中主控台的節點結構。

>[!NOTE]
>
>本教學課程也可用來擴充下列管理主控台：
>
>* 數位資產主控台
>* 社群主控台
>


### 建立OSGI服務 {#creating-the-osgi-service}

此 `ListInfoProvider` 介面定義兩種方法：

* `updateListGlobalInfo`，以更新清單的全局屬性，
* `updateListItemInfo`，以更新單一清單項目。

這兩種方法的引數為：

* `request`，相關的Sling HTTP要求物件，
* `info`，即要更新的JSON物件，分別是全域清單或目前清單項目，
* `resource`，即Sling資源。

以下是範例實作：

* 新增 *主演* 屬性，即 `true` 如果頁面名稱開頭為 *e*，和 `false` 否則。

* 新增 *stardedCount* 屬性，此屬性對清單而言為全域，並包含星號清單項目的數量。

若要建立OSGI服務：

1. 在CRXDE Lite中， [建立套件組合](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. 新增下列范常式式碼。
1. 建立套件組合。

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
>* 您的實作應根據提供的要求和/或資源，決定是否應將資訊新增至JSON物件。
>* 若您的 `ListInfoProvider` 實作會定義回應物件中已存在的屬性，其值將會由您提供的屬性覆寫。
>
>  您可以使用 [服務排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 管理多個 `ListInfoProvider` 實作。

### 測試新服務 {#testing-the-new-service}

當您開啟網站管理主控台並瀏覽您的網站時，瀏覽器會發出ajax呼叫，以取得用來建置主控台的JSON物件。 例如，當您瀏覽至 `/content/geometrixx` 資料夾中，系統會傳送下列請求至AEM伺服器以建置主控台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要確保新服務在部署包含該服務的包後運行：

1. 將瀏覽器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 回應應會依下列方式顯示新屬性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 顯示新列 {#displaying-the-new-column}

最後一步是調整網站管理控制台的節點結構，以透過覆蓋來顯示所有Geometrixx頁面的新屬性 `/libs/wcm/core/content/siteadmin`. 按如下步驟進行：

1. 在CRXDE Lite中，建立節點結構 `/apps/wcm/core/content` 節點類型 `sling:Folder` 來反映結構 `/libs/wcm/core/content`.

1. 複製節點 `/libs/wcm/core/content/siteadmin` 貼到下面 `/apps/wcm/core/content`.

1. 複製節點 `/apps/wcm/core/content/siteadmin/grid/assets` to `/apps/wcm/core/content/siteadmin/grid/geometrixx` 並變更其屬性：

   * 移除 **pageText**

   * 設定 **pathRegex** to `/content/geometrixx(/.*)?`
這會使網格設定在所有geometrixx網站中都處於作用中狀態。

   * 設定 **storeProxySuffix** to `.pages.json`

   * 編輯 **storeReaderFields** 多值屬性並添加 `starred` 值。

   * 若要啟用MSM功能，請將下列MSM參數新增至multi-String屬性 **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 新增 `starred` 節點（類型） **nt：非結構化**) `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` ，並搭配下列屬性：

   * **dataIndex**: `starred` 類型字串

   * **標題**: `Starred` 類型字串

   * **xtype**: `gridcolumn` 類型字串

1. （選用）拖放您不想顯示於的欄 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是虛名路徑，預設會指向 `/libs/wcm/core/content/siteadmin`.
若要將此內容重新導向至您的網站管理員版本，請依 `/apps/wcm/core/content/siteadmin` 定義屬性 `sling:vanityOrder` 的值高於定義的值 `/libs/wcm/core/content/siteadmin`. 預設值為300，因此任何高於的值都合適。

1. 前往「網站管理」主控台，並導覽至Geometrixx網站：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 名為的新欄 **星級** 可用，依下列方式顯示自訂資訊：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多個網格配置與 **pathRegex** 屬性，第一個屬性會使用，而非最具體的屬性，這表示設定的順序很重要。

### 範例套件 {#sample-package}

本教學課程的結果可在 [自訂網站管理控制台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 封裝共用上的封裝。
