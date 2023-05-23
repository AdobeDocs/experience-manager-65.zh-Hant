---
title: 獲取JSON格式的頁資訊
seo-title: Obtaining Page Information in JSON Format
description: 要獲取頁面資訊，請向PageInfo servlet發送請求，以獲取JSON格式的頁面元資料
seo-description: To obtain the page information, send a request to the PageInfo servlet to obtain the page metadata in JSON format
uuid: fb4f56b9-55e2-4622-a0d1-a86d6f2cce86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 505bf3e3-ce3c-40aa-9619-e1b9f6634deb
exl-id: 7c856e87-9f90-435d-aceb-994f10ea6f50
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 1%

---

# 獲取JSON格式的頁資訊{#obtaining-page-information-in-json-format}

要獲取頁面資訊，請向PageInfo servlet發送請求，以獲取JSON格式的頁面元資料。

PageInfo Servlet返回有關儲存庫中資源的資訊。 Servlet綁定到URL `https://<server>:<port>/libs/wcm/core/content/pageinfo.json` 使用 `path` 參數來標識資源。 以下示例URL返回有關 `/content/we-retail/us/en` 節點：

```shell
http://localhost:4502/libs/wcm/core/content/pageinfo.json?path=/content/we-retail/us/en
```

>[!NOTE]
>
>如果您需要JSON格式的頁面資訊來向非傳統網頁的通道提供內AEM容，例如：
>
>* 單頁應用程式
>* 本機移動應用程式
>* 外部的其他通道和觸AEM點
>
>查看文檔 [Content Services的JSON導出器](/help/sites-developing/json-exporter.md)。

## 頁面資訊提供程式 {#page-information-providers}

頁面元件可以與一個或多個關聯 `com.day.cq.wcm.api.PageInfoProvider` 生成頁元資料的服務。 PageInfo Servlet調用每個PageInfoProvider服務並聚合元資料：

1. HTTP客戶端向PageInfo Servlet發送請求，該PageInfo Servlet包括該頁的URL。
1. PageInfo Servlet可發現呈現頁面的元件。
1. PageInfo Servlet調用與元件關聯的每個PageInfoProvider。
1. Servlet聚合每個PageInfoProvider返回的元資料，並將元資料添加到JSON對象中的HTTP響應。

![chlimage_1-2](assets/chlimage_1-2a.png)

>[!NOTE]
>
>與PageInfoProviders類似，使用ListInfoProviders以JSON格式更新資訊清單。 (請參閱 [自定義網站管理控制台](/help/sites-developing/customizing-siteadmin.md)。)

## 預設頁面資訊提供程式 {#default-page-information-providers}

的 `/libs/foundation/components/page` 元件與以下PageInfoProvider服務關聯：

* **預設頁面狀態提供程式：** 有關頁面狀態的資訊，如是否已鎖定、頁面是否是活動工作流的負載以及頁面可用的工作流。
* **即時關係資訊提供程式：** 有關多站點管理(MSM)的資訊，如頁面是否是藍色打印的一部分，以及它是否是即時拷貝。
* **內容語言Servlet:** 當前頁面的語言，以及有關頁面可用的每種語言的資訊。
* **工作流狀態提供程式：** 有關將頁面作為負載的正在運行的工作流的狀態資訊。
* **工作流包資訊提供程式：** 有關儲存在儲存庫中的每個工作流包的資訊，以及每個包是否包含當前資源。
* **模擬器資訊提供程式：** 有關可用於此資源的移動設備模擬器的資訊。 如果頁面元件未呈現移動頁面，則沒有模擬器可用。
* **注釋資訊提供程式：** 有關頁面上注釋的資訊。

例如，PageInfo servlet為 `/content/we-retail/us/en` 節點：

