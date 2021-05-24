---
title: 體驗片段
seo-title: 體驗片段
description: 了解自訂體驗片段。
seo-description: 了解自訂體驗片段。
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---

# 體驗片段{#experience-fragments}

## 基本知識{#the-basics}

[體驗片段](/help/sites-authoring/experience-fragments.md)是一組一或多個元件，包括可在頁面中參照的內容和版面。

體驗片段主版和/或變體使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

由於沒有`/libs/cq/experience-fragments/components/xfpage/xfpage.html`，因此它會回復為

* `sling:resourceSuperType` :  `wcm/foundation/components/page`

## 純HTML格式副本{#the-plain-html-rendition}

使用URL中的`.plain.`選取器，可以存取純HTML轉譯。

這可從瀏覽器取得，但其主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動實作）僅使用URL直接存取體驗片段的內容。

純HTML轉譯會將通訊協定、主機和內容路徑新增至以下路徑：

* 類型：`src`、`href`或`action`

* 或結尾為：`-src`或`-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>連結一律會參考發佈例項。 協力廠商會使用這些連結，因此系統一律會從發佈例項呼叫連結，而非作者。

![xf-12](assets/xf-14.png)

純格式副本選擇器使用變壓器，而不使用其他指令碼；[Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)用作變壓器。 此設定於

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## 社交變異{#social-variations}

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

未使用本公約的部分將不予考慮。

## 體驗片段{#templates-for-experience-fragments}的範本

>[!CAUTION]
>
>****** [體驗](/help/sites-developing/page-templates-editable.md) 片段支援可內嵌的範本。

為體驗片段開發新範本時，您可以遵循[可編輯範本](/help/sites-developing/page-templates-editable.md)的標準實務。

若要建立由&#x200B;**建立體驗片段**&#x200B;精靈偵測到的體驗片段範本，您必須遵循下列其中一個規則集：

1. 兩者:

   1. 模板的資源類型（初始節點）必須繼承自：
      `cq/experience-fragments/components/xfpage`

   1. 而範本的名稱必須以下項目開頭：
      `experience-fragments`
這可讓使用者在/content/experience-fragments中建立體驗片段，作為 
`cq:allowedTemplates` 此資料夾的屬性包含名稱開頭為的所有范 `experience-fragment`本。客戶可更新此屬性以包含其自己的命名配置或範本位置。

1. [允許](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 的範本掃描可在體驗片段主控台中設定。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 體驗片段{#components-for-experience-fragments}的元件

[開發](/help/sites-developing/components.md) 元件以與體驗片段搭配使用/在體驗片段中使用遵循標準實務。

唯一的額外配置是確保模板上允許的元件為[，這是通過內容策略](/help/sites-developing/page-templates-editable.md#content-policies)實現的。

## 體驗片段連結重寫器提供者 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以建立體驗片段。 體驗片段：

* 包含一組元件和佈局，
* 可獨立於AEM頁面存在。

此類群組的使用案例之一，是將內容內嵌在協力廠商接觸點，例如Adobe Target。

### 預設連結重寫{#default-link-rewriting}

使用[匯出至Target](/help/sites-administering/experience-fragments-target.md)功能，您可以：

* 建立體驗片段，
* 添加元件，
* 然後以HTML格式或JSON格式將其匯出為Adobe Target選件。

可在AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites)的製作例項上啟用此功能[。 它需要有效的Adobe Target設定，以及連結外部化程式的設定。

Link Externalizer可用來判斷建立Target選件的HTML版本時所需的正確URL，該版本隨後會傳送至Adobe Target。 這是必要的，因為Adobe Target要求Target HTML選件內的所有連結都可公開存取；這表示連結參考的任何資源，以及體驗片段本身，都必須先發佈，才可使用。

依預設，當您建構Target HTML選件時，會傳送要求給AEM中的自訂Sling選取器。 此選擇器稱為`.nocloudconfigs.html`。 如其名稱所示，它會建立體驗片段的純HTML轉譯，但不包含雲端設定（這會是多餘的資訊）。

產生HTML頁面後，Sling Rewriter管道會對輸出進行修改：

1. `html`、`head`和`body`元素會取代為`div`元素。 移除`meta`、`noscript`和`title`元素（它們是原始`head`元素的子元素，當此元素被`div`元素取代時，不會考慮）。

   這麼做是為了確保HTML Target選件可包含在Target活動中。

1. AEM會修改HTML中出現的任何內部連結，使其指向已發佈的資源。

   若要決定要修改的連結，AEM會遵循以下HTML元素屬性模式：

   1. `src` 屬性
   1. `href` 屬性
   1. `*-src` 屬性（例如data-src、custom-src等）
   1. `*-href` 屬性( `data-href`如、  `custom-href`、  `img-href`等)

   >[!NOTE]
   >
   >在大多數情況下，HTML中的內部連結都是相對連結，但某些情況下，自訂元件可能會在HTML中提供完整的URL。 依預設，AEM會忽略這些完整的URL，而不會進行修改。

   這些屬性中的連結會透過AEM Link Externalizer `publishLink()`執行，以便重新建立URL，就像它在已發佈的執行個體上一樣，且可公開使用。

使用現成可用的實作時，上述程式應足以從體驗片段產生Target選件，然後將其匯出至Adobe Target。 但是，有些使用案例在此過程中沒有說明；包括：

* Sling對應僅適用於發佈執行個體
* Dispatcher重新導向

在這些使用案例中，AEM提供連結重寫器提供者介面。

### 連結重寫器提供程式介面{#link-rewriter-provider-interface}

>[!NOTE]
>
>此介面在[AEM 6.5 SP1(6.5.1.0)](/help/release-notes/sp-release-notes.md)中導入。

對於[default](#default-link-rewriting)未涵蓋的更複雜情況，AEM提供連結重寫器提供程式介面。 這是`ConsumerType`介面，您可以在套件組合中以服務形式實作。 它會略過AEM對從體驗片段轉譯之HTML選件的內部連結所執行的修改。 此介面可讓您自訂重新寫入內部HTML連結的程式，以符合您的業務需求。

以服務形式實作此介面的使用案例包括：

* Sling對應是在發佈執行個體上啟用，但不是在製作執行個體上啟用
* Dispatcher或類似的技術可用於在內部重新導向URL
* 資源有`sling:alias mechanisms`

>[!NOTE]
>
>此介面只會處理來自產生Target選件的內部HTML連結。

連結重寫器提供程式介面(`ExperienceFragmentLinkRewriterProvider`)如下：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用連結重寫器提供程式介面{#how-to-use-the-link-rewriter-provider-interface}

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

* `src`中的連結

* `href` 僅限屬性

* 針對特定體驗片段：
   `/content/experience-fragment/master`

透過匯出至Target系統的任何其他體驗片段都會遭到忽略，不會受此服務中實作的變更影響。

#### rewriteLink {#rewritelink}

對於受重新寫入程式影響的體驗片段變數，接著會繼續讓服務處理連結重新寫入。 每當在內部HTML中遇到連結時，就會叫用下列方法：

`rewriteLink(String link, String tag, String attribute)`

作為輸入，方法接收以下參數：

* `link`
此 
`String` 表示目前正在處理的連結。這通常是指向製作例項上資源的相對URL。

* `tag`
目前正在處理的HTML元素名稱。

* `attribute`
確切的屬性名稱。

例如，如果「匯出至目標」系統目前正在處理此元素，您可以將`CSSInclude`定義為：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

對`rewriteLink()`方法的呼叫是使用下列參數完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

當您建立服務時，可以根據指定的輸入進行決策，然後據以重寫連結。

例如，我們要移除URL的`/etc.clientlibs`部分，並新增適當的外部網域。 為了簡單起見，我們會考慮可以存取您服務的資源解析器，如`rewriteLinkExample2`中：

>[!NOTE]
>
>如需如何透過服務使用者取得資源解析器的詳細資訊，請參閱AEM](/help/sites-administering/security-service-users.md)中的[服務使用者。

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
>如果上述方法傳回`null`，則匯出至目標系統會保留原樣的連結，即資源的相對連結。

#### 優先順序 — getPriority {#priorities-getpriority}

需要數種服務來應付不同類型的體驗片段，甚至需要一般服務來處理所有體驗片段的外部化和對應，這並不罕見。 在這些情況下，可能會發生與要使用哪些服務有關的衝突，因此AEM提供了為不同服務定義&#x200B;**優先順序**&#x200B;的可能性。 使用以下方法指定優先順序：

* `getPriority()`

此方法允許使用數個服務，其中`shouldRewrite()`方法對相同的體驗片段傳回true。 從`getPriority()`方法傳回最高數字的服務，是處理體驗片段變異的服務。

例如，您可以有`GenericLinkRewriterProvider`來處理所有體驗片段的基本對應，以及當`shouldRewrite()`方法為所有體驗片段變體傳回`true`時。 對於數個特定體驗片段，您可能需要特殊處理，因此在此情況下，您可以提供`SpecificLinkRewriterProvider`，其中`shouldRewrite()`方法僅對某些體驗片段變異傳回true。 若要確定已選擇`SpecificLinkRewriterProvider`處理這些體驗片段變化，它必須在其`getPriority()`方法中傳回高於`GenericLinkRewriterProvider.`的數字
