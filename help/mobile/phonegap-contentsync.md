---
title: Adobe PhoneGap Enterprise與Adobe Experience Manager的內容同步
description: 瞭解使用Adobe Experience Manager進行Adobe PhoneGap Enterprise的Content Sync。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2924'
ht-degree: 0%

---

# 具有內容同步功能的行動裝置{#mobile-with-content-sync}

{{ue-over-mobile}}

>[!NOTE]
>
>此檔案是[Adobe Experience Manager (AEM) Mobile快速入門](/help/mobile/getting-started-aem-mobile.md)指南的一部分，此指南是AEM Mobile參考的建議起點。

使用Content Sync來封裝內容，以便用於原生行動應用程式。 在AEM中編寫的頁面可作為應用程式內容，即使裝置離線亦然。 此外，由於AEM頁面是根據網頁標準，因此可跨平台運作，而讓您將其內嵌在任何原生包裝函式中。 此策略可減少開發工作量，並可讓您輕鬆更新應用程式內容。

>[!NOTE]
>
>您使用AEM Tools建立的PhoneGap應用程式已設定為透過Content Sync使用AEM頁面作為內容。

Content Sync架構會建立包含網頁內容的封存檔案。 內容可以是簡單頁面、影像和PDF檔案或整個網頁應用程式的內容。 內容同步API提供從行動應用程式或建置程式存取封存檔案的許可權，以便內容可擷取並納入應用程式中。

下列步驟順序說明了Content Sync的典型使用案例：

1. AEM開發人員會建立Content Sync設定，指定要包含的內容。
1. 內容同步架構會收集並快取內容。
1. 在行動裝置上啟動行動應用程式，並向伺服器請求內容（以ZIP檔案傳送）。
1. 使用者端會將ZIP內容解壓縮至本機檔案系統。 ZIP檔案中的資料夾結構會模擬使用者端（例如瀏覽器）一般會從伺服器要求的路徑。
1. 使用者端會在內嵌瀏覽器中開啟內容，或以其他方式使用內容。
1. 稍後，使用者端會向伺服器要求更新內容。 Content Sync架構提供漸進式更新，以減少下載大小和時間，由於頻寬或資料量有限，這對於行動裝置而言可能很重要。

>[!NOTE]
>
>若要取得有關開發內容同步處理常式的准則的詳細資訊，請參閱開箱即用的應用程式處理常式，請參閱[開發內容同步處理常式](/help/mobile/contentsync-app-handlers.md)。

## 設定內容同步內容 {#configuring-the-content-sync-content}

建立Content Sync設定，以指定傳遞至使用者端的ZIP檔案內容。 您可以建立任意數量的Content Sync設定。 每個設定都有名稱用於識別。

若要建立Content Sync設定，請將`cq:ContentSyncConfig`節點新增至存放庫，並將`sling:resourceType`屬性設定為`contentsync/config`。 `cq:ContentSyncConfig`節點可以位於存放庫中的任何位置，但AEM發佈執行個體上的使用者必須可以存取該節點。 因此，您應該在`/content`底下新增節點。

若要指定Content Sync ZIP檔案的內容，請將子節點新增至cq：ContentSyncConfig節點。 每個子節點的下列屬性會識別要包含的內容專案，以及新增內容專案時的處理方式：

* `path`：內容的位置。
* `type`：用於處理內容的設定型別名稱。 有數種型別可供使用，在組態型別中有所說明。

請參閱Content Sync設定範例。

建立Content Sync設定後，該設定會顯示在Content Sync主控台中。

>[!NOTE]
>
>Content Sync架構不會檢查Content Sync套件中是否包含資產和設計相關檔案的相依性。 請務必將所有必要的檔案包含在ZIP檔案中。

### 設定Content Sync下載的存取權 {#configuring-access-to-content-sync-downloads}

指定可從Content Sync下載的使用者或群組。 您可以設定可從所有Content Sync快取下載的預設使用者或群組，也可以覆寫預設值並設定特定Content Sync設定的存取權。

安裝AEM後，管理員群組的成員預設可從Content Sync下載。

### 設定Content Sync下載的預設存取權 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager服務可控制Content Sync的存取權。 設定此服務，以指定預設可從Content Sync下載的使用者或群組。

如果您正在[使用Web主控台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)設定服務，請鍵入使用者或群組的名稱，作為Fallback Cache Authorizable屬性值。