```
{
   "status":{
      "path":"/content/we-retail/us/en",
      "isLocked":false,
      "lockOwner":"",
      "canUnlock":false,
      "lastModified":1467202845038,
      "lastModifiedBy":"admin",
      "timeUntilValid":0,
      "onTime":0,
      "offTime":0,
      "replication":{
         "numQueued":0
      },
      "isDesignable":true,
      "isDeveloper":true
   },
   "isPage":true,
   "pageResourceType":"weretail/components/structure/page",
   "enableFragmentIdentifier":false,
   "workflow":{
      "isRunning":false
   },
   "workflows":{
      "wcm":{
         "models":[
            {
               "wid":"/etc/workflow/models/dam/adddamsize/jcr:content/model",
               "label":"Add Asset Size",
               "label_xss":"Add Asset Size"
            },
            {
               "wid":"/etc/workflow/models/ac-newsletter-workflow-simple/jcr:content/model",
               "label":"Approve for Adobe Campaign",
               "label_xss":"Approve for Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/dam/dam-autotag-assets/jcr:content/model",
               "label":"DAM Smart Tag Assets",
               "label_xss":"DAM Smart Tag Assets"
            },
            {
               "wid":"/etc/workflow/models/dam/update_asset/jcr:content/model",
               "label":"DAM Update Asset",
               "label_xss":"DAM Update Asset"
            },
            {
               "wid":"/etc/workflow/models/cloudservices/DTM_bundle_download/jcr:content/model",
               "label":"Default DTM Bundle Download",
               "label_xss":"Default DTM Bundle Download"
            },
            {
               "wid":"/etc/workflow/models/dam/dam_download_asset/jcr:content/model",
               "label":"Download Asset",
               "label_xss":"Download Asset"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-thumbnail-replacement/jcr:content/model",
               "label":"Dynamic Media Video Thumbnail Replacement",
               "label_xss":"Dynamic Media Video Thumbnail Replacement"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail/jcr:content/model",
               "label":"Dynamic Media Video User Uploaded Thumbnail Process",
               "label_xss":"Dynamic Media Video User Uploaded Thumbnail Process"
            },
            {
               "wid":"/etc/workflow/models/projects/approval_workflow/jcr:content/model",
               "label":"Project Approval Workflow",
               "label_xss":"Project Approval Workflow"
            },
            {
               "wid":"/etc/workflow/models/publish_example/jcr:content/model",
               "label":"Publish Example",
               "label_xss":"Publish Example"
            },
            {
               "wid":"/etc/workflow/models/publish_to_campaign/jcr:content/model",
               "label":"Publish to Adobe Campaign",
               "label_xss":"Publish to Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_publish_to_youtube/jcr:content/model",
               "label":"Publish to YouTube",
               "label_xss":"Publish to YouTube"
            },
            {
               "wid":"/etc/workflow/models/projects/request_copy/jcr:content/model",
               "label":"Request Copy",
               "label_xss":"Request Copy"
            },
            {
               "wid":"/etc/workflow/models/request_for_activation/jcr:content/model",
               "label":"Request for Activation",
               "label_xss":"Request for Activation"
            },
            {
               "wid":"/etc/workflow/models/request_for_deactivation/jcr:content/model",
               "label":"Request for Deactivation",
               "label_xss":"Request for Deactivation"
            },
            {
               "wid":"/etc/workflow/models/request_for_deletion/jcr:content/model",
               "label":"Request for Deletion",
               "label_xss":"Request for Deletion"
            },
            {
               "wid":"/etc/workflow/models/request_to_complete_move_operation/jcr:content/model",
               "label":"Request to complete Move operation",
               "label_xss":"Request to complete Move operation"
            },
            {
               "wid":"/etc/workflow/models/screens-update-asset/jcr:content/model",
               "label":"Screens Update Asset",
               "label_xss":"Screens Update Asset"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_remove_from_youtube/jcr:content/model",
               "label":"Unpublish from YouTube",
               "label_xss":"Unpublish from YouTube"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/create_language_copy/jcr:content/model",
               "label":"WCM: Create Language Copy",
               "label_xss":"WCM: Create Language Copy"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/prepare_translation_project/jcr:content/model",
               "label":"WCM: Prepare Translation Project",
               "label_xss":"WCM: Prepare Translation Project"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/translate-i18n-dictionary/jcr:content/model",
               "label":"WCM: Prepare and Translate I18n-Dictionary",
               "label_xss":"WCM: Prepare and Translate I18n-Dictionary"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/sync_translation_job/jcr:content/model",
               "label":"WCM: Sync Translation Job",
               "label_xss":"WCM: Sync Translation Job"
            },
            {
               "wid":"/etc/workflow/models/wcm-translation/update_language_copy/jcr:content/model",
               "label":"WCM: Update Language Copy",
               "label_xss":"WCM: Update Language Copy"
            }
         ]
      },
      "translation":{
         "models":[
            {
               "wid":"/etc/workflow/models/dam/adddamsize/jcr:content/model",
               "label":"Add Asset Size",
               "label_xss":"Add Asset Size"
            },
            {
               "wid":"/etc/workflow/models/ac-newsletter-workflow-simple/jcr:content/model",
               "label":"Approve for Adobe Campaign",
               "label_xss":"Approve for Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/dam/dam-autotag-assets/jcr:content/model",
               "label":"DAM Smart Tag Assets",
               "label_xss":"DAM Smart Tag Assets"
            },
            {
               "wid":"/etc/workflow/models/cloudservices/DTM_bundle_download/jcr:content/model",
               "label":"Default DTM Bundle Download",
               "label_xss":"Default DTM Bundle Download"
            },
            {
               "wid":"/etc/workflow/models/dam/dam_download_asset/jcr:content/model",
               "label":"Download Asset",
               "label_xss":"Download Asset"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-thumbnail-replacement/jcr:content/model",
               "label":"Dynamic Media Video Thumbnail Replacement",
               "label_xss":"Dynamic Media Video Thumbnail Replacement"
            },
            {
               "wid":"/etc/workflow/models/dam/dynamic-media-video-user-uploaded-thumbnail/jcr:content/model",
               "label":"Dynamic Media Video User Uploaded Thumbnail Process",
               "label_xss":"Dynamic Media Video User Uploaded Thumbnail Process"
            },
            {
               "wid":"/etc/workflow/models/projects/approval_workflow/jcr:content/model",
               "label":"Project Approval Workflow",
               "label_xss":"Project Approval Workflow"
            },
            {
               "wid":"/etc/workflow/models/publish_to_campaign/jcr:content/model",
               "label":"Publish to Adobe Campaign",
               "label_xss":"Publish to Adobe Campaign"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_publish_to_youtube/jcr:content/model",
               "label":"Publish to YouTube",
               "label_xss":"Publish to YouTube"
            },
            {
               "wid":"/etc/workflow/models/projects/request_copy/jcr:content/model",
               "label":"Request Copy",
               "label_xss":"Request Copy"
            },
            {
               "wid":"/etc/workflow/models/request_for_deletion/jcr:content/model",
               "label":"Request for Deletion",
               "label_xss":"Request for Deletion"
            },
            {
               "wid":"/etc/workflow/models/request_to_complete_move_operation/jcr:content/model",
               "label":"Request to complete Move operation",
               "label_xss":"Request to complete Move operation"
            },
            {
               "wid":"/etc/workflow/models/screens-update-asset/jcr:content/model",
               "label":"Screens Update Asset",
               "label_xss":"Screens Update Asset"
            },
            {
               "wid":"/etc/workflow/models/translation/jcr:content/model",
               "label":"Translation Prepare",
               "label_xss":"Translation Prepare"
            },
            {
               "wid":"/etc/workflow/models/s7dam/request_to_remove_from_youtube/jcr:content/model",
               "label":"Unpublish from YouTube",
               "label_xss":"Unpublish from YouTube"
            }
         ]
      }
   },
   "translation":{

   },
   "design":{
      "path":"/conf/we-retail/settings/wcm/templates/hero-page/policies",
      "lastModified":0
   },
   "componentsRef":"/libs/wcm/core/content/components.1497341312569.json",
   "editableTemplate":"/conf/we-retail/settings/wcm/templates/hero-page",
   "msm":{
      "msm:isLiveCopy":true,
      "msm:isInBlueprint":false,
      "msm:isSource":false
   },
   "launches":{
      "isLaunch":false,
      "isInLaunch":false
   },
   "language":"en",
   "languages":{
      "rows":[
         {
            "path":"/content/we-retail/us/en",
            "exists":true,
            "hasContent":true,
            "lastModified":0,
            "iso":"en",
            "country":"gb",
            "language":"English"
         },
         {
            "path":"/content/we-retail/us/es",
            "exists":true,
            "hasContent":true,
            "lastModified":0,
            "iso":"es",
            "country":"es",
            "language":"Spanish"
         }
      ]
   },
   "workflowInfo":{
      "isRunning":false
   },
   "workflowPackageInfo":{
      "workflowPackages":[

      ],
      "selectedWorkflowPackages":[

      ],
      "runningSelectedWorkflowPackages":[

      ]
   },
   "emulators":{
      "groups":{
         "responsive":{
            "title":"Responsive Devices",
            "description":"The devices in this group are able to display a website built using responsive design patterns.",
            "path":"/etc/mobile/groups/responsive",
            "galaxy5":{
               "text":"Galaxy S5",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/galaxy5",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":1080,
               "height":1920,
               "device-pixel-ratio":3
            },
            "ipad":{
               "text":"iPad",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/ipad",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":768,
               "height":1024,
               "device-pixel-ratio":1
            },
            "iphone5":{
               "text":"iPhone 5",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone5",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":640,
               "height":1136,
               "device-pixel-ratio":2
            },
            "iphone6":{
               "text":"iPhone 6",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone6",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":750,
               "height":1334,
               "device-pixel-ratio":2
            },
            "iphone4":{
               "text":"iPhone 4",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone4",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":640,
               "height":960,
               "device-pixel-ratio":2
            },
            "iphone6plus":{
               "text":"iPhone 6 Plus",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/ios/iphone6plus",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":1080,
               "height":1920,
               "device-pixel-ratio":2.6
            },
            "nexuss":{
               "text":"Nexus S",
               "action":"start",
               "path":"/libs/wcm/mobile/components/emulators/nexuss",
               "canRotate":true,
               "hasTouchScrolling":true,
               "contentCssPath":"/etc/mobile/groups/responsive/static.css",
               "width":320,
               "height":533,
               "device-pixel-ratio":1
            }
         }
      }
   },
   "annotations":[

   ],
   "permissions":{
      "modify":true,
      "replicate":true,
      "read":true,
      "create":true,
      "delete":true,
      "acl_read":true,
      "acl_edit":true
   },
   "isTargetable":"true",
   "responsive":{
      "breakpoints":{
         "phone":{
            "width":650,
            "title":"Smaller Screen"
         },
         "tablet":{
            "width":1200,
            "title":"Tablet"
         }
      }
   }
}
```

