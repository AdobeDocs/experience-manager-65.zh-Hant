---
title: 將Adobe Analytics追蹤新增至元件
seo-title: Adding Adobe Analytics Tracking to Components
description: 將Adobe Analytics追蹤新增至元件
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

# 將Adobe Analytics追蹤新增至元件{#adding-adobe-analytics-tracking-to-components}

## 在頁面元件中納入Adobe Analytics模組 {#including-the-adobe-analytics-module-in-a-page-component}

頁面範本元件(例如 `head.jsp, body.jsp`)需要JSP包含，才能載入ContextHub和Adobe Analytics整合(這是Cloud Services的一部分)。 全部包含載入JavaScript檔案。

ContextHub項目應緊接在 `<head>` 標籤，而Cloud Services應包含在 `<head>` 和之前 `</body>` 部分；例如：

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

此 `contexthub` 在 `<head>` 元素會將ContextHub功能新增至頁面。

此 `cloudservices` 您新增到 `<head>` 和 `<body>` 區段會套用至新增至頁面的雲端服務設定。 (如果頁面使用多個Cloud Services配置，則只需包含ContextHub jsp和Cloud Servicesjsp一次。)

將Adobe Analytics架構新增至頁面時， `cloudservices` 指令碼會產生Adobe Analytics相關的javascript和用戶端程式庫的參考，類似於下列範例：

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

所有AEM範例網站(例如Geometrixx Outdoors)都包含此程式碼。

### sitecatalystAfterCollect事件 {#the-sitecatalystaftercollect-event}

此 `cloudservices` 指令碼觸發 `sitecatalystAfterCollect` 事件：

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

此事件會觸發，指出頁面追蹤已完成。 如果您要在此頁面上執行其他追蹤操作，則應監聽此事件，而不是檔案載入或檔案就緒事件。 使用 `sitecatalystAfterCollect` 事件可避免衝突或其他無法預測的行為。

>[!NOTE]
>
>此 `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` 程式庫包含Adobe Analytics中的程式碼 `s_code.js` 檔案。

## 為自訂元件實作Adobe Analytics追蹤 {#implementing-adobe-analytics-tracking-for-custom-components}

啟用AEM元件以與Adobe Analytics架構互動。 接著，設定您的架構，讓Adobe Analytics追蹤元件資料。

編輯架構時，與Adobe Analytics架構互動的元件會顯示在SideKick中。 將元件拖曳至架構後，元件屬性隨即顯示，您可以使用Adobe Analytics屬性對應元件。 (請參閱 [設定基本追蹤的架構](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework).)

元件具有名為的子節點時，元件可與Adobe Analytics架構互動 `analytics`. 此 `analytics` 節點具有以下屬性：

* `cq:trackevents`:識別元件公開的CQ事件。 （請參閱自訂事件。）
* `cq:trackvars`:為與Adobe Analytics屬性對應的CQ變數命名。
* `cq:componentName`:出現在Sidekick中的元件的名稱。
* `cq:componentGroup`:Sidekick中包含元件的群組。

元件JSP中的代碼將javascript添加到觸發跟蹤的頁面，並定義所跟蹤的資料。 Javascript中使用的事件名稱和資料名稱必須符合 `analytics` 節點屬性。

* 使用資料追蹤屬性來追蹤頁面載入時的事件資料。 (請參閱 [在頁面載入時追蹤自訂事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load).)
* 使用CQ_Analytics.record函式，在使用者與頁面功能互動時追蹤事件資料。 (請參閱 [在頁面載入後追蹤自訂事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load).)

使用這些資料追蹤方法時，Adobe Analytics整合模組會自動執行對Adobe Analytics的呼叫，以記錄事件和資料。

### 範例：追蹤頂端導覽點按次數 {#example-tracking-topnav-clicks}

擴充foundation topnav元件，讓Adobe Analytics可追蹤頁面頂端導覽連結上的點按次數。 按一下導覽連結時，Adobe Analytics會記錄已點按的連結及其點按的頁面。

以下過程要求您已執行以下任務：

* 建立CQ應用程式。
* 建立Adobe Analytics設定和Adobe Analytics架構。

#### 複製頂端導覽元件 {#copy-the-topnav-component}

將topnav元件複製到CQ應用程式。 該過程要求以CRXDE Lite設定應用程式。

1. 以滑鼠右鍵按一下 `/libs/foundation/components/topnav` 節點，然後按一下「複製」。
1. 以滑鼠右鍵按一下應用程式資料夾下的「元件」資料夾，然後按一下「貼上」。
1. 按一下「全部儲存」 。

