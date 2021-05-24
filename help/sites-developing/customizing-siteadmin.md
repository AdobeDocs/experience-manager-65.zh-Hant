---
title: 自訂網站主控台（傳統UI）
seo-title: 自訂網站主控台（傳統UI）
description: 網站管理控制台可延伸，以顯示自訂欄
seo-description: 網站管理控制台可延伸，以顯示自訂欄
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
source-wordcount: '798'
ht-degree: 0%

---

# 自訂網站主控台（傳統UI）{#customizing-the-websites-console-classic-ui}

## 新增自訂欄至網站（網站管理員）主控台{#adding-a-custom-column-to-the-websites-siteadmin-console}

網站管理控制台可延伸，以顯示自訂欄。 主控台是根據JSON物件建置，可透過建立實作`ListInfoProvider`介面的OSGI服務來擴充。 此類服務會修改傳送至用戶端的JSON物件，以建置主控台。

本逐步教學課程說明如何透過實作`ListInfoProvider`介面，在「網站管理控制台」中顯示新欄。 它包含下列步驟：

1. [建立OSGI服](#creating-the-osgi-service) 務並將包含該服務的套件組合部署至AEM伺服器。
1. （選用）[發出JSON呼叫以要求用於建置主控台的JSON物件，以測試新服務](#testing-the-new-service)。
1. [通過擴展儲](#displaying-the-new-column) 存庫中控制台的節點結構來顯示新列。

>[!NOTE]
>
>本教學課程也可用來擴充下列管理主控台：
>
>* 數位資產主控台
>* 社群主控台

>



### 建立OSGI服務{#creating-the-osgi-service}

`ListInfoProvider`介面定義兩種方法：

* `updateListGlobalInfo`，以更新清單的全局屬性，
* `updateListItemInfo`，以更新單一清單項目。

這兩種方法的引數為：

* `request`，相關的Sling HTTP要求物件，
* `info`，即要更新的JSON物件，分別是全域清單或目前清單項目，
* `resource`，即Sling資源。

以下是範例實作：

* 為每個項目新增&#x200B;*星形*&#x200B;屬性，如果頁面名稱以&#x200B;*e*&#x200B;開頭，則為`true`，否則為`false`。

* 新增&#x200B;*stardedCount*&#x200B;屬性，此屬性是清單的全域屬性，並包含星號清單項目的數量。

若要建立OSGI服務：

1. 在CRXDE Lite中，[建立套件](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
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
>* 如果您的`ListInfoProvider`實作定義了回應物件中已存在的屬性，則其值將由您提供的屬性覆寫。

>
>  
您可以使用[服務排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING)來管理多個`ListInfoProvider`實作的執行順序。

### 測試新服務{#testing-the-new-service}

當您開啟網站管理主控台並瀏覽您的網站時，瀏覽器會發出ajax呼叫，以取得用來建置主控台的JSON物件。 例如，當您瀏覽至`/content/geometrixx`資料夾時，會傳送下列要求至AEM伺服器以建置主控台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要確保新服務在部署包含該服務的包後運行：

1. 將瀏覽器指向以下URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 回應應會依下列方式顯示新屬性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 顯示新列{#displaying-the-new-column}

最後一步是調整網站管理控制台的節點結構，以透過覆蓋`/libs/wcm/core/content/siteadmin`來顯示所有Geometrixx頁面的新屬性。 按如下步驟進行：

1. 在CRXDE Lite中，使用類型`sling:Folder`的節點建立結構`/apps/wcm/core/content`以反映結構`/libs/wcm/core/content`。

1. 複製節點`/libs/wcm/core/content/siteadmin`並貼到`/apps/wcm/core/content`下方。

1. 將節點`/apps/wcm/core/content/siteadmin/grid/assets`複製到`/apps/wcm/core/content/siteadmin/grid/geometrixx`並更改其屬性：

   * 移除&#x200B;**pageText**

   * 將&#x200B;**pathRegex**&#x200B;設為`/content/geometrixx(/.*)?`
這會使網格設定在所有geometrixx網站中都處於作用中狀態。

   * 將&#x200B;**storeProxySuffix**&#x200B;設為`.pages.json`

   * 編輯&#x200B;**storeReaderFields**&#x200B;多值屬性並新增`starred`值。

   * 若要啟用MSM功能，請將下列MSM參數新增至multi-String屬性&#x200B;**storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 在`/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`下添加`starred`節點（類型為&#x200B;**nt:unstructured**），其屬性如下：

   * **dataIndex**: `starred` 類型字串

   * **標題**: `Starred` 類型字串

   * **xtype**: `gridcolumn` 類型字串

1. （可選）將您不想顯示在`/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`的列拖放

1. `/siteadmin` 虛名路徑，預設會指 `/libs/wcm/core/content/siteadmin`向若要將此重新導向至您`/apps/wcm/core/content/siteadmin`上的網站管理員版本，請定義屬性`sling:vanityOrder`，使其值高於`/libs/wcm/core/content/siteadmin`上定義的值。 預設值為300，因此任何高於的值都合適。

1. 前往「網站管理」主控台，並導覽至Geometrixx網站：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 名為&#x200B;**Starded**&#x200B;的新列可用，按如下所示顯示自定義資訊：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多個網格配置與&#x200B;**pathRegex**&#x200B;屬性定義的請求路徑匹配，則將使用第一個網格配置，而不是最具體的網格配置，這表示配置的順序非常重要。

### 示例包{#sample-package}

本教學課程的結果可在[Customizing the Websites Administration Console](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin)套件共用上取得。
