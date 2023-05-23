---
title: 用於Adobe PhoneGap企業的內容同AEM步
description: 有關Adobe PhoneGap企業的內容同步的資訊，請訪問此AEM頁。
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
exl-id: 2cadd9c5-4335-48d0-8d1c-941fca717409
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '2977'
ht-degree: 0%

---

# 帶內容同步的移動{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>此文檔是 [AEM Mobile入門](/help/mobile/getting-started-aem-mobile.md) 指南，推薦的AEM Mobile參考起點。

使用內容同步對內容進行打包，以便可以在本機移動應用程式中使用。 在中創作的頁AEM面可以用作應用內容，即使設備處於離線狀態。 此外，由於AEM頁面基於Web標準，因此它們可以跨平台工作，使您能夠將它們嵌入任何本機包裝中。 此策略可減少開發工作，並使您能夠輕鬆更新應用內容。

>[!NOTE]
>
>您使用工具建立的PhoneGap應AEM用已配置為通過內AEM容同步將頁面用作內容。

內容同步框架建立包含Web內容的存檔檔案。 內容可以是簡單頁面、影像和PDF檔案或整個Web應用程式中的任何內容。 內容同步API提供從移動應用或生成進程訪問存檔檔案的權限，以便可以檢索內容並將其包括在應用中。

以下步驟序列說明了內容同步的典型使用情形：

1. 開發AEM人員建立指定要包括的內容的內容同步配置。
1. 內容同步框架將收集和快取內容。
1. 在移動設備上，啟動移動應用並從伺服器請求內容，該內容以ZIP檔案的形式傳送。
1. 客戶端將ZIP內容解包到本地檔案系統。 ZIP檔案中的資料夾結構模擬客戶端（如瀏覽器）通常從伺服器請求的路徑。
1. 客戶端在嵌入式瀏覽器中開啟內容或以其他方式使用內容。
1. 稍後，客戶端從伺服器請求更新的內容。 內容同步框架提供增量更新以減少下載大小和時間，這對移動設備來說非常重要，因為頻寬或資料卷有限。

>[!NOTE]
>
>要獲取有關開發內容同步處理程式的指導原則的詳細資訊，請參閱框外的應用程式處理程式，請參閱 [開發內容同步處理程式](/help/mobile/contentsync-app-handlers.md)。

## 配置內容同步內容 {#configuring-the-content-sync-content}

建立內容同步配置以指定傳送到客戶端的ZIP檔案的內容。 您可以建立任意數量的內容同步配置。 每個配置都有一個用於標識的名稱。

要建立內容同步配置，請添加 `cq:ContentSyncConfig` 節點到儲存庫， `sling:resourceType` 屬性設定為 `contentsync/config`。 的 `cq:ContentSyncConfig` 節點可以位於儲存庫中的任意位置，但發佈實例上的用戶必須能夠訪AEM問該節點。 因此，您應在下面添加節點 `/content`。

要指定內容同步ZIP檔案的內容，請將子節點添加到cq:ContentSyncConfig節點。 每個子節點的以下屬性標識要包括的內容項以及添加該內容項時如何處理它：

* `path`:內容的位置。
* `type`:用於處理內容的配置類型的名稱。 有幾種類型可用，在「配置類型」中有說明。

請參閱內容同步配置示例。

建立內容同步配置後，它將顯示在內容同步控制台中。

>[!NOTE]
>
>內容同步框架不會檢查內容同步包中是否包含資產和與設計相關的檔案的依賴關係。 確保在ZIP檔案中包含所有所需檔案。

### 配置對內容同步下載的訪問 {#configuring-access-to-content-sync-downloads}

指定可以從內容同步下載的用戶或組。 您可以配置可從所有內容同步快取下載的預設用戶或組，並可以覆蓋預設用戶或組並配置特定內容同步配置的訪問權限。

安AEM裝後，預設情況下，管理員組成員可以從內容同步下載。

### 設定內容同步下載的預設訪問權限 {#setting-the-default-access-for-content-sync-downloads}

第CQ天內容同步管理器服務控制對內容同步的訪問。 配置此服務以指定預設情況下可以從內容同步下載的用戶或組。

如果 [使用Web控制台配置服務](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)，鍵入用戶或組的名稱作為「回退快取授權」屬性的值。

