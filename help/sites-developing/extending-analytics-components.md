---
title: 將Adobe Analytics跟蹤添加到元件
seo-title: Adding Adobe Analytics Tracking to Components
description: 將Adobe Analytics跟蹤添加到元件
seo-description: null
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
exl-id: e6c1258c-81d5-48e4-bdf1-90d7cc13a22d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# 將Adobe Analytics跟蹤添加到元件{#adding-adobe-analytics-tracking-to-components}

## 在頁面元件中包括Adobe Analytics模組 {#including-the-adobe-analytics-module-in-a-page-component}

頁面模板元件(例如 `head.jsp, body.jsp`)需要JSP來載入ContextHub和Adobe Analytics整合(這是Cloud Services的一部分)。 所有內容都包括載入JavaScript檔案。

ContextHub條目應包括在 `<head>` 標籤，而Cloud Services應包含在 `<head>` 在 `</body>` 部分；例如：

```xml
<head>
   <sling:include path="contexthub" resourceType="granite/contexthub/components/contexthub" />
...
   <cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
...
</head>
<body>
...
    <cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
</body>
```

的 `contexthub` 在其後插入的指令碼 `<head>` 元素將ContextHub功能添加到頁面。

的 `cloudservices` 添加到中的指令碼 `<head>` 和 `<body>` 節適用於添加到頁面的雲服務配置。 (如果頁面使用多個Cloud Services配置，則只需包含一次ContextHub jsp和Cloud Servicesjsp。)

將Adobe Analytics框架添加到頁面時， `cloudservices` 指令碼生成與Adobe Analytics相關的javascript和對客戶端庫的引用，與以下示例類似：

```xml
<div class="sitecatalyst cloudservice">
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/util.js"></script>
<script type="text/javascript" src="/content/geometrixx-outdoors/_jcr_content/analytics.sitecatalyst.js"></script>
<script type="text/javascript" src="/etc/clientlibs/mac/mac-sc.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/sitecatalyst/plugins.js"></script>
<script type="text/javascript">
<!--
CQ_Analytics.Sitecatalyst.frameworkComponents = ['foundation/components/page'];
/**
 * Sets Adobe Analytics variables accordingly to mapped components. If <code>options</code>
 * object is provided only variables matching the options.componentPath are set.
 *
 * @param {Object} options Parameter object from CQ_Analytics.record() call. Optional.
 */
CQ_Analytics.Sitecatalyst.updateEvars = function(options) {
    this.frameworkMappings = [];
 this.frameworkMappings.push({scVar:"pageName",cqVar:"pagedata.title",resourceType:"foundation/components/page"});
    for (var i=0; i<this.frameworkMappings.length; i++){
  var m = this.frameworkMappings[i];
  if (!options || options.compatibility || (options.componentPath == m.resourceType)) {
   CQ_Analytics.Sitecatalyst.setEvar(m);
  }
    }
}

CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
 var collect = true;
    var lte = s.linkTrackEvents;
    s.pageName="content:geometrixx-outdoors:en";
    CQ_Analytics.Sitecatalyst.collect(collect);
    if (collect) {
  CQ_Analytics.Sitecatalyst.updateEvars();
     /************* DO NOT ALTER ANYTHING BELOW THIS LINE ! **************/
     var s_code=s.t();if(s_code)document.write(s_code);
     s.linkTrackEvents = lte;
     if(s.linkTrackVars.indexOf('events')==-1){delete s.events};
     $CQ(document).trigger("sitecatalystAfterCollect");
    }
});
//-->
</script>
<script type="text/javascript">
<!--
if(navigator.appVersion.indexOf('MSIE')>=0)document.write(unescape('%3C')+'\!-'+'-')
//-->
</script>
<noscript><img src="https://daydocumentation.112.2o7.net/b/ss/daydocumentation/1/H.25--NS/1380120772954?cdp=3&gn=content%3Ageometrixx-outdoors%3Aen" height="1" width="1" border="0" alt=""/></noscript>
<span data-tracking="{event:'pageView', values:{}, componentPath:'foundation/components/page'}"></span>
<div id="cq-analytics-texthint" style="background:white; padding:0 10px; display:none;">
 <h3 class="cq-texthint-placeholder">Component clientcontext is missing or misplaced.</h3>
</div>
<script type="text/javascript">
$CQ(function(){
 if( CQ_Analytics &&
  CQ_Analytics.ClientContextMgr &&
  !CQ_Analytics.ClientContextMgr.isConfigLoaded )
  {
   $CQ("#cq-analytics-texthint").show();
  }
});
</script>
</div>
```