## 篩選工作流包資訊 {#filtering-workflow-package-information}

配置「第一天CQ WCM工作流包資訊提供程式」服務，以便它僅返回有關您感興趣的工作流包的資訊。 預設情況下，工作流包資訊提供程式服務返回有關儲存庫中每個工作流包的資訊。 對工作流包的子集進行迭代使用較少的伺服器資源。

>[!NOTE]
>
>Sidekick的「工作流」頁籤使用PageInfo servlet獲取工作流包的清單。 從清單中，可以選擇要向其添加當前頁面的包。 您建立的篩選器會影響此清單。

服務的ID為 `com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider`。 要建立篩選器，請為 `workflowpackageinfoprovider.filter` 屬性。

屬性值的前置詞為+或 — 字元，後跟包路徑：

* 路徑是工作流包的根節點的路徑。 路徑使用FileVault語法。
* 要包括包，請使用+前置詞。
* 要排除包，請使用 — 前置詞。

該服務應用所有篩選器的累積結果。 例如，以下篩選器值排除了除Editions資料夾中的工作流包以外的所有工作流包：

```
-/etc/workflow/packages(/.*)?
+/etc/workflow/packages/Editions(/.&ast;)?
```

>[!NOTE]
>
>使用時，AEM有多種方法管理此類服務的配置設定。 請參閱 [配置OSGi](/help/sites-deploying/configuring-osgi.md) 的雙曲餘切值。