如果 [在儲存庫中配置](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)，使用以下有關服務的資訊：

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 屬性名稱：contensync.fallback.可授權

#### 覆蓋內容同步快取的下載訪問 {#overriding-download-access-for-a-content-sync-cache}

要配置特定內容同步配置的下載訪問，請將以下屬性添加到 `cq:ContentSyncConfig` 節點：

* 名稱：授權
* 類型：字串
* 值：可下載的用戶或組的名稱。

例如，您的應用允許用戶直接從內容同步安裝更新。 要使所有用戶都能下載更新，請將可授權屬性的值設定為 `everyone`。

如果 `cq:ContentSyncConfig` node沒有可授權屬性，為Day CQ內容同步管理器服務的「可回退快取授權」屬性配置的預設用戶或組將確定可下載的用戶。

### 配置用戶以更新內容同步快取 {#configuring-the-user-for-updating-a-content-sync-cache}

當用戶對內容同步快取執行更新時，特定用戶帳戶代表用戶執行該操作。 預設情況下，匿名用戶更新所有內容同步快取。

您可以覆蓋預設用戶並指定更新特定內容同步快取的用戶或組。

要覆蓋預設用戶，請通過向cq:ContentSyncConfig節點添加以下屬性來指定執行特定內容同步配置更新的用戶或組：

* 名稱：更新用戶
* 類型：字串
* 值：可執行更新的用戶或組的名稱。

如果cq:ContentSyncConfig節點沒有updateuser屬性，則預設匿名用戶將更新快取。

### 配置類型 {#configuration-types}

處理範圍從呈現簡單JSON到完全呈現頁（包括其引用的資產）。 本節列出可用的配置類型及其特定參數：

**複製** 只需複製檔案和資料夾即可。

* **路徑**  — 如果路徑指向單個檔案，則僅複製檔案。 如果指向資料夾（包括頁面節點），則將複製下面的所有檔案和資料夾。

**內容** 使用標準Sling請求處理呈現內容。

* **路徑**  — 應輸出的資源路徑。
* **擴展**  — 請求中應使用的擴展。 常見示例有 *html* 和 *jon*，但任何其他擴展都是可能的。

* **選擇器**  — 可選選擇器以點分隔。 常見示例有 *觸摸* 用於呈現頁面或 *無限* 用於JSON輸出。

**客戶端庫** 將Javascript或CSS客戶端庫打包。

* **路徑**  — 客戶端庫的根路徑。
* **擴展**  — 客戶端庫的類型。 此值應設定為 *j* 或 *cs* 在此刻。

* **包括資料夾**  — 類型是字串的陣列，它允許用戶指定要在客戶端庫中掃描的其他資料夾以提取檔案（如自定義字型）。

**資產**

收集資產的原始格式副本。

* **路徑** - /content/dam下的資產資料夾路徑。
* **格式**  — 類型是字串陣列，允許用戶指定要使用的格式副本而不是預設影像。 以下清單匯總了一些現成格式副本，但您也可以使用工作流建立的任何格式副本：

   * *原始文件*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**影像** 收集影像。

* **路徑**  — 映像資源的路徑。

影像類型用於在zip檔案中包括We.Retail徽標。

**頁** 呈AEM現頁面並收集引用的資產。

* **路徑**  — 頁面路徑。
* **擴展**  — 請求中應使用的擴展。 對於頁面，這幾乎總是 *html*&#x200B;但其他方面仍有可能。

* **選擇器**  — 可選選擇器以點分隔。 常見示例有 *觸摸* 用於呈現頁面的移動版本。

* **深**  — 可選布爾屬性，確定是否還應包括子頁。 預設值為 *是的。*

* **包括影像**  — 確定是否應包括影像的可選布爾屬性。 預設值為 *真*。
預設情況下，只考慮包含資源類型為foundation/components/image的映像元件。 通過配置 **第CQ WCM頁更新處理程式** 的下界。

**重寫** 重寫節點定義如何在導出的頁面中重寫連結。 重寫的連結可以指向zip檔案中包含的檔案或指向伺服器上的資源。

的 `rewrite` 節點需要位於 `page` 的下界。

的 `rewrite` 節點可以具有以下一個或多個屬性：

* `clientlibs`:重寫客戶端清單路徑。

* `images`:重寫影像路徑。
* `links`:重寫連結路徑。

