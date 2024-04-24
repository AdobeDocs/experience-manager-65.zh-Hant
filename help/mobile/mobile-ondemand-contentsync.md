---
title: 具有內容同步功能的行動裝置
description: 請依照本頁所述瞭解Content Sync。 在Adobe Experience Manager (AEM)中編寫的頁面可作為應用程式內容，即使裝置離線亦然。 此外，由於AEM頁面是根據網頁標準，因此可跨平台運作，而讓您將其內嵌在任何原生包裝函式中。 此策略可減少開發工作量，並可讓您輕鬆更新應用程式內容。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2971'
ht-degree: 0%

---

# 具有內容同步功能的行動裝置{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建議針對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案，使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md)。

使用Content Sync來封裝內容，以便用於原生行動應用程式。 在Adobe Experience Manager (AEM)中編寫的頁面可作為應用程式內容，即使裝置離線亦然。 此外，由於AEM頁面是根據網頁標準，因此可跨平台運作，而讓您將其內嵌在任何原生包裝函式中。 此策略可減少開發工作量，並可讓您輕鬆更新應用程式內容。

Content Sync架構會建立包含網頁內容的封存檔案。 內容可以是簡單頁面、影像和PDF檔案或整個網頁應用程式的內容。 內容同步API提供從行動應用程式或建置程式存取封存檔案的許可權，以便內容可擷取並納入應用程式中。

下列步驟順序說明了Content Sync的典型使用案例：

1. AEM開發人員會建立Content Sync設定，指定要包含的內容。
1. 內容同步架構會收集並快取內容。
1. 在行動裝置上啟動行動應用程式，並向伺服器請求內容（以ZIP檔案傳送）。
1. 使用者端會將ZIP內容解壓縮至本機檔案系統。 ZIP檔案中的資料夾結構會模擬使用者端（例如瀏覽器）一般會從伺服器要求的路徑。
1. 使用者端會在內嵌瀏覽器中開啟內容，或以其他方式使用內容。
1. 稍後，使用者端會向伺服器要求更新內容。 Content Sync架構提供漸進式更新，以減少下載大小和時間，由於頻寬或資料量有限，這對於行動裝置而言可能很重要。

## 開發內容同步處理常式 {#developing-the-content-sync-handlers}

開發內容同步處理常式的部分准則如下：

* 處理常式必須實施 *com.day.cq.contentsync.handler.ContentUpdateHandler* （直接或擴充有此功能的類別）
* 處理常式可以擴充 *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 如果處理常式更新ContentSync快取，則只能報告true。 錯誤報告true會讓AEM在實際上並未發生更新時建立更新。
* 處理常式只應在內容變更時更新快取。 如果不需要白色，請勿寫入快取。 這會導致建立不必要的更新。

>[!NOTE]
>
>啟用 *ContentSync偵錯記錄* 透過封裝上的OSGI記錄器設定 *com.day.cq.contentsync*. 這可讓您追蹤哪些處理常式已執行，以及它們是否更新快取並回報更新快取。

## 設定內容同步內容 {#configuring-the-content-sync-content}

建立Content Sync設定，以指定傳遞至使用者端的ZIP檔案內容。 您可以建立任意數量的Content Sync設定。 每個設定都有名稱用於識別。

若要建立Content Sync設定，請新增 `cq:ContentSyncConfig` 節點到存放庫，使用 `sling:resourceType` 屬性設定為 `contentsync/config`. 此 `cq:ContentSyncConfig` 節點可以位於存放庫中的任何位置，但AEM發佈執行個體上的使用者必須能夠存取節點。 因此，您應該在下方新增節點 `/content`.

若要指定Content Sync ZIP檔案的內容，請將子節點新增至cq：ContentSyncConfig節點。 每個子節點的下列屬性會識別要包含的內容專案，以及新增內容專案時的處理方式：

* `path`：內容的位置。
* `type`：用於處理內容的設定型別名稱。 有數種型別可供使用，並在一節中說明 *設定型別*.

另請參閱 *Content Sync設定範例* 以取得詳細資訊。

建立Content Sync設定後，該設定會顯示在Content Sync主控台中。

>[!NOTE]
>
>Content Sync架構不會檢查Content Sync套件中是否包含資產和設計相關檔案的相依性。 請務必將所有必要的檔案包含在ZIP檔案中。

### 設定Content Sync下載的存取權 {#configuring-access-to-content-sync-downloads}

