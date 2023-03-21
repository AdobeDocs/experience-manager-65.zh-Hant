---
title: AEM核心概念
seo-title: The Basics
description: 概略說明AEM的結構化方式及如何在其上開發的核心概念，包括了解JCR、Sling、OSGi、Dispatcher、工作流程和MSM
seo-description: An overview of the core concepts of how AEM is structured and how to develop on top of it including understanding the JCR, Sling, OSGi, the dispatcher, workflows, and MSM
uuid: e49f29db-a5d6-48a0-af32-f8785156746e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 6e913190-be92-4862-a8b9-517f8bde0044
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '3324'
ht-degree: 1%

---

# AEM核心概念 {#aem-core-concepts}

>[!NOTE]
>
>在深入探討AEM的核心概念之前，Adobe建議您先完成 [開始開發AEM Sites](/help/sites-developing/getting-started.md) 檔案以概略了解AEM開發流程，並介紹核心概念。

## 在AEM上開發的必要條件 {#prerequisites-for-developing-on-aem}

若要在AEM上開發，您需要下列技能：

* Web應用技術的基本知識，包括：

   * 要求 — 回應(XMLHttpRequest / XMLHttpResponse)週期
   * HTML
   * CSS
   * JavaScript

* Experience Server(CRX)的使用知識，包括內容總管
* 在傳統UI中開發時，還需要JSP(JavaServer Pages)的基本知識，包括了解和修改簡單JSP示例的能力。

此外，建議您閱讀並遵循 [准則和最佳實務](/help/sites-developing/dev-guidelines-bestpractices.md).

## Java™內容儲存庫 {#java-content-repository}

Java™ Content Repository(JCR)標準， [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)，指定一種獨立於供應商且獨立於實施的方式，以在內容儲存庫的精細級別上雙向訪問內容。

Adobe研究（瑞士）AG持有規格領頭。

