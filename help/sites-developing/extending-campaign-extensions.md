---
title: 建立自定義擴展
seo-title: Creating Custom Extensions
description: 您可以從Adobe Campaign或從Adobe CampaignAEM調用您AEM的自定義代碼
seo-description: You can call your custom code in Adobe Campaign from AEM or from AEM to Adobe Campaign
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
exl-id: 0702858e-5e46-451f-9ac3-40a4fec68ca0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 1%

---

# 建立自定義擴展{#creating-custom-extensions}

通常，在實施項目時，您在兩個項目中都有自AEM定義代碼。 使用現有API，您可以從Adobe Campaign或從Adobe Campaign調AEM用自AEM定義代碼。 本文檔介紹如何執行此操作。

## 必備條件 {#prerequisites}

您需要安裝以下元件：

* Adobe Experience Manager
* Adobe Campaign6.1

請參閱 [與AEMAdobe Campaign](/help/sites-administering/campaignonpremise.md) 的子菜單。

## 示例1:AEMAdobe Campaign {#example-aem-to-adobe-campaign}

與Campaign之間的標AEM準整合基於JSON和JSSP（JavaScript伺服器頁）。 這些JSSP檔案可在市場活動控制台中找到，所有檔案都以 **資產** (Adobe Marketing Cloud)

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[有關此示例，請參閱Geometrixx](/help/sites-developing/we-retail.md)，可從包共用中獲得。

在此示例中，我們建立一個新的自定義JSSP檔案，並從一側調用該AEM檔案以檢索結果。 例如，這可用於從Adobe Campaign檢索資料或將資料保存到Adobe Campaign。

1. 在Adobe Campaign，要建立新的JSSP檔案，請按一下 **新建** 表徵圖

   ![](do-not-localize/chlimage_1-4a.png)

1. 輸入此JSSP檔案的名稱。 在本例中，我們使用 **cus:custom.jssp** (意味著它將在 **番** 命名空間)。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 將以下代碼放在jssp-file中：

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 保存您的工作。 其餘工作在AEM。
1. 在側面建立一個簡單AEM的Servlet以調用此JSSP。 在本示例中，我們假定：

   * 您與市場活動之AEM間有聯繫
   * 市場活動雲服務已配置在 **/content/geometrixx outdoors**

   此示例中最重要的對象是 **一般市場活動連接器**，允許您在Adobe Campaign側調用（獲取和發佈）jssp檔案。

   下面是一小段代碼：

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 正如您在本示例中看到的，您需要將憑據傳遞到調用中。 您可以通過getCredentials()方法獲取此資訊，在該方法中，您將在已配置了市場活動雲服務的頁面中傳遞該資訊。

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

完整代碼如下：

```java
import java.io.IOException;
import java.io.PrintWriter;
import java.util.HashMap;
import java.util.Map;

import javax.servlet.ServletException;

import org.apache.felix.scr.annotations.Reference;
import org.apache.felix.scr.annotations.sling.SlingServlet;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.mcm.campaign.CallResults;
import com.day.cq.mcm.campaign.CampaignCredentials;
import com.day.cq.mcm.campaign.GenericCampaignConnector;
import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageManager;
import com.day.cq.wcm.api.PageManagerFactory;
import com.day.cq.wcm.webservicesupport.Configuration;

@SlingServlet(paths="/bin/campaign", methods="GET")
public class CustomServlet extends SlingSafeMethodsServlet {

 private final Logger log = LoggerFactory.getLogger(this.getClass());

 @Reference
 private GenericCampaignConnector campaignConnector;

 @Reference
 private PageManagerFactory pageManagerFactory;

 @Override
 protected void doGet(SlingHttpServletRequest request,
   SlingHttpServletResponse response) throws ServletException,
   IOException {

  PageManager pm = pageManagerFactory.getPageManager(request.getResourceResolver());

  Page page = pm.getPage("/content/geometrixx-outdoors");

  String result = null;
  if ( page != null) {
   result = callCustomFunction(page);
  }
  if ( result != null ) {
   PrintWriter pw = response.getWriter();
   pw.print(result);
  }
 }

 private String callCustomFunction(Page page ) {
  try {
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);

   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
  } catch (Exception e ) {
   log.error("Something went wrong during the connection", e);
  }
  return null;

 }

}
```

## 示例2:Adobe CampaignAEM {#example-adobe-campaign-to-aem}

提AEM供現成API，以檢索siteadmin資源管理器視圖中任何位置可用的對象。

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[有關此示例，請參閱Geometrixx](/help/sites-developing/we-retail.md)，可從包共用中獲得。

對於資源管理器中的每個節點，都有一個連結到它的API。 例如，節點：

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

API是：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

URL的結尾 **.1.json** 可替換為 **.2.json**。 **.3.json**，根據您希望獲取的子級數，獲取所有子級的關鍵字 **無限** 可用：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

現在，要使用API，我們必須知AEM道預設情況下使用基本驗證。

名為的JS庫 **amcIntegration.js** 6.1.1（build 8624及更高版本）中提供了該邏輯與多個其他邏輯實現。

### API調AEM用 {#aem-api-call}

```java
loadLibrary("nms:amcIntegration.js");

var cmsAccountId = sqlGetInt("select iExtAccountId from NmsExtAccount where sName=$(sz)","aemInstance")
var cmsAccount = nms.extAccount.load(String(cmsAccountId));
var cmsServer = cmsAccount.server;

var request = new HttpClientRequest(cmsServer+"/content/campaigns/geometrixx.infinity.json")
aemAddBasicAuthentication(cmsAccount, request);
request.method = "GET"
request.header["Content-Type"] = "application/json; charset=UTF-8";
request.execute();
var response = request.response;
```