每個屬性都可以具有以下值之一：

* `REWRITE_RELATIVE`:在檔案系統上用相對位置重寫page .html檔案的路徑。

* `REWRITE_EXTERNAL`:通過指向伺服器上的資源，使用 [外部化程式服務](/help/sites-developing/externalizer.md)。

名AEM為 **PathRewriterTransformerFactory** 允許您配置要重寫的特定html屬性。 服務可以在Web控制台中配置，並且為 `rewrite` 節點： `clientlibs`。 `images` 和 `links`。

此功能已在五點AEM五中添加。

### 內容同步配置示例 {#example-content-sync-configuration}

下面的清單顯示了內容同步的配置示例。

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

**等設計、預設等設計、移動** 配置的前兩個條目應該非常明顯。 由於我們將包括許多移動頁面，因此需要在/etc/designs下提供相關設計檔案。 由於不需要額外處理，因此複製就足夠了。

**事件.plist** 這個條目有點特別。 如導言中所述，應用程式應提供帶有事件位置標籤的地圖視圖。 我們將以PLIST格式作為單獨的檔案提供必要的位置資訊。 為了使此功能正常工作，在索引頁上使用的事件清單元件有一個名為plist.jsp的指令碼。 當使用.plist副檔名請求元件的資源時，將執行此指令碼。 與往常一樣，元件路徑在path屬性中給定，類型設定為內容，因為我們希望利用Sling請求處理。

**事件.touch.html** 接下來是應用中顯示的實際頁面。 路徑屬性設定為事件的根頁。 該頁下的所有事件頁也將包括在內，因為deep屬性預設為true。 我們將頁面用作配置類型，以便將包含任何可能從頁面上的影像或下載元件引用的影像或其他檔案。 此外，設定觸摸選擇器還為我們提供了移動版本的頁面。 功能包中的配置包含更多此類條目，但為了簡單起見，這些條目被排除在外。

**標誌** 徽標配置類型目前尚未提及，它不是任何內置類型。 但是，內容同步框架在一定程度上是可擴展的，這是一個示例，將在下一節中介紹。

**清單** 通常希望在zip檔案中包含某種元資料，例如內容的起始頁。 但是，對此類資訊進行硬編碼後，您以後不會輕易更改它。 內容同步框架通過在配置中查找清單節點支援此使用情形，清單節點只是通過名稱標識，不需要配置類型。 在該特定節點上定義的每個屬性都會添加到檔案中，該檔案也稱為清單，並駐留在zip檔案的根中。

在示例中，事件清單頁應是初始頁。 此資訊在 **索引頁** 因此，可以隨時容易地改變屬性。 第二個屬性定義 *事件.plist* 的子菜單。 正如我們稍後將看到的，客戶端應用程式現在可以讀取清單並根據清單執行操作。

一旦設定配置，就可以使用瀏覽器或任何其他HTTP客戶端下載內容，或者如果您正在為iOS開發，則可以使用專用的WAppKitSync客戶端庫。 下載位置由配置的路徑和 *.zip* 擴展，例如，使用本地實例AEM時： *https://localhost:4502/content/weretail_go.zip*

### 內容同步控制台 {#the-content-sync-console}

內容同步控制台列出儲存庫中的所有內容同步配置（所有類型的節點） `cq:ContentSyncConfig`)，並且對於每個配置，您可以執行以下操作：

* 更新快取。
* 清除快取。
* 下載完整的zip。
* 下載現在與特定日期和時間之間的差異zip。

它可用於開發和故障排除。

控制台可訪問：

`https://localhost:4502/libs/cq/contentsync/content/console.html`

如下所示：

![chlimage_1](assets/chlimage_1.png)

### 擴展內容同步框架 {#extending-the-content-sync-framework}

雖然配置選項的數量已經相當多，但可能不涵蓋您特定使用案例的所有要求。 本節介紹內容同步框架的擴展點以及如何建立自定義配置類型。

對於每種配置類型， *內容更新處理程式*，它是為該特定類型註冊的OSGi元件工廠。 這些處理程式收集內容、處理內容並將其添加到由內容同步框架維護的快取中。 實現以下介面或抽象基類：

