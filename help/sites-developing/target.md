---
title: 針對目標內容進行開發
seo-title: 針對目標內容進行開發
description: 有關開發元件以搭配內容定位的主題
seo-description: 有關開發元件以搭配內容定位的主題
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5

---


# 針對目標內容進行開發{#developing-for-targeted-content}

本節說明有關開發與內容定位搭配使用的元件的主題。

* 如需有關連線Adobe Target的詳細資訊，請參 [閱與Adobe Target整合](/help/sites-administering/target.md)。
* 如需製作目標內容的詳細資訊，請參閱「使 [用目標模式製作目標內容」](/help/sites-authoring/content-targeting-touch.md)。

>[!NOTE]
>
>當您在AEM作者中定位元件時，元件會對Adobe Target進行一連串的伺服器端呼叫，以註冊促銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 AEM發佈至Adobe Target時，不會進行伺服器端呼叫。

## 在您的頁面上使用Adobe target啟用定位 {#enabling-targeting-with-adobe-target-on-your-pages}

若要在頁面中使用與Adobe target互動的目標元件，請在&lt;head>元素中加入特定用戶端程式碼。

### 標題區 {#the-head-section}

將下列兩個程式碼區塊新增至頁面的&lt;head>區段：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此程式碼會新增必要的分析javascript物件，並載入與網站相關的雲端服務程式庫。 對於Target服務，程式庫會透過 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

載入的程式庫集會視Target組態所使用的目標用戶端程式庫（mbox.js或at.js）類型而定：

**針對預設mbox.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**針對自訂mbox.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**For at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>僅支援隨 `at.js` 附產品的版本。 您可在 `at.js` 以下位置查看檔案，以取得產品隨附 `at.js` 的版本：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**針對自訂at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

用戶端的Target功能由物件管 `CQ_Analytics.TestTarget` 理。 因此，該頁將包含一些init代碼，如以下示例：

```
<script type="text/javascript">
            if ( !window.CQ_Analytics ) {
                window.CQ_Analytics = {};
            }
            if ( !CQ_Analytics.TestTarget ) {
                CQ_Analytics.TestTarget = {};
            }
            CQ_Analytics.TestTarget.clientCode = 'my_client_code';
        </script>
      ...

    <div class="cloudservice testandtarget">
  <script type="text/javascript">
  CQ_Analytics.TestTarget.maxProfileParams = 11;

  if (CQ_Analytics.CCM) {
   if (CQ_Analytics.CCM.areStoresInitialized) {
    CQ_Analytics.TestTarget.registerMboxUpdateCalls();
   } else {
    CQ_Analytics.CCM.addListener("storesinitialize", function (e) {
     CQ_Analytics.TestTarget.registerMboxUpdateCalls();
    });
   }
  } else {
   // client context not there, still register calls
   CQ_Analytics.TestTarget.registerMboxUpdateCalls();
  }
  </script>
 </div>
```

JSP會新增所需的分析javascript物件和用戶端javascript程式庫的參考。 testandtarget.js檔案包含mbox.js函式。 指令碼生成的HTML與以下示例類似：

```xml
<script type="text/javascript">
        if ( !window.CQ_Analytics ) {
            window.CQ_Analytics = {};
        }
        if ( !CQ_Analytics.TestTarget ) {
            CQ_Analytics.TestTarget = {};
        }
        CQ_Analytics.TestTarget.clientCode = 'MyClientCode';
</script>
<link rel="stylesheet" href="/etc/clientlibs/foundation/testandtarget/testandtarget.css" type="text/css">
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/testandtarget.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/testandtarget/init.js"></script>
```

#### 主體部分（開始） {#the-body-section-start}