所有示AEM例站點(如Geometrixx Outdoors)都包含此代碼。

### sitecalystAfterCollect事件 {#the-sitecatalystaftercollect-event}

的 `cloudservices` 指令碼觸發器 `sitecatalystAfterCollect` 事件：

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

觸發此事件以指示已完成頁面跟蹤。 如果要在此頁面上執行其他跟蹤操作，則應偵聽此事件，而不是文檔載入或文檔就緒事件。 使用 `sitecatalystAfterCollect` 事件可避免衝突或其他不可預知的行為。

>[!NOTE]
>
>的 `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` 圖書館裡有Adobe Analytics `s_code.js` 的子菜單。

## 實施Adobe Analytics定制元件跟蹤 {#implementing-adobe-analytics-tracking-for-custom-components}

使元件AEM能夠與Adobe Analytics框架交互。 然後，配置框架，以便Adobe Analytics跟蹤元件資料。

在編輯框架時，與Adobe Analytics框架交互的元件將出現在SideKick中。 將元件拖到框架後，將顯示元件屬性，然後可以使用Adobe Analytics屬性映射它們。 (請參閱 [設定基本跟蹤框架](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework)。)

當元件具有名為的子節點時，元件可以與Adobe Analytics框架交互 `analytics`。 的 `analytics` 節點具有以下屬性：

* `cq:trackevents`:標識元件公開的CQ事件。 （請參閱自定義事件。）
* `cq:trackvars`:命名與Adobe Analytics屬性映射的CQ變數。
* `cq:componentName`:出現在Sidekick中的元件的名稱。
* `cq:componentGroup`:Sidekick中包含該元件的組。

元件JSP中的代碼將javascript添加到觸發跟蹤的頁面，並定義跟蹤的資料。 Javascript中使用的事件名稱和資料名稱必須與 `analytics` 節點屬性。

* 使用資料跟蹤屬性在載入頁面時跟蹤事件資料。 (請參閱 [跟蹤頁面載入上的自定義事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load)。)
* 使用CQ_Analytics.record函式在用戶與頁面功能交互時跟蹤事件資料。 (請參閱 [載入頁後跟蹤自定義事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load)。)

使用這些資料跟蹤方法時，Adobe Analytics整合模組會自動執行對Adobe Analytics的呼叫，以記錄事件和資料。

### 示例：跟蹤頂部導航按一下 {#example-tracking-topnav-clicks}

擴展基礎頂部導航元件，以便Adobe Analytics跟蹤頁面頂部導航連結的按一下。 按一下導航連結時，Adobe Analytics會記錄按一下的連結以及按一下該連結的頁面。

以下過程要求您已執行以下任務：

* 已建立CQ應用程式。
* 已建立Adobe Analytics配置和Adobe Analytics框架。

#### 複製頂部導航元件 {#copy-the-topnav-component}

將topnav元件複製到CQ應用程式。 此過程要求在CRXDE Lite中設定應用程式。

1. 按一下右鍵 `/libs/foundation/components/topnav` ，然後按一下「複製」。
1. 按一下右鍵應用程式資料夾下的「元件」資料夾，然後按一下「貼上」。
1. 按一下「全部保存」。

#### 將topnav與Adobe Analytics框架整合 {#integrating-topnav-with-the-adobe-analytics-framework}

配置topnav元件並編輯JSP檔案以定義跟蹤事件和資料。

1. 按一下右鍵頂部導航節點，然後按一下「建立」>「建立節點」。 指定以下屬性值，然後按一下確定：

   * 名稱: `analytics`
   * 類型: `nt:unstructured`

1. 將以下屬性添加到分析節點以命名跟蹤事件：

   * 名稱：cq：跟蹤事件
   * 類型：字串
   * 值：topnav按一下

1. 將以下屬性添加到分析節點以命名資料變數：

   * 名稱：cq：跟蹤
   * 類型：字串
   * 值：topnavTarget,topnavLocation