* `com.day.cq.contentsync.handler.ContentUpdateHandler`  — 所有更新處理程式都需要實現的介面
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler`  — 一個抽象類，它使用Sling簡化資源的呈現

將類註冊為OSGi元件工廠，並將其部署到捆綁包中的OSGi容器中。 可以使用 [Maven SCR插件](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) 使用JavaDoc標籤或注釋。 以下示例顯示JavaDoc版本：

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

請注意 *工廠* 定義包含公共介面和以斜槓分隔的自定義類型。 此策略使內容同步框架能夠在識別配置條目中的自定義類型時查找並建立自定義類的實例。 下一節提供了自定義更新處理程式的具體示例。

>[!CAUTION]
>
>在構建AbstractSlingResourceUpdateHandler基類時，必須添加 *繼承* 定義。 否則，OSGi容器將不設定在基類中聲明的必需引用。

### 實現自定義更新處理程式 {#implementing-a-custom-update-handler}

每個We.Retail Mobile頁面的左上角都有一個徽標，當然，我們希望在zip檔案中包括這些徽標。 但是，對於快取優化，AEM不會引用映像檔案在儲存庫中的實際位置，這會阻止我們簡單地使用 **複製** 配置類型。 相反，我們需要提供自己的 **標誌** 配置類型，使映像在請求的位置可AEM用。 以下代碼清單顯示了徽標更新處理程式的完整實現：

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

的 `LogoUpdateHandler` 類實現 `ContentUpdateHandler` 介面 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 方法，它採用多個參數：

* A `ConfigEntry` 提供對調用此處理程式的配置項及其屬性的訪問權限的實例。
* A `lastUpdated` 時間戳，指示內容同步上次更新其快取的時間。 處理程式不應更新在該時間戳之後未修改的內容。
* A `configCacheRoot` 參數，指定快取的根路徑。 所有更新的檔案必須儲存在此路徑下才能添加到zip檔案。
* 應用於所有與快取相關的儲存庫操作的管理會話。
* 一種用戶會話，其可用於在特定用戶的上下文中更新內容並因此提供一種個性化內容。

要實現自定義處理程式，請首先根據配置條目中提供的資源建立Image類的實例。 這基本上和我們頁面上實際的徽標元件所做的步驟相同。 它確保影像的目標路徑與從頁面引用的路徑相同。

接下來，檢查自上次更新後是否修改了資源。 自定義實現應避免對快取進行不必要的更新，並在無更改時返回false。 如果資源已修改，請將映像複製到與快取根目錄相關的預期目標位置。 終於， `true` 返回以向框架指示已更新快取。

## 使用客戶端上的內容 {#using-the-content-on-the-client}

為了在內容同步提供的移動應用中使用內容，您需要通過HTTP或HTTPS連接請求內容。 結果，可以提取檢索到的內容（打包在ZIP檔案中）並將其本地儲存在移動設備上。 請注意，內容不僅指資料，還指邏輯，即完整的Web應用程式；由此，即使沒有網路連接，移動用戶也能夠執行檢索到的web應用和相應資料。

Content Sync以智慧方式提供內容：只傳送自上次成功資料同步以來的資料更改，從而減少資料傳輸所需的時間。 自1970年1月1日以來，在首次運行應用程式資料時請求更改，隨後只請求自上次成功同步以來更改的資料。 利AEM用iOS的客戶端通信框架簡化資料通信和傳輸，以便啟用基於iOS的Web應用程式需要最少量的本機代碼。

所有傳輸的資料都可以提取到相同的目錄結構中，在提取資料時不需要其他步驟（例如依賴性檢查）。 對於iOS，所有資料都儲存在iOS應用的「文檔」資料夾中的子資料夾中。

基於iOS的AEM Mobile應用的典型執行路徑：

* 用戶在iOS設備上啟動應用。
* 應用嘗試連接到後AEM端並請求自上次運行以來的資料更改。
* 伺服器檢索有問題的資料並將其壓縮到檔案中。
* 資料將返回到客戶機設備，資料將被提取到文檔資料夾中。
* UIWebView元件啟動/刷新。

如果無法建立連接，則將顯示以前下載的資料。

### 前進 {#getting-ahead}

要瞭解管理員和開發人員的角色和職責，請參閱以下資源：

* [為Adobe PhoneGap企業創AEM作](/help/mobile/phonegap.md)
* [為Adobe PhoneGap企業管理內AEM容](/help/mobile/administer-phonegap.md)
