---
title: 自訂網站主控台（傳統UI）
description: 網站管理控制檯可以延伸以顯示自訂欄
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 2b9b4857-821c-4f2f-9ed9-78a1c9f5ac67
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# 自訂網站主控台（傳統UI）{#customizing-the-websites-console-classic-ui}

## 新增自訂欄到網站(siteadmin)主控台 {#adding-a-custom-column-to-the-websites-siteadmin-console}

可延伸網站管理主控台以顯示自訂欄。 主控台是根據JSON物件建置的，可透過建立OSGI服務來實作 `ListInfoProvider` 介面。 此類服務會修改傳送至使用者端的JSON物件，以建置主控台。

此逐步教學課程說明如何透過實作「 」，在「網站管理」主控台中顯示新欄。 `ListInfoProvider` 介面。 此教學課程包含下列步驟：

1. [建立OSGI服務](#creating-the-osgi-service) 並將包含該檔案包的套件部署至AEM伺服器。
1. （選擇性） [測試新服務](#testing-the-new-service) 藉由發出JSON呼叫以請求用來建置主控台的JSON物件。
1. [顯示新欄](#displaying-the-new-column) 藉由擴充存放庫中主控台的節點結構。

>[!NOTE]
>
>本教學課程也可用來擴充下列管理主控台：
>
>* 數位資產主控台
>* 社群主控台
>

### 建立OSGI服務 {#creating-the-osgi-service}

此 `ListInfoProvider` 介面會定義兩種方法：

* `updateListGlobalInfo`，更新清單的全域屬性，
* `updateListItemInfo`，以更新單一清單專案。

這兩種方法的引數為：

* `request`，相關聯的Sling HTTP要求物件，
* `info`，此為要更新的JSON物件，分別為全域清單或目前清單專案，
* `resource`，Sling資源。

實作範例如下：

* 新增 *星號* 每個專案的屬性，也就是 `true` 如果頁面名稱開頭為 *è*、和 `false` 否則。

* 新增 *starredCount* 屬性，此屬性是清單的全域屬性，包含星級清單專案的數目。

若要建立OSGI服務：

1. 在CRXDE Lite中， [建立套件組合](/help/sites-developing/developing-with-crxde-lite.md#managing-a-bundle).
1. 在下方新增範常式式碼。
1. 建立套件組合。

新服務已啟動且執行中。

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
>* 您的實作應根據提供的請求和/或資源，決定是否應將資訊新增至JSON物件。
>* 若您的 `ListInfoProvider` 實施會定義回應物件中存在的屬性，其值會由您提供的值覆寫。
>
>  您可以使用 [服務排名](https://docs.osgi.org/javadoc/r2/org/osgi/framework/Constants.html#SERVICE_RANKING) 若要管理多個專案的執行順序 `ListInfoProvider` 實作。

### 測試新服務 {#testing-the-new-service}

當您開啟網站管理主控台並瀏覽您的網站時，瀏覽器會發出Ajax呼叫以取得用來建置主控台的JSON物件。 例如，當您瀏覽至 `/content/geometrixx` 資料夾中，下列請求會傳送至AEM伺服器以建置主控台：

[https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

若要確定新服務在部署包含該服務的套件組合後仍在執行：

1. 將瀏覽器指向下列URL：
   [https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin](https://localhost:4502/content/geometrixx.pages.json?start=0&amp;limit=30&amp;predicate=siteadmin)

1. 回應應依照以下方式顯示新屬性：

![screen_shot_2012-02-13at163046](assets/screen_shot_2012-02-13at163046.png)

### 顯示新欄 {#displaying-the-new-column}

最後一個步驟包含調整網站管理主控台的節點結構，透過覆蓋來顯示所有Geometrixx頁面的新屬性 `/libs/wcm/core/content/siteadmin`. 請依照下列步驟進行：

1. 在CRXDE Lite中，建立節點結構 `/apps/wcm/core/content` 具有型別節點 `sling:Folder` 以反映結構 `/libs/wcm/core/content`.

1. 複製節點 `/libs/wcm/core/content/siteadmin` 並在下方貼上 `/apps/wcm/core/content`.

1. 複製節點 `/apps/wcm/core/content/siteadmin/grid/assets` 至 `/apps/wcm/core/content/siteadmin/grid/geometrixx` 並變更其屬性：

   * 移除 **pageText**

   * 設定 **pathRegex** 至 `/content/geometrixx(/.*)?`
如此一來，所有Geometrixx網站的網格設定都會生效。

   * 設定 **storeProxySuffix** 至 `.pages.json`

   * 編輯 **storeReaderFields** 多值屬性並新增 `starred` 值。

   * 若要啟用MSM功能，請將下列MSM引數新增至多字串屬性 **storeReaderFields**：

      * **msm：isSource**
      * **msm：isInBlueprint**
      * **msm：isLiveCopy**

1. 新增 `starred` 節點（型別） **nt：unstructured**)下 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns` 具有以下屬性：

   * **dataIndex**： `starred` 型別為String

   * **頁首**： `Starred` 型別為String

   * **xtype**： `gridcolumn` 型別為String

1. （選擇性）拖放您不想要顯示的欄 `/apps/wcm/core/content/siteadmin/grid/geometrixx/columns`

1. `/siteadmin` 是虛名路徑，預設會指向 `/libs/wcm/core/content/siteadmin`.
若要將此重新導向至您在上的網站管理員版本 `/apps/wcm/core/content/siteadmin`，定義屬性 `sling:vanityOrder` ，使其值高於上定義的 `/libs/wcm/core/content/siteadmin`. 預設值為300，因此適用更高的值。

1. 前往「網站管理」主控台，並導覽至Geometrixx網站：
   [https://localhost:4502/siteadmin#/content/geometrixx](https://localhost:4502/siteadmin#/content/geometrixx).

1. 名為的新欄 **星號** 可用，依下列方式顯示自訂資訊：

![screen_shot_2012-02-14at104602](assets/screen_shot_2012-02-14at104602.png)

>[!CAUTION]
>
>如果多個格線設定符合由定義的請求路徑 **pathRegex** 屬性使用，但不會使用最具體的屬性，這表示設定的順序很重要。

### 範例套件 {#sample-package}

本教學課程的結果可在以下網址取得： [自訂網站管理主控台](https://localhost:4502/crx/packageshare/index.html/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/helper/customizing-siteadmin) 封裝共用。
