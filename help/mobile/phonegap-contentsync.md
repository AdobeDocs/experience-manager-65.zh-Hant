---
title: 具備內容同步功能的行動裝置
seo-title: 具備內容同步功能的行動裝置
description: 請依照本頁進行，以瞭解「使用AEM進行Adobe PhoneGap Enterprise的內容同步」。
seo-description: 請依照本頁進行，以瞭解「使用AEM進行Adobe PhoneGap Enterprise的內容同步」。
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '2989'
ht-degree: 0%

---


# 具備內容同步功能的行動裝置{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>本檔案是[《AEM Mobile](/help/mobile/getting-started-aem-mobile.md)快速入門手冊》的一部分，此手冊是AEM Mobile參考的建議起點。

使用內容同步來封裝內容，以便用於原生行動應用程式。 在AEM中撰寫的頁面可以當做應用程式內容使用，即使裝置已離線亦然。 此外，由於AEM頁面是以Web標準為基礎，因此可跨平台運作，讓您將它們內嵌在任何原生包裝函式中。 此策略可減少開發工作，並讓您輕鬆更新應用程式內容。

>[!NOTE]
>
>您使用AEM工具建立的PhoneGap應用程式已設定為透過「內容同步」將AEM頁面用作內容。

內容同步框架建立包含Web內容的存檔檔案。 內容可以是簡單頁面、影像和PDF檔案，或整個Web應用程式的任何內容。 內容同步API可讓您從行動應用程式存取封存檔案或建立程式，以便擷取內容並加入應用程式中。

以下步驟順序說明內容同步的典型使用案例：

1. AEM開發人員會建立「內容同步」設定，以指定要包含的內容。
1. 內容同步架構會收集並快取內容。
1. 在行動裝置上，行動應用程式會啟動並要求伺服器的內容，而伺服器會以ZIP檔案傳送。
1. 客戶端將ZIP內容解包到本地檔案系統。 ZIP檔案中的檔案夾結構會模擬用戶端（例如瀏覽器）通常會從伺服器要求的路徑。
1. 用戶端會在內嵌的瀏覽器中開啟內容，或以其他方式使用內容。
1. 之後，用戶端會向伺服器要求更新內容。 Content Sync架構提供增量更新，以減少下載大小和時間，這對行動裝置而言很重要，因為頻寬或資料量有限。

>[!NOTE]
>
>如需有關開發內容同步處理常式的詳細資訊，請參閱開發內容同步處理常式的方塊外應用程式處理常式，請參閱[開發內容同步處理常式](/help/mobile/contentsync-app-handlers.md)。

## 配置內容同步內容{#configuring-the-content-sync-content}

建立內容同步設定，以指定傳送至用戶端的ZIP檔案內容。 您可以建立任意數量的「內容同步」設定。 每個配置都有一個用於標識的名稱。

要建立內容同步配置，請將`cq:ContentSyncConfig`節點添加到儲存庫，並將`sling:resourceType`屬性設定為`contentsync/config`。 `cq:ContentSyncConfig`節點可以位於儲存庫的任何位置，但AEM發佈例項的使用者必須能存取該節點。 因此，您應在`/content`下添加節點。

若要指定「內容同步ZIP」檔案的內容，請將子節點新增至cq:ContentSyncConfig節點。 每個子節點的以下屬性標識要包含的內容項，以及添加該內容項時如何處理該內容項：

* `path`:內容的位置。
* `type`:用於處理內容的配置類型的名稱。有幾種類型可用，並在配置類型中說明。

請參閱內容同步設定範例。

在您建立「內容同步」設定後，該設定會顯示在「內容同步」主控台中。

>[!NOTE]
>
>Content Sync框架不會檢查Content Sync包中是否包含資產和與設計相關的檔案的相關性。 請確定您在ZIP檔案中包含所有必要的檔案。

### 設定內容同步下載的存取權{#configuring-access-to-content-sync-downloads}

指定可從「內容同步」下載的使用者或群組。 您可以設定可從所有內容同步快取下載的預設使用者或群組，並且可以覆寫預設值並設定特定內容同步設定的存取權。

當安裝AEM時，管理員群組的成員預設可從「內容同步」下載。

### 設定內容同步下載的預設存取權{#setting-the-default-access-for-content-sync-downloads}

CQ Content Sync Manager服務控制對Content Sync的訪問。 設定此服務，以指定預設可從「內容同步」下載的使用者或群組。

如果您[使用Web Console](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)配置服務，請鍵入用戶或組的名稱作為「備援快取可授權」屬性的值。

