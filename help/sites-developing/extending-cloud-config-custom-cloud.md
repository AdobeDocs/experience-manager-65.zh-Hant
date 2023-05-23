---
title: 建立自定義Cloud Service
seo-title: Creating a Custom Cloud Service
description: 預設Cloud Services集可以使用自定義Cloud Service類型進行擴展
seo-description: The default set of Cloud Services can be extended with custom Cloud Service types
uuid: b105a0c1-b68c-4f57-8e3b-561c8051a08e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e48e87c6-43ca-45ba-bd6b-d74c969757cd
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 10%

---

# 建立自定義Cloud Service{#creating-a-custom-cloud-service}

預設Cloud Services集可以使用自定義Cloud Service類型進行擴展。 這允許您以結構化方式將自定義標籤注入頁面。 這將主要用於第三方分析提供商，例如Google Analytics、Chartbeat等。 Cloud Services從父頁繼承到子頁，能夠在任何級別中斷繼承。

>[!NOTE]
>
>此用於建立新Cloud Service的逐步指南是使用Google Analytics的示例。 你的用例可能不適用。

1. 在CRXDE Lite中，在 `/apps`:

   * **名稱**: `acs`
   * **類型**: `nt:folder`

1. 在 `/apps/acs`:

   * **名稱**: `analytics`
   * **類型**: `sling:Folder`

1. 在下面建立2個新節點 `/apps/acs/analytics`:

   * **名稱**:元件
   * **類型**: `sling:Folder`

   和

   * **名稱**:模板
   * **類型**: `sling:Folder`


1. 按一下右鍵 `/apps/acs/analytics/components`。 選擇 **建立……** 後跟 **建立元件……** 開啟的對話框允許您指定：

   * **標籤**: `googleanalyticspage`
   * **標題**: `Google Analytics Page`
   * **超級類型**: `cq/cloudserviceconfigs/components/configpage`
   * **組**: `.hidden`

1. 按一下 **下一個** 兩次，然後指定：

   * **允許的父項:** `acs/analytics/templates/googleanalytics`

   按一下 **下一個** 按一下兩次 **確定**。

1. 將屬性添加到 `googleanalyticspage`:

   * **名稱:** `cq:defaultView`
   * **值:** `html`

1. 建立名為 `content.jsp` 在 `/apps/acs/analytics/components/googleanalyticspage`，內容如下：

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

1. 在 `/apps/acs/analytics/components/googleanalyticspage/`:

   * **名稱**: `dialog`
   * **類型**: `cq:Dialog`
   * **屬性**:

      * **名稱**: `title`
      * **類型**: `String`
      * **值**: `Google Analytics Config`
      * **名稱**: `xtype`
      * **類型**: `String`
      * **值**: `dialog`

1. 在 `/apps/acs/analytics/components/googleanalyticspage/dialog`:

   * **名稱**: `items`
   * **類型**: `cq:Widget`
   * **屬性**:

      * **名稱**: `xtype`
      * **類型**: `String`
      * **值**: `tabpanel`

1. 在 `/apps/acs/analytics/components/googleanalyticspage/dialog/items`:

   * **名稱**: `items`
   * **類型**: `cq:WidgetCollection`

1. 在 `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`:

   * **名稱**:頁籤
   * **類型**: `cq:Panel`
   * **屬性**:

      * **名稱**: `title`
      * **類型**: `String`
      * **值**: `Config`

1. 在 `/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`:

   * **名稱**:項目
   * **類型**: `nt:unstructured`
   * **屬性**:

      * **名稱**: `fieldLabel`
      * **類型**:字串
      * **值**:帳戶ID

      * **名稱**: `fieldDescription`
      * **類型**: `String`
      * **值**: `The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **名稱**: `name`
      * **類型**: `String`
      * **值**: `./accountID`
      * **名稱**: `validateOnBlur`
      * **類型**: `String`
      * **值**: `true`
      * **名稱**: `xtype`
      * **類型**: `String`
      * **值**: `textfield`

1. 複製 `/libs/cq/cloudserviceconfigs/components/configpage/body.jsp` 至 `/apps/acs/analytics/components/googleanalyticspage/body.jsp` 改變 `libs` 至 `apps` 將指令碼引用線上79作為完全限定的路徑。
1. 在 `/apps/acs/analytics/templates/`:

   * 與 **資源類型** = `acs/analytics/components/googleanalyticspage`
   * 與 **標籤** = `googleanalytics`
   * 與 **標題**= `Google Analytics Configuration`
   * 與 **允許的路徑** = `/etc/cloudservices/googleanalytics(/.*)?`
   * 與 **允許的子項** = `/apps/acs/analytics/templates/googleanalytics`
   * 與 **sling:resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` （在模板節點上，而不是jcr:content節點）
   * 與 **cq:designPath** = `/etc/designs/cloudservices/googleanalytics` （關於jcr：內容）

1. 建立新元件： `/apps/acs/analytics/components/googleanalytics`。

   將以下內容添加到 `googleanalytics.jsp`:

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

   這應基於配置屬性輸出自定義標籤。

1. 導航到 `http://localhost:4502/miscadmin#/etc/cloudservices` 並建立新頁面：

   * **標題**: `Google Analytics`
   * **名稱**: `googleanalytics`

   回到CRXDE Lite，然後 `/etc/cloudservices/googleanalytics`，將以下屬性添加到 `jcr:content`:

   * **名稱**: `componentReference`
   * **類型**: `String`
   * **值**: `acs/analytics/components/googleanalytics`


1. 導航到新建立的「服務」頁( `http://localhost:4502/etc/cloudservices/googleanalytics.html`)，然後按一下 **+** 建立新配置：

   * **父設定**: `/etc/cloudservices/googleanalytics`
   * **標題:**  `My First GA Config`

   選擇 **Google Analytics配置** 按一下 **建立**。

1. 輸入 **帳戶ID**，例如 `AA-11111111-1`。 按一下&#x200B;**「確定」**。
1. 導航到頁面，並在頁面屬性中的 **Cloud Services** 頁籤。
1. 該頁面將添加自定義標籤。
