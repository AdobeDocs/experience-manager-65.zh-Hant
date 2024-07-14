---
title: 建立自訂Cloud Service
description: 預設Cloud Services集可使用自訂Cloud Service型別擴展
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 9414c77a-b180-4440-8386-e6eb4426e475
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 11%

---

# 建立自訂Cloud Service{#creating-a-custom-cloud-service}

預設Cloud Services集可使用自訂Cloud Service型別擴展。 這可讓您以結構化的方式將自訂標籤插入頁面中。 這主要用於協力廠商分析提供者，例如Google Analytics、圖表等。 Cloud Service會從父頁面繼承至子頁面，且能夠在任何層級中斷繼承。

>[!NOTE]
>
>此建立Cloud Service的逐步指南是使用Google Analytics的範例。 並非所有事項都適用於您的使用案例。

1. 在CRXDE Lite中，在`/apps`下建立節點：

   * **名稱**：`acs`
   * **類型**：`nt:folder`

1. 在`/apps/acs`下建立節點：

   * **名稱**：`analytics`
   * **類型**：`sling:Folder`

1. 在`/apps/acs/analytics`下建立兩個節點：

   * **名稱**：元件
   * **類型**：`sling:Folder`

   和

   * **名稱**：範本
   * **類型**：`sling:Folder`

1. 用滑鼠右鍵按一下`/apps/acs/analytics/components`。 選取&#x200B;**建立……**，然後選取&#x200B;**建立元件……**&#x200B;開啟的對話方塊可讓您指定：

   * **標籤**： `googleanalyticspage`
   * **標題**： `Google Analytics Page`
   * **超級型別**： `cq/cloudserviceconfigs/components/configpage`
   * **群組**： `.hidden`

1. 按兩次「下一步&#x200B;****」並指定：

   * **允許的父系：** `acs/analytics/templates/googleanalytics`

   按兩下&#x200B;**下一步**，然後按一下&#x200B;**確定**。

1. 新增屬性至`googleanalyticspage`：

   * **名稱：** `cq:defaultView`
   * **值：** `html`

1. 在`/apps/acs/analytics/components/googleanalyticspage`下建立名為`content.jsp`的檔案，其內容如下：

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

1. 在`/apps/acs/analytics/components/googleanalyticspage/`下建立節點：

   * **名稱**：`dialog`
   * **類型**：`cq:Dialog`
   * **屬性**：

      * **名稱**：`title`
      * **類型**：`String`
      * **值**：`Google Analytics Config`
      * **名稱**：`xtype`
      * **類型**：`String`
      * **值**：`dialog`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog`下建立節點：

   * **名稱**：`items`
   * **類型**：`cq:Widget`
   * **屬性**：

      * **名稱**：`xtype`
      * **類型**：`String`
      * **值**：`tabpanel`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items`下建立節點：

   * **名稱**：`items`
   * **類型**：`cq:WidgetCollection`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items`下建立節點：

   * **名稱**： tab1
   * **類型**：`cq:Panel`
   * **屬性**：

      * **名稱**：`title`
      * **類型**：`String`
      * **值**：`Config`

1. 在`/apps/acs/analytics/components/googleanalyticspage/dialog/items/items/tab1`下建立節點：

   * **名稱**：專案
   * **類型**：`nt:unstructured`
   * **屬性**：

      * **名稱**：`fieldLabel`
      * **型別**：字串
      * **值**：帳戶識別碼

      * **名稱**：`fieldDescription`
      * **類型**：`String`
      * **值**：`The account ID assigned by Google. Usually in the form UA-NNNNNN-N`

      * **名稱**：`name`
      * **類型**：`String`
      * **值**：`./accountID`
      * **名稱**：`validateOnBlur`
      * **類型**：`String`
      * **值**：`true`
      * **名稱**：`xtype`
      * **類型**：`String`
      * **值**：`textfield`

1. 將`/libs/cq/cloudserviceconfigs/components/configpage/body.jsp`複製到`/apps/acs/analytics/components/googleanalyticspage/body.jsp`並在第34行將`libs`變更為`apps`，並將第79行的指令碼參考設為完整路徑。
1. 在`/apps/acs/analytics/templates/`下建立範本：

   * 具有&#x200B;**資源型別** = `acs/analytics/components/googleanalyticspage`
   * 具有&#x200B;**標籤** = `googleanalytics`
   * 具有&#x200B;**標題**= `Google Analytics Configuration`
   * **allowedPath** = `/etc/cloudservices/googleanalytics(/.*)?`
   * 具有&#x200B;**allowedChildren** = `/apps/acs/analytics/templates/googleanalytics`
   * 具有&#x200B;**sling：resourceSuperType** = `cq/cloudserviceconfigs/templates/configpage` （在範本節點上，而非jcr：content節點）
   * 使用&#x200B;**cq：designPath** = `/etc/designs/cloudservices/googleanalytics` （在jcr：content上）

1. 建立元件： `/apps/acs/analytics/components/googleanalytics`。

   將下列內容新增至`googleanalytics.jsp`：

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

1. 導覽至`http://localhost:4502/miscadmin#/etc/cloudservices`並建立頁面：

   * **標題**： `Google Analytics`
   * **名稱**：`googleanalytics`

   返回CRXDE Lite，並在`/etc/cloudservices/googleanalytics`底下，將下列屬性新增到`jcr:content`：

   * **名稱**：`componentReference`
   * **類型**：`String`
   * **值**：`acs/analytics/components/googleanalytics`

1. 導覽至新建立的服務頁面( `http://localhost:4502/etc/cloudservices/googleanalytics.html`)，然後按一下&#x200B;**+**&#x200B;以建立設定：

   * **父設定**： `/etc/cloudservices/googleanalytics`
   * **標題：** `My First GA Config`

   選擇&#x200B;**Google Analytics組態**&#x200B;並按一下&#x200B;**建立**。

1. 輸入&#x200B;**帳戶ID**，例如`AA-11111111-1`。 按一下&#x200B;**「確定」**。
1. 導覽至頁面，並在&#x200B;**Cloud Service**&#x200B;標籤下方的頁面屬性中新增新建立的設定。
1. 頁面中將會新增自訂標籤。
