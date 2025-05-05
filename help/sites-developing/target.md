---
title: 針對目標內容開發
description: 有關開發元件以與內容鎖定目標搭配使用的主題
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# 針對目標內容開發{#developing-for-targeted-content}

本節說明有關開發元件以與內容鎖定目標搭配使用的主題。

* 如需有關連線至Adobe Target的資訊，請參閱[與Adobe Target整合](/help/sites-administering/target.md)。
* 如需有關編寫目標內容的資訊，請參閱[使用目標模式編寫目標內容](/help/sites-authoring/content-targeting-touch.md)。

>[!NOTE]
>
>當您在AEM製作中鎖定元件時，元件會對Adobe Target發出一系列伺服器端呼叫，以註冊行銷活動、設定選件及擷取Adobe Target區段（如果已設定）。 不會從AEM發佈對Adobe Target發出伺服器端呼叫。

## 在您的頁面上使用Adobe Target啟用鎖定目標 {#enabling-targeting-with-adobe-target-on-your-pages}

若要在與Adobe Target互動的頁面中使用目標元件，請在&lt;head>元素中包含特定使用者端代碼。

### 標題區段 {#the-head-section}

將下列兩個程式碼區塊新增至頁面的&lt;head>區段：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此程式碼會新增必要的Analytics JavaScript物件，並載入與網站相關聯的雲端服務程式庫。 針對Target服務，程式庫是透過`/libs/cq/analytics/components/testandtarget/headlibs.jsp`載入

載入的程式庫組取決於Target設定中所使用的Target使用者端程式庫型別（mbox.js或at.js）：

**針對預設的mbox.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**適用於自訂mbox.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

針對at.js **的**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>僅支援產品隨附的`at.js`版本。 透過檢視以下位置的`at.js`檔案，可取得產品隨附的`at.js`版本：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**。

**適用於自訂at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

使用者端的Target功能是由`CQ_Analytics.TestTarget`物件所管理。 因此，頁面將包含一些init程式碼，如以下範例中的：

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

JSP會將必要的Analytics JavaScript物件及參照新增至使用者端JavaScript程式庫。 testandtarget.js檔案包含mbox.js函式。 指令碼產生的HTML類似於以下範例：

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

#### 主體區段（開始） {#the-body-section-start}

