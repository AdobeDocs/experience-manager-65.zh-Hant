---
title: 新增Adobe Analytics追蹤至元件
seo-title: 新增Adobe Analytics追蹤至元件
description: 'null'
seo-description: 'null'
uuid: 447b140c-678c-428d-a1c9-ecbdec75cd42
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: a11c39b4-c23b-4207-8898-33aea25f2ad0
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 新增Adobe Analytics追蹤至元件{#adding-adobe-analytics-tracking-to-components}

## 將Adobe Analytics模組納入頁面元件 {#including-the-adobe-analytics-module-in-a-page-component}

頁面範本元件(例如 `head.jsp, body.jsp`)需要JSP包含才能載入ContextHub和Adobe Analytics整合（Cloud services的一部分）。 全部都包含載入JavaScript檔案。

ContextHub項目應立即包含在標 `<head>` 簽下方，而Cloud services應包含在 `<head>` 區段和 `</body>` 之前；例如：

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

在元 `contexthub` 素後插入的指令碼 `<head>` 會將ContextHub功能新增至頁面。

您 `cloudservices` 在和章節中添加的腳 `<head>` 本 `<body>` 適用於添加到頁面的雲服務配置。 （如果頁面使用多個雲端服務設定，則您只需要加入一次ContextHub jsp和Cloud Services jsp。）

將Adobe Analytics架構新增至頁面時，指令碼會產生 `cloudservices` Adobe Analytics相關的javascript和用戶端資料庫的參考，類似下列範例：

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

所有AEM範例網站（例如Geometrixx Outdoors）都包含此程式碼。

### sitecatalystAfterCollect事件 {#the-sitecatalystaftercollect-event}

指令 `cloudservices` 碼會觸發事 `sitecatalystAfterCollect` 件：

```
$CQ(document).trigger("sitecatalystAfterCollect");
```

此事件會觸發以指出頁面追蹤已完成。 如果您要在此頁面執行其他追蹤作業，則應監聽此事件，而非檔案載入或檔案就緒事件。 使用事件可 `sitecatalystAfterCollect` 避免衝突或其他無法預測的行為。

>[!NOTE]
>
>程式 `/libs/cq/analytics/clientlibs/sitecatalyst/sitecatalyst.js` 庫包含Adobe Analytics檔案中的程式 `s_code.js` 碼。

## 實作自訂元件的Adobe Analytics追蹤 {#implementing-adobe-analytics-tracking-for-custom-components}

讓您的AEM元件與Adobe Analytics架構互動。 然後，設定您的架構，讓Adobe Analytics追蹤元件資料。

當您編輯架構時，與Adobe Analytics架構互動的元件會出現在SideKick中。 將元件拖曳至架構後，會顯示元件屬性，然後您可以使用Adobe Analytics屬性來對應這些屬性。 (請參 [閱設定基本追蹤的架構](/help/sites-administering/adobeanalytics-connect.md#creating-a-adobe-analytics-framework))。

當元件具有名為的子節點時，元件可與Adobe Analytics架構互動 `analytics`。 節 `analytics` 點具有以下屬性：

* `cq:trackevents`:識別元件公開的CQ事件。 （請參閱自訂事件。）
* `cq:trackvars`:命名與Adobe Analytics屬性映射的CQ變數。
* `cq:componentName`:出現在Sidekick中的元件名稱。
* `cq:componentGroup`:Sidekick中包含元件的群組。

元件JSP中的程式碼會將javascript新增至觸發追蹤的頁面，並定義所追蹤的資料。 javascript中使用的事件名稱和資料名稱必須符合節點屬性的相 `analytics` 應值。

* 使用資料追蹤屬性，在頁面載入時追蹤事件資料。 (請參 [閱追蹤頁面載入上的自訂事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-on-page-load)。)
* 使用CQ_Analytics.record函式，在使用者與頁面功能互動時追蹤事件資料。 (請參 [閱「載入頁面後追蹤自訂事件](/help/sites-developing/extending-analytics.md#tracking-custom-events-after-page-load)」)。

當您使用這些資料追蹤方法時，Adobe Analytics整合模組會自動執行對Adobe Analytics的呼叫，以記錄事件和資料。

### 範例：追蹤頂導覽點按次數 {#example-tracking-topnav-clicks}

延伸基礎topnav元件，讓Adobe Analytics追蹤頁面頂端導覽連結的點按次數。 點按導覽連結時，Adobe Analytics會記錄已點按的連結及其點按的頁面。

以下過程要求您已執行下列任務：

* 已建立CQ應用程式。
* 已建立Adobe Analytics設定和Adobe Analytics Framework。

#### 複製topnav元件 {#copy-the-topnav-component}

將topnav元件複製至您的CQ應用程式。 該過程要求在CRXDE Lite中設定應用程式。

1. 按一下右鍵該節 `/libs/foundation/components/topnav` 點，然後按一下複製。
1. 按一下右鍵應用程式資料夾下的「元件」資料夾，然後按一下「貼上」。
1. 按一下「全部儲存」。

#### 整合Topnav與Adobe Analytics Framework {#integrating-topnav-with-the-adobe-analytics-framework}

設定topnav元件並編輯JSP檔案以定義追蹤事件和資料。

1. 按一下右鍵topnav節點，然後按一下「建立」>「建立節點」。 指定下列屬性值，然後按一下「確定」:

   * 名稱: `analytics`
   * 類型: `nt:unstructured`

1. 新增下列屬性至分析節點，以命名追蹤事件：

   * 名稱：cq:trackevents
   * 類型：字串
   * 值：topnavClick

1. 將下列屬性新增至分析節點，以命名資料變數：

   * 名稱：cq:trackvars
   * 類型：字串
   * 值：topnavTarget,topnavLocation

1. 將下列屬性新增至分析節點，以命名Sidekick的元件：

   * 名稱：cq:componentName
   * 類型：字串
   * 值：topnav（追蹤）

1. 將下列屬性新增至分析節點，以命名Sidekick的元件群組：

   * 名稱：cq:componentGroup
   * 類型：字串
   * 值：一般

1. 按一下「全部儲存」。
1. 開啟檔 `topnav.jsp` 案。
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

1. 按一下「全部儲存」。

檔案的內 `topnav.jsp` 容應如下所示：

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
>您通常希望從ContextHub追蹤資料。 如需使用javascript取得此資訊的詳細資訊，請參 [閱ContextHub中的存取值](/help/sites-developing/extending-analytics.md#accessing-values-in-the-contexthub)。

#### 新增追蹤元件至Sidekick {#adding-the-tracking-component-to-sidekick}

將啟用Adobe Analytics追蹤的元件新增至Sidekick，以便您將它們新增至架構。

1. 從Adobe Analytics設定開啟您的Adobe Analytics架構。 ([http://localhost:4502/etc/cloudservices/sitecatalyst.html](http://localhost:4502/etc/cloudservices/sitecatalyst.html))
1. 在Sidekick上，按一下「設計」按鈕。

   ![](assets/chlimage_1a.png)

1. 在「連結追蹤設定」區域中，按一下「設定繼承」。

   ![chlimage_1](assets/chlimage_1aa.png)

1. 在「允許的元件」清單中，選取「一般」區段中的topnav（追蹤），然後按一下「確定」。
1. 展開Sidekick以進入編輯模式。 現在，「常規」組中提供該元件。

#### 將topnav元件新增至您的架構 {#adding-the-topnav-component-to-your-framework}

將topnav元件拖曳至Adobe Analytics架構，並將元件變數和事件對應至Adobe Analytics變數和事件。 (請參 [閱設定基本追蹤的架構](/help/sites-administering/adobeanalytics-connect.md))。

![chlimage_1-1](assets/chlimage_1-1a.png)

topnav元件現在已與Adobe Analytics架構整合。 將元件新增至頁面時，按一下頂端導覽列中的項目會將追蹤資料傳送至Adobe Analytics。

### 傳送s.products資料至Adobe Analytics {#sending-s-products-data-to-adobe-analytics}

元件可產生傳送至Adobe Analytics的s.products變數的資料。 設計您的元件，以提供s.products變數：

* 記錄名為特 `product` 定結構的值。
* 公開值的資料成 `product` 員，以便與Adobe Analytics架構中的Adobe Analytics變數對應。

Adobe Analytics s.products變數使用下列語法：

```
s.products="category;product;quantity;price;eventY={value}|eventZ={value};evarA={value}|evarB={value}"
```

Adobe Analytics整合模組會使用AEM `s.products` 元件產生的 `product` 值來建構變數。 AEM `product` 元件產生的javascript值是具有下列結構的值陣列：

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

當資料項目從值中省略 `product` 時，會以空字串的形式在s.products中傳送。

>[!NOTE]
>
>當沒有事件與產品值相關聯時，Adobe Analytics會依預設使 `prodView` 用事件。

組 `analytics` 件的節點必須使用以下屬性公開變數 `cq:trackvars` 名稱：

* product.category
* product.sku
* product.quantity
* product.price
* product.events.eventName1
* product.events.eventName_n
* product.evars.eVarName1
* product.evars.eVarName_n

eCommerce模組提供數個產生s.products變數資料的元件。 例如，提交順序元件([http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp](http://localhost:4502/crx/de/index.jsp#/libs/commerce/components/submitorder/submitorder.jsp))生成與以下示例類似的javascript:

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

一般而言，網頁瀏覽器會限制GET要求的大小。 由於CQ產品和SKU值是儲存庫路徑，因此包含多個值的產品陣列可能會超過請求大小限制。 因此，您的元件應限制每個元件陣列中 `product` 的項目數 `CQ_Analytics.record function`。 如果您需要追蹤的項目數量超過限制，請建立多個函式。

例如，電子商務提交訂單元件將呼叫中 `product` 的項目數限制為4。 當購物車包含4種以上的產品時，它會產生多種 `CQ_Analytics.record` 功能。
