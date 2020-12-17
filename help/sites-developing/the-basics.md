---
title: AEM Core Concepts
seo-title: 基本概念
description: 概述AEM結構化的核心概念，以及如何在此基礎上開發，包括瞭解JCR、Sling、OSGi、dispatcher、workflows和MSM
seo-description: 概述AEM結構化的核心概念，以及如何在此基礎上開發，包括瞭解JCR、Sling、OSGi、dispatcher、workflows和MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
translation-type: tm+mt
source-git-commit: 28fdb57f51a5bd97ce78b626db86f4a59de6f0be
workflow-type: tm+mt
source-wordcount: '3386'
ht-degree: 0%

---


# AEM Core Concepts {#aem-core-concepts}

>[!NOTE]
>
>在深入探討AEM的核心概念之前，Adobe建議先完成[開始開發AEM Sites](/help/sites-developing/getting-started.md)檔案中的WKND教學課程，以取得AEM開發流程的概觀和核心概念的簡介。

## AEM {#prerequisites-for-developing-on-aem}開發的必要條件

您需要下列技巧才能在AEM上進行開發：

* Web應用程式技術的基本知識，包括：

   * request -response(XMLHttpRequest / XMLHttpResponse)週期
   * HTML
   * CSS
   * JavaScript

* Experience Server(CRX)的使用知識，包括Content Explorer
* 在傳統的UI中開發時，還需要具備JSP(JavaServer Pages)的基本知識，包括瞭解和修改簡單JSP範例的能力。

建議您閱讀並遵循[准則和最佳實務](/help/sites-developing/dev-guidelines-bestpractices.md)。

## Java內容儲存庫{#java-content-repository}

Java內容儲存庫(JCR)標準[JSR 283](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/index.html)指定了一種獨立於供應商和獨立於實施的方式，以在內容儲存庫的精細級別上雙向訪問內容。

規格領導由Adobe Research（瑞士）AG負責。

[JCR API 2.0](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/index.html)套件javax.jcr。&amp;ast;用於直接訪問和控制儲存庫內容。

## Experience Server(CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供AEM所建立的Experience Services，並可用來建立自訂應用程式，並內嵌以Jackrabbit為基礎的內容存放庫。

