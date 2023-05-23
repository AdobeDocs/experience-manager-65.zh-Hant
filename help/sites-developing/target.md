---
title: 為目標內容開發
seo-title: Developing for Targeted Content
description: 有關開發用於內容目標的元件的主題
seo-description: Topics about developing components for use with content targeting
uuid: 2449347e-7e1c-427b-a5b0-561055186934
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: bff078cd-c390-4870-ad1d-192807c67ca4
docset: aem65
exl-id: 92b62532-4f79-410d-903e-d2bca6d0fd1c
source-git-commit: fb9363a39ffc9d3929a31a3a19a124b806607ef4
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---

# 為目標內容開發{#developing-for-targeted-content}

本節介紹有關開發用於內容目標的元件的主題。

* 有關與Adobe Target連接的資訊，請參見 [與Adobe Target整合](/help/sites-administering/target.md)。
* 有關創作目標內容的資訊，請參見 [使用目標模式創作目標內容](/help/sites-authoring/content-targeting-touch.md)。

>[!NOTE]
>
>當您針對作者中的元件AEM時，該元件會向Adobe Target發出一系列伺服器端呼叫，以註冊市場活動、設定優惠和檢索Adobe Target段（如果已配置）。 發佈到Adobe Target時不會進行AEM伺服器端呼叫。

## 在您的頁面上啟用Adobe Target目標 {#enabling-targeting-with-adobe-target-on-your-pages}

要在頁面中使用與Adobe Target交互的目標元件，請在 &lt;head> 的子菜單。

### 頭部 {#the-head-section}

將以下兩個代碼塊添加到 &lt;head> 的下一頁：

```xml
<!--/* Include Context Hub */-->
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

```xml
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
```

此代碼添加所需的分析Javascript對象並載入與網站關聯的雲服務庫。 對於目標服務，通過 `/libs/cq/analytics/components/testandtarget/headlibs.jsp`

載入的庫集取決於目標配置上使用的目標客戶端庫（mbox.js或at.js）的類型：

**對於預設mbox.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/mbox.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**對於自定義mbox.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/mbox.js"></script>
        <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/personalization/integrations/commons.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/util.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/init.js"></script>
```

**對於at.js**

```
<script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs.js"></script>
```

>[!NOTE]
>
>僅版本 `at.js` 支援隨產品一起提供。 版本 `at.js` 通過查看產品 `at.js` 檔案位於位置：
>
>**/libs/cq/testandtarget/clientlibs/testandtarget/atjs/source/at.js**。

**對於自定義at.js**

```
<script type="text/javascript" src="/etc/cloudservices/testandtarget/<CLIENT-CODE>/_jcr_content/public/at.js"></script>
    <script type="text/javascript" src="/libs/cq/foundation/testandtarget/parameters.js"></script>
 <script type="text/javascript" src="/libs/cq/foundation/testandtarget/atjs-integration.js"></script>
```

客戶端上的目標功能由 `CQ_Analytics.TestTarget` 的雙曲餘切值。 因此，該頁將包含一些init代碼，如以下示例中：

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

JSP將添加所需的分析Javascript對象和對客戶端Javascript庫的引用。 testandtarget.js檔案包含mbox.js函式。 指令碼生成的HTML與以下示例類似：

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

#### 正文節（開始） {#the-body-section-start}

在 &lt;body> 將客戶端上下文功能添加到頁面的標籤：

```xml
<cq:include path="clientcontext" resourceType="cq/personalization/components/clientcontext"/>
```

#### 主體部分（尾） {#the-body-section-end}

在 &lt;/body> 結束標籤：

```xml
<cq:include path="cloudservices" resourceType="cq/cloudserviceconfigs/components/servicecomponents"/>
```

此元件的JSP指令碼將生成對目標javascript API的調用，並實現其他所需配置。 指令碼生成的HTML與以下示例類似：

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

### 使用自定義目標庫檔案 {#using-a-custom-target-library-file}

>[!NOTE]
>
>如果不使用DTM或其他目標市場營銷系統，則可以使用自定義目標庫檔案。

>[!NOTE]
>
>預設情況下，mboxes是隱藏的 — mboxDefault類確定此行為。 隱藏框可確保訪問者在交換預設內容之前不會看到它；但是，隱藏框會影響感知效能。

用於建立mboxes的預設mbox.js檔案位於/etc/clientlibs/foundation/testandtarget/mbox/source/mbox.js。 要使用customer mbox.js檔案，請將該檔案添加到目標雲配置。 要添加檔案，mbox.js檔案必須在檔案系統上可用。

