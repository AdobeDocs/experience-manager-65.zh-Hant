---
title: 以JSON格式取得頁面資訊
seo-title: 以JSON格式取得頁面資訊
description: 若要取得頁面資訊，請傳送要求至PageInfo servlet以取得JSON格式的頁面中繼資料
seo-description: 若要取得頁面資訊，請傳送要求至PageInfo servlet以取得JSON格式的頁面中繼資料
uuid: fb4f56b9-55e2-4622-a0d1-a86d6f2cce86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 505bf3e3-ce3c-40aa-9619-e1b9f6634deb
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71

---


# 以JSON格式取得頁面資訊{#obtaining-page-information-in-json-format}

若要取得頁面資訊，請傳送要求至PageInfo servlet以取得JSON格式的頁面中繼資料。

PageInfo servlet返回有關儲存庫中資源的資訊。 servlet會綁定到URL, `https://<server>:<port>/libs/wcm/core/content/pageinfo.json` 並使用參 `path` 數來標識資源。 以下範例URL會傳回有關節點的 `/content/we-retail/us/en` 資訊：

```shell
http://localhost:4502/libs/wcm/core/content/pageinfo.json?path=/content/we-retail/us/en
```

>[!NOTE]
>
>如果您需要JSON格式的頁面資訊，以提供內容傳送至非傳統AEM網頁的頻道，例如：
>
>* 單頁應用程式
>* 原生行動應用程式
>* AEM外部的其他通道和觸點
>
>
請參閱內容服 [務的檔案JSON匯出器](/help/sites-developing/json-exporter.md)。

## 頁面資訊提供者 {#page-information-providers}

頁面元件可與產生頁面中繼資料的一 `com.day.cq.wcm.api.PageInfoProvider` 或多個服務相關聯。 PageInfo servlet會呼叫每個PageInfoProvider服務並匯總中繼資料：

1. HTTP用戶端會傳送請求至PageInfo servlet，其中包含頁面的URL。
1. PageInfo servlet會發現哪個元件轉換頁面。
1. PageInfo servlet會呼叫與元件相關聯的每個PageInfoProvider。
1. servlet會匯整每個PageInfoProvider傳回的中繼資料，並將中繼資料新增至JSON物件的HTTP回應。

![chlimage_1-2](assets/chlimage_1-2a.png)

>[!NOTE]
>
>與PageInfoProviders類似，請使用ListInfoProviders來更新JSON格式的資訊清單。 (請參 [閱自訂網站管理控制台](/help/sites-developing/customizing-siteadmin.md))。

## 預設頁面資訊提供者 {#default-page-information-providers}

該 `/libs/foundation/components/page` 元件與以下PageInfoProvider服務關聯：

* **** 預設頁面狀態提供者：頁面狀態的相關資訊，例如是否已鎖定頁面、頁面是否為作用中工作流程的裝載，以及頁面可使用哪些工作流程。
* **** 即時關係資訊提供者：有關多網站管理(MSM)的資訊，例如頁面是否屬於藍色印刷，以及是否為即時文案。
* **** 內容語言Servlet:目前頁面的語言，以及頁面可用之每種語言的相關資訊。
* **** 工作流狀態提供程式：將頁面作為裝載的執行工作流程的狀態資訊。
* **** 工作流包資訊提供程式：有關儲存在儲存庫中的每個工作流包的資訊，以及每個包是否包含當前資源。
* **** 模擬器資訊提供者：有關此資源可用之行動裝置模擬器的資訊。 如果頁面元件未演算行動頁面，則不提供模擬器。
* **** 注釋資訊提供程式：頁面上的註解相關資訊。

例如，PageInfo servlet會傳回節點的下列JSON回 `/content/we-retail/us/en` 應：

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

## 篩選工作流程套件資訊 {#filtering-workflow-package-information}

配置Day CQ WCM Workflow Package Info Provider服務，使其僅返回您感興趣的工作流程包的相關資訊。 預設情況下，Workflow Package Info Provider服務返回有關儲存庫中每個工作流包的資訊。 重複處理工作流程套件的子集會佔用較少的伺服器資源。