在&lt;body>標籤後立即新增下列程式碼，將用戶端內容功能新增至頁面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 主體部分（端） {#the-body-section-end}

在&lt;/body>結束標籤前加入下列程式碼：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此元件的JSP指令碼會產生對Target javascript API的呼叫，並實作其他必要的設定。 指令碼生成的HTML與以下示例類似：

```xml
<div class="servicecomponents cloudservices">
  <div class="cloudservice testandtarget">
    <script type="text/javascript">
      CQ_Analytics.TestTarget.maxProfileParams = 11;
      CQ_Analytics.CCM.addListener("storesinitialize", function(e) {
        CQ_Analytics.TestTarget.registerMboxUpdateCalls();
      });
    </script>
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
</div>
```

### 使用自訂目標程式庫檔案 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您未使用DTM或其他目標行銷系統，則可使用自訂目標程式庫檔案。

>[!NOTE]
>
>依預設，mbox會隱藏- mboxDefault類別會決定此行為。 隱藏mbox可確保訪客在交換預設內容之前不會看到預設內容；但是，隱藏mbox會影響感知的效能。

用於建立mbox的預設mbox.js檔案位於/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 若要使用客戶mbox.js檔案，請將檔案新增至Target雲端設定。 若要新增檔案，mbox.js檔案必須可在檔案系統上使用。

例如，如果您想要使用 [Marketing Cloud ID服務](https://marketing.adobe.com/resources/help/en_US/mcvid/) ，則需要下載mbox.js，以便其包含以您的租用戶為基礎之變數的 `imsOrgID` 正確值。 此變數是與Marketing Cloud ID服務整合的必要項。 如需詳細資訊，請 [參閱「Adobe Analytics」作為Adobe Target的報表來源](https://marketing.adobe.com/resources/help/en_US/target/a4t/a4t.html) ，以 [及實作之前](https://marketing.adobe.com/resources/help/en_US/target/a4t/c_before_implement.html)。

>[!NOTE]
>
>如果自訂mbox是在Target設定中定義，則每個人都必須擁有發佈伺服器上 **/etc/cloudservices的讀取存取權** 。 若沒有此存取權，在發佈網站上載入mbox.js檔案會產生404錯誤。

1. 前往CQ工具頁 **面** ，然後選 **取Cloud Services**。 ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在樹狀結構中，選取「Adobe Target」，然後在設定清單中，按兩下您的Target設定。
1. 在設定頁面上，按一下編輯。
1. 對於自訂mbox.js屬性，按一下「瀏覽」並選取檔案。
1. 若要套用變更，請輸入Adobe target帳戶的密碼，按一下「重新連線至目標」，然後在連線成功時按一下「確定」。 然後，在「編輯元件」(Edit Component)對話方塊中按一下「確定」(OK)。

您的Target設定包含自訂mbox.js檔案， [](/help/sites-developing/target.md#p-the-head-section-p) 頁面標題區段中的必要程式碼會將檔案新增至用戶端程式庫架構，而非對testandtarget.js程式庫的參考。

## 禁用元件的Target命令 {#disabling-the-target-command-for-components}

大部分的元件都可使用內容選單上的Target命令轉換為目標元件。

![chlimage_1-21](assets/chlimage_1-21.png)

要從上下文菜單中刪除Target命令，請將以下屬性添加到元件的cq:editConfig節點：

* 名稱：cq:disableTargeting
* 類型：布林值
* 值：True

例如，若要停用Geometrixx Demo Site頁面標題元件的定位，請將屬性新增至/apps/geometrixx/components/title/cq:editConfig節點。

![chlimage_1-22](assets/chlimage_1-22.png)

## 傳送訂單確認資訊至Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您未使用DTM，請傳送訂單確認至Adobe Target。

若要追蹤您網站的效能，請從訂購確認頁面傳送購買資訊至Adobe Target。 (請參 [閱Adobe Target檔案中的建立orderConfirmPage Mbox](https://marketing.adobe.com/resources/help/en_US/dtm/target/order-confirmation-mbox.html) 。)當您的MBox名稱為且使用下列特定參數名稱時，Adobe Target會將mbox資料辨識 `orderConfirmPage` 為訂購確認資料：

* productPurchasedId:識別購買產品的ID清單。
* orderId:訂單的ID。
* orderTotal:購買的總金額。

建立mbox的轉譯HTML頁面上的程式碼類似下列範例：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每個順序的每個參數值都不同。 因此，您需要一個元件，根據購買的屬性產生程式碼。 CQ [eCommerce Integration Framework](/help/sites-administering/ecommerce.md) 可讓您整合產品目錄，並建置購物車和結帳頁面。

當訪客購買產品時，Geometrixx Outdoors範例會顯示下列確認頁面：

![chlimage_1-23](assets/chlimage_1-23.png)

下列元件的JSP指令碼會存取購物車的屬性，然後列印建立mbox的程式碼。

```java
<%--

  confirmationmbox component.

--%><%
%><%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"
          import="com.adobe.cq.commerce.api.CommerceService,
                  com.adobe.cq.commerce.api.CommerceSession,
                  com.adobe.cq.commerce.common.PriceFilter,
                  com.adobe.cq.commerce.api.Product,
                  java.util.List, java.util.Iterator"%><%

/* obtain the CommerceSession object */
CommerceService commerceservice = resource.adaptTo(CommerceService.class);
CommerceSession session = commerceservice.login(slingRequest, slingResponse);

/* obtain the cart items */
List<CommerceSession.CartEntry> entries = session.getCartEntries();
Iterator<CommerceSession.CartEntry> cartiterator = entries.iterator();

/* iterate the items and get the product IDs */
String productIDs = new String();
while(cartiterator.hasNext()){
 CommerceSession.CartEntry entry = cartiterator.next();
 productIDs = productIDs + entry.getProduct().getSKU();
    if (cartiterator.hasNext()) productIDs = productIDs + ", ";
}

/* get the cart price and orderID */
String total = session.getCartPrice(new PriceFilter("CART", "PRE_TAX"));
String orderID = session.getOrderId();

%><div class="mboxDefault"></div>
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=<%= productIDs %>',
     'orderId=<%= orderID %>',
     'orderTotal=<%= total %>');
</script>
```

當元件包含在上一個範例的結帳頁面中時，頁面來源會包含下列建立mbox的指令碼：

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## 瞭解Target元件 {#understanding-the-target-component}

Target元件可讓作者從CQ內容元件建立動態mbox。 (請參閱 [內容定位](/help/sites-authoring/content-targeting-touch.md)。)Target元件位於/libs/cq/personalization/components/target。

target.jsp指令碼會存取頁面屬性，以決定要用於元件的定位引擎，然後執行適當的指令碼：

* Adobe Target:/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target含AT.JS](/help/sites-administering/target.md):/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md):/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 用戶端規則/ContextHub:/libs/cq/personalization/components/target/engine_cq.jsp

### 建立mbox {#the-creation-of-mboxes}

>[!NOTE]
>
>依預設，mbox會隱藏- mboxDefault類別會決定此行為。 隱藏mbox可確保訪客在交換預設內容之前不會看到預設內容；但是，隱藏mbox會影響感知的效能。

當Adobe target推動內容定位時，engine_tnt.jsp指令碼會建立包含定位體驗內容的mbox:

* 根據 `div` Adobe Target API的要 `mboxDefault`求，新增包含類別的元素。

* 在元素中新增mbox內容（目標體驗的內容）。 `div`

在div元 `mboxDefault` 素後，會插入建立mbox的javascript:

* mbox名稱、ID和位置是以元件的儲存庫路徑為基礎。
* 該指令碼獲取「客戶端上下文」參數名稱和值。
* 會呼叫mbox.js和其他用戶端程式庫所定義的函式，以建立mbox。

#### 用於內容定位的用戶端程式庫 {#client-libraries-for-content-targeting}

以下是可用的clientlib類別：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