1. 將以下屬性添加到分析節點以為Sidekick的元件命名：

   * 名稱：cq：元件名稱
   * 類型：字串
   * 值：topnav（跟蹤）

1. 將以下屬性添加到分析節點以為Sidekick的元件組命名：

   * 名稱：cq：元件組
   * 類型：字串
   * 值：常規

1. 按一下「全部保存」。
1. 開啟 `topnav.jsp` 的子菜單。
1. 在元素中，添加以下屬性：

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. 在頁面底部添加以下javascript代碼：

   ```xml
   <script type="text/javascript">
       function tracknav(target) {
               if (CQ_Analytics.Sitecatalyst) {
                   CQ_Analytics.record({
                       event: 'topnavClick',
                       values: {
                           topnavTarget: target,
                           topnavLocation:'<%=currentPage.getPath() %>.html'
                       },
                       componentPath: '<%=resource.getResourceType()%>'
                   });
               }
       }
   </script>
   ```

1. 按一下「全部保存」。

內容 `topnav.jsp` 檔案應如下所示：

```xml
<%@page session="false"%><%--
  Copyright 1997-2008 Day Management AG
  Barfuesserplatz 6, 4001 Basel, Switzerland
  All Rights Reserved.

  This software is the confidential and proprietary information of
  Day Management AG, ("Confidential Information"). You shall not
  disclose such Confidential Information and shall use it only in
  accordance with the terms of the license agreement you entered into
  with Day.

  ==============================================================================

  Top Navigation component

  Draws the top navigation

--%><%@include file="/libs/foundation/global.jsp"%><%
%><%@ page import="java.util.Iterator,
        com.day.text.Text,
        com.day.cq.wcm.api.PageFilter,
        com.day.cq.wcm.api.Page,
        com.day.cq.commons.Doctype,
        org.apache.commons.lang3.StringEscapeUtils" %><%

    // get starting point of navigation
    long absParent = currentStyle.get("absParent", 2L);
    String navstart = Text.getAbsoluteParent(currentPage.getPath(), (int) absParent);

    //if not deep enough take current node
    if (navstart.equals("")) navstart=currentPage.getPath();

    Resource rootRes = slingRequest.getResourceResolver().getResource(navstart);
    Page rootPage = rootRes == null ? null : rootRes.adaptTo(Page.class);
    String xs = Doctype.isXHTML(request) ? "/" : "";
    if (rootPage != null) {
        Iterator<Page> children = rootPage.listChildren(new PageFilter(request));
        while (children.hasNext()) {
            Page child = children.next();
            %><a onclick = "tracknav('<%= child.getPath() %>.html')"  href="<%= child.getPath() %>.html"><%
            %><img alt="<%= StringEscapeUtils.escapeXml(child.getTitle()) %>" src="<%= child.getPath() %>.navimage.png"<%= xs %>></a><%
        }
    }
%><script type="text/javascript">
    function tracknav(target) {
            if (CQ_Analytics.Sitecatalyst) {
                CQ_Analytics.record({
                    event: 'topnavClick',
                    values: {
                        topnavTarget:target,
                        topnavLocation:'<%=currentPage.getPath() %>.html'
                    },
                    componentPath: '<%=resource.getResourceType()%>'
                });
            }
    }
</script>
```

