---
title: 針對目標內容開發
seo-title: Developing for Targeted Content
description: 關於開發元件以搭配內容鎖定的主題
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 0%

---

# 針對目標內容開發{#developing-for-targeted-content}

本節說明有關開發元件以搭配內容定位的主題。

* 如需連線Adobe Target的詳細資訊，請參閱 [與Adobe Target整合](/help/sites-administering/target.md).
* 如需製作目標內容的詳細資訊，請參閱 [使用定位模式製作定位內容](/help/sites-authoring/content-targeting-touch.md).

>[!NOTE]
>
>當您在AEM作者中定位元件時，元件會向Adobe Target發出一系列伺服器端呼叫，以註冊促銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈至Adobe Target進行伺服器端呼叫。

## 在您的頁面上使用Adobe Target啟用目標定位 {#enabling-targeting-with-adobe-target-on-your-pages}

若要在與Adobe Target互動的頁面中使用目標元件，請在 &lt;head> 元素。

### 頭部 {#the-head-section}

將下列兩個程式碼區塊新增至 &lt;head> 區段：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此程式碼會新增所需的analytics javascript物件，並載入與網站相關聯的雲端服務程式庫。 若為Target服務，程式庫會透過 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

載入的程式庫集取決於Target設定上使用的目標用戶端程式庫（mbox.js或at.js）類型：

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

**針對at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>僅限 `at.js` 支援隨產品一起提供。 版本 `at.js` 可透過查看 `at.js` 檔案位置：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**.

**針對自訂at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

用戶端上的Target功能由 `CQ_Analytics.TestTarget` 物件。 因此，頁面將包含一些init程式碼，如下列範例：

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

JSP會將所需的analytics javascript物件和參考新增至用戶端javascript程式庫。 testandtarget.js檔案包含mbox.js函式。 指令碼產生的HTML與以下範例類似：

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

