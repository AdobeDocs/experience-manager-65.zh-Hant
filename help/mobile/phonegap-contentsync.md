---
title: 具有內容同步的行動裝置
seo-title: 具有內容同步的行動裝置
description: 請詳閱本頁，了解使用AEM同步Adobe PhoneGap Enterprise的內容。
seo-description: 請詳閱本頁，了解使用AEM同步Adobe PhoneGap Enterprise的內容。
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2989'
ht-degree: 0%

---

# 具有內容同步的行動裝置{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案是[AEM Mobile](/help/mobile/getting-started-aem-mobile.md)快速入門手冊的一部分，此指南是AEM Mobile參考的建議起點。

使用「內容同步」來封裝內容，以便用於原生行動應用程式。 在AEM中撰寫的頁面可作為應用程式內容，即使裝置離線亦然。 此外，由於AEM頁面是以網頁標準為基礎，因此可跨平台運作，讓您將其內嵌於任何原生包裝函式中。 此策略可降低開發工作量，並讓您輕鬆更新應用程式內容。

>[!NOTE]
>
>您使用AEM工具建立的PhoneGap應用程式已設定為透過「內容同步」將AEM頁面設為內容。

內容同步框架將建立包含Web內容的存檔檔案。 內容可以是簡單頁面、影像和PDF檔案，或整個Web應用程式中的任何內容。 內容同步API可從行動應用程式或建置程式存取封存檔案，以便擷取內容並納入應用程式中。

下列步驟順序說明內容同步的典型使用案例：

1. AEM開發人員會建立「內容同步」設定，以指定要包含的內容。
1. 內容同步架構會收集和快取內容。
1. 在行動裝置上，行動應用程式會啟動，並從伺服器要求內容，伺服器會以ZIP檔案傳送。
1. 用戶端會將ZIP內容解封至本機檔案系統。 ZIP檔案中的資料夾結構會模擬用戶端（例如瀏覽器）一般會從伺服器要求的路徑。
1. 用戶端會在內嵌瀏覽器中開啟內容，或以其他方式使用。
1. 稍後，客戶端從伺服器請求更新內容。 內容同步框架提供增量更新以減少下載大小和時間，這對於移動設備非常重要，因為頻寬或資料量有限。

>[!NOTE]
>
>若要取得有關開發內容同步處理常式的准則的詳細資訊，請參閱現成應用程式處理常式，請參閱[開發內容同步處理常式](/help/mobile/contentsync-app-handlers.md)。

## 配置內容同步內容{#configuring-the-content-sync-content}

建立「內容同步」設定，以指定傳送至用戶端的ZIP檔案內容。 您可以建立任意數量的「內容同步」設定。 每個設定都有識別用途的名稱。

要建立「內容同步」配置，請向儲存庫添加`cq:ContentSyncConfig`節點，並將`sling:resourceType`屬性設定為`contentsync/config`。 `cq:ContentSyncConfig`節點可位於存放庫中的任何位置，但AEM發佈執行個體上的使用者必須能存取該節點。 因此，您應在`/content`下新增節點。

若要指定「內容同步ZIP」檔案的內容，請將子節點新增至cq:ContentSyncConfig節點。 每個子節點的以下屬性標識要包含的內容項目，以及添加內容時如何處理該內容項目：

* `path`:內容的位置。
* `type`:用於處理內容的配置類型的名稱。有數種類型可用，如配置類型中所述。

請參閱範例內容同步設定。

建立「內容同步」設定後，它會顯示在「內容同步」控制台中。

>[!NOTE]
>
>內容同步架構不會檢查內容同步套件中是否包含資產的相依性以及與設計相關的檔案。 請務必將所有必要的檔案納入ZIP檔案中。

### 配置對內容同步下載的訪問{#configuring-access-to-content-sync-downloads}

指定可從「內容同步」下載的使用者或群組。 您可以配置預設用戶或組，這些用戶或組可以從所有內容同步快取中下載，並且可以覆蓋預設用戶或組並配置特定內容同步配置的訪問權限。

安裝AEM時，管理員群組的成員預設可從「內容同步」下載。

### 設定內容同步下載的預設訪問{#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager服務會控制對「內容同步」的存取。 設定此服務以指定預設可從「內容同步」下載的使用者或群組。