[Apache ](https://jackrabbit.apache.org/) Jackrabbitis是開放原始碼、完全符合規範的JCR API 2.0實作。

## Sling Request Processing {#sling-request-processing}

### Sling {#introduction-to-sling}簡介

AEM是使用[Sling](https://sling.apache.org/site/index.html)建立的，此為以REST原則為基礎的Web應用程式架構，提供內容導向應用程式的輕鬆開發。 Sling會使用JCR儲存庫（例如Apache Jackrabbit），或在AEM中使用CRX Content Repository（CRX內容儲存庫）做為其資料儲存。 Sling已對Apache Software Foundation做出貢獻——如需詳細資訊，請參閱Apache。

使用Sling，要轉譯的內容類型不是第一個處理考量。 主要考量是URL是否解析為內容物件，然後可找到指令碼來執行轉譯。 這為網頁內容製作者提供絕佳的支援，讓他們建立可輕鬆依其需求自訂的頁面。

此彈性的優點在具有多種不同內容元素的應用程式中，或當您需要可輕鬆自訂的頁面時，都十分明顯。 尤其是在實作網頁內容管理系統（例如AEM解決方案中的WCM）時。

請參閱[Discover Sling in 15 minutes](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html)，以取得使用Sling進行開發的第一步驟。

下圖說明Sling指令碼解析度：它說明如何從HTTP請求到內容節點，從內容節點到資源類型，從資源類型到指令碼，以及可用的指令碼變數。

![瞭解Apache Sling指令碼解析度](assets/sling-cheatsheet-01.png)

下圖說明處理SlingPostServlet時，您可使用的所有隱藏但功能強大的請求參數，SlingPostServlet是所有POST請求的預設處理常式，提供您無限選項，以建立、修改、刪除、複製和移動儲存庫中的節點。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling is Content Centric {#sling-is-content-centric}

Sling為&#x200B;*content-centric*。 這表示處理會以JCR資源（儲存庫節點）的形式，將每個(HTTP)請求映射至內容時，將重點放在內容上：

* 第一個目標是保存內容的資源（JCR節點）
* 其次，表示或指令碼與請求的某些部分（如選擇器和／或擴展）組合從資源屬性中定位

### RESTful Sling {#restful-sling}

由於內容導向的理念，Sling建置了REST導向的伺服器，因此在Web應用程式架構中具備新概念。 其優點是：

* 非常REST風格，不只是表面上；資源和表示法在伺服器內正確建模
* 刪除一個或多個資料模型

   * 之前需要下列項目：URL結構、業務對象、資料庫模式；
   * 現在，此功能已簡化為：URL =資源= JCR結構

### URL分解{#url-decomposition}

在Sling中，處理是由使用者要求的URL所驅動。 這定義了要由相應指令碼顯示的內容。 若要這麼做，會從URL擷取資訊。

如果我們分析下列URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 | 內容路徑 | 選擇器 | extension |  | 尾碼 |  | param(s) |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具／間諜 | .printable.a4. | html | / | a/b | ? | x=12 |

**通** 訊協定HTTP

**主** 機網站名稱。

**content** path指定要呈現的內容的路徑。與擴展結合使用；在此範例中，它們會轉譯為tools/spy.html。

**selector(s)用** 於轉換內容的替代方法；在此示例中，A4格式的打印機友好版本。

**extensionContent** 格式；也指定要用於呈現的指令碼。

**尾碼** 可用於指定其他資訊。

**param(s)動態** 內容所需的任何參數。

#### 從URL到內容和指令碼{#from-url-to-content-and-scripts}

使用下列原則：

* 映射使用從請求中提取的內容路徑來定位資源
* 當找到適當的資源時，會擷取sling資源類型，並用來找出要用來呈現內容的指令碼

下圖說明所使用的機制，將在以下各節中詳細討論。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可指定要轉譯特定實體的指令碼（透過在JCR節點中設定`sling:resourceType`屬性）。 此機制提供比指令碼訪問資料實體（如PHP指令碼中的SQL陳述式）更多的自由，因為資源可以有多個轉譯。

#### 將請求映射到資源{#mapping-requests-to-resources}

請求會細分並擷取必要的資訊。 系統將搜索儲存庫以查找請求的資源（內容節點）:

* first Sling會檢查節點是否存在於請求中指定的位置；例如，`../content/corporate/jobs/developer.html`
* 如果沒有找到節點，則會丟棄擴展，並重複搜索；例如，`../content/corporate/jobs/developer`
* 如果找不到節點，Sling將會傳回http code 404(Not Found)。

Sling也允許JCR節點以外的項目成為資源，但這是進階功能。

### 查找指令碼{#locating-the-script}

當找到適當的資源（內容節點）時，會擷取&#x200B;**sling資源類型**。 這是路徑，可找到要用於呈現內容的指令碼。

`sling:resourceType`所指定的路徑可以是：

* 絕對值
* 相對，到配置參數

   Adobe建議使用相對路徑，因為相對路徑可提升可攜性。

所有Sling指令碼都儲存在`/apps`或`/libs`的子檔案夾中，會依此順序搜尋（請參閱[自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

還需注意的一點是：

* 當需要方法(GET、POST)時，會根據HTTP規格（例如jobs.POST.esp）以大寫指定方法（請參閱下面）
* 支援各種指令碼引擎：

   * HTL（HTML範本語言- Adobe Experience Manager針對HTML偏好且建議的伺服器端範本系統）:`.html`
   * ECMAScript(JavaScript)頁面（伺服器端執行）:`.esp, .ecma`
   * Java伺服器頁（伺服器端執行）:`.jsp`
   * Java Servlet編譯器（伺服器端執行）:`.java`
   * JavaScript範本（用戶端執行）:`.jst`

AEM的指定例項支援的指令碼引擎清單列在Felix Management Console(`http://<host>:<port>/system/console/slingscripting`)上。

此外，Apache Sling支援與其他常用指令碼引擎（例如Groovy、JRuby、Freemarker）的整合，並提供整合新指令碼引擎的方式。

使用上述範例，如果`sling:resourceType`是`hr/jobs`，則表示：

* 以。html結尾的GET/HEAD請求和URL（預設請求類型，預設格式）

   指令碼將為/apps/hr/jobs/jobs.esp;sling:resourceType的最後一個區段會形成檔案名稱。

* POST請求（除GET/HEAD外的所有請求類型，方法名稱必須大寫）

   POST將用於指令碼名稱。

   指令碼將為`/apps/hr/jobs/jobs.POST.esp`。

* 其他格式的URL，不以。html結尾

   例如`../content/corporate/jobs/developer.pdf`

   指令碼將為`/apps/hr/jobs/jobs.pdf.esp`;尾碼將添加到指令碼名稱中。

* 具有選擇器的URL

   選擇器可用來以替代格式顯示相同的內容。 例如，印表機友好版本、RSS饋送或摘要。

   如果查看打印機友好版本，選擇器可以是&#x200B;*print*;as in `../content/corporate/jobs/developer.print.html`

   指令碼將為`/apps/hr/jobs/jobs.print.esp`;選取器會新增至指令碼名稱。

* 如果未定義sling:resourceType，則：

   * 內容路徑將用於搜索適當的指令碼（如果基於路徑的ResourceTypeProvider處於活動狀態）。

      例如，`../content/corporate/jobs/developer.html`的指令碼將在`/apps/content/corporate/jobs/`中生成搜索。

   * 將使用主節點類型。

* 如果根本找不到指令碼，則將使用預設指令碼。

   預設轉譯目前支援純文字(.txt)、HTML(.html)和JSON(.json)，所有這些都會列出節點的屬性（適當格式化）。 副檔名。res（或請求副檔名沒有請求副檔名）的預設轉譯，是將資源轉存（如果可能）。
* 對於http錯誤處理（代碼403或404）,Sling會在下列任一處尋找指令碼：

   * [自訂指令碼](/help/sites-developing/customizing-errorhandler-pages.md)的位置/apps/sling/servlet/errorhandler
   * 或標準指令碼/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果多個指令碼套用至指定的請求，則會選取最符合的指令碼。 比賽越具體，越好；換言之，無論任何請求副檔名或方法名稱相符，選擇器與選取器的匹配程度都越高。

例如，考慮請求訪問資源
`/content/corporate/jobs/developer.print.a4.html`
類型
`sling:resourceType="hr/jobs"`

假設我們在正確位置有下列指令碼清單：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

優先順序為(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除了資源類型（主要由`sling:resourceType`屬性定義）外，還有資源super類型。 這通常由`sling:resourceSuperType`屬性指示。 嘗試尋找指令碼時，也會考慮這些超類型。 資源超類型的優勢在於，它們可以形成資源的層次結構，其中預設資源類型`sling/servlet/default`（由預設servlet使用）實際上是根資源。

資源的資源超類型可以用兩種方式定義：

* 按資源的`sling:resourceSuperType`屬性。
* 由`sling:resourceType`指向的節點的`sling:resourceSuperType`屬性。

例如：

* /

   * a
   * b

      * sling:resourceSuperType = a
   * c

      * sling:resourceSuperType = b
   * x

      * sling:resourceType = c
   * y

      * sling:resourceType = c
      * sling:resourceSuperType = a




以下類型的層次結構：

* `/x`
   * 是 `[ c, b, a, <default>]`
* while `/y`
   * 階層為`[ c, a, <default>]`

這是因為`/y`具有`sling:resourceSuperType`屬性，而`/x`沒有，因此其超類型取自其資源類型。

#### Sling Scripts無法直接呼叫{#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接呼叫指令碼，因為這會打破REST伺服器的嚴格概念；你會混合資源和陳述。

如果您直接呼叫表示法（指令碼），就會隱藏指令碼內的資源，因此架構(Sling)不再知道。 因此，您會失去某些功能：

* 自動處理http方法（GET除外），包括：

   * POST、PUT、DELETE，這些處理方式都包含sling預設實作
   * sling:resourceType位置中的`POST.jsp`指令碼

* 您的程式碼架構已不再簡潔，也不再像原本那樣清晰；對於大規模發展至關重要

### Sling API {#sling-api}

這會使用Sling API套件org.apache.sling。&amp;ast；和標籤庫。

### 使用sling:include {#referencing-existing-elements-using-sling-include}參照現有元素

最後考慮的是，需要參考指令碼中的現有元素。

更複雜的指令碼（匯整指令碼）可能需要存取多個資源（例如導覽、側欄、頁尾、清單的元素），並加入&#x200B;*resource*。

若要這麼做，您可以使用sling:include(&quot;/&lt;path>/&lt;resource>&quot;)命令。 這將有效地包括引用資源的定義，如以下語句中引用用於渲染影像的現有定義：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Java動態模組系統）。 OSGi容器可讓您將應用程式分割為個別模組（在OSGi術語中，是包含額外中繼資訊的jar檔案，並稱為bundles），並透過下列功能管理它們之間的跨相依性：

* 容器內實作的服務
* 容器與您的應用程式之間的合約

這些服務和合約提供一種架構，可讓個別元素動態發現彼此以進行協作。

然後，OSGi框架可為您提供這些捆綁包的動態載入／卸載、配置和控制——無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊可在[OSGi網站](https://www.osgi.org)中找到。
>
>尤其是，其「基本教育」頁面包含一系列簡報和教學課程。

此架構可讓您使用應用程式特定模組來擴充Sling。 Sling，因此CQ5使用[Apache Felix](https://felix.apache.org/)實作OSGI（Open Services Gateway計畫），並以OSGi Service Platform Release 4 Version 4.2 Specifications為基礎。 它們都是在OSGi框架內運行的OSGi捆綁包的集合。

這可讓您對安裝中的任何軟體包執行以下操作：

* 安裝
* start
* 停止
* 更新
* 卸載
* 查看當前狀態
* 存取有關特定組合的更多詳細資訊（例如符號名稱、版本、位置等）

如需詳細資訊，請參閱[Web Console](/help/sites-deploying/web-console.md)、[OSGI Configuration](/help/sites-deploying/configuring-osgi.md)和[OSGi Configuration Settings](/help/sites-deploying/osgi-configuration-settings.md)。

## AEM環境中的開發物件{#development-objects-in-the-aem-environment}

以下是對發展感興趣的事項：

**項** 目項目是節點或屬性。

有關控制項對象的詳細資訊，請參閱介面javax.jcr.Item的[Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html)

**Node（及其屬性）** Nodes及其屬性在JCR API 2.0規範(JSR 283)中定義。它們儲存內容、物件定義、轉換指令碼和其他資料。

節點定義內容結構，其屬性儲存實際內容和中繼資料。

內容節點會推動演算。 Sling會從傳入的請求取得內容節點。 此節點的屬性sling:resourceType會指向要使用的Sling轉譯元件。

A node, is a JCR name, also called a resource in the Sling environment.

例如，要獲取當前節點的屬性，可以在指令碼中使用以下代碼：

`PropertyIterator properties = currentNode.getProperties();`

當前節點對象為currentNode。

有關操作節點對象的詳細資訊，請參閱[Javadocs](https://docs.adobe.com/docs/en/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)。

**Widget** 在AEM中，所有使用者輸入都由Widget管理。這些常用於控制內容的編輯。

對話方塊是結合Widget而建立的。

AEM已使用Widget的ExtJS程式庫來開發。

**對** 話方塊是特殊的介面工具集類型。

若要編輯內容，AEM會使用應用程式開發人員所定義的對話方塊。 這些工具組合了一系列Widget，以向使用者呈現編輯相關內容所需的所有欄位和動作。

對話框也用於編輯元資料，並由各種管理工具使用。

**組** 件軟體元件是提供預定義服務或事件的系統元件，能夠與其他元件通信。

在AEM中，元件通常用於轉譯資源的內容。 當資源是頁面時，轉換該資源的元件稱為頂層元件或分頁元件。 但是，元件不需要轉譯內容，也不需要連結至特定資源；例如，導覽元件將顯示多個資源的相關資訊。

元件的定義包括：,

* 用來呈現內容的程式碼
* 對話方塊，供使用者輸入及產生的內容設定。

**范** 本範本範本是特定頁面類型的基礎。在「網站」索引標籤中建立頁面時，使用者必須選取範本。 然後，複製此範本即可建立新頁面。

範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

它定義用於呈現頁面的頁面元件和預設內容（主要頂層內容）。 內容會定義如何呈現為AEM以內容為中心。

**頁面元件（頂層元件）** 用於呈現頁面的元件。

**PageA** 頁面是範本的「例項」。

頁面具有類型cq:Page的階層節點和類型cq:PageContent的內容節點。 內容節點的屬性sling:resourceType會指向用於轉譯頁面的Page Component。

例如，若要取得目前頁面的名稱，您可以在指令碼中使用下列程式碼：

S`tring pageName = currentPage.getName();`

當前頁面物件為currentPage。 有關控制頁面對象的詳細資訊，請參閱[Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/Page.html)。

**頁面** 管理器頁面管理器是提供頁面層級操作方法的「介面」。

例如，要獲取資源的包含頁，您可以在指令碼中使用以下代碼：

Page myPage = pageManager.getContainingPage(myResource);

以pageManager作為頁面管理器對象，myResource作為資源對象。 有關頁面管理器提供的方法的詳細資訊，請參閱[Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html)。

## 資料庫{#structure-within-the-repository}中的結構

以下清單概述了在儲存庫中將看到的結構。

>[!CAUTION]
>
>對此結構或其中的檔案進行更改時應小心謹慎。
>
>在進行開發時，需要進行變更，但您應小心，充分瞭解所做變更的影響。

>[!CAUTION]
>
>您不得變更`/libs`路徑中的任何項目。 對於配置和其他更改，請將項目從`/libs`複製到`/apps`，並在`/apps`中進行任何更改。

* `/apps`

   與申請有關；包含您網站專屬的元件定義。 您開發的元件可以以`/libs/foundation/components`中可用的現成元件為基礎。

* `/content`

   為您的網站建立的內容。

* `/etc`

* `/home`

   使用者和群組資訊。

* `/libs`

   屬於AEM核心的程式庫和定義。 `/libs`中的子資料夾代表現成可用的AEM功能，例如搜尋或複製。 `/libs`中的內容不應加以修改，因為它會影響AEM的運作方式。 您網站的特定功能應在`/apps`下開發（請參閱[自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements)）。

* `/tmp`

   臨時工作區。

* `/var`

   系統更改和更新的檔案；例如審核記錄、統計資料、事件處理。 子資料夾`/var/classes`包含源和編譯表單中已從元件指令碼生成的Java servlet。

## 環境 {#environments}

有了AEM，生產環境通常包含兩種不同的例項類型：an [Author and a Publish instances](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher是Adobe的快取和／或負載平衡工具。 有關詳細資訊，請參閱[ Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/user-guide.html)下。

## FileVault（源修訂版系統）{#filevault-source-revision-system}

FileVault為JCR儲存庫提供檔案系統映射和版本控制。 它可用來管理AEM開發專案，完全支援在標準版控制系統（例如Subversion）中儲存和修訂專案程式碼、內容、設定等。

有關詳細資訊，請參閱[FileVault工具](/help/sites-developing/ht-vlttool.md)文檔。

## 工作流程 {#workflows}

您的內容通常受組織流程的約束，包括許可和由不同參與者簽署等步驟。 這些程式可以表示為在AEM](/help/sites-developing/workflows-models.md)中定義和開發的[工作流程，然後視需要套用至[適當的內容頁面](/help/sites-administering/workflows.md)或[數位資產](/help/assets/assets-workflow.md)。

工作流引擎用於管理工作流及其後續應用程式對內容的實施。

## 多站點管理{#multi-site-management}

Multi Site Manager(MSM)可讓您輕鬆管理多個共用共同內容的網站。 MSM可讓您定義網站之間的關係，讓一個網站的內容變更自動複製到其他網站。

例如，網站通常以多種語言提供給國際觀眾。 當相同語言的網站數量較少（3到5個）時，就可以手動跨網站同步內容。 不過，當網站數量增加或涉及多種語言時，自動化程式就會變得更有效率。

* 有效率地管理網站的不同語言版本。
* 根據來源網站自動更新一或多個網站：

   * 在多個網站上強制執行共同的基本結構，並使用共同內容。
   * 充份運用可用資源。
   * 保持一致的外觀和感覺。
   * 著重管理不同網站的內容。

如需詳細資訊，請參閱[多網站管理員](/help/sites-administering/msm.md)。