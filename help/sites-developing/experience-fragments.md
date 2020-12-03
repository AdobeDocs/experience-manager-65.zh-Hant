---
title: 體驗片段
seo-title: 體驗片段
description: 瞭解自訂體驗片段。
seo-description: 瞭解自訂體驗片段。
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# 體驗片段{#experience-fragments}

## The Basics {#the-basics}

[體驗片段](/help/sites-authoring/experience-fragments.md)是一組或多個元件，包括可在頁面中參考的內容和版面。

體驗片段主版和／或變體使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

因為沒有`/libs/cq/experience-fragments/components/xfpage/xfpage.html`，它會回復為

* `sling:resourceSuperType` :  `wcm/foundation/components/page`

## 純HTML轉譯{#the-plain-html-rendition}

使用URL中的`.plain.`選擇器，您可以存取純HTML轉譯。

這可從瀏覽器取得，但其主要用途是允許其他應用程式（例如協力廠商網頁應用程式、自訂行動裝置實作）僅使用URL直接存取體驗片段的內容。

純HTML轉譯會將通訊協定、主機和內容路徑新增至下列路徑：

* 類型：`src`、`href`或`action`

* 或結尾為：`-src`或`-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>連結一律會參照發佈例項。 這些連結會由協力廠商使用，因此一律會從發佈例項呼叫連結，而非作者。

![xf-14](assets/xf-14.png)

普通轉譯選擇器使用變壓器，而不是其他指令碼；[Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html)用作變壓器。 此設定位於

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## 社交變數{#social-variations}

社交變體可張貼在社交媒體（文字和影像）上。 在AEM中，這些社交變數可以包含元件；例如，文字元件、影像元件。

社交貼文的影像和文字可從任何深度等級的影像資源類型或文字資源類型（在建置區塊或版面容器中）擷取。

社交變化也允許建立區塊，並在進行社交動作時（在發佈環境上）加以考慮。

若要將正確的文字和影像張貼至社交媒體網路，若您要開發自訂的元件，就必須遵守一些慣例。

為此，必須使用下列屬性：

* 擷取影像

   * `fileReference`
   * `fileName`

* 用於提取文本

   * `text`

不使用本公約的部分將不予考慮。

## 體驗片段範本{#templates-for-experience-fragments}

>[!CAUTION]
>
>***體*** [驗片](/help/sites-developing/page-templates-editable.md) 段支援可線上範本。

開發體驗片段的新範本時，您可以遵循[可編輯範本](/help/sites-developing/page-templates-editable.md)的標準實務。

要建立由&#x200B;**建立體驗片段**&#x200B;嚮導檢測到的體驗片段模板，必須遵循以下規則集之一：

1. 兩者:

   1. 模板的資源類型（初始節點）必須繼承自：
      `cq/experience-fragments/components/xfpage`

   1. 範本名稱必須以下列項目開頭：
      `experience-fragments`
這可讓使用者在/content/experience-fragments中建立體驗片段， 
`cq:allowedTemplates` 屬性包含名稱以開頭的所有模板 `experience-fragment`客戶可以更新此屬性以包含其自己的命名方案或範本位置。

1. [允許](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 的範本掃描可在「體驗片段」主控台中設定。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 體驗片段的元件{#components-for-experience-fragments}

[開發](/help/sites-developing/components.md) 元件以搭配使用／在Experience片段時，遵循標準實務。

唯一額外的配置是確保模板上允許[元件，這是通過內容策略](/help/sites-developing/page-templates-editable.md#content-policies)實現的。

## 體驗片段連結重新寫入器提供者- HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM中，您可以建立「體驗片段」。 體驗片段：

* 由一組元件和一個版面組成，
* 可以獨立於AEM頁面存在。

此類群組的其中一個使用案例是將內容內嵌至第三方觸點，例如Adobe Target。

### 預設鏈路重寫{#default-link-rewriting}

使用[匯出至Target](/help/sites-administering/experience-fragments-target.md)功能，您可以：

* 建立體驗片段，
* 新增元件，
* 然後匯出為Adobe Target選件，以HTML格式或JSON格式。

此功能可在AEM[的作者例項上啟用。 ](/help/sites-administering/experience-fragments-target.md#Prerequisites)它需要有效的Adobe Target設定，以及連結外部化程式的設定。

Link Externalizer可用來判斷建立Target選件的HTML版本時所需的正確URL，此HTML版本隨後會傳送至Adobe Target。 這是必要的，因為Adobe Target要求Target HTML選件內的所有連結都可公開存取；這表示必須先發佈連結參考的任何資源，以及體驗片段本身，才能加以使用。

依預設，當您建構Target HTML選件時，會將請求傳送至AEM中的自訂Sling選擇器。 此選擇器稱為`.nocloudconfigs.html`。 正如其名稱所暗示的，它會建立體驗片段的純HTML轉換，但不包含雲端設定（這將是多餘的資訊）。

在您產生HTML頁面後，Sling Rewriter管道會修改輸出：

1. `html`、`head`和`body`元素會以`div`元素取代。 `meta`、`noscript`和`title`元素會被移除（它們是原始`head`元素的子元素，當由`div`元素取代時，不會考慮這些元素）。

   這麼做是為了確保HTML Target選件可包含在Target活動中。

1. AEM會修改HTML中顯示的任何內部連結，以便它們指向已發佈的資源。

   若要決定要修改的連結，AEM會遵循此HTML元素屬性的模式：

   1. `src` 屬性
   1. `href` 屬性
   1. `*-src` 屬性（如data-src、custom-src等）
   1. `*-href` 屬性( `data-href`如 `custom-href`、 `img-href`等)

   >[!NOTE]
   >
   >在大多數情況下，HTML中的內部連結是相對連結，但是當自訂元件在HTML中提供完整的URL時，可能會有此情況。 依預設，AEM會忽略這些羽翼豐滿的URL，且不會進行任何修改。

   這些屬性中的連結會透過AEM Link Externalizer `publishLink()`執行，以重新建立URL，就像它在已發佈的例項上一樣，而且可公開使用。

使用現成可用的實作時，上述程式應足以從體驗片段產生目標選件，然後將其匯出至Adobe Target。 但是，有些使用案例在此過程中沒有說明；這些包括：

* Sling Mapping僅適用於發佈例項
* Dispatcher redirects

針對這些使用案例，AEM提供「連結重寫器提供者介面」。

### 鏈路重寫器提供程式介面{#link-rewriter-provider-interface}

>[!NOTE]
>
>此介面已在[AEM 6.5 SP1(6.5.1.0)](/help/release-notes/sp-release-notes.md)中引入。

對於更複雜的情況，AEM提供「連結重寫器提供者介面」，但未涵蓋在[default](#default-link-rewriting)中。 這是一個`ConsumerType`介面，您可以在捆綁包中作為服務實施。 它會略過AEM在從「體驗片段」轉譯的HTML選件內部連結上所執行的修改。 此介面可讓您自訂重寫內部HTML連結的程式，以符合您的業務需求。

將此介面作為服務實現的使用案例包括：

* Sling Mappings are enabled on the publish instances, but not on the author instance
* 使用分派程式或類似技術，在內部重新導向URL
* 資源有`sling:alias mechanisms`

>[!NOTE]
>
>此介面僅處理產生之Target選件的內部HTML連結。

連結重寫器提供程式介面(`ExperienceFragmentLinkRewriterProvider`)如下：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用鏈路重寫器提供程式介面{#how-to-use-the-link-rewriter-provider-interface}

要使用該介面，首先需要建立一個包，其中包含實現連結重寫器提供程式介面的新服務元件。

此服務將用於插入「體驗片段匯出至目標」重寫，以便存取各種連結。

例如，`ComponentService`:

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

為了讓服務發揮作用，現在需要在服務中實施三種方法：

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

您需要向系統指出，當對特定體驗片段變數的「匯出至目標」進行呼叫時，是否需要重寫連結。 您可透過實作方法來執行此動作：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

此方法會接收「匯出至目標」系統目前正在重寫的「體驗片段變數」(Experience Fragment Variation)作為參數。

在上述範例中，我們想要重寫：

* `src`中的連結

* `href` 僅限

* 針對特定體驗片段：
   `/content/experience-fragment/master`

透過「匯出至目標」系統的其他任何體驗片段都會被忽略，不受本服務中實作變更的影響。

#### rewriteLink {#rewritelink}

對於受重寫過程影響的體驗片段變化，它會繼續讓服務處理鏈路重寫。 每當在內部HTML中遇到連結時，就會呼叫下列方法：

`rewriteLink(String link, String tag, String attribute)`

作為輸入，方法接收以下參數：

* `link`
The 
`String` 表示目前正在處理的連結。這通常是指向作者實例上資源的相對URL。

* `tag`
目前正在處理的HTML元素名稱。

* `attribute`
確切的屬性名稱。

例如，如果「導出到目標」系統當前正在處理此元素，則可以將`CSSInclude`定義為：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

對`rewriteLink()`方法的調用使用以下參數完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

當您建立服務時，您可以根據指定的輸入做出決策，然後據以重寫連結。

對於我們的範例，我們想移除URL的`/etc.clientlibs`部分，並新增適當的外部網域。 為了保持簡單，我們將考慮我們有權訪問您的服務的資源解析器，如`rewriteLinkExample2`中：

>[!NOTE]
>
>如需如何透過服務使用者取得資源解析程式的詳細資訊，請參閱「AEM中的服務使用者」。[](/help/sites-administering/security-service-users.md)

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
>如果上述方法返回`null`，則「導出到目標」系統將保留連結的原狀，即資源的相對連結。

#### 優先順序- getPriority {#priorities-getpriority}

需要數種服務來迎合不同類型的體驗片段，甚至需要一般服務來處理所有體驗片段的外部化和對應，這種情況並不少見。 在這些情況下，可能會發生使用哪些服務的衝突，因此AEM提供為不同服務定義&#x200B;**優先順序**&#x200B;的可能性。 優先順序通過使用方法指定：

* `getPriority()`

此方法允許使用數個服務，其中`shouldRewrite()`方法針對相同的體驗片段傳回true。 從其`getPriority()`方法傳回最高數目的服務是處理體驗片段變化的服務。

例如，您可以有`GenericLinkRewriterProvider`來處理所有體驗片段的基本對應，以及當`shouldRewrite()`方法傳回所有體驗片段變化的`true`時。 對於多個特定的體驗片段，您可能需要特殊處理，因此在此例中，您可以提供`SpecificLinkRewriterProvider`，其中`shouldRewrite()`方法僅針對某些體驗片段變數傳回true。 為確保選擇`SpecificLinkRewriterProvider`來處理這些體驗片段變化，它必須在`getPriority()`方法中傳回高於`GenericLinkRewriterProvider.`的數字