在&lt;body>標籤後立即新增下列程式碼，以將使用者端內容功能新增至頁面：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 主體區段（結束） {#the-body-section-end}

在&lt;/body>結尾標籤前面加上下列程式碼：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此元件的JSP指令碼會產生對Target javascript API的呼叫，並實作其他必要的設定。 指令碼產生的HTML類似於以下範例：

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

### 使用自訂Target資料庫檔案 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果您沒有使用DTM或其他目標行銷系統，則可以使用自訂目標資料庫檔案。

>[!NOTE]
>
>預設會隱藏mbox - mboxDefault類別會決定此行為。 隱藏mbox可確保訪客在交換預設內容之前不會看到該內容；但是，隱藏mbox會影響感知的效能。

用來建立mbox的預設mbox.js檔案位於/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 若要使用客戶mbox.js檔案，請新增檔案至Target雲端設定。 若要新增檔案，mbox.js檔案必須在檔案系統上可用。

例如，如果您想要使用[Marketing Cloud識別碼服務](https://experienceleague.adobe.com/docs/id-service/using/home.html)，您必須下載mbox.js，使其包含以您的租使用者為基礎之`imsOrgID`變數的正確值。 若要與Marketing CloudID服務整合，此變數為必要專案。 如需詳細資訊，請參閱[Adobe Analytics作為Adobe Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)和[的報表Source，再執行](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html)。

>[!NOTE]
>
>如果在Target設定中定義了自訂mbox，則每個人都必須擁有發佈伺服器上&#x200B;**/etc/cloudservices**&#x200B;的讀取存取權。 若沒有此存取權，在發佈網站上載入mbox.js檔案會導致404錯誤。

1. 移至CQ **工具**&#x200B;頁面並選取&#x200B;**Cloud Service**。 ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在樹狀結構中選取「Adobe Target」，然後在設定清單中按兩下Target設定。
1. 在設定頁面上，按一下編輯。
1. 針對「自訂mbox.js」屬性，按一下「瀏覽」並選取檔案。
1. 若要套用變更，請輸入Adobe Target帳戶的密碼，按一下「重新連線至Target」，然後在連線成功時按一下「確定」。 然後，按一下「編輯元件」對話方塊上的「確定」。

您的Target設定包含自訂mbox.js檔案，在網頁的head區段[&#128279;](/help/sites-developing/target.md#p-the-head-section-p)中必要的程式碼會將檔案新增至使用者端資料庫架構，而非testandtarget.js資料庫的參考。

## 停用元件的目標命令 {#disabling-the-target-command-for-components}

大部分的元件都可以使用快顯選單上的「目標」指令轉換成目標元件。

![chlimage_1-21](assets/chlimage_1-21.png)

若要從內容選單中移除Target命令，請將下列屬性新增至元件的cq：editConfig節點：

* 名稱：cq：disableTargeting
* 型別：布林值
* 值： True

例如，若要停用Geometrixx示範網站頁面標題元件的鎖定目標，請將屬性新增至/apps/geometrixx/components/title/cq：editConfig節點。

![chlimage_1-22](assets/chlimage_1-22.png)

## 傳送訂單確認資訊至Adobe Target {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您沒有使用DTM，請傳送訂單確認給Adobe Target。

為了追蹤您網站的效能，請從您的訂單確認頁面將購買資訊傳送到Adobe Target。 (請參閱[建立orderConfirmPage Mbox](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en)和[訂單確認Mbox — 新增自訂引數。](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779))當您的MBox名稱為`orderConfirmPage`時，Adobe Target會將mbox資料辨識為訂購確認資料，並使用下列特定引數名稱：

* productPurchasedId：識別已購買產品的ID清單。
* orderId：訂單的ID。
* orderTotal：購買的總金額。

在轉譯HTML頁面上建立mbox的程式碼類似於以下範例：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每個訂單的每個引數值都不同。 因此，您需要根據購買屬性產生代碼的元件。 CQ [電子商務整合架構](/help/commerce/cif-classic/administering/ecommerce.md)可讓您與產品目錄整合，並實作購物車與結帳頁面。

訪客購買產品時，Geometrixx Outdoors範例會顯示下列確認頁面：

![chlimage_1-23](assets/chlimage_1-23.png)

以下元件的JSP指令碼程式碼會存取購物車的屬性，然後列印建立mbox的程式碼。

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

在上一個範例中，當元件包含在結帳頁面中時，頁面來源會包含以下建立mbox的指令碼：

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

Target元件可讓作者從CQ內容元件建立動態mbox。 （請參閱[內容目標定位](/help/sites-authoring/content-targeting-touch.md)。） Target元件位於/libs/cq/personalization/components/target。

target.jsp指令碼會存取頁面屬性，以決定要用於元件的目標定位引擎，然後執行適當的指令碼：

* Adobe Target： /libs/cq/personalization/components/target/engine_tnt.jsp
* [使用AT.JS的Adobe Target](/help/sites-administering/target.md)： /libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md)： /libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 使用者端規則/ContextHub： /libs/cq/personalization/components/target/engine_cq.jsp

### Mbox的建立 {#the-creation-of-mboxes}

>[!NOTE]
>
>預設會隱藏mbox - mboxDefault類別會決定此行為。 隱藏mbox可確保訪客在交換預設內容之前不會看到該內容；但是，隱藏mbox會影響感知的效能。

當Adobe Target驅動內容鎖定目標時，engine_tnt.jsp指令碼會建立包含目標體驗內容的mbox：

* 根據Adobe Target API的要求，新增類別為`mboxDefault`的`div`元素。

* 在`div`元素中新增mbox內容（目標體驗的內容）。

在`mboxDefault` div元素之後，會插入建立mbox的javascript：

* mbox名稱、ID和位置是根據元件的存放庫路徑。
* 指令碼會取得Client Context引數名稱和值。
* 系統會呼叫mbox.js和其他使用者端程式庫所定義的函式，以建立mbox。

#### 內容鎖定的使用者端資料庫 {#client-libraries-for-content-targeting}

以下是可用的clientlib類別：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
