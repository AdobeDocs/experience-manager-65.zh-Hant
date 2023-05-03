---
title: AEM Sites開發中的體驗片段
description: 了解自訂體驗片段。
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
source-git-commit: a8616b3b30ac04ea24c4a869cabd47518af1a35f
workflow-type: tm+mt
source-wordcount: '1781'
ht-degree: 0%

---

# 體驗片段{#experience-fragments}

## 基本概念 {#the-basics}

安 [體驗片段](/help/sites-authoring/experience-fragments.md) 是一組一或多個元件，包含可在頁面中參照的內容和版面。

體驗片段主版和/或變體使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

因為沒有 `/libs/cq/experience-fragments/components/xfpage/xfpage.html` 它回復為

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 純HTML轉譯 {#the-plain-html-rendition}

使用 `.plain.` 選取器，您可以存取純HTML轉譯。

這可從瀏覽器取得，但其主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL直接存取體驗片段的內容。

純HTML格式副本會將通訊協定、主機和內容路徑新增至以下路徑：

* 類型： `src`, `href`，或 `action`

* 或結尾為： `-src`，或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>連結一律會參考發佈例項。 協力廠商會使用這些連結，因此系統一律會從發佈例項呼叫連結，而非作者。

![xf-14](assets/xf-14.png)

純格式副本選擇器使用變壓器，而不使用其他指令碼；the [Sling重寫器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 用作變壓器。 此設定於

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### 設定HTML轉譯產生 {#configuring-html-rendition-generation}

HTML轉譯是使用Sling Rewriter管道產生。 管道定義於 `/libs/experience-fragments/config/rewriter/experiencefragments`. HTML變壓器支援下列選項：

* `allowedCssClasses`
   * RegEx運算式，符合最終轉譯中應保留的CSS類別。
   * 如果客戶想要移除某些特定CSS類別，這個功能會很實用
* `allowedTags`
   * 要在最終轉譯中允許的HTML標籤清單。
   * 依預設，允許下列標籤（不需要設定）:html, head，標題， body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h5, h6, br, noscript, div, link和script

建議使用覆蓋來設定重寫器。 請參閱 [覆蓋](/help/sites-developing/overlays.md)

## 社交變數 {#social-variations}

社交變體可張貼在社交媒體（文字和影像）上。 在AEM中，這些社交變體可以包含元件；例如，文本元件、影像元件。

社交貼文的影像和文字可從任何深度層級（在建置區塊或版面容器中）的任何影像資源類型或文字資源類型擷取。

社交變異也允許建置區塊，並在進行社交動作（在發佈環境中）時加以考量。

若要將正確的文字和影像發佈至社交媒體網路，如果您要開發自己的自訂元件，則需要遵守一些慣例。

為此，必須使用下列屬性：

* 用於提取影像

   * `fileReference`
   * `fileName`

* 用於提取文本

   * `text`

未使用本公約的元件不予考慮。

## 體驗片段的範本 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***僅*** [可編輯的範本](/help/sites-developing/page-templates-editable.md) 支援體驗片段。

開發體驗片段的新範本時，您可以遵循 [可編輯的範本](/help/sites-developing/page-templates-editable.md).

若要建立由 **建立體驗片段** 嚮導中，您必須遵循以下規則集之一：

1. 兩者:

   1. 模板的資源類型（初始節點）必須繼承自：
      `cq/experience-fragments/components/xfpage`

   1. 而範本的名稱必須以下項目開頭：
      `experience-fragments`
這可讓使用者在/content/experience-fragments中建立體驗片段，作為 
`cq:allowedTemplates` 此資料夾的屬性包括名稱開頭為的所有模板 `experience-fragment`. 客戶可更新此屬性以包含其自己的命名配置或範本位置。

1. [允許的範本](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 可在體驗片段主控台中設定。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 體驗片段的元件 {#components-for-experience-fragments}

[開發元件](/help/sites-developing/components.md) 若要與體驗片段搭配使用/使用，請遵循標準實務。

唯一的額外設定是確保元件為 [允許在範本上，這是使用內容原則來實現的](/help/sites-developing/page-templates-editable.md#content-policies).

## 體驗片段連結重寫器提供者 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以建立體驗片段。 體驗片段：

* 包含一組元件和佈局，
* 可獨立於AEM頁面存在。

此類群組的使用案例之一，是將內容內嵌在協力廠商接觸點，例如Adobe Target。

### 預設連結重寫 {#default-link-rewriting}

使用 [匯出至Target](/help/sites-administering/experience-fragments-target.md) 功能，您可以：

* 建立體驗片段，
* 添加元件，
* 然後以「HTML格式」或「JSON格式」將其匯出為「Adobe Target選件」。

此功能可以是 [在AEM的製作例項上啟用](/help/sites-administering/experience-fragments-target.md#Prerequisites). 它需要有效的Adobe Target設定，以及連結外部化程式的設定。

Link Externalizer可用來判斷建立Target選件的HTML版本時所需的正確URL，該版本隨後會傳送至Adobe Target。 這是必要的，因為Adobe Target要求TargetHTML選件內的所有連結都可公開存取；這表示連結參考的任何資源，以及體驗片段本身，都必須先發佈，才可使用。

依預設，當您建立TargetHTML選件時，會傳送要求給AEM中的自訂Sling選取器。 此選取器稱為 `.nocloudconfigs.html`. 如其名稱所示，它會建立體驗片段的純HTML轉譯，但不包含雲端設定（這會是多餘的資訊）。

產生HTML頁面後，Sling Rewriter管道會對輸出進行修改：

1. 此 `html`, `head`，和 `body` 元素取代為 `div` 元素。 此 `meta`, `noscript` 和 `title` 元素被移除(它們是原始元素的子元素 `head` 元素，並且會在以 `div` 元素)。

   這麼做是為了確保HTMLTarget選件可包含在Target活動中。

1. AEM會修改HTML中出現的任何內部連結，使其指向已發佈的資源。

   若要決定要修改的連結，AEM會依照以下模式處理HTML元素的屬性：

   1. `src` 屬性
   1. `href` 屬性
   1. `*-src` 屬性（例如data-src、custom-src等）
   1. `*-href` 屬性(如 `data-href`, `custom-href`, `img-href`、等)

   >[!NOTE]
   >
   >在大多數情況下，HTML中的內部連結都是相對連結，但在某些情況下，自訂元件可能會在HTML中提供完整URL。 依預設，AEM會忽略這些完整的URL，而不會進行修改。

   這些屬性中的連結會透過AEM Link Externalizer執行 `publishLink()` 以便將URL重新建立為位於已發佈的執行個體，並依此公開提供。

使用現成可用的實作時，上述程式應足以從體驗片段產生Target選件，然後將其匯出至Adobe Target。 但是，有些使用案例在此過程中沒有說明；包括：

* Sling對應僅適用於發佈執行個體
* Dispatcher重新導向

在這些使用案例中，AEM提供連結重寫器提供者介面。

### 連結重寫器提供程式介面 {#link-rewriter-provider-interface}

>[!NOTE]
>
>此介面已於 [AEM 6.5 SP1(6.5.1.0)](/help/release-notes/previous/6.5.1.md).

對於更複雜的案例， [預設](#default-link-rewriting), AEM提供連結重寫器提供者介面。 這是 `ConsumerType` 介面（以服務形式）。 它會略過AEM對從體驗片段轉譯之HTML選件的內部連結所執行的修改。 此介面可讓您自訂重新寫入內部HTML連結的程式，以符合您的業務需求。

以服務形式實作此介面的使用案例包括：

* Sling對應是在發佈執行個體上啟用，但不是在製作執行個體上啟用
* Dispatcher或類似的技術可用於在內部重新導向URL
* 有 `sling:alias mechanisms` 就地

>[!NOTE]
>
>此介面只會處理來自產生的Target選件的內部HTML連結。

連結重寫器提供程式介面( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用連結重寫器提供程式介面 {#how-to-use-the-link-rewriter-provider-interface}

若要使用介面，您首先需要建立包含新服務元件的套件組合，此元件會實施連結重寫器提供者介面。

此服務將用於外掛至Target轉存的體驗片段，以便存取各種連結。

例如， `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

為了讓服務運作，現在有三種方法需要在服務內實施：

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

您必須向系統指出，當對特定體驗片段變數的匯出目標發出呼叫時，是否需要重寫連結。 若要這麼做，請實作方法：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法會接收「匯出至目標」系統目前正在重新寫入的體驗片段變異，作為參數。

在上述範例中，我們想重新寫入：

* 存在的連結 `src`

* `href` 僅限屬性

* 針對特定體驗片段：
   `/content/experience-fragment/master`

透過匯出至Target系統的任何其他體驗片段都會遭到忽略，不會受此服務中實作的變更影響。

#### rewriteLink {#rewritelink}

對於受重新寫入程式影響的體驗片段變數，接著會繼續讓服務處理連結重新寫入。 每當在內部HTML中遇到連結時，就會叫用下列方法：

`rewriteLink(String link, String tag, String attribute)`

作為輸入，方法接收以下參數：

* `link`  
`String` 表示目前正在處理的連結。 這通常是指向製作例項上資源的相對URL。

* `tag`
目前正在處理的HTML元素名稱。

* `attribute`
確切的屬性名稱。

例如，如果匯出至目標系統目前正在處理此元素，您可以定義 `CSSInclude` 如下：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

呼叫 `rewriteLink()` 方法會使用下列參數完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

當您建立服務時，可以根據指定的輸入進行決策，然後據以重寫連結。

例如，我們要移除 `/etc.clientlibs` URL的一部分，並新增適當的外部網域。 為了讓事情簡單明瞭，我們會考慮您可以存取您服務的資源解析程式，如 `rewriteLinkExample2`:

>[!NOTE]
>
>如需如何透過服務使用者取得資源解析器的詳細資訊，請參閱 [AEM中的服務使用者](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>如果上述方法傳回 `null`，則「匯出至目標」系統會保留連結原樣，即資源的相對連結。

#### 優先順序 — getPriority {#priorities-getpriority}

需要數種服務來應付不同類型的體驗片段，甚至需要一般服務來處理所有體驗片段的外部化和對應，這並不罕見。 在這些情況下，可能會產生與要使用的服務相關的衝突，因此AEM可提供定義 **優先順序** 不同服務。 使用以下方法指定優先順序：

* `getPriority()`

此方法允許使用數個服務，其中 `shouldRewrite()` 方法會針對相同的體驗片段傳回true。 從中傳回最高數量的服務 `getPriority()`方法是處理體驗片段變異的服務。

例如，您可以 `GenericLinkRewriterProvider` 可處理所有體驗片段的基本對應，以及 `shouldRewrite()` 方法傳回 `true` 適用於所有體驗片段變化。 若為數個特定體驗片段，您可能需要特殊處理，因此在此案例中，您可以提供 `SpecificLinkRewriterProvider` 對於 `shouldRewrite()` 方法僅對某些體驗片段變體傳回true。 確保 `SpecificLinkRewriterProvider` 選擇用來處理這些體驗片段變化，它必須傳回 `getPriority()` 方法大於 `GenericLinkRewriterProvider.`
