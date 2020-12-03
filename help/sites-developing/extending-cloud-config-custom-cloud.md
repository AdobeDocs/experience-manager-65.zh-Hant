---
title: 建立自訂雲端服務
seo-title: 建立自訂雲端服務
description: 預設的雲端服務集可以與自訂雲端服務類型一起擴充
seo-description: 預設的雲端服務集可以與自訂雲端服務類型一起擴充
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 3%

---


# 建立自訂雲端服務{#creating-a-custom-cloud-service}

預設的雲端服務集可以與自訂雲端服務類型一起擴充。 這可讓您以結構化方式將自訂標籤插入頁面。 這主要用於第三方分析提供者，例如Google Analytics、Chartbeat等。 雲端服務會從父頁面繼承至子頁面，並能夠在任何層級中斷繼承。

>[!NOTE]
>
>此建立新雲端服務的逐步指南是使用Google Analytics的範例。 您的使用案例可能不適用。

1. 在CRXDE Lite中，在`/apps`下建立新節點：

   * **名稱**:  `acs`
   * **類型**:  `nt:folder`

1. 在`/apps/acs`下建立新節點：

   * **名稱**:  `analytics`
   * **類型**:  `sling:Folder`

1. 在`/apps/acs/analytics`下建立2個新節點：

   * **名稱**:元件
   * **類型**:  `sling:Folder`

   和

   * **名稱**:模板
   * **類型**:  `sling:Folder`


1. 按一下右鍵`/apps/acs/analytics/components`。 選擇&#x200B;**建立……**&#x200B;後跟&#x200B;**建立元件……**&#x200B;開啟的對話方塊可讓您指定：

   * **標籤**:  `googleanalyticspage`
   * **標題**: `Google Analytics Page`
   * **超級類型**: `cq/cloudserviceconfigs/components/configpage`
   * **群組**:  `.hidden`

1. 按兩下&#x200B;**Next**&#x200B;並指定：

   * **允許的父項:** `acs/analytics/templates/googleanalytics`

   按兩下「**Next**」，然後按一下「確定&#x200B;**OK**」。

1. 新增屬性至`googleanalyticspage`:

   * **名稱：** `cq:defaultView`
   * **值：** `html`

1. 在`/apps/acs/analytics/components/googleanalyticspage`下建立名為`content.jsp`的新檔案，並包含以下內容：

   ```xml
   <%@page contentType="text/html"
               pageEncoding="utf-8"%><%
   %><%@include file="/libs/foundation/global.jsp"%><div>
   
   <div>
       <h3>Google Analytics Settings</h3>
       <ul>
           <li><div class="li-bullet"><strong>accountID: </strong><br><%= xssAPI.encodeForHTML(properties.get("accountID", "")) %></div></li>
       </ul>
   </div>
   ```

1. 在`/apps/acs/analytics/components/googleanalyticspage/`下建立新節點：

   * **名稱**:  `dialog`
   * **類型**:  `cq:Dialog`
   * **屬性**:

      * **名稱**:  `title`
      * **類型**:  `String`
      * **值**:  `Google Analytics Config`
      * **名稱**:  `xtype`
      * **類型**:  `String`
      * **值**:  `dialog`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog`下建立新節點：

   * **名稱**:  `items`
   * **類型**:  `cq:Widget`
   * **屬性**:

      * **名稱**:  `xtype`
      * **類型**:  `String`
      * **值**:  `tabpanel`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items`下建立新節點：

   * **名稱**:  `items`
   * **類型**:  `cq:WidgetCollection`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`下建立新節點：

   * **名稱**:tab1
   * **類型**:  `cq:Panel`
   * **屬性**:

      * **名稱**:  `title`
      * **類型**:  `String`
      * **值**:  `Config`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`下建立新節點：

   * **名稱**:項目
   * **類型**:  `nt:unstructured`
   * **屬性**:

      * **名稱**:  `fieldLabel`
      * **類型**:字串
      * **值**:帳戶ID

      * **名稱**:  `fieldDescription`
      * **類型**:  `String`
      * **值**:  `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **名稱**:  `name`
      * **類型**:  `String`
      * **值**:  `./accountID`
      * **名稱**:  `validateOnBlur`
      * **類型**:  `String`
      * **值**:  `true`
      * **名稱**:  `xtype`
      * **類型**:  `String`
      * **值**:  `textfield`

1. 將`/libs/cq/cloudserviceconfigs/components/configpage/body.jsp`複製到`/apps/acs/analytics/components/googleanalyticspage/body.jsp`，並將第34行的`libs`更改為`apps`，將第79行的指令碼參考設為完全限定的路徑。
1. 在`/apps/acs/analytics/templates/`下建立新模板：

   * 具有&#x200B;**資源類型** = `acs/analytics/components/googleanalyticspage`
   * 具有&#x200B;**標籤** = `googleanalytics`
   * with **Title**= `Google Analytics Configuration`
   * 具有&#x200B;**allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * with **allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * with **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage`(on template node, not the jcr:content node)
   * with **cq:designPath** = `/etc/designs/cloudservices/googleanalytics`(on jcr:content)

1. 建立新元件：`/apps/acs/analytics/components/googleanalytics`。

   將下列內容新增至`googleanalytics.jsp`:

   ```xml
   <%@page import="org.apache.sling.api.resource.Resource,
                   org.apache.sling.api.resource.ValueMap,
                   org.apache.sling.api.resource.ResourceUtil,
                   com.day.cq.wcm.webservicesupport.Configuration,
                   com.day.cq.wcm.webservicesupport.ConfigurationManager" %>
   <%@include file="/libs/foundation/global.jsp" %><%
   
   String[] services = pageProperties.getInherited("cq:cloudserviceconfigs", new String[]{});
   ConfigurationManager cfgMgr = resource.getResourceResolver().adaptTo(ConfigurationManager.class);
   if(cfgMgr != null) {
       String accountID = null;
       Configuration cfg = cfgMgr.getConfiguration("googleanalytics", services);
       if(cfg != null) {
           accountID = cfg.get("accountID", null);
       }
   
       if(accountID != null) {
       %>
   <script type="text/javascript">
   
     var _gaq = _gaq || [];
     _gaq.push(['_setAccount', '<%= accountID %>']);
     _gaq.push(['_trackPageview']);
   
     (function() {
       var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
       ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
       var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
     })();
   
   </script><%
       }
   }
   %>
   ```

   這應該會根據設定屬性輸出自訂標籤。

1. 導覽至`http://localhost:4502/miscadmin#/etc/cloudservices`並建立新頁面：

   * **標題**: `Google Analytics`
   * **名稱**:  `googleanalytics`

   返回CRXDE Lite，在`/etc/cloudservices/googleanalytics`下，將下列屬性新增至`jcr:content`:

   * **名稱**:  `componentReference`
   * **類型**:  `String`
   * **值**:  `acs/analytics/components/googleanalytics`


1. 導覽至新建立的「服務」頁面(`http://localhost:4502/etc/cloudservices/googleanalytics.html`)，然後按一下&#x200B;**+**&#x200B;以建立新的設定：

   * **父設定**: `/etc/cloudservices/googleanalytics`
   * **標題:**  `My First GA Config`

   選擇&#x200B;**Google Analytics Configuration**，然後按一下&#x200B;**Create**。

1. 輸入&#x200B;**帳戶ID**，例如`AA-11111111-1`。 按一下&#x200B;**「確定」**。
1. 導覽至頁面，並在頁面屬性中的&#x200B;**雲端服務**&#x200B;標籤下新增新建立的設定。
1. 頁面將會新增自訂標籤。