例如，要使用CRXDE Lite配置服務：

1. 開啟CRXDE Lite([http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在應用程式的config資料夾中，建立一個節點：

   * 名稱: `com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider`
   * 類型: `sling:OsgiConfig`

1. 選擇節點並添加屬性：

   * 名稱: `workflowpackageinfoprovider.filter`
   * 類型: `String[]`
   * 值：使用正確格式的工作流包路徑。

1. 按一下「全部保存」。

要在項目源中配置服務，請執行以下操作：

1. 在項目源中查找或創AEM建應用程式的配置資料夾。

   例如，如果使用內容包Maven插件的多模組原型建立項目，則資料夾路徑為 `<projectroot>/content/src/ for example content/src/main/content/jcr_root/apps/<appname>/config`。
1. 在配置資料夾中，建立一個名為com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider.xml的文本檔案
1. 將以下文本複製到檔案：

   ```
   <?xml version="1.0" encoding="UTF-8"?>
    <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:OsgiConfig"
    workflowpackageinfoprovider.filter="[]"/>
   ```

1. 括弧內(`[]`) `workflowpackageinfoprovider.filter` 屬性，鍵入與以下示例類似的以逗號分隔的篩選器值清單：

   `workflowpackageinfoprovider.filter="[-/etc/workflow/packages(/.*)?,+/etc/workflow/packages/Editions(/.*)?]"/>`

1. 儲存檔案。

## 建立頁面資訊提供程式 {#creating-a-page-information-provider}

建立自定義頁面資訊提供程式服務，以添加應用程式可以輕鬆獲取的頁面元資料。

1. 實作 `com.day.cq.wcm.api.PageInfoProvider` 介面。 
1. 將類捆綁並部署為OSGi服務。
1. 在應用程式中建立頁面元件。 使用 `foundation/components/page` 值 `sling:resourceSuperType` 屬性。

1. 在名為的元件節點下添加節點 `cq:infoProviders`。
1. 在 `cq:infoProviders` 節點，為PageInfoProvider服務添加節點。 可以為節點指定任何名稱。
1. 將以下屬性添加到PageInfoProvider節點：

   * 名稱：類名
   * 類型：字串
   * 值：PageInfoProvider服務的PID。

對於將應用程式頁元件用作 `sling:resourceType`,PageInfo servlet除了預設的PageInfoProvider元資料外，還返回自定義PageInfoProvider元資料。

### 示例PageInfoProvider實現 {#example-pageinfoprovider-implementation}

以下Java類實現 [PageInfoProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) 並返回當前頁資源的已發佈URL。

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.ReferenceCardinality;
import org.apache.felix.scr.annotations.Service;
import org.apache.felix.scr.annotations.Reference;

import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;

import org.apache.sling.commons.json.JSONException;
import org.apache.sling.commons.json.JSONObject;

import com.day.cq.wcm.api.Page;
import com.day.cq.wcm.api.PageInfoProvider;

@Component(metatype = false)
@Properties({
 @Property(name="service.description", value="Returns the public URL of a resource.")
})
@Service
public class PageUrlInfoProvider implements PageInfoProvider {

 @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
 private com.day.cq.commons.Externalizer externalizer;

 private String fetchExternalUrl(ResourceResolver rr, String path) {
  return externalizer.publishLink(rr, path);
 }

 public void updatePageInfo(SlingHttpServletRequest request, JSONObject info, Resource resource)
   throws JSONException {

  Page page = resource.adaptTo(Page.class);
  JSONObject urlinfo = new JSONObject();
  urlinfo.put("publishURL", fetchExternalUrl(null,page.getPath()));
  info.put("URLs",urlinfo);
 }
}
```

下面的示例在CRXDE Lite中顯示了配置為使用PageUrlInfoProvider服務的頁元件：

![chlimage_1-3](assets/chlimage_1-3a.png)

PageUrlInfoProvider服務返回以下資料 `/content/we-retail/us/en` 節點：

```xml
"URLs": {
    "publishURL": "http://localhost:4503/content/we-retail/us/en"
}
```
