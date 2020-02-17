---
title: 建立自訂擴充功能
seo-title: 建立自訂擴充功能
description: 您可以在Adobe Campaign中從AEM或從AEM到Adobe Campaign呼叫自訂代碼
seo-description: 您可以在Adobe Campaign中從AEM或從AEM到Adobe Campaign呼叫自訂代碼
uuid: 8392aa0d-06cd-4b37-bb20-f67e6a0550b1
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: f536bcc1-7744-4f05-ac6a-4cec94a1ffb6
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# 建立自訂擴充功能{#creating-custom-extensions}

通常，當您實作專案時，AEM和Adobe Campaign中都有自訂代碼。 使用現有的API，您可以在Adobe Campaign中從AEM或從AEM呼叫自訂代碼至Adobe Campaign。 本檔案說明如何進行此作業。

## 必備條件 {#prerequisites}

您需要安裝下列程式碼：

* Adobe Experience Manager
* Adobe Campaign 6.1

如需 [詳細資訊，請參閱「整合AEM與Adobe Campaign 6.1](/help/sites-administering/campaignonpremise.md) 」。

## 範例1:AEM到Adobe Campaign {#example-aem-to-adobe-campaign}

AEM和Campaign之間的標準整合是以JSON和JSSP（JavaScript伺服器頁面）為基礎。 這些JSSP檔案可在Campaign主控台中找到，所有檔案都以 **amc** (Adobe Marketing Cloud)開始。

![chlimage_1-15](assets/chlimage_1-15a.png)

>[!NOTE]
>
>[如需此範例，請參閱Geometrixx](/help/sites-developing/we-retail.md)，它可從Package Share取得。

在此範例中，我們建立新的自訂JSSP檔案，並從AEM端呼叫該檔案以擷取結果。 例如，這可用來擷取Adobe Campaign中的資料，或將資料儲存至Adobe Campaign。

1. 在Adobe Campaign中，若要建立新的JSSP檔案，請按一下「新 **增** 」圖示。

   ![](do-not-localize/chlimage_1-4a.png)

1. 輸入此JSSP檔案的名稱。 在此範例中，我們使 **用cus:custom.jssp** (這表示它將位於 **cus** namespace中)。

   ![chlimage_1-16](assets/chlimage_1-16a.png)

1. 將下列程式碼放入jssp-file中：

   ```
   <%
   var origin = request.getParameter("origin");
   document.write("Hello from Adobe Campaign, origin : " + origin);
   %>
   ```

1. 儲存您的作品。 剩下的工作是在AEM中完成。
1. 在AEM端建立簡單的servlet以呼叫此JSSP。 在此範例中，我們假設：

   * 您的AEM和Campaign之間有運作的連線
   * 促銷活動cloudservice是設定在 **/content/geometrixx-outdoors上**
   此範例中最重要的物件是 **GenericCampaignConnector**，可讓您在Adobe Campaign側呼叫（取得和張貼）jssp檔案。

   以下是一小段程式碼：

   ```
   @Reference
   private GenericCampaignConnector campaignConnector;
   ...
   Map<String, String> params = new HashMap<String, String>();
   params.put("origin", "AEM");
   CallResults results = campaignConnector.callGeneric("/jssp/cus/custom.jssp", params, credentials);
   return results.bodyAsString();
   ```

1. 如您在此範例中所見，您需要將認證傳入呼叫中。 您可以透過getCredentials()方法取得此資訊，您可在該方法中傳入已設定Campaign雲端服務的頁面。

   ```xml
   // page containing the cloudservice for Adobe Campaign
   Configuration config = campaignConnector.getWebserviceConfig(page.getContentResource().getParent());
   CampaignCredentials credentials = campaignConnector.retrieveCredentials(config);
   ```

完整的程式碼如下：

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

## 範例2:Adobe Campaign到AEM {#example-adobe-campaign-to-aem}

AEM提供現成可用的API，以擷取網站管理員檔案總管檢視中任何地方可用的物件。

![chlimage_1-17](assets/chlimage_1-17a.png)

>[!NOTE]
>
>[如需此範例，請參閱Geometrixx](/help/sites-developing/we-retail.md)，它可從Package Share取得。

對於瀏覽器中的每個節點，都有一個連結到該節點的API。 例如，節點：

* [http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends](http://localhost:4502/siteadmin#/content/campaigns/geometrixx/scott-recommends)

api是：

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.1.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

URL **.1.json** 結尾可以 **.2.json**、 **.3.json**，根據您想要取得To obtain all they of sub levels the keyword **** infinity be used:

* [http://localhost:4502/content/campaigns/geometrixx/scott-recommends.infinity.json](http://localhost:4502/content/campaigns/geometrixx/scott-recommends.2.json)

現在，若要使用API，我們必須知道AEM依預設會使用基本驗證。

在6.1.1（build 8624及更新版本）中提供名為 **amcIntegration.js** 的JS程式庫，可在其他數種程式庫中實施該邏輯。

### AEM API呼叫 {#aem-api-call}

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

