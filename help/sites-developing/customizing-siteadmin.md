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
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# 自訂網站主控台(Classic UI){#customizing-the-websites-console-classic-ui}

## 新增自訂欄至網站（網站管理）主控台{#adding-a-custom-column-to-the-websites-siteadmin-console}

「網站管理」主控台可以延伸，以顯示自訂欄。 主控台是以JSON物件為基礎建立的，可透過建立實作`ListInfoProvider`介面的OSGI服務來擴充。 此類服務會修改傳送至用戶端的JSON物件，以建立主控台。

本逐步教學課程說明如何透過實作`ListInfoProvider`介面，在「網站管理」主控台中顯示新欄。 它包含下列步驟：

1. [建立OSGI服](#creating-the-osgi-service) 務並將包含它的套件部署至AEM伺服器。
1. （可選）[發出JSON呼叫來請求用來建立主控台的JSON物件，以測試新服務](#testing-the-new-service)。
1. [通過擴展存](#displaying-the-new-column) 儲庫中控制台的節點結構來顯示新列。

>[!NOTE]
>
>本教學課程也可用來擴充下列管理控制台：
>
>* 數位資產主控台
>* 社群主控台

>



### 建立OSGI服務{#creating-the-osgi-service}

`ListInfoProvider`介面定義了兩種方法：

* `updateListGlobalInfo`，以更新清單的全局屬性，
* `updateListItemInfo`，以更新單一清單項目。

兩種方法的引數為：

* `request`，關聯的Sling HTTP請求物件，
* `info`，則JSON物件要更新，這分別是全域清單或目前清單項目，
* `resource`, a Sling resource.

實作範例如下：

* 新增每個項目的&#x200B;*starized*&#x200B;屬性，如果頁面名稱以&#x200B;*e*&#x200B;開頭，則為`false`。`true`

* 新增&#x200B;*stargedCount*&#x200B;屬性，此屬性是清單的全域屬性，並包含星號清單項目的數目。

要建立OSGI服務：

1. 在CRXDE Lite中，[建立包](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle)。
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
>* 如果您的`ListInfoProvider`實作定義了回應物件中已存在的屬性，則其值將被您提供的屬性覆寫。

>
>  
您可以使用[服務排名](https://www.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING)來管理多個`ListInfoProvider`實施的執行順序。

### 測試新服務{#testing-the-new-service}

當您開啟「網站管理」主控台並瀏覽您的網站時，瀏覽器會發出ajax呼叫，以取得用來建立主控台的JSON物件。 例如，當您瀏覽至`/content/geometrixx`檔案夾時，會傳送下列要求至AEM伺服器以建立主控台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

要確保新服務在部署包含該服務的包後正在運行：

1. 將您的瀏覽器指向下列URL:
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 響應應按如下方式顯示新屬性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 顯示新列{#displaying-the-new-column}

最後一個步驟是改變「網站管理」主控台的節點結構，以覆蓋`/libs/wcm/core/content/siteadmin`來顯示所有Geometrixx頁面的新屬性。 按如下步驟進行：

1. 在CRXDE Lite中，建立具有類型`sling:Folder`的節點的節點結構`/apps/wcm/core/content`以反映結構`/libs/wcm/core/content`。

1. 複製節點`/libs/wcm/core/content/siteadmin`並貼至`/apps/wcm/core/content`下方。

1. 將節點`/apps/wcm/core/content/siteadmin/grid/assets`複製到`/apps/wcm/core/content/siteadmin/grid/geometrixx`並更改其屬性：

   * 移除&#x200B;**pageText**

   * 將&#x200B;**pathRegex**&#x200B;設為`/content/geometrixx(/.*)?`
這會讓網格設定在所有幾何網站上都啟用。

   * 將&#x200B;**storeProxySuffix**&#x200B;設為`.pages.json`

   * 編輯&#x200B;**storeReaderFields**&#x200B;多值屬性並新增`starred`值。

   * 若要啟用MSM功能，請將下列MSM參數新增至多字串屬性&#x200B;**storeReaderFields**:

      * **msm:isSource**
      * **msm:isInBlueprint**
      * **msm:isLiveCopy**

1. 在`/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`下添加`starred`節點（類型&#x200B;**nt:unstructured**），並包含以下屬性：

   * **dataIndex**: `starred` 字串類型

   * **header**: `Starred` 字串類型

   * **xtype**: `gridcolumn` 字串類型

1. （可選）拖放您不想顯示在`/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`的欄

1. `/siteadmin` 是虛名的路徑，預設情況下指向 `/libs/wcm/core/content/siteadmin`。若要將此重新導向至您`/apps/wcm/core/content/siteadmin`上的網站管理員版本，請定義屬性`sling:vanityOrder`，使其值高於`/libs/wcm/core/content/siteadmin`上定義的值。 預設值為300，因此任何較高的值都適用。

1. 前往「網站管理」主控台，並導覽至Geometrixx網站：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 有名為&#x200B;**Stardered**&#x200B;的新欄可供使用，顯示自訂資訊如下：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多個網格配置與&#x200B;**pathRegex**&#x200B;屬性所定義的請求路徑匹配，則會使用第一個網格配置，而不是最具體的網格配置，這表示配置的順序很重要。

### 示例軟體包{#sample-package}

本教學課程的結果可在「套件共用」上的「自訂網站管理控制台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin)」套件中取得。[
