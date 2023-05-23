---
title: AEM Sites發展的經驗片段
description: 瞭解自定義體驗片段。
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

## 基礎 {#the-basics}

安 [體驗片段](/help/sites-authoring/experience-fragments.md) 是一個或多個元件的組，包括可在頁面中引用的內容和佈局。

經驗片段主和/或變型使用：

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

因為沒有 `/libs/cq/experience-fragments/components/xfpage/xfpage.html` 它會恢復

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## 純HTML格式副本 {#the-plain-html-rendition}

使用 `.plain.` selector，您可以訪問純HTML格式副本。

這可從瀏覽器獲得，但其主要用途是允許其他應用程式（例如，第三方Web應用程式、自定義移動實現）僅使用URL直接訪問體驗片段的內容。

純HTML格式副本將協定、主機和上下文路徑添加到以下路徑：

* 類型： `src`。 `href`或 `action`

* 或以： `-src`或 `-href`

例如：

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>連結始終引用發佈實例。 這些連結旨在由第三方使用，因此連結將始終從發佈實例調用，而不是作者。

![xf-14](assets/xf-14.png)

普通格式副本選擇器使用變壓器而不是附加指令碼；這樣 [斯林重寫器](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) 用作變壓器。 此配置在

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### 配置HTML格式副本生成 {#configuring-html-rendition-generation}

HTML格式副本使用Sling Rewriter管道生成。 管線在 `/libs/experience-fragments/config/rewriter/experiencefragments`。 HTML變壓器支援以下選項：

* `allowedCssClasses`
   * RegEx表達式，它與應保留在最終格式副本中的CSS類匹配。
   * 如果客戶要刪除某些特定的CSS類，則此功能非常有用
* `allowedTags`
   * 要在最終格式副本中允許的HTML標籤清單。
   * 預設情況下，允許使用以下標籤（不需要配置）:html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h5, h6, br, noscript, div, link，指令碼

建議使用覆蓋配置重寫器。 請參閱 [覆蓋](/help/sites-developing/overlays.md)

## 社會變異 {#social-variations}

社交變體可以在社交媒體（文本和影像）上發佈。 在這AEM些社交變體中，可以包含元件；例如，文本元件、影像元件。

社交帖子的影像和文本可以從任何深度級別（在構建塊或佈局容器中）的任何影像資源類型或文本資源類型中獲取。

社會差異還允許在進行社會行動（在出版環境上）時考慮建構要素。

若要將正確的文本和影像發佈到社交媒體網路，如果您正在開發自己的定製元件，則需要遵守一些約定。

為此，必須使用以下屬性：

* 用於提取影像

   * `fileReference`
   * `fileName`

* 用於提取文本

   * `text`

不使用本公約的部分不予考慮。

## 體驗片段模板 {#templates-for-experience-fragments}

>[!CAUTION]
>
>***僅*** [可編輯模板](/help/sites-developing/page-templates-editable.md) 支援體驗片段。

在為「體驗片段」開發新模板時，您可以遵循 [可編輯模板](/help/sites-developing/page-templates-editable.md)。

建立由 **建立體驗片段** 嚮導，您必須遵循以下規則集之一：

1. 兩者:

   1. 模板的資源類型（初始節點）必須從以下位置繼承：
      `cq/experience-fragments/components/xfpage`

   1. 模板名稱必須以下列內容開頭：
      `experience-fragments`
這允許用戶在/content/experience-fragments中建立體驗片段作為 
`cq:allowedTemplates` 此資料夾的屬性包含名稱以開頭的所有模板 `experience-fragment`。 客戶可以更新此屬性以包括其自己的命名方案或模板位置。

1. [允許的模板](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) 可以在「體驗片段」控制台中配置。

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## 經驗片段的元件 {#components-for-experience-fragments}

[開發元件](/help/sites-developing/components.md) 與「經驗」(Experience)「片段」(Fragments)配合使用，遵循標準慣例。