>[!NOTE]
>
>通常最好從ContextHub跟蹤資料。 有關使用javascript獲取此資訊的資訊，請參見 [訪問ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。

#### 將跟蹤元件添加到Sidekick {#adding-the-tracking-component-to-sidekick}

將啟用用於跟蹤Adobe Analytics的元件添加到Sidekick中，以便您可以將它們添加到框架中。

1. 從您的Adobe Analytics配置中開啟您的Adobe Analytics框架。 ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. 在Sidekick上，按一下Design按鈕。

   ![](assets/chlimage_1a.png)

1. 在「鏈路跟蹤配置」區域，按一下「配置繼承」。

   ![chlimage_1](assets/chlimage_1aa.png)

1. 在「允許的元件」清單中，在「常規」部分選擇topnav（跟蹤），然後按一下「確定」。
1. 展開Sidek以進入編輯模式。 該元件現在在「一般」組中可用。

#### 將topnav元件添加到框架 {#adding-the-topnav-component-to-your-framework}

將topnav元件拖到Adobe Analytics框架，並將元件變數和事件映射到Adobe Analytics變數和事件。 (請參閱 [設定基本跟蹤框架](/help/sites-administering/adobeanalytics-connect.md)。)

![chlimage_1-1](assets/chlimage_1-1a.png)

頂部導航元件現在與Adobe Analytics框架整合。 將元件添加到頁面時，按一下頂部導航欄中的項會將跟蹤資料發送到Adobe Analytics。

### 將s.products資料發送到Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

元件可以為發送到Adobe Analytics的s.products變數生成資料。 設計元件以幫助s.products變數：

* 記錄名為 `product` 具體結構。
* 公開 `product` 值，以便在Adobe Analytics框架中用Adobe Analytics變數映射。

Adobe Analytics的s.products變數使用以下語法：

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics整合模組構建 `s.products` 變數使用 `product` 元件生AEM成的值。 的 `product` 元件生成AEM的javascript中的值是具有以下結構的值陣列：

```
"product": [{
    "category": "",
    "sku"     : "path to product node",
    "quantity": quantity,
    "price"   : price,
    "events   : {
      "eventName1": "eventValue1",
      "eventName_n": "eventValue_n"
    }
    "evars"   : {
      "eVarName1": "eVarValue1",
      "eVarName_n": "eVarValue_n"
    }
}]
```

當資料項從 `product` 值，它在s.products中作為空字串發送。

>[!NOTE]
>
>當沒有事件與產品值關聯時，Adobe Analytics使用 `prodView` 事件。

的 `analytics` 元件的節點必須使用 `cq:trackvars` 屬性：

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

電子商務模組提供了幾個生成s.products變數資料的元件。 例如，提交訂單元件([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp))生成與以下示例類似的javascript:

```
<script type="text/javascript">
    function trackCartPurchase() {
        if (CQ_Analytics.Sitecatalyst) {
            CQ_Analytics.record({
                "event": ["productsCartPurchase"],
                "values": {
                    "product": [
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/1",
                            "quantity": 3,
                            "price"   : 179.7,
                            "evars"   : {
                                "childSku": "/path/to/prod/1/green/xs",
                                "size"    : "XS"
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/2",
                            "quantity": 10,
                            "price"   : 150,
                            "evars"   : {
                                "childSku": "/path/to/prod/2",
                                "size"    : ""
                            }
                        },
                        {
                            "category": "",
                            "sku"     : "/path/to/prod/3",
                            "quantity": 2,
                            "price"   : 102,
                            "evars"   : {
                                "childSku": "/path/to/prod/3/m",
                                "size"    : "M"
                            }
                        }
                    ]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["discountRedemption"],
                "values": {
                    "discount": "/path/to/discount/1 - /path/to/discount/2",
                    "product" : [{
                        "category": "",
                        "sku"     : "Promotional Discount",
                        "events"  : {"discountRedemption": 20.00}
                    }]
                },
                "componentPath": "commerce/components/submitorder"
            });
            CQ_Analytics.record({
                "event": ["cartPurchase"],
                "values": {
                    "orderId"       : "00e40e2d-13a2-4a00-a8ee-01a9ebb0bf68",
                    "shippingMethod": "overnight",
                    "paymentMethod" : "Amex",
                    "billingState"  : "NY",
                    "billingZip"    : "10458",
                    "product"       : [{"category": "", "sku": "", "quantity": "", "price": ""}]
                },
                "componentPath": "commerce/components/submitorder"
            });
        }
        return true;
    }
</script>
```

#### 限制跟蹤呼叫的大小 {#limiting-the-size-of-tracking-calls}

通常，Web瀏覽器會限制GET請求的大小。 由於CQ產品和SKU值是儲存庫路徑，因此包含多個值的產品陣列可能超過請求大小限制。 因此，元件應限制 `product` 每個 `CQ_Analytics.record function`。 如果需要跟蹤的項數可能超過限制，則建立多個函式。

例如，電子商務提交訂單元件限制 `product` 4號呼叫中的項目。 當購物車包含四個以上的產品時，它將生成多個 `CQ_Analytics.record` 的子菜單。
