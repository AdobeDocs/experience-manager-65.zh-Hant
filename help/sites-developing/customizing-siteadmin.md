---
title: 自訂網站主控台(Classic UI)
seo-title: 自訂網站主控台(Classic UI)
description: 「網站管理」主控台可延伸以顯示自訂欄
seo-description: 「網站管理」主控台可延伸以顯示自訂欄
uuid: 9163fdff-5351-477d-b91c-8a74f8b41d34
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: aeb37103-541d-4235-8a78-980b78c8de66
docset: aem65
translation-type: tm+mt
source-git-commit: 4d47310ebf9d450de52c925642978ba92ef9c1d4

---


# 自訂網站主控台(Classic UI){#customizing-the-websites-console-classic-ui}

## 新增自訂欄至網站（網站管理）主控台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

「網站管理」主控台可以延伸，以顯示自訂欄。 主控台是以JSON物件為基礎建立，可透過建立實作介面的OSGI服務來擴充 `ListInfoProvider` 物件。 此類服務會修改傳送至用戶端的JSON物件，以建立主控台。

本逐步教學課程說明如何透過實作介面，在「網站管理」主控台中顯示新 `ListInfoProvider` 欄。 它包含下列步驟：

1. [建立OSGI服務](#creating-the-osgi-service) ，並將包含它的套件部署至AEM伺服器。
1. （可選） [](#testing-the-new-service) 發出JSON呼叫以請求用於建立主控台的JSON物件，以測試新服務。
1. [通過擴展儲存庫中](#displaying-the-new-column) 控制台的節點結構來顯示新列。

>[!NOTE]
>
>本教學課程也可用來擴充下列管理控制台：
>
>* 數位資產主控台
>* 社群主控台
>



### 建立OSGI服務 {#creating-the-osgi-service}

介面 `ListInfoProvider` 定義了兩種方法：

* `updateListGlobalInfo`，以更新清單的全局屬性，
* `updateListItemInfo`，以更新單一清單項目。

兩種方法的引數為：

* `request`，關聯的Sling HTTP請求物件，
* `info`，則JSON物件要更新，這分別是全域清單或目前清單項目，
* `resource`, a Sling resource.

實作範例如下：

* 新增每 *個項目的星號屬性* ，這是 `true` 如果頁面名稱以 *e開頭*, `false` 否則。

* 新增星 *星號Count屬性* ，此屬性是清單的全域屬性，並包含星號清單項目的數目。

要建立OSGI服務：

1. 在CRXDE Lite中， [建立套件](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
1. 新增下方的范常式式碼。
1. 建立套件。

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
>* 您的實作應根據提供的請求和／或資源，決定是否應將資訊新增至JSON物件。
>* 如果您 `ListInfoProvider` 的實作定義了回應物件中已存在的屬性，其值將由您提供的屬性覆寫。
   >  您可以使用 [服務排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) ，管理多個實施的執行 `ListInfoProvider` 順序。
>



### 測試新服務 {#testing-the-new-service}

當您開啟「網站管理」主控台並瀏覽您的網站時，瀏覽器會發出ajax呼叫，以取得用來建立主控台的JSON物件。 例如，當您瀏覽至檔案夾時， `/content/geometrixx` 下列請求會傳送至AEM伺服器以建立主控台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&limit=30&predicate=siteadmin)

要確保新服務在部署包含該服務的包後正在運行：

1. 將您的瀏覽器指向下列URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&limit=30&predicate=siteadmin)

1. 響應應按如下方式顯示新屬性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 顯示新列 {#displaying-the-new-column}

最後一個步驟是調整「網站管理」主控台的節點結構，以覆蓋顯示所有Geometrixx頁面的新屬性 `/libs/wcm/core/content/siteadmin`。 按如下步驟進行：

1. 在CRXDE Lite中，使用類型節點建立 `/apps/wcm/core/content` 節點結構以 `sling:Folder` 反映結構 `/libs/wcm/core/content`。

1. 複製節點 `/libs/wcm/core/content/siteadmin` 並貼到下面 `/apps/wcm/core/content`。

1. 將節點復 `/apps/wcm/core/content/siteadmin/grid/assets` 制到 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 並更改其屬性：

   * 移除pageText(英 **文)**

   * 將 **pathRegex設為**`/content/geometrixx(/.*)?`This will make the grid configuration active for all geometrixx websites.

   * 將 **storeProxySuffix設為**`.pages.json`

   * 編輯 **storeReaderFields** multivalued屬性並新增 `starred` 值。

   * 若要啟用MSM功能，請將下列MSM參數新增至multi-String屬性 **storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 在下面添 `starred` 加一個節點(類 **型為nt:antrustructured**), `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 並包含以下屬性：

   * **dataIndex**:字 `starred` 串類型

   * **header**:字 `Starred` 串類型

   * **xtype**:字 `gridcolumn` 串類型

1. （可選）拖放您不想在 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是虛名的路徑，預設情況下指向 `/libs/wcm/core/content/siteadmin`。
若要將此重新導向至您的網站管理員版 `/apps/wcm/core/content/siteadmin` 本，請定 `sling:vanityOrder` 義屬性，使其值高於上定義的值 `/libs/wcm/core/content/siteadmin`。 預設值為300，因此任何較高的值都適用。

1. 前往「網站管理」主控台，並導覽至Geometrixx網站：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 新欄名為 **Starder** ，可顯示自訂資訊，如下所示：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多個網格配置與 **pathRegex屬性定義的請求路徑匹配** ，則會使用第一個網格配置，而不是最具體的網格配置，這表示配置的順序很重要。

### 範例套件 {#sample-package}

本教學課程的結果可在Package Share的 [Customizing the Websites Administration Console](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) package中取得。