此 [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 包， javax.jcr。&amp;ast;用於直接存取和操控存放庫內容。

## Experience Server(CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供AEM建置的Experience Services，可用來建置自訂應用程式，並內嵌於Jackrabbit的內容存放庫。

[阿帕奇·傑克拉布特](https://jackrabbit.apache.org/jcr/index.html) 是JCR API 2.0的開放原始碼，完全符合。

## Sling要求處理 {#sling-request-processing}

### Sling簡介 {#introduction-to-sling}

AEM是使用 [Sling](https://sling.apache.org/index.html)，此Web應用程式框架基於REST原則，可輕鬆開發麵向內容的應用程式。 Sling會使用JCR存放庫，例如Apache Jackrabbit，或(在AEM的例子中)CRX Content Repository，做為其資料存放區。 Sling已對Apache Software Foundation作出貢獻 — 如需詳細資訊，請參閱Apache。

使用Sling時，要轉譯的內容類型不是第一個處理考量。 相反，主要考量是URL是否解析至內容物件，接著便找到指令碼來執行轉譯。 這為網頁內容作者提供絕佳的支援，以建立可輕鬆根據其需求自訂的頁面。

在具有廣泛不同內容元素的應用程式中，或當您需要可輕鬆自訂的頁面時，這種靈活性的優勢就顯而易見。 尤其是在AEM解決方案中實作網頁內容管理系統（例如WCM）時。

請參閱 [15分鐘後探索Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 以了解使用Sling開發的前幾個步驟。

下圖說明Sling指令碼解析度：它會顯示如何從HTTP請求到內容節點、從內容節點到資源類型、從資源類型到指令碼，以及哪些指令碼變數可用。

![了解Apache Sling指令碼解析度](assets/sling-cheatsheet-01.png)

下圖說明處理SlingPostServlet時可使用的所有隱藏但功能強大的請求參數，SlingPostServlet是所有POST請求的預設處理程式，為您提供建立、修改、刪除、複製和移動儲存庫中節點的無數選項。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以內容為中心 {#sling-is-content-centric}

Sling是 *以內容為中心*. 這表示處理作業會聚焦在內容上，因為每個(HTTP)請求會以JCR資源（存放庫節點）的形式對應至內容：

* 第一個目標是保存內容的資源（JCR節點）
* 其次，表示法或指令碼是從與請求的某些部分（例如選取器和/或擴充功能）結合的資源屬性中找到

### RESTful Sling {#restful-sling}

由於以內容為中心的理念，Sling實作了REST導向的伺服器，因此在Web應用程式架構中提供新概念。 優點如下：

* 非常RESTful，而不只是表面；資源和表示在伺服器內正確建模
* 刪除一個或多個資料模型

   * 之前需要下列項目：URL結構、業務對象、資料庫架構；
   * 現在已簡化為：URL =資源= JCR結構

### URL分解 {#url-decomposition}

在Sling中，處理是由使用者要求的URL驅動。 這會定義要由適當指令碼顯示的內容。 為此，會從URL中擷取資訊。

如果我們分析下列URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 | 內容路徑 | 選取器 | 擴充功能 |  | 尾碼 |  | 參數 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具/間諜 | .printable.a4。 | html | / | a/b | ? | x=12 |

**協定** HTTP

**主機** 網站名稱。

**內容路徑** 指定要呈現的內容的路徑。 與擴充功能搭配使用；在此範例中，它們會轉譯為tools/spy.html。

**選取器** 用於轉譯內容的替代方法；在此示例中，為A4格式的打印機友好版本。

**擴充功能** 內容格式；也指定用於呈現的指令碼。

**尾碼** 可用來指定其他資訊。

**參數** 動態內容所需的任何參數。

#### 從URL到內容和指令碼 {#from-url-to-content-and-scripts}

使用下列原則：

* 對應使用從請求中擷取的內容路徑來尋找資源
* 找到適當的資源時，會擷取sling資源類型，並用來找出要用於轉譯內容的指令碼

下圖說明所使用的機制，將在以下各節中詳細討論。

![chlimage_1-86](assets/chlimage_1-86a.png)

透過Sling，您可以指定哪個指令碼會轉譯特定實體(透過設定 `sling:resourceType` 屬性)。 此機制提供的自由比指令碼訪問資料實體（PHP指令碼中的SQL陳述式會這樣做）的自由多，因為資源可以有多個格式副本。

#### 將請求對應至資源 {#mapping-requests-to-resources}

會劃分要求並擷取必要資訊。 系統會搜索所請求的資源（內容節點）:

* first Sling會檢查節點是否存在於要求中指定的位置；例如 `../content/corporate/jobs/developer.html`
* 如果未找到節點，則刪除擴展並重複搜索；例如 `../content/corporate/jobs/developer`
* 如果找不到節點，Sling會傳回http程式碼404（找不到）。

Sling也允許JCR節點以外的其他項目成為資源，但這是進階功能。

### 找到指令碼 {#locating-the-script}

找到適當的資源（內容節點）時， **sling資源類型** 會擷取。 這是路徑，可找出要用於轉譯內容的指令碼。

由 `sling:resourceType` 可以是：

* 絕對值
* 相對，至配置參數

   相對路徑因可移植性提高而建議由Adobe使用。

所有Sling指令碼都儲存在其中一個的子資料夾中 `/apps` 或 `/libs`，會依此順序搜尋(請參閱 [自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

其他注意事項包括：

* 當需要方法(GET、POST)時，將根據HTTP規範(如jobs.POST.esp)以大寫形式指定（請參見下面）
* 支援各種指令碼引擎：

   * HTL(HTML範本語言 — Adobe Experience Manager偏好且建議的HTML伺服器端範本系統): `.html`
   * ECMAScript(JavaScript)頁面（伺服器端執行）: `.esp, .ecma`
   * Java™伺服器頁（伺服器端執行）: `.jsp`
   * Java™ Servlet編譯器（伺服器端執行）: `.java`
   * JavaScript範本（用戶端執行）: `.jst`

指定AEM例項支援的指令碼引擎清單會列在Felix Management Console( `http://<host>:<port>/system/console/slingscripting`)。

此外，Apache Sling支援與其他常用指令碼引擎（例如Groovy、JRuby、Freemarker）整合，並提供整合新指令碼引擎的方法。

使用上述範例，若 `sling:resourceType` is `hr/jobs` 然後針對：

* GET/HEAD要求，以及結尾為.html的URL（預設請求類型、預設格式）

   劇本是/apps/hr/jobs/jobs.esp;sling:resourceType的最後一節會形成檔案名稱。

* POST請求(所有請求類型，除GET/HEAD外，方法名稱必須為大寫)

   POST用於指令碼名稱中。

   指令碼是 `/apps/hr/jobs/jobs.POST.esp`.

* 其他格式的URL，不會以.html結尾

   例如, `../content/corporate/jobs/developer.pdf`

   指令碼將是 `/apps/hr/jobs/jobs.pdf.esp`;尾碼會新增至指令碼名稱。

* 具有選取器的URL

   選取器可用來以替代格式顯示相同的內容。 例如，打印機友好版本、RSS源或摘要。

   如果查看打印機友好版本，選擇器可能是 *打印*;和 `../content/corporate/jobs/developer.print.html`

   指令碼將是 `/apps/hr/jobs/jobs.print.esp`;選取器會新增至指令碼名稱。

* 如果未定義sling:resourceType，則：

   * 內容路徑將用於搜索適當的指令碼（如果基於路徑的ResourceTypeProvider處於活動狀態）。

      例如， `../content/corporate/jobs/developer.html` 會在 `/apps/content/corporate/jobs/`.

   * 將使用主節點類型。

* 如果完全找不到指令碼，則將使用預設指令碼。

   預設轉譯目前支援為純文字(.txt)、HTML(.html)和JSON(.json)，所有這些都會列出節點的屬性（適當的格式）。 副檔名.res或不含請求副檔名的請求的預設轉譯，是將資源轉存（如果可能）。
* 若是http錯誤處理（程式碼403或404）,Sling會在下列任一位置尋找指令碼：

   * 用於的位置/apps/sling/servlet/errorhandler [自訂指令碼](/help/sites-developing/customizing-errorhandler-pages.md)
   * 或標準指令碼/libs/sling/servlet/errorhandler/403.esp的位置，或分別是404.esp。

如果指定請求套用多個指令碼，則會選取最符合的指令碼。 比賽越具體，越好；換言之，無論任何請求擴充功能或方法名稱相符，選取器符合的越多越好。

例如，請考慮存取資源的請求
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

除資源類型外(主要由 `sling:resourceType` 屬性)也包含資源super類型。 這通常由 `sling:resourceSuperType` 屬性。 嘗試尋找指令碼時，也會考量這些超類型。 資源超類型的優勢在於，它們可能形成預設資源類型的資源層次結構 `sling/servlet/default` （由預設servlet使用）有效地是根。

資源的資源超類型可以用兩種方式定義：

* 按 `sling:resourceSuperType` 資源的屬性。
* 按 `sling:resourceSuperType` 其屬性 `sling:resourceType` 點。

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




類型階層：

* `/x`
   * 是 `[ c, b, a, <default>]`
* 而 `/y`
   * 階層為 `[ c, a, <default>]`

這是因為 `/y` 有 `sling:resourceSuperType` 屬性， `/x` 不會，因此會從其資源類型中取用其超類型。

#### 無法直接呼叫Sling指令碼 {#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接呼叫指令碼，因為這會打破REST伺服器的嚴格概念；你會混合資源和陳述。

如果您直接呼叫表示法（指令碼），會隱藏指令碼內的資源，讓架構(Sling)不再知道。 因此，您會失去某些功能：

* 自動處理GET以外的http方法，包括：

   * POST、PUT、DELETE，使用sling預設實作處理
   * the `POST.jsp` sling:resourceType位置中的指令碼

* 您的程式碼架構已不再像原來那樣簡潔，也不再像原來那樣清晰；對大規模發展至關重要

### Sling API {#sling-api}

這會使用Sling API套件org.apache.sling。&amp;ast；和標籤庫。

### 使用sling:include參考現有元素 {#referencing-existing-elements-using-sling-include}

最後考量是必須參考指令碼內的現有元素。

更複雜的指令碼（匯總指令碼）可能需要存取多個資源（例如導覽、側欄、頁尾、清單的元素），並加入 *資源*.

若要這麼做，您可以使用sling:include(&quot;/&lt;path>/&lt;resource>&quot;)命令。 這將有效地包括所引用資源的定義，如下列語句中所示，該語句引用用於呈現影像的現有定義：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Dynamic Module System for Java）。 OSGi容器可讓您將應用程式分成個別模組（是含有其他中繼資訊的jar檔案，在OSGi術語中稱為套件組合），並透過以下功能管理應用程式之間的交叉相依性：

* 在容器內實作的服務
* 集裝箱和申請書之間的合同

這些服務和合同提供了一個體系結構，它使各個元素能夠動態地發現彼此以進行協作。

然後，OSGi框架將為您提供這些套件組合的動態載入/卸載、配置和控制 — 無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊，請參閱 [OSGi網站](https://www.osgi.org).
>
>其「基礎教育」頁面尤其包含一系列簡報和教學課程。

此架構可讓您使用應用程式特定模組來擴充Sling。 Sling會使用 [阿帕奇費利克斯](https://felix.apache.org/documentation/index.html) OSGI（開放服務閘道計畫）的實作以OSGi服務平台第4版4.2版規格為基礎。 它們都是在OSGi架構內執行的OSGi套件組合集合。

這可讓您對安裝中的任何套件執行下列動作：

* 安裝
* 開始
* 停止
* 更新
* 解除安裝
* 查看當前狀態
* 存取有關特定套件組合的詳細資訊（例如符號名稱、版本、位置等）

請參閱 [Web主控台](/help/sites-deploying/web-console.md), [OSGI設定](/help/sites-deploying/configuring-osgi.md) 和 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md) 以取得更多資訊。

## AEM環境中的開發物件 {#development-objects-in-the-aem-environment}

以下是對發展感興趣的事項：

**項目** 項目是節點或屬性。

有關操作項目對象的詳細資訊，請參閱 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) 介面javax.jcr.Item的

**節點（及其屬性）** 節點及其屬性在JCR API 2.0規範(JSR 283)中定義。 它們儲存內容、物件定義、轉譯指令碼和其他資料。

節點定義內容結構，其屬性會儲存實際內容和中繼資料。

內容節點會推動轉譯。 Sling會從傳入的請求中取得內容節點。 此節點的屬性sling:resourceType指向要使用的Sling轉譯元件。

節點（即JCR名稱）在Sling環境中也稱為資源。

例如，若要取得目前節點的屬性，您可以在指令碼中使用下列程式碼：

`PropertyIterator properties = currentNode.getProperties();`

當前節點對象為currentNode。

有關操作節點對象的詳細資訊，請參閱 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**介面工具集** 在AEM中，所有使用者輸入由Widget管理。 這些檔案通常用於控制內容片段的編輯。

對話框是通過組合Widget而構建的。

AEM已使用Widget的ExtJS程式庫開發。

**對話方塊** 對話方塊是特殊類型的Widget。

若要編輯內容，AEM會使用應用程式開發人員定義的對話方塊。 這些組合了一系列小部件，用於向用戶呈現編輯相關內容所需的所有欄位和操作。

對話方塊也用於編輯中繼資料，以及供各種管理工具使用。

**元件** 軟體元件是提供預定義服務或事件的系統元素，並且能夠與其他元件通信。

在AEM內，元件通常用於轉譯資源的內容。 當資源為頁面時，呈現該資源的元件稱為頂級元件或Pagecomponent。 不過，元件不必轉譯內容，也不必連結至特定資源；例如，導覽元件將顯示有關多個資源的資訊。

元件的定義包括：

* 用於呈現內容的代碼
* 對話方塊，供使用者輸入，並設定產生的內容。

**範本** 範本是特定類型頁面的基礎。 在「網站」索引標籤中建立頁面時，使用者必須選取範本。 然後複製此範本即可建立新頁面。

範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

它定義用於呈現頁面的頁面元件和預設內容（主要頂層內容）。 內容會定義其轉譯為AEM的方式，以內容為中心。

**頁面元件（頂層元件）** 用於呈現頁面的元件。

**頁面** 頁面是範本的「例項」。

頁面具有cq:Page類型的階層節點和cq:PageContent類型的內容節點。 內容節點的屬性sling:resourceType指向用於轉譯頁面的頁面元件。

例如，若要取得目前頁面的名稱，您可以在指令碼中使用下列程式碼：

S`tring pageName = currentPage.getName();`

將currentPage作為當前頁對象。 有關操控頁面對象的詳細資訊，請參閱 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**頁面管理員** 頁面管理器是一個介面，提供頁面層級操作的方法。

例如，若要取得資源的容納頁面，您可以在指令碼中使用下列程式碼：

頁面myPage = pageManager.getContainingPage(myResource);

將pageManager作為頁面管理器物件，將myResource作為資源物件。 如需頁面管理員所提供方法的詳細資訊，請參閱 [Javadocs](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## 存放庫內的結構 {#structure-within-the-repository}

下列清單提供您在存放庫中所看到結構的概述。

>[!CAUTION]
>
>應謹慎變更此結構或其內的檔案。
>
>進行開發時需要進行變更，但您應謹慎了解所進行任何變更的影響。

>[!CAUTION]
>
>請勿變更 `/libs` 路徑。 對於配置和其他更改，請從 `/libs` to `/apps` 在 `/apps`.

* `/apps`

   與申請有關；包含您網站專屬的元件定義。 您開發的元件可以根據以下提供的現成元件： `/libs/foundation/components`.

* `/content`

   為您的網站建立的內容。

* `/etc`

* `/home`

   使用者和群組資訊。

* `/libs`

   屬於AEM核心的程式庫和定義。 中的子資料夾 `/libs` 代表現成可用的AEM功能，例如搜尋或復寫。 中的內容 `/libs` 不應加以修改，因為它會影響AEM的運作方式。 您網站的特定功能應在 `/apps` (請參閱 [自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

* `/tmp`

   臨時工作區。

* `/var`

   系統更改和更新的檔案；例如審核日誌、統計資訊、事件處理。

## 環境 {#environments}

透過AEM，生產環境通常包含兩種不同的例項類型：an [製作和發佈例項](/help/sites-deploying/deploy.md#author-and-publish-installs).

## Dispatcher {#the-dispatcher}

Dispatcher是Adobe的快取和/或負載平衡工具。 如需詳細資訊，請參閱 [dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant).

## FileVault（源修訂系統） {#filevault-source-revision-system}

FileVault為JCR儲存庫提供檔案系統映射和版本控制。 它可用於管理AEM開發項目，在標準版本控制系統（例如Subversion）中完全支援儲存和版本化項目代碼、內容、配置等。

請參閱 [FileVault工具](/help/sites-developing/ht-vlttool.md) 檔案以取得詳細資訊。

## 工作流程 {#workflows}

您的內容通常受組織流程的約束，包括許可和由不同參與者簽核等步驟。 這些程式可以表示為工作流程， [在AEM中定義和開發](/help/sites-developing/workflows-models.md)，然後套用至 [適當的內容頁面](/help/sites-administering/workflows.md) 或 [數位資產](/help/assets/assets-workflow.md) 視需要。

工作流程引擎可用來管理工作流程的實施，以及其後續對內容的應用程式。

## 多網站管理 {#multi-site-management}

Multi Site Manager(MSM)可讓您輕鬆管理多個共用相同內容的網站。 MSM可讓您定義網站之間的關係，以便一個網站中的內容變更會自動複製到其他網站。

例如，網站通常以多種語言提供給國際受眾。 當使用相同語言的網站數量較少時（3到5個），便可執行手動程式，跨網站同步內容。 不過，當網站數量增加或涉及多種語言時，自動化程式會變得更有效率。

* 有效管理網站的不同語言版本。
* 根據源站點自動更新一個或多個站點：

   * 強制執行通用基礎結構，並跨多個網站使用通用內容。
   * 最大限度地利用可用資源。
   * 保持共同的外觀和感覺。
   * 著重於管理不同網站的內容。

如需詳細資訊，請參閱 [多網站管理員](/help/sites-administering/msm.md).