如果您是使用Web控制台](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)配置服務，請鍵入用戶或組的名稱作為「備援快取可授權」屬性的值。[

如果您在儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中進行[配置，請使用有關該服務的以下資訊：

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 屬性名稱：contentsync.fallback.authorized

#### 覆蓋內容同步快取{#overriding-download-access-for-a-content-sync-cache}的下載訪問

要配置特定「內容同步」配置的下載訪問，請將以下屬性添加到`cq:ContentSyncConfig`節點：

* 名稱：可授權
* 類型：字串
* 值：可下載的使用者或群組名稱。

例如，您的應用程式可讓使用者直接從內容同步安裝更新。 若要讓所有使用者下載更新，請將可授權屬性的值設為`everyone`。

如果`cq:ContentSyncConfig`節點沒有可授權的屬性，則為Day CQ Content Sync Manager服務的「備援快取可授權」屬性配置的預設用戶或組將確定可下載的內容。

### 配置用於更新內容同步快取{#configuring-the-user-for-updating-a-content-sync-cache}的用戶

當使用者執行內容同步快取的更新時，特定使用者帳戶會代表使用者執行動作。 匿名用戶預設會更新所有內容同步快取。

您可以覆寫預設使用者，並指定更新特定「內容同步」快取的使用者或群組。

若要覆寫預設使用者，請指定一個使用者或群組，將下列屬性新增至cq:ContentSyncConfig節點，以執行特定內容同步設定的更新：

* 名稱：updateuser
* 類型：字串
* 值：可執行更新的用戶或組的名稱。

如果cq:ContentSyncConfig節點沒有更新用戶屬性，則預設匿名用戶會更新快取。

### 配置類型{#configuration-types}

處理作業的範圍包括轉譯簡單JSON到完整轉譯頁面（包括其參考的資產）。 本節列出可用的配置類型及其特定參數：

**** copy只需複製檔案和資料夾即可。

* **路徑**  — 如果路徑指向單一檔案，則只會複製檔案。如果指向資料夾（這包括頁面節點），則將複製下面的所有檔案和資料夾。

**** contentRender內容（使用標準Sling請求處理）。

* **path**  — 應輸出的資源路徑。
* **擴充功能**  — 要求中應使用的擴充功能。常見的範例有&#x200B;*html*&#x200B;和&#x200B;*json*，但可能有任何其他擴充功能。

* **選取器**  — 以點分隔的選用選取器。轉譯行動版頁面的常見範例為&#x200B;*touch*，或JSON輸出的&#x200B;*infinity*。

**** clientlib封裝Javascript或CSS用戶端程式庫。

* **path**  — 用戶端程式庫根目錄的路徑。
* **擴充功能**  — 用戶端程式庫類型。此時應將此值設為&#x200B;*js*&#x200B;或&#x200B;*css*。

* **includeFolders**  - Type是字串的陣列，可讓使用者指定要在用戶端程式庫中掃描的其他資料夾，以擷取檔案（例如自訂字型）。

**資產**

收集資產的原始轉譯。

* **path**  - /content/dam下資產資料夾的路徑。
* **轉譯**  — 類型是字串的陣列，可讓使用者指定要使用的轉譯，而非預設影像。下列清單會摘要一些現成的轉譯，但您也可以使用工作流程建立的任何轉譯：

   * *原始文件*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**** image收集影像。

* **path**  — 影像資源的路徑。

影像類型可用來在zip檔案中包含We.Retail標誌。

**** pagesRender AEM頁面並收集參考的資產。

* **路徑**  — 頁面路徑。
* **擴充功能**  — 要求中應使用的擴充功能。若是頁面，這幾乎一律為&#x200B;*html*，但其他仍可能。

* **選取器**  — 以點分隔的選用選取器。轉譯行動版頁面的常見範例為&#x200B;*touch*。

* **deep**  — 選用布林屬性會決定是否應包含子頁面。預設值為&#x200B;*true。*

* **includeImages**  — 選用布林屬性，決定是否應包含影像。預設值為&#x200B;*true*。
預設情況下，僅考慮包含資源類型為foundation/components/image的影像元件。 您可以在Web主控台中設定**Day CQ WCM Pages Update Handler**&#x200B;以新增更多資源類型。

**** rewrite重新寫入節點定義如何在匯出的頁面中重寫連結。重寫的連結可以指向zip檔案中包含的檔案或指向伺服器上的資源。

`rewrite`節點必須位於`page`節點下方。

`rewrite`節點可以具有以下一個或多個屬性：

* `clientlibs`:重新寫入clientlibs路徑。

* `images`:重寫影像路徑。
* `links`:重寫連結路徑。

每個屬性都可以有下列其中一個值：

* `REWRITE_RELATIVE`:以相對位置重寫路徑至檔案系統上的page .html檔案。

* `REWRITE_EXTERNAL`:使用AEM Externalizer服務，指向伺服器上的資源來重寫 [路徑](/help/sites-developing/externalizer.md)。

名為&#x200B;**PathRewriterTransformerFactory**&#x200B;的AEM服務允許您配置要重寫的特定html屬性。 該服務可在Web控制台中配置，並具有`rewrite`節點的每個屬性的配置：`clientlibs`、`images`及`links`。

AEM 5.5新增了此功能。

### 內容同步配置示例{#example-content-sync-configuration}

下列清單顯示「內容同步」的範例設定。

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

**etc.designs.default等.designs.** mobile設定的前兩個項目應該相當明顯。由於我們將包含許多行動頁面，因此需要/etc/designs下方的相關設計檔案。 由於不需要額外處理，複製就足夠了。

**events.** plist此項目有點特殊。如簡介所述，應用程式應提供具有事件位置標籤的地圖檢視。 我們將以PLIST格式的單獨檔案提供必要的位置資訊。 為了讓此功能發揮作用，索引頁上使用的事件清單元件有一個名為plist.jsp的指令碼。 當以.plist副檔名要求元件的資源時，就會執行此指令碼。 如同往常，元件路徑會在path屬性中指定，且類型會設為內容，因為我們想要運用Sling要求處理。

**events.touch.** htmlNext即為應用程式中將顯示的實際頁面。路徑屬性會設為事件的根頁面。 該頁面下方的所有事件頁面也會納入，因為深層屬性預設為true。 我們使用頁面作為配置類型，因此可能會從頁面上的影像或下載元件參照的任何影像或其他檔案都將包含在內。 此外，設定觸控選取器可提供行動版頁面。 Feature Pack中的設定包含更多這類項目，但此處僅供簡單使用。

**** logo目前尚未提及標誌組態類型，且並非內建類型。不過，「內容同步」架構在某個程度上可擴充，此為範例，將於下一節中說明。

**** manifestZip檔案中通常需要包含某種中繼資料，例如內容的開始頁面。但是，對此類資訊進行硬式編碼會使您以後無法輕鬆更改它。 內容同步架構可透過在設定中尋找資訊清單節點來支援此使用案例，此節點只需依名稱識別，不需要設定類型。 該特定節點上定義的每個屬性都會新增至檔案，該檔案也稱為manifest，且位於zip檔案的根目錄中。

在範例中，事件清單頁面應是初始頁面。 此資訊在&#x200B;**indexPage**&#x200B;屬性中提供，因此可以隨時輕鬆更改。 第二個屬性定義&#x200B;*events.plist*&#x200B;檔案的路徑。 正如我們稍後將看到的，客戶端應用程式現在可以讀取清單並根據清單進行操作。

設定後，內容即可隨瀏覽器或任何其他HTTP用戶端下載，或者如果您正在為iOS開發，則可以使用專用的WAppKitSync客戶端庫。 下載位置由設定的路徑和&#x200B;*.zip*&#x200B;擴充功能組成，例如使用本機AEM例項時：*https://localhost:4502/content/weretail_go.zip*

### 內容同步控制台{#the-content-sync-console}

「內容同步」控制台列出儲存庫中的所有「內容同步」配置（`cq:ContentSyncConfig`類型的所有節點），並且對於每個配置，您可以執行以下操作：

* 更新快取。
* 清除快取。
* 下載完整的zip。
* 下載現在與特定日期和時間之間的比較zip。

這可供開發和疑難排解使用。

此主控台可從以下位置存取：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1](assets/chlimage_1.png)

### 擴充內容同步架構{#extending-the-content-sync-framework}

雖然配置選項的數量已相當廣泛，但可能不涵蓋您的特定使用案例的所有要求。 本節說明內容同步架構的擴充功能點，以及如何建立自訂設定類型。

對於每個配置類型，都有一個&#x200B;*內容更新處理程式*，它是針對該特定類型註冊的OSGi元件工廠。 這些處理常式會收集內容、處理內容，並將其新增至由內容同步架構維護的快取。 實現以下介面或抽象基類：

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — 所有更新處理程式都需要實作的介面
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`  — 使用Sling簡化資源轉譯的抽象類別

將類註冊為OSGi元件工廠，並將其部署在OSGi容器中，並成套。 您可以使用[Maven SCR外掛程式](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html)使用JavaDoc標籤或註解來完成此操作。 以下範例顯示JavaDoc版本：

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

請注意，*factory*&#x200B;定義包含通用介面和以斜線分隔的自訂類型。 此策略使內容同步框架能夠查找和建立自定義類的實例，因為它可識別配置項中的自定義類型。 下一節提供自訂更新處理常式的具體範例。

>[!CAUTION]
>
>在構建AbstractSlingResourceUpdateHandler基類時，必須添加&#x200B;*inherit*&#x200B;定義。 否則，OSGi容器將不會設定在基類中聲明的必需引用。

### 實作自訂更新處理常式{#implementing-a-custom-update-handler}

當然，每個We.Retail Mobile頁面的左上角都會包含我們要加入zip檔案的標誌。 但是，對於快取優化，AEM不會參考影像檔案在儲存庫中的實際位置，這會防止我們僅使用&#x200B;**copy**&#x200B;配置類型。 我們需要做的是提供我們自己的&#x200B;**logo**&#x200B;配置類型，使影像可在AEM要求的位置使用。 下列程式碼清單顯示標誌更新處理常式的完整實施：

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

`LogoUpdateHandler`類實現了`ContentUpdateHandler`介面的`updateCacheEntry(ConfigEntry, Long, String, Session, Session)`方法，該方法採用多個參數：

* `ConfigEntry`實例，提供對配置項的訪問（為此項調用了此處理程式）及其屬性。
* `lastUpdated`時間戳記，指出內容同步上次更新其快取的時間。 處理常式不應更新在該時間戳記之後未修改的內容。
* 指定快取根路徑的`configCacheRoot`參數。 所有更新的檔案都必須儲存在此路徑下，才能新增至zip檔案。
* 應用於所有快取相關儲存庫操作的管理會話。
* 一種用戶會話，可用於更新特定用戶上下文中的內容，從而提供一種個性化內容。

若要實作自訂處理常式，請先根據設定項目中提供的資源，建立Image類別的例項。 這基本上和我們頁面上實際的標誌元件所執行的程式相同。 它可確保影像的目標路徑與從頁面參照的路徑相同。

接下來，檢查自上次更新後是否修改了資源。 自訂實作應避免不必要的快取更新，若無任何變更，則傳回false。 如果已修改資源，請將影像複製到快取根的預期目標位置。 最後，返回`true`以向框架指示快取已更新。

## 在客戶端{#using-the-content-on-the-client}上使用內容

若要使用內容同步提供的行動應用程式中的內容，您需透過HTTP或HTTPS連線要求內容。 因此，擷取的內容（封裝在ZIP檔案中）可以擷取，並儲存在行動裝置上本機。 請注意，內容不僅指資料，也指邏輯，即完整的Web應用程式；由此，即使沒有網路連接，移動用戶也能夠執行檢索到的web應用程式和相應的資料。

「內容同步」以智慧方式提供內容：只傳送自上次成功資料同步以來的資料變更，因此減少資料傳輸所需的時間。 自1970年1月1日以來，在首次運行應用程式時，請求更改資料，隨後只請求自上次成功同步以來更改的資料。 AEM利用iOS的用戶端通訊架構來簡化資料通訊和傳輸，以便啟用iOS型網頁應用程式時需要最少量的原生程式碼。

所有傳輸的資料都可以提取到相同的目錄結構中，在提取資料時不需要其他步驟（例如依賴性檢查）。 若是iOS，所有資料都會儲存在iOS應用程式之「檔案」資料夾的子資料夾中。

iOS型AEM Mobile應用程式的一般執行路徑：

* 使用者在iOS裝置上啟動應用程式。
* 應用程式會嘗試連線至AEM後端，並要求自上次執行以來的資料變更。
* 伺服器會擷取相關資料，並將其壓縮至檔案中。
* 資料會傳回至用戶端裝置，並擷取至檔案資料夾。
* UIWebView元件啟動/刷新。

如果無法建立連線，則會顯示先前下載的資料。

### 搶先一步{#getting-ahead}

若要了解管理員和開發人員的角色和責任，請參閱下列資源：

* [使用AEM編寫Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)