例如，如果要使用 [Marketing CloudID服務](https://experienceleague.adobe.com/docs/id-service/using/home.html) 您需要下載mbox.js，以便它包含的 `imsOrgID` 變數，基於您的租戶。 此變數是與Marketing CloudID服務整合所必需的。 有關資訊，請參見 [Adobe Analytics為Adobe Target報導來源](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) 和 [實施前](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html)。

>[!NOTE]
>
>如果在目標配置中定義了自定義框，則每個人都必須具有對 **/etc/cloudservices** 在發佈伺服器上。 如果沒有此訪問權限，則在發佈網站上載入mbox.js檔案將導致404錯誤。

1. 轉到CQ **工具** 選擇 **Cloud Services**。 ([https://localhost:4502/libs/cq/core/content/tools/cloudservices.html](https://localhost:4502/libs/cq/core/content/tools/cloudservices.html))
1. 在樹中，選擇Adobe Target，在配置清單中，按兩下目標配置。
1. 在配置頁上，按一下編輯。
1. 對於Custom mbox.js屬性，按一下「瀏覽」並選擇檔案。
1. 要應用更改，請輸入Adobe Target帳戶的密碼，按一下重新連接到目標，然後在連接成功時按一下確定。 然後，在「編輯元件」(Edit Component)對話框中按一下「確定」(OK)。

您的目標配置包括自定義mbox.js檔案， [頭部所需的代碼](/help/sites-developing/target.md#p-the-head-section-p) 將檔案添加到客戶端庫框架，而不是引用testandtarget.js庫。

## 禁用元件的目標命令 {#disabling-the-target-command-for-components}

大多數元件都可以使用上下文菜單上的「目標」(Target)命令轉換為目標元件。

![chlimage_1-21](assets/chlimage_1-21.png)

要從上下文菜單中刪除「目標」命令，請將以下屬性添加到元件的cq:editConfig節點：

* 名稱：cq：禁用目標
* 類型：布爾型
* 值：真

例如，要禁用「Geometrixx演示網站」頁的標題元件的目標，請將該屬性添加到/apps/geometrixx/components/title/cq:editConfig節點。

![chlimage_1-22](assets/chlimage_1-22.png)

## 向Adobe Target發送訂單確認資訊 {#sending-order-confirmation-information-to-adobe-target}

>[!NOTE]
>
>如果您不使用DTM，則向Adobe Target發送訂單確認。

要跟蹤網站的效能，請將訂單確認頁中的採購資訊發送到Adobe Target。 (請參閱 [建立orderConfirmPage複選框](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager/?lang=en) 和 [訂單確認框 — 添加自定義參數。](https://experienceleaguecommunities.adobe.com/t5/adobe-target-questions/order-confirmation-mbox-add-custom-parameters/m-p/275779))當您的MBox名稱為 `orderConfirmPage` 並使用以下特定參數名稱：

* productPewhiedId:標識所購買產品的ID清單。
* orderId:訂單的ID。
* 訂單合計：採購的總額。

建立該框的呈現HTML頁上的代碼與以下示例類似：

```xml
<script type="text/javascript">
     mboxCreate('orderConfirmPage',
     'productPurchasedId=product1 product2 product3',
     'orderId=order1234',
     'orderTotal=24.54');
</script>
```

每個順序的每個參數的值都不同。 因此，您需要一個元件，它根據採購的屬性生成代碼。 CQ [電子商務整合框架](/help/commerce/cif-classic/administering/ecommerce.md) 使您能夠與產品目錄整合併實施購物車和結帳頁。

Geometrixx Outdoors示例顯示訪問者購買產品時的以下確認頁：

![chlimage_1-23](assets/chlimage_1-23.png)

元件的JSP指令碼的以下代碼訪問購物車的屬性，然後打印用於建立框的代碼。

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

當元件包含在上例的簽出頁中時，頁面源包括建立框的以下指令碼：

```
<div class="mboxDefault"></div>
<script type="text/javascript">

     mboxCreate('orderConfirmPage',
     'productPurchasedId=47638-S, 46587',
     'orderId=d03cb015-c30f-4bae-ab12-1d62b4d105ca',
     'orderTotal=US$677.00');

</script>
```

## 瞭解目標元件 {#understanding-the-target-component}

「目標」元件使作者能夠從CQ內容元件建立動態框。 (請參閱 [內容目標](/help/sites-authoring/content-targeting-touch.md)。) 目標元件位於/libs/cq/personalization/components/target。

target.jsp指令碼訪問頁面屬性以確定要用於元件的目標引擎，然後執行相應的指令碼：

* Adobe Target:/libs/cq/personalization/components/target/engine_tnt.jsp
* [Adobe Target與AT.JS](/help/sites-administering/target.md):/libs/cq/personalization/components/target/engine_atjs.jsp
* [Adobe Campaign](/help/sites-authoring/target-adobe-campaign.md):/libs/cq/personalization/components/target/engine_cq_campaign.jsp
* 客戶端規則/ContextHub:/libs/cq/personalization/components/target/engine_cq.jsp

### 框的建立 {#the-creation-of-mboxes}

>[!NOTE]
>
>預設情況下，mboxes是隱藏的 — mboxDefault類確定此行為。 隱藏框可確保訪問者在交換預設內容之前不會看到它；但是，隱藏框會影響感知效能。

當Adobe Target驅動內容目標時，engine_tnt.jsp指令碼將建立包含目標體驗內容的框：

* 添加 `div` 具有類的元素 `mboxDefault`，按Adobe TargetAPI的要求。

* 將框內內容（目標體驗的內容）添加到 `div` 的子菜單。

遵循 `mboxDefault` div元素，插入建立mbox的javascript:

* mbox名稱、ID和位置基於元件的儲存庫路徑。
* 指令碼獲取客戶端上下文參數名稱和值。
* 調用mbox.js和其他客戶端庫定義的函式以建立mboxes。

#### 針對內容目標的客戶端庫 {#client-libraries-for-content-targeting}

以下是可用的客戶端庫類別：

* testandtarget.mbox
* testandtarget.init
* testandtarget.util
* testandtarget.atjs
* testandtarget.atjs-integration