在 &lt;body> 標籤來將用戶端內容功能新增至頁面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 主體部分（結束） {#the-body-section-end}

在 &lt;/body> 結束標籤：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此元件的JSP指令碼會產生對Target javascript API的呼叫，並實作其他必要的設定。 指令碼產生的HTML與以下範例類似：

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

### 使用自訂Target程式庫檔案 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您未使用DTM或其他目標行銷系統，則可使用自訂目標程式庫檔案。

>[!NOTE]
>
>依預設，會隱藏mbox - mboxDefault類別會決定此行為。 隱藏mbox可確保訪客在交換預設內容之前不會看到該內容；不過，隱藏mbox會影響感知的效能。

用於建立mbox的預設mbox.js檔案位於/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 若要使用客戶mbox.js檔案，請將檔案新增至Target雲端設定。 若要新增檔案，檔案系統上必須有mbox.js檔案。

例如，如果您想使用 [Marketing CloudID服務](https://experienceleague.adobe.com/docs/id-service/using/home.html) 您需要下載mbox.js，使其包含 `imsOrgID` 變數，此變數會以您的租用戶為基礎。 若要與Marketing CloudID服務整合，此變數為必要項目。 如需詳細資訊，請參閱 [Adobe Analytics作為Adobe Target的報表來源](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 和 [實作之前](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html).

>[!NOTE]
>
>如果在Target設定中定義了自訂mbox，則每個人都必須擁有的讀取存取權 **/etc/cloudservices** 在發佈伺服器上。 若無此存取權，在發佈的網站上載入mbox.js檔案會產生404錯誤。

1. 前往CQ **工具** 頁面和選取 **Cloud Services**. ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在樹狀結構中，選取Adobe Target，然後在設定清單中，連按兩下您的Target設定。
1. 在設定頁面上，按一下「編輯」 。
1. 若為自訂mbox.js屬性，請按一下「瀏覽」並選取檔案。
1. 若要套用變更，請輸入Adobe Target帳戶的密碼，按一下重新連線至Target，然後在連線成功時按一下確定。 然後，在「編輯元件」(Edit Component)對話框中按一下「確定」(OK)。

您的Target設定包含自訂mbox.js檔案， [標題區段中的必要程式碼](/help/sites-developing/target.md#p-the-head-section-p) 頁面的會將檔案新增至用戶端程式庫架構，而非testandtarget.js程式庫的參考。

## 禁用元件的目標命令 {#disabling-the-target-command-for-components}

大部分元件都可使用內容功能表上的Target命令轉換為目標元件。

![chlimage_1-21](assets/chlimage_1-21.png)

若要從內容功能表移除Target命令，請將下列屬性新增至元件的cq:editConfig節點：

* 名稱：cq:disableTargeting
* 類型：布林值
* 值：True

例如，若要停用Geometrixx示範網站頁面標題元件的定位，請將屬性新增至/apps/geometrixx/components/title/cq:editConfig節點。

![chlimage_1-22](assets/chlimage_1-22.png)

## 傳送訂單確認資訊至Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>若您未使用DTM，請將訂單確認傳送至Adobe Target。

若要追蹤網站效能，請從訂單確認頁面傳送購買資訊至Adobe Target。 (請參閱 [建立orderConfirmPage mbox](https://experienceleague.adobe.com/docs/dtm/implementing/target/configure-target/mboxes/order-confirmation-mbox.html) (在Adobe Target檔案中)。 當您的MBox名稱為 `orderConfirmPage` 並使用下列特定參數名稱：

* productPurchasedId:識別已購買產品的ID清單。
* orderId:訂單ID。
* orderTotal:購買的總金額。

建立mbox的轉譯HTML頁面上的程式碼與下列範例類似：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每個順序的每個參數值都不同。 因此，您需要元件根據購買的屬性產生代碼。 CQ [電子商務整合架構](/help/commerce/cif-classic/administering/ecommerce.md) 可讓您與產品目錄整合，並實作購物車和結帳頁面。

Geometrixx Outdoors範例會在訪客購買產品時顯示下列確認頁面：

![chlimage_1-23](assets/chlimage_1-23.png)

元件的JSP指令碼的以下代碼訪問購物車的屬性，然後打印用於建立mbox的代碼。

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

在上一個範例的結帳頁面中包含元件時，頁面來源會包含下列指令碼，用以建立mbox:

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## 了解目標元件 {#understanding-the-target-component}

Target元件可讓作者從CQ內容元件建立動態mbox。 (請參閱 [內容鎖定](/help/sites-authoring/content-targeting-touch.md).) Target元件位於/libs/cq/personalization/components/target。

target.jsp指令碼訪問頁面屬性以確定要用於元件的目標引擎，然後執行相應的指令碼：

* Adobe Target:/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target搭配AT.JS](/help/sites-administering/target.md):/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md):/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 用戶端規則/ContextHub:/libs/cq/personalization/components/target/engine_cq.jsp

### Mbox的建立 {#the-creation-of-mboxes}

>[!NOTE]
>
>依預設，會隱藏mbox - mboxDefault類別會決定此行為。 隱藏mbox可確保訪客在交換預設內容之前不會看到該內容；不過，隱藏mbox會影響感知的效能。

當Adobe Target驅動內容目標定位時，engine_tnt.jsp指令碼會建立包含目標體驗內容的mbox:

* 新增 `div` 具有類別的元素 `mboxDefault`，如Adobe Target API所要求。

* 在內新增mbox內容（目標體驗的內容） `div` 元素。

遵循 `mboxDefault` div元素中，會插入建立mbox的javascript:

* mbox名稱、ID和位置以元件的存放庫路徑為基礎。
* 指令碼獲取客戶端上下文參數名稱和值。
* 會呼叫mbox.js和其他用戶端程式庫所定義的函式，以建立mbox。

#### 用於內容鎖定的用戶端程式庫 {#client-libraries-for-content-targeting}

以下是可用的clientlib類別：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