唯一的附加配置是確保 [允許在模板上，這是通過內容策略實現的](/help/sites-developing/page-templates-editable.md#content-policies)。

## 體驗片段連結重寫器提供程式 — HTML {#the-experience-fragment-link-rewriter-provider-html}

在AEM您可以建立體驗片段。 體驗片段：

* 由一組元件和一個佈局組成，
* 可以獨立於頁面存AEM在。

此類組的一個使用案例是將內容嵌入第三方觸點，如Adobe Target。

### 預設連結重寫 {#default-link-rewriting}

使用 [導出到目標](/help/sites-administering/experience-fragments-target.md) 功能，您可以：

* 建立體驗片段，
* 添加元件，
* 然後以HTML格式或JSON格式將其導出為Adobe Target優惠。

此功能可以是 [在的作者實例上啟AEM用](/help/sites-administering/experience-fragments-target.md#Prerequisites)。 它需要有效的Adobe Target配置和連結外部化程式的配置。

連結外部化程式用於確定建立目標服務的HTML版本時所需的正確URL，該版本隨後將發送到Adobe Target。 這是必要的，因為Adobe Target要求可以公開訪問目標HTML服務內的所有連結；這意味著必須先發佈連結引用的任何資源以及體驗片段本身，然後才能使用這些資源。

預設情況下，在構建目標HTML提供時，會向中的自定義Sling選擇器發送請AEM求。 此選擇器被調用 `.nocloudconfigs.html`。 正如其名稱所暗示的，它建立體驗片段的純HTML渲染，但不包括雲配置（這將是多餘的資訊）。

生成HTML頁後，Sling Rewriter管線將修改輸出：

1. 的 `html`。 `head`, `body` 元素替換為 `div` 元素。 的 `meta`。 `noscript` 和 `title` 元素被移除(它們是原始元素的子元素 `head` 元素，並且當替換為 `div` 元素)。

   這樣做是為了確保HTML目標優惠可以包括在目標活動中。

1. 修AEM改HTML中存在的任何內部連結，以便它們指向已發佈的資源。

   要確定要修改的連結，請AEM遵循以下HTML元素屬性模式：

   1. `src` 屬性
   1. `href` 屬性
   1. `*-src` 屬性（如data-src、custom-src等）
   1. `*-href` 屬性(如 `data-href`。 `custom-href`。 `img-href`等等

   >[!NOTE]
   >
   >在大多數情況下，HTML中的內部連結是相對連結，但在自定義元件在HTML中提供完整URL時，可能會出現這種情況。 預設情況下，AEM將忽略這些完整的URL，並且不進行任何修改。

   這些屬性中的連結通過連結外部AEM化程式運行 `publishLink()` 以重新建立URL，就像它位於已發佈實例上一樣，可公開使用。

使用現成實施時，上述過程應足以從經驗片段生成目標優惠，然後將其導出到Adobe Target。 但是，有些使用案例在此過程中沒有說明；這些包括：

* 僅在發佈實例上提供Sling映射
* 調度程式重定向

對於這些使用AEM情形，提供「連結重寫器提供程式介面」。

### 連結重寫器提供程式介面 {#link-rewriter-provider-interface}

>[!NOTE]
>
>此介面在 [AEM6.5 SP1(6.5.1.0)](/help/release-notes/previous/6.5.1.md)。

對於更複雜的案例， [預設](#default-link-rewriting)，提供AEM連結重寫器提供程式介面。 這是 `ConsumerType` 作為服務在捆綁包中實現的介面。 它繞過從體驗AEM片段呈現的HTML要約的內部連結執行的修改。 此介面允許您自定義改寫內部HTML連結的過程，以符合您的業務需要。

將此介面作為服務實現的使用案例包括：

* 在發佈實例上啟用Sling映射，但在作者實例上未啟用
* 調度程式或類似技術用於在內部重定向URL
* 有 `sling:alias mechanisms` 已到位

>[!NOTE]
>
>此介面僅處理生成的目標優惠中的內部HTML連結。

連結重寫器提供程式介面( `ExperienceFragmentLinkRewriterProvider`)如下所示：

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### 如何使用連結重寫器提供程式介面 {#how-to-use-the-link-rewriter-provider-interface}

要使用介面，您首先需要建立一個包，其中包含實現連結重寫器提供程式介面的新服務元件。

此服務將用於插入「將體驗片段導出到目標重寫」，以便能夠訪問各種連結。

比如說， `ComponentService`:

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

對於服務工作，現在需要在服務內部實現三種方法：

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### 應重寫 {#shouldrewrite}

您需要向系統指示，在對特定體驗片段變體的「導出到目標」發出調用時，系統是否需要重寫連結。 通過實現以下方法，可以執行此操作：

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例如：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

該方法接收作為參數的導出到目標系統當前正在重寫的經驗片段變化。

在上例中，我們要重寫：

* 存在的連結 `src`

* `href` 僅屬性

* 特定體驗片段：
   `/content/experience-fragment/master`

通過「導出到目標」系統的任何其他體驗片段將被忽略，並且不受此服務中實現的更改的影響。

#### 重寫連結 {#rewritelink}

對於受重寫過程影響的體驗片段變化，再由服務處理鏈路重寫。 每當在內部HTML中遇到連結時，都會調用以下方法：

`rewriteLink(String link, String tag, String attribute)`

作為輸入，該方法接收參數：

* `link`  
`String` 當前正在處理的連結的表示形式。 這通常是指向作者實例上的資源的相對URL。

* `tag`
當前正在處理的HTML元素的名稱。

* `attribute`
確切的屬性名。

例如，如果「導出到目標」系統當前正在處理此元素，則可以定義 `CSSInclude` 為：

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

呼叫 `rewriteLink()` 方法使用以下參數完成：

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

在建立服務時，您可以根據給定的輸入做出決策，然後相應地重寫連結。

例如，我們要刪除 `/etc.clientlibs` 添加相應的外部域。 為了保持簡單，我們將考慮我們有權訪問您的服務的資源解析程式，如 `rewriteLinkExample2`:

>[!NOTE]
>
>有關如何通過服務用戶獲取資源解析程式的詳細資訊，請參閱 [服務用AEM戶](/help/sites-administering/security-service-users.md)。

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
>如果以上方法返回 `null`，則「導出到目標」系統將保留連結原樣，即資源的相對連結。

#### 優先順序 — getPriority {#priorities-getpriority}

需要多種服務來滿足不同種類的體驗片段，甚至需要通用服務來處理所有體驗片段的外部化和映射，這種情況並不少見。 在這些情況下，可能會發生與要使用哪些服務有關的衝突，AEM因此可以定義 **優先順序** 不同服務。 使用以下方法指定優先順序：

* `getPriority()`

此方法允許使用多個服務， `shouldRewrite()` 方法對於同一經驗片段返回true。 返回其中最大數目的服務 `getPriority()`方法是處理體驗片段變化的服務。

例如，您可以 `GenericLinkRewriterProvider` 處理所有體驗片段的基本映射，以及 `shouldRewrite()` 方法返回 `true` 所有體驗片段變體。 對於幾個特定的體驗片段，您可能需要特殊處理，因此在本例中，您可以提供 `SpecificLinkRewriterProvider` 對於 `shouldRewrite()` 方法僅對某些經驗片段變體返回true。 確保 `SpecificLinkRewriterProvider` 被選擇處理這些體驗片段變體，它必須返回 `getPriority()` 方法大於 `GenericLinkRewriterProvider.`