如果您正在[設定存放庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，請使用下列服務相關資訊：

* PID： com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 屬性名稱： contentsync.fallback.authorizable

#### 覆寫內容同步快取的下載存取權 {#overriding-download-access-for-a-content-sync-cache}

若要設定特定Content Sync設定的下載存取權，請將下列屬性新增至`cq:ContentSyncConfig`節點：

* 名稱：可授權
* 型別：字串
* 值：可下載的使用者或群組名稱。

例如，您的應用程式可讓使用者直接從Content Sync安裝更新。 若要讓所有使用者下載更新，請將可授權屬性的值設為`everyone`。

如果`cq:ContentSyncConfig`節點沒有可授權屬性，為Day CQ Content Sync Manager服務的Fallback Cache Authorizable屬性設定的預設使用者或群組會決定誰可以下載。

### 設定使用者以更新內容同步快取 {#configuring-the-user-for-updating-a-content-sync-cache}

當使用者對內容同步快取執行更新時，特定使用者帳戶會代表使用者執行動作。 依預設，匿名使用者會更新所有Content Sync快取。

您可以覆寫預設使用者，並指定使用者或群組來更新特定的Content Sync快取。

若要覆寫預設使用者，請指定使用者或群組，透過將下列屬性新增到cq：ContentSyncConfig節點來執行特定Content Sync設定的更新：

* 名稱： updateuser
* 型別：字串
* 值：可執行更新的使用者或群組名稱。

如果cq：ContentSyncConfig節點沒有`updateuser`屬性，則預設的匿名使用者會更新快取。

### 設定型別 {#configuration-types}

處理範圍包括從呈現簡單的JSON到完全呈現頁面（包括其參考資產）。 本節列出可用的組態型別及其特定引數：

**複製**&#x200B;僅複製檔案和資料夾。

* **path** — 如果路徑指向單一檔案，則只會複製檔案。 如果它指向資料夾（這包含頁面節點），則會複製下面的所有檔案和資料夾。

**content** — 使用標準Sling請求處理來轉譯內容。

* **path** — 應輸出的資源路徑。
* **延伸模組** — 應該用於要求中的延伸模組。 常見的範例是&#x200B;*html*&#x200B;和&#x200B;*json*，但任何其他擴充功能都是可能的。

* **選取器** — 選用的選取器（以點分隔）。 常見的範例是&#x200B;*觸控式* （用於轉譯頁面的行動版本）或&#x200B;*無限* （用於JSON輸出）。

**clientlib** — 封裝JavaScript或CSS使用者端資料庫。

* **path** — 使用者端資料庫根目錄的路徑。
* **延伸模組** — 使用者端資料庫的型別。 目前應將此專案設定為&#x200B;*js*&#x200B;或&#x200B;*css*。

* **includeFolders** - Type是字串陣列，可讓使用者指定要在使用者端資料庫中掃描的其他資料夾，以擷取檔案（例如自訂字型）。

**資產** — 收集資產的原始轉譯。

* **path** - /content/dam下的資產資料夾路徑。
* **轉譯** — 型別是字串陣列，可讓使用者指定要使用哪些轉譯，而非預設影像。 下列清單總結列出一些現成的轉譯，但您也可以使用工作流程建立的任何轉譯：

   * *原始*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**映像** — 收集映像。

* **path** — 影像資源的路徑。

影像型別是用來在zip檔案中包含We.Retail標誌。

**頁面** — 轉譯AEM頁面並收集參考的資產。

* **path** — 頁面的路徑。
* **延伸模組** — 應該用於要求中的延伸模組。 對於頁面，這幾乎總是&#x200B;*html*，但其他仍然可能。

* **選取器** — 選用的選取器（以點分隔）。 轉譯頁面行動版本的常見範例為&#x200B;*touch*。

* **deep** — 決定是否也應該包含子頁面的選用布林屬性。 預設值為&#x200B;*true。*

* **includeImages** — 決定是否應包含影像的選用布林屬性。 預設值為&#x200B;*true*。
依預設，只有資源型別為foundation/components/image的影像元件才會被視為包含。 您可以在Web主控台中設定**Day CQ WCM Pages更新處理常式**，以新增更多資源型別。

**rewrite** — 重寫節點會定義如何在匯出的頁面中重寫連結。 重寫的連結可以指向zip檔案中包含的檔案或伺服器上的資源。

`rewrite`節點必須位於`page`節點下方。

`rewrite`節點可以有一或多個下列屬性：

* `clientlibs`：重寫clientlibs路徑。

* `images`：重寫影像路徑。
* `links`：重寫連結路徑。

每個屬性可以有下列其中一個值：

* `REWRITE_RELATIVE`：以相對檔案系統上頁面.html檔案的位置重寫路徑。

* `REWRITE_EXTERNAL`：使用AEM [Externalizer服務](/help/sites-developing/externalizer.md)，指向伺服器上的資源來重寫路徑。

名為&#x200B;**PathRewriterTransformerFactory**&#x200B;的AEM服務可讓您設定要重寫的特定html屬性。 服務可以在Web主控台中設定，而且具有`rewrite`節點的每個屬性的組態： `clientlibs`、`images`和`links`。

AEM 5.5已新增此功能。

### Content Sync設定範例 {#example-content-sync-configuration}

以下清單顯示Content Sync的設定範例。

```java
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

**etc.designs.default和etc.designs.mobile** — 組態的前兩個專案顯而易見。 由於我們將包含數個行動頁面，因此我們需要/etc/designs底下的相關設計檔案。 由於不需要額外處理，因此只需複製即可。

**events.plist** — 此專案是特別的。 如簡介中所述，應用程式應提供包含事件位置標籤的地圖檢視。 我們將以PLIST格式的個別檔案形式提供必要的位置資訊。 為了使此功能發揮作用，索引頁面上使用的事件清單元件具有一個名為plist.jsp的指令碼。 當以`.plist`副檔名請求元件的資源時，會執行此指令碼。 和往常一樣，元件路徑在path屬性中指定，而型別設定為content，因為我們要使用Sling請求處理。

**events.touch.html** — 接下來是應用程式中顯示的實際頁面。 path屬性會設定為事件的根頁面。 也會包含該頁面下方的所有事件頁面，因為deep屬性預設為true。 我們使用頁面作為設定型別，因此納入了任何影像或其他檔案，這些影像或其他檔案可能會從頁面上的影像或下載元件參照。 此外，設定觸控選擇器也會提供頁面的行動版本。 Feature Pack中的設定包含更多此類專案，但為了簡單起見，這裡沒有包含這些專案。

**logo** — 目前尚未提及標誌組態型別，而且不是任何內建型別。 不過，Content Sync架構在某種程度上可以擴充，以下章節將說明相關範例。

**資訊清單** — 通常需要在zip檔案中包含某種中繼資料，例如內容的起始頁面。 不過，以硬式編碼撰寫這類資訊，可防止您日後輕易加以變更。 內容同步架構支援此使用案例，方法是尋找設定中的資訊清單節點（以名稱識別，不需要設定型別）。 該特定節點上定義的每個屬性都會新增至檔案（也稱為資訊清單），並位於zip檔案的根目錄中。

在此範例中，事件清單頁面應該是初始頁面。 此資訊是在&#x200B;**indexPage**&#x200B;屬性中提供，因此可以隨時輕鬆變更。 第二個屬性會定義&#x200B;*events.plist*&#x200B;檔案的路徑。 如我們稍後所見，使用者端應用程式現在可以讀取資訊清單並根據資訊清單採取行動。

設定好設定後，內容可使用瀏覽器或任何其他HTTP使用者端下載，或者，如果您是針對iOS開發，則可以使用專用的WAppKitSync使用者端程式庫。 下載位置由設定的路徑和&#x200B;*.zip*&#x200B;副檔名組成，例如，使用本機AEM執行個體時： *https://localhost:4502/content/weretail_go.zip*

### 內容同步主控台 {#the-content-sync-console}

Content Sync主控台會列出存放庫中的所有Content Sync設定（所有型別為`cq:ContentSyncConfig`的節點），而針對每個設定，您可以執行下列動作：

* 更新快取。
* 清除快取。
* 下載完整的壓縮檔。
* 下載現在和特定日期和時間的差異zip檔。

這對於開發和疑難排解非常有用。

可在下列位置存取主控台：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1](assets/chlimage_1.png)

### 擴充內容同步架構 {#extending-the-content-sync-framework}

雖然設定選項的數量已經相當龐大，但可能未涵蓋您特定使用案例的所有需求。 本節說明Content Sync架構的擴充點，以及如何建立自訂組態型別。

每個組態型別都有&#x200B;*內容更新處理常式*，這是針對該特定型別註冊的OSGi元件處理常式。 這些處理常式會收集內容、處理內容，並將其新增至Content Sync架構所維護的快取。 實作下列介面或抽象基底類別：

* `com.day.cq.contentsync.handler.ContentUpdateHandler` — 所有更新處理常式都必須實作的介面
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` — 使用Sling簡化資源轉譯的抽象類別

將類別註冊為OSGi元件工廠，並將其部署在套件組合的OSGi容器中。 您可以使用[Maven SCR外掛程式](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html)使用JavaDoc標籤或註解來完成此操作。 下列範例顯示JavaDoc版本：

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

請注意，*factory*&#x200B;定義包含公用介面和以斜線分隔的自訂型別。 此策略可讓內容同步架構在辨識設定專案中的自訂型別時，尋找並建立自訂類別的執行個體。 下一節提供自訂更新處理常式的具體範例。

>[!CAUTION]
>
>以AbstractSlingResourceUpdateHandler基底類別建置時，您必須新增&#x200B;*inherit*&#x200B;定義。 否則，OSGi容器不會設定在基底類別中宣告的必要參考。

### 實作自訂更新處理常式 {#implementing-a-custom-update-handler}

每個We.Retail Mobile頁面左上角都有一個標誌，我們想要將該標誌納入zip檔案中。 但是，針對快取最佳化，AEM不會參考影像檔案在存放庫中的實際位置，這會防止我們單純使用&#x200B;**副本**&#x200B;設定型別。 我們必須改為提供我們自己的&#x200B;**標誌**&#x200B;設定型別，以便在AEM要求的位置提供影像。 下列程式碼清單顯示完整實施的標誌更新處理常式：

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

`LogoUpdateHandler`類別實作`ContentUpdateHandler`介面的`updateCacheEntry(ConfigEntry, Long, String, Session, Session)`方法，此方法會採用數個引數：

* `ConfigEntry`執行個體，提供組態專案（呼叫此處理常式）及其屬性的存取權。
* `lastUpdated`時間戳記，指出Content Sync上次更新其快取的時間。 處理常式不應更新在該時間戳記之後未修改的內容。
* 指定快取根路徑的`configCacheRoot`引數。 所有更新的檔案都必須儲存在此路徑下方，才能新增至zip檔案。
* 適用於所有快取相關存放庫作業的管理工作階段。
* 可用於更新特定使用者內容並因此提供個人化內容的使用者工作階段。

若要實作自訂處理常式，請先根據設定專案中指定的資源建立Image類別的執行個體。 此程式基本上與頁面上實際標誌元件執行的程式相同。 它會確保影像的目標路徑與頁面參照的路徑相同。

接下來，檢查自上次更新後資源是否被修改。 自訂實施應避免快取不必要的更新，若沒有變更則傳回false。 如果資源已修改，請將影像複製到相對於快取根目錄的預期目標位置。 最後，會傳回`true`以向架構指出快取已更新。

## 在使用者端上使用內容 {#using-the-content-on-the-client}

若要在Content Sync提供的行動應用程式中使用內容，您必須透過HTTP或HTTPS連線要求內容。 因此，擷取的內容（壓縮到ZIP檔案中）可以擷取並儲存在行動裝置本機。 內容不僅是指資料，也指邏輯，即完整的網頁應用程式，因此即使沒有網路連線，行動使用者也能執行擷取的網頁應用程式和對應資料。

Content Sync會以智慧型方式提供內容：只會傳送自上次成功資料同步處理以來的資料變更，因此可減少資料傳輸所需的時間。 第一次執行應用程式資料時，會要求自1970年1月1日起進行變更，而之後只會要求自上次成功同步後變更的資料。 AEM使用iOS的使用者端通訊架構來簡化資料通訊和傳輸，因此只需最少量的原生程式碼，即可啟用iOS架構的網頁應用程式。

所有傳輸的資料都可擷取至相同的目錄結構，擷取資料時不需要執行額外的步驟（例如相依性檢查）。 如果有iOS，所有資料都會儲存在iOS應用程式的「檔案」資料夾內的子資料夾中。

iOS型AEM Mobile應用程式的典型執行路徑：

* 使用者在iOS裝置上啟動應用程式。
* 應用程式會嘗試連線至AEM後端，並要求自上次執行以來的資料變更。
* 伺服器會擷取有問題的資料，並將其壓縮到檔案中。
* 資料會傳回至使用者端裝置，並擷取至檔案資料夾。
* UIWebView元件啟動/重新整理。

如果無法建立連線，會顯示先前下載的資料。

### 快速入門 {#getting-ahead}

若要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