指定可從Content Sync下載的使用者或群組。 您可以設定可從所有Content Sync快取下載的預設使用者或群組，也可以覆寫預設值並設定特定Content Sync設定的存取權。

安裝AEM後，管理員群組的成員預設可從Content Sync下載。

#### 設定Content Sync下載的預設存取權 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager服務可控制Content Sync的存取權。 設定此服務，以指定預設可從Content Sync下載的使用者或群組。

如果您是 [使用Web主控台設定服務](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，輸入使用者或群組的名稱，作為「可授權遞補快取」屬性的值。

如果您是 [在存放庫中設定](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，請使用下列服務的相關資訊：

* PID： com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 屬性名稱： contentsync.fallback.authorizable

#### 覆寫內容同步快取的下載存取權 {#overriding-download-access-for-a-content-sync-cache}

若要設定特定內容同步設定的下載存取權，請將下列屬性新增至 `cq:ContentSyncConfig` 節點：

* 名稱：可授權
* 型別：字串
* 值：可下載的使用者或群組名稱。

例如，您的應用程式可讓使用者直接從Content Sync安裝更新。 若要讓所有使用者都能下載更新，您可以將可授權屬性的值設為 `everyone`.

如果 `cq:ContentSyncConfig` 節點沒有可授權屬性，為Day CQ Content Sync Manager服務的Fallback Cache Authorizable屬性設定的預設使用者或群組會決定誰可以下載。

### 設定使用者以更新內容同步快取 {#configuring-the-user-for-updating-a-content-sync-cache}

當使用者對內容同步快取執行更新時，特定使用者帳戶會代表使用者執行動作。 依預設，匿名使用者會更新所有Content Sync快取。

您可以覆寫預設使用者，並指定使用者或群組來更新特定的Content Sync快取。

若要覆寫預設使用者，請指定使用者或群組，透過將下列屬性新增到cq：ContentSyncConfig節點來執行特定Content Sync設定的更新：

* 名稱：`updateuser`
* 類型：`String`
* 值：可執行更新的使用者或群組名稱。

如果 `cq:ContentSyncConfig` 節點沒有 `updateuser` 屬性，預設 `anonymous` 使用者更新快取。

### 設定型別 {#configuration-types}

處理範圍包括從呈現簡單的JSON到完全呈現頁面（包括其參考資產）。 本節列出可用的組態型別及其特定引數：

**複製**  — 複製檔案和資料夾。

* **路徑**  — 如果路徑指向單一檔案，則只會複製檔案。 如果它指向資料夾（這包含頁面節點），則會複製下面的所有檔案和資料夾。

**內容** 使用標準呈現內容 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing).

* **路徑**  — 應輸出的資源路徑。
* **副檔名**  — 請求中應使用的擴充功能。 常見範例為 *html* 和 *json*，但任何其他擴充功能皆可。

* **選擇器**  — 選用的選取器，以點分隔。 常見範例為 *觸控* 用於轉譯行動版頁面或 *無限* 用於JSON輸出。

**clientlib**  — 封裝JavaScript或CSS使用者端程式庫。

* **路徑**  — 使用者端資料庫根目錄的路徑。
* **副檔名**  — 使用者端程式庫的型別。 這應該設定為 *js* 或 *css* 目前。

**資產**

收集資產的原始轉譯。

* **路徑** - /content/dam下的資產資料夾路徑。

**影像**  — 收集影像。

* **路徑**  — 影像資源的路徑。

影像型別用於在zip檔案中包含We Retail標誌。

**頁面**  — 呈現AEM頁面並收集引用的資產。

* **路徑**  — 頁面的路徑。
* **副檔名**  — 請求中應使用的擴充功能。 對於頁面，這幾乎永遠都是 *html*，但仍可使用其他方法。

* **選擇器**  — 選用的選取器，以點分隔。 常見範例為 *觸控* 用於轉譯頁面的行動版本。

* **深入**  — 決定是否應包含子頁面的選用布林屬性。 預設值為 *true.*

* **includeImages**  — 決定是否應包含影像的選用布林屬性。 預設值為 *true*.

  依預設，只有資源型別為foundation/components/image的影像元件才會被視為包含。 您可以透過設定 **Day CQ WCM頁面更新處理常式** 在Web主控台中。

**重寫**  — 重新寫入節點會定義在匯出頁面中重新寫入連結的方式。 重寫的連結可以指向zip檔案中包含的檔案或伺服器上的資源。

此 `rewrite` 節點必須位於 `page` 節點。

此 `rewrite` 節點可以有一或多個下列屬性：

* `clientlibs`：重寫clientlibs路徑。

* `images`：重寫影像路徑。
* `links`：重寫連結路徑。

每個屬性可以有下列其中一個值：

* `REWRITE_RELATIVE`：以檔案系統上頁面.html檔案的相對位置重寫路徑。

* `REWRITE_EXTERNAL`：使用AEM指向伺服器上的資源來重寫路徑 [外部化器服務](/help/sites-developing/externalizer.md).

AEM服務已呼叫 **PathRewriterTransformerFactory** 可讓您設定將重寫的特定html屬性。 此服務可在Web主控台中設定，且每個屬性的設定都為 `rewrite` 節點： `clientlibs`， `images`、和 `links`.

AEM 5.5已新增此功能。

### Content Sync設定範例 {#example-content-sync-configuration}

以下清單顯示Content Sync的設定範例。

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default和etc.designs.mobile**  — 設定的前兩個專案顯而易見。 由於您即將包含數個行動頁面，因此您需要在/etc/designs底下建立相關設計檔案。 由於不需要額外處理，因此只需複製即可。

**events.plist**  — 此專案有些特殊。 如簡介中所述，應用程式應提供包含事件位置標籤的地圖檢視。 必要的位置資訊將以PLIST格式作為單獨的檔案提供。 為了使此功能發揮作用，索引頁面上使用的事件清單元件具有一個名為plist.jsp的指令碼。 當以請求元件的資源時，執行此指令碼 `.plist` 副檔名。 和往常一樣，元件路徑在path屬性中給出，而型別設定為content，因為您想要使用 [Sling請求處理](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html**  — 接下來是應用程式中顯示的實際頁面。 path屬性會設定為事件的根頁面。 該頁面下方的所有事件頁面也會包括在內，因為深層屬性預設為true。 您使用頁面作為設定型別，以便納入任何可從頁面上的影像或下載元件參照的影像或其他檔案。 此外，設定觸控選擇器也會提供頁面的行動版本。 Feature Pack中的設定包含更多此類專案，但為了簡單起見，這裡沒有包含這些專案。

**標誌**  — 目前尚未提及標誌設定型別，因此不屬於任何內建型別。 不過，Content Sync架構在某種程度上可以擴充，以下章節將說明相關範例。

**資訊清單**  — 我們通常希望在zip檔案中加入某種中繼資料，例如內容的起始頁面。 不過，以硬式編碼撰寫這類資訊，可防止您日後輕易加以變更。 內容同步架構支援此使用案例，方法是尋找設定中的資訊清單節點（以名稱識別，不需要設定型別）。 該特定節點上定義的每個屬性都會新增至檔案（也稱為資訊清單），並位於zip檔案的根目錄中。

在此範例中，事件清單頁面應該是初始頁面。 此資訊提供於 **indexPage** 屬性，因此隨時都可以輕鬆變更。 第二個屬性會定義 *events.plist* 檔案。 如您稍後所見，使用者端應用程式現在可以讀取資訊清單並根據資訊清單採取行動。

設定好設定後，內容可使用瀏覽器或任何其他HTTP使用者端下載，或者，如果您是針對iOS開發，則可以使用專用的WAppKitSync使用者端程式庫。 下載位置由設定的路徑和 *.zip* 擴充功能，例如，使用本機AEM例項時： *http://localhost:4502/content/weretail_go.zip*

### 內容同步主控台 {#the-content-sync-console}

Content Sync主控台會列出存放庫中的所有內容同步設定（所有型別的節點） `cq:ContentSyncConfig`)並針對每個設定，執行下列動作：

* 更新快取。
* 清除快取。
* 下載完整的壓縮檔。
* 下載現在和特定日期和時間的差異zip檔。

這對於開發和疑難排解非常有用。

可在下列位置存取主控台：

`http://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1-50](assets/chlimage_1-50.png)

### 擴充內容同步架構 {#extending-the-content-sync-framework}

雖然設定選項的數量已經相當龐大，但可能未涵蓋您特定使用案例的所有需求。 本節說明Content Sync架構的擴充點，以及如何建立自訂組態型別。

每種設定型別都有 *內容更新處理常式*，此元件工廠是為該特定型別註冊的OSGi元件工廠。 這些處理常式會收集內容、處理內容，並將其新增至Content Sync架構所維護的快取。 實作下列介面或抽象基底類別：

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — 所有更新處理常式都必須實作的介面
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`  — 抽象類別，使用Sling簡化資源的呈現

將類別註冊為OSGi元件工廠，並將其部署在套件組合的OSGi容器中。 這項操作可透過以下方式完成： [Maven SCR外掛程式](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) 使用JavaDoc標籤或註解。 下列範例顯示JavaDoc版本：

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

請注意 *工廠* 定義包含公用介面和以斜線分隔的自訂型別。 此策略可讓內容同步架構在辨識設定專案中的自訂型別時，尋找並建立自訂類別的執行個體。 下一節提供自訂更新處理常式的具體範例。

>[!CAUTION]
>
>以AbstractSlingResourceUpdateHandler基底類別為基礎建立時，您必須新增 *繼承* 定義。 否則，OSGi容器不會設定在基底類別中宣告的必要參考。

### 實作自訂更新處理常式 {#implementing-a-custom-update-handler}

每個We.Retail Mobile頁面的左上角都有一個標誌，應包含在zip檔案中。 不過，針對快取最佳化，AEM不會參考影像檔案在存放庫中的實際位置，這可防止我們單純使用 **複製** 設定型別。 而您必須提供我們自己的服務 **標誌** 設定型別，可在AEM要求的位置使用影像。 下列程式碼清單顯示完整實施的標誌更新處理常式：

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

此 `LogoUpdateHandler` 類別實作 `ContentUpdateHandler` 介面的 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 方法，此方法會採用數個引數：

* A `ConfigEntry` 提供組態專案（呼叫此處理常式）及其屬性存取權的執行個體。
* A `lastUpdated` 時間戳記，指出Content Sync上次更新其快取的時間。 處理常式不應更新在該時間戳記之後未修改的內容。
* A `configCacheRoot` 指定快取根路徑的引數。 所有更新的檔案都必須儲存在此路徑下方，才能新增至zip檔案。
* 適用於所有快取相關存放庫作業的管理工作階段。
* 可用於更新特定使用者內容並因此提供個人化內容的使用者工作階段。

若要實作自訂處理常式，請先根據設定專案中指定的資源建立Image類別的執行個體。 此程式與頁面上實際標誌元件執行的程式相同。 它會確保影像的目標路徑與頁面參照的路徑相同。

接下來，檢查自上次更新後資源是否被修改。 自訂實施應避免快取不必要的更新，若沒有變更則傳回false。 如果資源已修改，請將影像複製到相對於快取根目錄的預期目標位置。 最後， `true` 會傳回，向架構指出快取已更新。

## 在使用者端上使用內容 {#using-the-content-on-the-client}

若要在Content Sync提供的行動應用程式中使用內容，您必須透過HTTP或HTTPS連線要求內容。 因此，擷取的內容（壓縮到ZIP檔案中）可以擷取並儲存在行動裝置本機。 內容不僅是指資料，也指邏輯，即完整的網頁應用程式，因此即使沒有網路連線，行動使用者也能執行擷取的網頁應用程式和對應資料。

Content Sync會以智慧型方式提供內容：只會傳送自上次成功資料同步處理以來的資料變更，因此可減少資料傳輸所需的時間。 第一次執行應用程式時，會要求自1970年1月1日起變更資料，稍後則只會要求自上次成功同步後變更的資料。 AEM使用iOS的使用者端通訊架構來簡化資料通訊和傳輸，因此只需最少量的原生程式碼，即可啟用iOS架構的網頁應用程式。

所有傳輸的資料都可擷取至相同的目錄結構，擷取資料時不需要執行額外的步驟（例如相依性檢查）。 如果有iOS，所有資料都會儲存在iOS應用程式的「檔案」資料夾內的子資料夾中。

iOS型AEM Mobile應用程式的典型執行路徑：

* 使用者在iOS裝置上啟動應用程式。
* 應用程式會嘗試連線至AEM後端，並要求自上次執行以來的資料變更。
* 伺服器會擷取有問題的資料，並將其壓縮到檔案中。
* 資料會傳回至使用者端裝置，並擷取至檔案資料夾。
* UIWebView元件啟動/重新整理。

如果先前無法建立連線，則會顯示已下載的資料。

### 其他資源 {#additional-resources}

若要瞭解管理員與作者的角色與責任，請參閱下列資源：

* [為AEM Mobile On-demand Services編寫AEM內容](/help/mobile/mobile-apps-ondemand.md)
* [管理內容以使用AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