#### 將Topnav與Adobe Analytics架構整合 {#integrating-topnav-with-the-adobe-analytics-framework}

配置topnav元件並編輯JSP檔案以定義跟蹤事件和資料。

1. 以滑鼠右鍵按一下頂端導覽節點，然後按一下「建立>建立節點」。 指定下列屬性值，然後按一下「確定」：

   * 名稱: `analytics`
   * 類型: `nt:unstructured`

1. 將下列屬性新增至分析節點，以命名追蹤事件：

   * 名稱：cq:trackevents
   * 類型：字串
   * 值：topnavClick

1. 將下列屬性新增至分析節點，以命名資料變數：

   * 名稱：cq:trackvars
   * 類型：字串
   * 值：topnavTarget,topnavLocation

1. 將下列屬性新增至分析節點，以為Sidekick的元件命名：

   * 名稱：cq:componentName
   * 類型：字串
   * 值：topnav（追蹤）

1. 將下列屬性新增至分析節點，以為Sidekick的元件群組命名：

   * 名稱：cq:componentGroup
   * 類型：字串
   * 值：一般

1. 按一下「全部儲存」 。
1. 開啟 `topnav.jsp` 檔案。
1. 在元素中，新增下列屬性：

   ```xml
   onclick = "tracknav('<%= child.getPath() %>.html')"
   ```

1. 在頁面底部新增下列javascript程式碼：

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

1. 按一下「全部儲存」 。

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
>通常需要從ContextHub追蹤資料。 如需使用javascript取得此資訊的相關資訊，請參閱 [存取ContextHub中的值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub).

#### 將追蹤元件新增至Sidekick {#adding-the-tracking-component-to-sidekick}

新增已啟用以透過Adobe Analytics追蹤的元件至Sidekick，以便您將其新增至架構。

1. 從Adobe Analytics設定開啟Adobe Analytics架構。 ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. 在Sidekick上，按一下「設計」按鈕。

   ![](assets/chlimage_1a.png)

1. 在「連結追蹤設定」區域中，按一下「設定繼承」。

   ![chlimage_1](assets/chlimage_1aa.png)

1. 在「允許的元件」清單中，選取「一般」區段中的頂端導覽（追蹤），然後按一下「確定」。
1. 展開Sidekick以進入編輯模式。 元件現在可在「一般資訊」組中使用。

#### 將topnav元件新增至架構 {#adding-the-topnav-component-to-your-framework}

將頂端導覽元件拖曳至Adobe Analytics架構，並將元件變數和事件對應至Adobe Analytics變數和事件。 (請參閱 [設定基本追蹤的架構](/help/sites-administering/adobeanalytics-connect.md).)

![chlimage_1-1](assets/chlimage_1-1a.png)

topnav元件現已與Adobe Analytics架構整合。 將元件新增至頁面時，按一下頂端導覽列中的項目會將追蹤資料傳送至Adobe Analytics。

### 傳送s.products資料至Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

元件可產生傳送至Adobe Analytics之s.products變數的資料。 設計您的元件以貢獻s.products變數：

* 記錄名為 `product` 特定結構。
* 公開 `product` 值，以便與Adobe Analytics架構中的Adobe Analytics變數對應。

Adobe Analytics s.products變數使用下列語法：

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics整合模組建構 `s.products` 變數，使用 `product` AEM元件所產生的值。 此 `product` AEM元件所產生的javascript中的值是具有下列結構的值陣列：

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

若從 `product` 值，則會以s.products中的空字串形式傳送。

>[!NOTE]
>
>當沒有任何事件與產品值相關聯時，Adobe Analytics會使用 `prodView` 事件。

此 `analytics` 元件的節點必須使用 `cq:trackvars` 屬性：

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

電子商務模組提供數個元件，可產生s.products變數資料。 例如，提交訂單元件([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp))會產生與下列範例類似的javascript:

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

#### 限制追蹤呼叫的大小 {#limiting-the-size-of-tracking-calls}

一般而言，網頁瀏覽器會限制GET要求的大小。 由於CQ產品和SKU值是存放庫路徑，因此包含多個值的產品陣列可能會超過要求大小限制。 因此，元件應限制 `product` 每個 `CQ_Analytics.record function`. 如果您需要追蹤的項目數可能超過限制，請建立多個函式。

例如，電子商務提交訂單元件會限制 `product` 對四的呼叫中的項目。 當購物車包含超過四項產品時，會產生多項 `CQ_Analytics.record` 函式。