如果您在儲存庫](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)中進行[配置，請使用有關服務的以下資訊：

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 屬性名稱：contentsync.fallback.authorizable

#### 覆蓋內容同步快取的下載訪問{#overriding-download-access-for-a-content-sync-cache}

要為特定內容同步配置配置下載訪問權，請向`cq:ContentSyncConfig`節點添加以下屬性：

* 名稱：授權
* 類型：字串
* 值：可下載的使用者或群組名稱。

例如，您的應用程式可讓使用者直接從「內容同步」安裝更新。 若要讓所有使用者下載更新，請將可授權屬性的值設定為`everyone`。

如果`cq:ContentSyncConfig`節點沒有可授權屬性，則為Day CQ Content Sync Manager服務的「備援快取可授權」屬性設定的預設使用者或群組會決定哪些人可以下載。

### 配置用戶以更新內容同步快取{#configuring-the-user-for-updating-a-content-sync-cache}

當用戶對「內容同步」快取執行更新時，特定用戶帳戶代表用戶執行該操作。 匿名使用者依預設會更新所有「內容同步」快取。

您可以覆寫預設使用者並指定更新特定內容同步快取的使用者或群組。

若要覆寫預設使用者，請指定對特定內容同步設定執行更新的使用者或群組，方法是將下列屬性新增至cq:ContentSyncConfig節點：

* 名稱：updateuser
* 類型：字串
* 值：可執行更新的用戶或組的名稱。

如果cq:ContentSyncConfig節點沒有更新user屬性，則預設匿名用戶會更新快取。

### 配置類型{#configuration-types}

處理範圍從轉譯簡單JSON到完全正式轉譯頁面（包括其參考資產）。 本節列出可用的配置類型及其特定參數：

**複製** 只要複製檔案和檔案夾。

* **路徑** -如果路徑指向單個檔案，則僅複製檔案。如果指向資料夾（這包括頁面節點），則將複製下面的所有檔案和資料夾。

**contentRender** content using standard Sling request processing.

* **path**  —— 應輸出的資源的路徑。
* **extension**  —— 請求中應使用的擴充功能。常見的範例有&#x200B;*html*&#x200B;和&#x200B;*json*，但可能有其他副檔名。

* **selector**  —— 可選選擇器以點分隔。常見的範例包括：用於轉譯頁面行動版本的&#x200B;*touch*，或用於JSON輸出的&#x200B;*infinity*。

**clientlib** 封裝Javascript或CSS用戶端程式庫。

* **path**  —— 客戶端庫根目錄的路徑。
* **extension**  —— 用戶端程式庫的類型。此時，此值應設為&#x200B;*js*&#x200B;或&#x200B;*css*。

* **includeFolders**  - Type是一組字串，可讓使用者指定其他資料夾以在用戶端程式庫中掃描以擷取檔案（例如自訂字型）。

**資產**

收集資產的原始轉譯。

* **path**  - /content/dam下資產資料夾的路徑。
* **轉譯** -類型是字串的陣列，可讓使用者指定要使用哪些轉譯，而非預設影像。下列清單會摘要一些現成可用的轉譯，但您也可以使用工作流程建立的任何轉譯：

   * *原始文件*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**影** 像收集影像。

* **路徑** -影像資源的路徑。

影像類型可用來將We.Retail標誌包含在zip檔案中。

**頁** 面演算AEM頁面並收集參考資產。

* **路徑** -頁面的路徑。
* **extension**  —— 請求中應使用的擴充功能。對於頁面，這幾乎總是&#x200B;*html*，但其他頁面仍然可能。

* **selector**  —— 可選選擇器以點分隔。常見的範例有&#x200B;*touch*，以呈現頁面的行動版本。

* **deep**  —— 可選的布林屬性，決定是否也應包含子頁面。預設值為&#x200B;*true。*

* **includeImages**  —— 可選布林屬性，決定是否應包含影像。預設值為&#x200B;*true*。
預設情況下，僅考慮包含資源類型為foundation/components/image的映像元件。 您可以在Web控制台中配置**Day CQ WCM Pages Update Handler**&#x200B;來添加更多資源類型。

**rewrite** 重寫節點定義如何在導出的頁面中重寫連結。重寫的連結可以指向包含在zip檔案中的檔案或指向伺服器上的資源。

`rewrite`節點必須位於`page`節點下方。

`rewrite`節點可以具有以下一個或多個屬性：

* `clientlibs`:重寫clientlibs路徑。

* `images`:重寫影像路徑。
* `links`:重寫連結路徑。

每個屬性都可以有下列其中一個值：

* `REWRITE_RELATIVE`:以相對位置重寫路徑至檔案系統上的頁面。html檔案。

* `REWRITE_EXTERNAL`:使用AEM  [Externalizer服務，指向伺服器上的資源，以重寫路徑](/help/sites-developing/externalizer.md)。

名為&#x200B;**PathRewriterTransformerFactory**&#x200B;的AEM服務可讓您設定要重寫的特定html屬性。 服務可在Web控制台中配置，並且對`rewrite`節點的每個屬性都具有配置：`clientlibs`、`images`和`links`。

此功能已新增至AEM 5.5。

### 內容同步配置示例{#example-content-sync-configuration}

下列清單顯示內容同步的範例設定。

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

**等等。設計。預設……** 移動配置的前兩個條目應該比較明顯。當我們將包含許多行動頁面時，我們需要/etc/designs下方的相關設計檔案。 由於不需要額外處理，複製就足夠了。

**events.** plist此項目有些特殊。如導言中所述，應用程式應提供具有事件位置標籤的映射視圖。 我們將以PLIST格式單獨提供必要的位置資訊。 為了達到此目的，在索引頁上使用的事件清單元件具有名為plist.jsp的指令碼。 當以。plist副檔名要求元件的資源時，就會執行此指令碼。 和往常一樣，元件路徑會在path屬性中指定，而且類型會設為content，因為我們想要運用Sling請求處理。

**events.touch.** htmlNext會顯示應用程式中將顯示的實際頁面。路徑屬性會設為事件的根頁面。 該頁面下方的所有事件頁面也會包含在內，因為deep屬性預設為true。 我們使用頁面做為設定類型，以便包含任何可從頁面上的影像或下載元件參考的影像或其他檔案。 此外，設定觸控選取器可提供行動版的頁面。 功能套件中的設定包含更多此類項目，但為了簡化程式，這些項目已排除。

**標** 志徽標配置類型到目前為止尚未提及，它不是內置類型。不過，Content Sync框架在某種程度上是可擴充的，這是其中的一個範例，將在下一節中介紹。

**manifest** 通常需要在zip檔案中包含某種中繼資料，例如您的內容開始頁面。不過，硬式編碼這類資訊可讓您日後無法輕鬆變更。 內容同步框架通過在配置中查找清單節點支援此使用案例，該節點僅由名稱標識，不需要配置類型。 在該特定節點上定義的每個屬性都會添加到檔案中，該檔案也稱為manifest，並駐留在zip檔案的根目錄中。

在範例中，事件清單頁面應是首頁。 此資訊會提供在&#x200B;**indexPage**&#x200B;屬性中，因此可隨時輕鬆變更。 第二個屬性定義&#x200B;*events.plist*&#x200B;檔案的路徑。 如我們稍後所見，用戶端應用程式現在可以讀取資訊清單，並依照資訊清單行事。

設定好後，您就可以使用瀏覽器或任何其他HTTP用戶端下載內容，或如果您正在針對iOS進行開發，則可使用專用的WAppKitSync用戶端程式庫。 下載位置由組態的路徑和&#x200B;*.zip*&#x200B;擴充功能組成，例如使用本機AEM例項時：*https://localhost:4502/content/weretail_go.zip*

### 內容同步控制台{#the-content-sync-console}

「內容同步」控制台列出儲存庫中的所有「內容同步」配置（`cq:ContentSyncConfig`類型的所有節點），並且對於每種配置，您都可以執行以下操作：

* 更新快取。
* 清除快取。
* 下載完整的zip。
* 下載現在與特定日期和時間之間的比較zip。

它可用於開發和疑難排解。

可從以下網址訪問控制台：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

其外觀如下：

![chlimage_1](assets/chlimage_1.png)

### 擴充內容同步架構{#extending-the-content-sync-framework}

雖然配置選項的數量已相當廣泛，但可能不涵蓋您特定使用案例的所有需求。 本節介紹Content Sync框架的擴展點以及如何建立自定義配置類型。

對於每種配置類型，都有一個&#x200B;*內容更新處理程式* ，它是為該特定類型註冊的OSGi元件工廠。 這些處理常式會收集內容、處理內容，並將它新增至由內容同步架構維護的快取。 實現以下介面或抽象基類：

* `com.day.cq.contentsync.handler.ContentUpdateHandler` -所有更新處理常式都需要實作的介面
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` -使用Sling簡化資源轉換的抽象類別

將您的類別註冊為OSGi元件工廠，並將它部署在OSGi容器的套件中。 這可以使用[Maven SCR plugin](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html)使用JavaDoc標籤或注釋來完成。 以下示例顯示JavaDoc版本：

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

請注意，*factory*&#x200B;定義包含公用介面和以斜線分隔的自定義類型。 此策略可讓Content Sync框架在識別配置條目中的自定義類型時，查找並建立自定義類的實例。 下一節提供自訂更新處理常式的具體範例。

>[!CAUTION]
>
>當建立在AbstractSlingResourceUpdateHandler基本類別上時，您必須新增&#x200B;*inherit*&#x200B;定義。 否則，OSGi容器將不設定在基類中聲明的必需引用。

### 實作自訂更新處理常式{#implementing-a-custom-update-handler}

每個We.Retail Mobile頁面都會在左上角包含一個標誌，當然，我們想要加入到zip檔案中。 不過，對於快取最佳化，AEM不會參考影像檔案在儲存庫中的實際位置，這會讓我們無法只使用&#x200B;**copy**&#x200B;組態類型。 我們需要做的是提供我們自己的&#x200B;**logo**&#x200B;組態類型，讓影像可在AEM要求的位置使用。 下列程式碼清單顯示標誌更新處理常式的完整實作：

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

`LogoUpdateHandler`類實現`ContentUpdateHandler`介面的`updateCacheEntry(ConfigEntry, Long, String, Session, Session)`方法，該方法採用多個參數：

* `ConfigEntry`實例，它提供對為其調用此處理程式的配置條目及其屬性的訪問。
* `lastUpdated`時間戳記，指出內容同步上次更新其快取的時間。 在該時間戳記後未修改的內容不應由處理常式更新。
* `configCacheRoot`參數，指定快取的根路徑。 所有更新的檔案都必須儲存在此路徑下方，才能新增至zip檔案。
* 應用於所有與快取相關的儲存庫操作的管理會話。
* 一種用戶會話，可用於在特定用戶的上下文中更新內容，從而提供一種個性化內容。

若要實作自訂處理常式，請先根據設定項目中提供的資源，建立Image類別的例項。 這基本上與我們頁面上實際標誌元件執行的程式相同。 它可確保影像的目標路徑與從頁面參考的路徑相同。

接下來，檢查自上次更新以來是否修改了資源。 自訂實作應避免不必要的快取更新，若無任何變更則傳回false。 如果資源已修改，請將映像複製到與快取根目錄相關的預期目標位置。 最後，返回`true`以向框架指示已更新快取。

## 使用客戶端{#using-the-content-on-the-client}上的內容

若要在內容同步提供的行動應用程式中使用內容，您必須透過HTTP或HTTPS連線來要求內容。 因此，擷取的內容（封裝在ZIP檔案中）可以擷取並儲存在行動裝置上。 請注意，內容不僅指資料，也指邏輯，即完整的Web應用程式；因此，即使沒有網路連接，移動用戶也能夠執行檢索到的Web應用程式和相應資料。

Content Sync以智慧方式提供內容：只傳送自上次成功資料同步以來的資料更改，從而減少資料傳輸所需的時間。 自1970年1月1日以來，首次運行應用程式資料時請求更改，隨後只請求自上次成功同步以來更改的資料。 AEM運用iOS的用戶端通訊架構來簡化資料通訊和傳輸，因此啟用以iOS為基礎的網頁應用程式時，需要最少數量的原生程式碼。

所有傳輸的資料都可以提取到相同的目錄結構中，在提取資料時不需要額外的步驟（例如相關性檢查）。 如果是iOS，所有資料都會儲存在iOS應用程式的「檔案」檔案夾內的子檔案夾中。

iOS型AEM Mobile應用程式的典型執行路徑：

* 使用者在iOS裝置上啟動應用程式。
* 應用程式會嘗試連線至AEM後端，並要求自上次執行以來的資料變更。
* 伺服器會擷取相關資料，並將其壓縮至檔案。
* 資料會傳回至用戶端裝置，並擷取至檔案資料夾。
* UIWebView元件啟動／刷新。

如果無法建立連線，則會顯示先前下載的資料。

### 搶先一步{#getting-ahead}

要瞭解管理員和開發人員的角色和責任，請參閱以下資源：

* [使用AEM製作Adobe PhoneGap Enterprise](/help/mobile/phonegap.md)
* [使用AEM管理Adobe PhoneGap Enterprise的內容](/help/mobile/administer-phonegap.md)