>[!NOTE]
>
>Sidekick的「工作流程」索引標籤使用PageInfo servlet來取得工作流程封裝的清單。 從清單中，您可以選擇要向其添加當前頁的包。 您建立的篩選器會影響此清單。


服務的ID為 `com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider`。 若要建立篩選，請指定屬性的 `workflowpackageinfoprovider.filter` 值。

屬性值的前置詞為+或——字元，後接包路徑：

* 路徑是工作流包的根節點的路徑。 路徑使用FileVault語法。
* 若要包含套件，請使用+首碼。
* 要排除包，請使用——前置詞。

服務會套用所有篩選器的累積結果。 例如，下列篩選值會排除除「版本」檔案夾中的工作流程套件以外的所有工作流程套件：

```
-/etc/workflow/packages(/.*)?
+/etc/workflow/packages/Editions(/.&ast;)?
```

>[!NOTE]
>
>使用AEM時，有數種方法可管理此類服務的組態設定。 如需 [完整詳細資訊](/help/sites-deploying/configuring-osgi.md) ，請參閱設定OSGi。

例如，若要使用CRXDE Lite來設定服務：

1. 開啟CRXDE Lite([http://localhost:4502/crx/de](http://localhost:4502/crx/de))。
1. 在應用程式的config資料夾中，建立節點：

   * 名稱: `com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider`
   * 類型: `sling:OsgiConfig`

1. 選擇節點並添加屬性：

   * 名稱: `workflowpackageinfoprovider.filter`
   * 類型: `String[]`
   * 值：使用正確格式的工作流包路徑。

1. 按一下「全部儲存」。

要在項目源中配置服務，請執行以下操作：

1. 在專案來源中尋找或建立AEM應用程式的設定檔案夾。

   例如，如果您使用Content Package Maven Plugin的多模組原型來建立專案，則資料夾路徑為 `<projectroot>/content/src/ for example content/src/main/content/jcr_root/apps/<appname>/config`。
1. 在config檔案夾中，建立名為com.day.cq.wcm.workflow.impl.WorkflowPackageInfoProvider.xml的文字檔案
1. 將下列文字複製至檔案：

   ```
   <?xml version="1.0" encoding="UTF-8"?>
    <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0"
    xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="sling:OsgiConfig"
    workflowpackageinfoprovider.filter="[]"/>
   ```

1. 在包含屬性`[]`的方括弧() `workflowpackageinfoprovider.filter` 內，輸入以逗號分隔的篩選值清單，類似下列範例：

   `workflowpackageinfoprovider.filter="[-/etc/workflow/packages(/.*)?,+/etc/workflow/packages/Editions(/.*)?]"/>`

1. 儲存檔案。

## 建立頁面資訊提供者 {#creating-a-page-information-provider}

建立自訂的頁面資訊提供者服務，以新增您的應用程式可輕鬆取得的頁面中繼資料。

1. 實作介 `com.day.cq.wcm.api.PageInfoProvider` 面。
1. 將類捆綁並部署為OSGi服務。
1. 在應用程式中建立頁面元件。 用 `foundation/components/page` 作屬性的 `sling:resourceSuperType` 值。

1. 在名為的元件節點下添加一個節點 `cq:infoProviders`。
1. 在節點 `cq:infoProviders` 下方，為PageInfoProvider服務新增節點。 您可以指定節點的任何名稱。
1. 將下列屬性新增至您的PageInfoProvider節點：

   * 名稱：className
   * 類型：字串
   * 值：PageInfoProvider服務的PID。

對於使用應用程式頁面元件作為資源 `sling:resourceType`的PageInfo servlet會除了傳回預設的PageInfoProvider中繼資料外，傳回自訂的PageInfoProvider中繼資料。

### 範例PageInfoProvider實作 {#example-pageinfoprovider-implementation}

下列Java類別會實 [作PageInfoProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) ，並傳回目前頁面資源的已發佈URL。

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

下列範例在CRXDE Lite中顯示已設定為使用PageUrlInfoProvider服務的頁面元件：

![chlimage_1-3](assets/chlimage_1-3a.png)

PageUrlInfoProvider服務會傳回節點的下列資 `/content/we-retail/us/en` 料：

```xml
"URLs": {
    "publishURL": "http://localhost:4503/content/we-retail/us/en"
}
```

