---
title: 核AEM心概念
seo-title: The Basics
description: 概述了結構化的核心概AEM念，以及如何在其上開發，包括瞭解JCR 、 Sling 、 OSGi 、 Dispatcher 、工作流和MSM
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

# 核AEM心概念 {#aem-core-concepts}

>[!NOTE]
>
>在深入瞭解核心概念之前AEM,Adobe建議在 [開發AEM Sites](/help/sites-developing/getting-started.md) 概述開發過AEM程和核心概念介紹。

## 開發的先決條件AEM {#prerequisites-for-developing-on-aem}

您需要以下技能才能進行開AEM發：

* Web應用技術的基本知識，包括：

   * 請求 — 響應(XMLHttpRequest / XMLHttpResponse)週期
   * HTML
   * CSS
   * JavaScript

* 體驗伺服器(CRX)的工作知識，包括內容瀏覽器
* 在標準UI中開發，還需要JSP(JavaServer Pages)的基礎知識，包括對簡單JSP實例的理解和修改能力。

還建議您閱讀並遵循 [准則和最佳做法](/help/sites-developing/dev-guidelines-bestpractices.md)。

## Java™內容儲存庫 {#java-content-repository}

Java™內容儲存庫(JCR)標準， [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)，指定一種獨立於供應商和獨立於實施的方法，以在內容儲存庫的粒度級別上雙向訪問內容。

規格線索由Adobe研究（瑞士）公司持有。

的 [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 包， javax.jcr。&amp;ast;用於直接訪問和處理儲存庫內容。

## 體驗伺服器(CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供基於的Experience ServicesAEM，可用於構建自定義應用程式，並嵌入基於Jackrabbit的內容儲存庫。

[阿帕奇·傑克拉比特](https://jackrabbit.apache.org/jcr/index.html) 是JCR API 2.0的開放源，完全符合。

## Sling請求處理 {#sling-request-processing}

### Sling簡介 {#introduction-to-sling}

AEM使用 [吊帶](https://sling.apache.org/index.html)Web應用程式框架，它基於REST原理，提供面向內容的應用程式的輕鬆開發。 Sling使用JCR儲存庫（如Apache Jackrabbit或CRX內容儲存庫）作為AEM其資料儲存。 Sling已經為Apache Software Foundation提供了幫助 — 有關詳細資訊，請參閱Apache。

使用Sling，要呈現的內容類型不是第一個處理考慮。 相反，主要考慮的是URL是否解析為內容對象，然後可以找到指令碼來執行呈現。 這為Web內容作者構建可輕鬆根據其要求定製的頁面提供了極好的支援。

這種靈活性的優點在具有多種不同內容元素的應用程式中，或在您需要可輕鬆定製的頁面時都顯而易見。 特別是，在實施Web內容管理系統（如解決方案中的WCM）時AEM。

請參閱 [在15分鐘內發現Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 和斯林一起發展的第一步。

下圖說明了Sling指令碼解析：它顯示如何從HTTP請求獲取內容節點、從內容節點獲取資源類型、從資源類型獲取指令碼以及哪些指令碼變數可用。

![瞭解Apache Sling指令碼解析](assets/sling-cheatsheet-01.png)

下圖說明了處理SlingPostServlet時可以使用的所有隱藏但功能強大的請求參數。 SlingPostServlet是所有POST請求的預設處理程式，為您提供了無窮盡的選項，用於在儲存庫中建立、修改、刪除、複製和移動節點。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以內容為中心 {#sling-is-content-centric}

吊帶 *以內容為中心*。 這意味著，當每個(HTTP)請求以JCR資源（儲存庫節點）的形式映射到內容時，處理將集中在內容上：

* 第一個目標是保存內容的資源（JCR節點）
* 其次，表示或指令碼是從資源屬性中與請求的某些部分（例如，選擇器和/或擴展）組合而來的

### REST風格吊帶 {#restful-sling}

由於以內容為中心的理念，Sling實現了面向REST的伺服器，因此在Web應用程式框架中具有新的概念。 其優點是：

* 非常REST風格，不僅僅在表面；資源和表示形式在伺服器內正確建模
* 刪除一個或多個資料模型

   * 以前需要以下內容：URL結構、業務對象、資料庫模式；
   * 現在，這一點已縮減為：URL =資源= JCR結構

### URL分解 {#url-decomposition}

在Sling中，處理由用戶請求的URL驅動。 這定義了由相應指令碼顯示的內容。 為此，從URL中提取資訊。

如果分析以下URL:

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

我們可以把它分解成複合部分：

| 協定 | 主機 | 內容路徑 | 選擇器 | 擴展 |  | 尾碼 |  | 參數 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具/間諜 | .printable.a4。 | html | / | a/b | ? | x=12 |

**協定** HTTP

**主機** 網站名稱。

**內容路徑** 指定要呈現的內容的路徑。 與擴展結合使用；在本例中，它們將轉換為tools/spy.html。

**選擇器** 用於繪製內容的替代方法；在本示例中，是A4格式的打印機友好版本。

**擴展** 內容格式；還指定要用於呈現的指令碼。

**尾碼** 可用於指定其他資訊。

**參數** 動態內容所需的任何參數。

#### 從URL到內容和指令碼 {#from-url-to-content-and-scripts}

使用以下原則：

* 映射使用從請求中提取的內容路徑來定位資源
* 當找到適當的資源時，提取sling資源類型，並用於定位用於呈現內容的指令碼

下圖說明了所使用的機制，將在以下各節中詳細討論該機制。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，可指定呈現特定實體的指令碼(通過設定 `sling:resourceType` 屬性)。 此機制提供了比指令碼訪問資料實體（如PHP指令碼中的SQL陳述式所做）更多的自由，因為資源可以具有多個格式副本。

#### 將請求映射到資源 {#mapping-requests-to-resources}

請求被分解並提取必要的資訊。 系統會搜索儲存庫以查找請求的資源（內容節點）:

* 首先，Sling檢查節點是否存在於請求中指定的位置；例如 `../content/corporate/jobs/developer.html`
* 如果找不到節點，則刪除擴展並重複搜索；例如 `../content/corporate/jobs/developer`
* 如果找不到節點，Sling將返回http代碼404（未找到）。

Sling還允許JCR節點以外的其他內容成為資源，但這是一個高級功能。

### 查找指令碼 {#locating-the-script}

找到相應的資源（內容節點）時， **sling資源類型** 的子菜單。 這是路徑，它定位用於呈現內容的指令碼。

由 `sling:resourceType` 可以選擇：

* 絕對值
* 相對於配置參數

   相對路徑是Adobe推薦的，因為它們增加了可移植性。

所有Sling指令碼都儲存在任意一個子資料夾中 `/apps` 或 `/libs`，將按此順序搜索(請參閱 [定制元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

還需注意的幾點是：

* 當需要Method(GET、POST)時，它將按照HTTP規範(例如jobs.POST.esp)的大寫指定（請參閱下文）
* 支援各種指令碼引擎：

   * HTL(HTML模板語言 — Adobe Experience Manager首選和推薦的HTML伺服器端模板系統): `.html`
   * ECMAScript(JavaScript)頁（伺服器端執行）: `.esp, .ecma`
   * Java™伺服器頁（伺服器端執行）: `.jsp`
   * Java™ Servlet編譯器（伺服器端執行）: `.java`
   * JavaScript模板（客戶端執行）: `.jst`

Felix管理控制台上列出了給定實例支援AEM的指令碼引擎清單( `http://<host>:<port>/system/console/slingscripting`)。

此外，Apache Sling支援與其他常用指令碼引擎（例如Groovy、JRuby、Freemarker）的整合，並提供了整合新指令碼引擎的方法。

使用上例，如果 `sling:resourceType` 是 `hr/jobs` 則為：

* GET/HEAD請求和以.html結尾的URL（預設請求類型，預設格式）

   指令碼為/apps/hr/jobs/jobs.esp;sling:resourceType的最後一部分構成檔案名。

* POST請求(除GET/HEAD外的所有請求類型，方法名稱必須為大寫)

   POST在指令碼名中使用。

   指令碼是 `/apps/hr/jobs/jobs.POST.esp`。

* 其他格式的URL，不以.html結尾

   例如 `../content/corporate/jobs/developer.pdf`

   指令碼將 `/apps/hr/jobs/jobs.pdf.esp`;尾碼將添加到指令碼名稱。

* 具有選擇器的URL

   選擇器可用於以替代格式顯示相同的內容。 例如，打印機友好版本、RSS源或摘要。

   如果查看打印機友好版本，選擇器可能位於 *打印*;在 `../content/corporate/jobs/developer.print.html`

   指令碼將 `/apps/hr/jobs/jobs.print.esp`;選擇器將添加到指令碼名稱。

* 如果尚未定義sling:resourceType，則：

   * 內容路徑將用於搜索相應的指令碼（如果基於路徑的ResourceTypeProvider處於活動狀態）。

      例如， `../content/corporate/jobs/developer.html` 會在 `/apps/content/corporate/jobs/`。

   * 將使用主節點類型。

* 如果根本找不到指令碼，則將使用預設指令碼。

   預設格式副本當前支援為純文字檔案(.txt)、HTML(.html)和JSON(.json)，所有格式副本都將列出節點的屬性（適當格式化）。 副檔名.res或沒有請求副檔名的請求的預設格式副本是將資源假離線（如果可能）。
* 對於http錯誤處理（代碼403或404）,Sling將在以下任一位置查找指令碼：

   * 位置/apps/sling/servlet/errorhandler [自定義指令碼](/help/sites-developing/customizing-errorhandler-pages.md)
   * 或標準指令碼/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果多個指令碼應用於給定的請求，則選擇匹配程度最佳的指令碼。 比賽越具體越好，換句話說，無論任何請求副檔名或方法名稱是否匹配，選擇器越匹配越好。

例如，考慮訪問資源的請求
`/content/corporate/jobs/developer.print.a4.html`
類型
`sling:resourceType="hr/jobs"`

假設我們在正確的位置有以下指令碼清單：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

然後優先順序是(8)-(7)-(6)-(5)-(4)-(3)-(2)-(1)。

除資源類型外(主要由 `sling:resourceType` 屬性)也有資源超級類型。 這通常由 `sling:resourceSuperType` 屬性。 在嘗試查找指令碼時，也會考慮這些超類型。 資源超級類型的優點是它們可以形成預設資源類型的資源層次結構 `sling/servlet/default` （由預設servlet使用）是根。

資源的資源超級類型可以用兩種方式定義：

* 的 `sling:resourceSuperType` 資源的屬性。
* 的 `sling:resourceSuperType` 節點的屬性 `sling:resourceType` 點。

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




類型層次結構：

* `/x`
   * 是 `[ c, b, a, <default>]`
* 而 `/y`
   * 層次 `[ c, a, <default>]`

這是因為 `/y` 的 `sling:resourceSuperType` 財產 `/x` 不是，因此其超類型從其資源類型中獲取。

#### 無法直接調用Sling指令碼 {#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接調用指令碼，因為這會打破REST伺服器的嚴格概念；你會把資源和陳述混為一談。

如果直接調用表示法（指令碼），則會在指令碼內隱藏資源，因此框架(Sling)不再知道它。 因此，您會丟失某些功能：

* 自動處理http方法(GET除外)，包括：

   * POST、PUT、DELETE，使用sling預設實現處理
   * 這樣 `POST.jsp` sling:resourceType位置中的指令碼

* 您的代碼體系結構不再像原來那樣乾淨，也不再像原來那樣清晰；對於大規模開發至關重要

### Sling API {#sling-api}

這使用Sling API包org.apache.sling。&amp;ast；和標籤庫。

### 使用sling:include引用現有元素 {#referencing-existing-elements-using-sling-include}

最後考慮的是需要引用指令碼中的現有元素。

更複雜的指令碼（聚合指令碼）可能需要訪問多個資源（例如導航、邊欄、腳注、清單元素），並通過包括 *資源*。

為此，可以使用sling:include(&quot;/&lt;path>/&lt;resource>」)命令。 這將有效地包括引用資源的定義，如以下語句中引用用於呈現影像的現有定義：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## 奧斯吉 {#osgi}

OSGi定義了用於開發和部署模組化應用程式和庫的體系結構（也稱為Java動態模組系統）。 OSGi容器允許您將應用程式拆分為各個模組（是包含附加元資訊的jar檔案，在OSGi術語中稱為捆綁包），並通過以下方式管理它們之間的交叉依賴關係：

* 在容器內實施的服務
* 集裝箱與你的申請之間的合同

這些服務和合同提供了一種使各個元素能夠動態發現彼此以進行協作的體系結構。

然後，OSGi框架將為您提供這些捆綁包的動態載入/卸載、配置和控制 — 無需重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊可在 [OSGi網站](https://www.osgi.org)。
>
>特別是，他們的「基礎教育」頁面包含一系列演示和教程。

此體系結構允許您擴展Sling與應用程式特定模組。 吊具，因此CQ5使用 [阿帕奇費利克斯](https://felix.apache.org/documentation/index.html) OSGI（開放服務網關計畫）的實施，基於OSGi服務平台4版4.2規範。 它們都是OSGi框架內運行的OSGi捆綁包的集合。

這使您能夠對安裝中的任何軟體包執行以下操作：

* 安裝
* 開始
* 停止
* 更新
* 卸載
* 查看當前狀態
* 訪問有關特定捆綁包的詳細資訊（如符號名稱、版本、位置等）

請參閱 [Web控制台](/help/sites-deploying/web-console.md)。 [OSGI配置](/help/sites-deploying/configuring-osgi.md) 和 [OSGi配置設定](/help/sites-deploying/osgi-configuration-settings.md) 的子菜單。

## 環境中的開發對AEM像 {#development-objects-in-the-aem-environment}

以下是對發展感興趣的問題：

**物料** 項是節點或屬性。

有關處理項目對象的詳細資訊，請參閱 [賈瓦多克](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) 介面javax.jcr.Item的

**節點（及其屬性）** 節點及其屬性在JCR API 2.0規範(JSR 283)中定義。 它們儲存內容、對象定義、呈現指令碼和其他資料。

節點定義內容結構，其屬性儲存實際內容和元資料。

內容節點驅動呈現。 Sling從傳入請求獲取內容節點。 此節點的屬性sling:resourceType指向要使用的Sling呈現元件。

節點（即JCR名稱）也稱為Sling環境中的資源。

例如，要獲取當前節點的屬性，可以在指令碼中使用以下代碼：

`PropertyIterator properties = currentNode.getProperties();`

當前Node是當前節點對象。

有關操作節點對象的詳細資訊，請參閱 [賈瓦多克](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html)。

**小部件** 在所AEM有用戶輸入中都由小部件管理。 這些檔案通常用於控制內容的編輯。

對話框通過組合小部件來構建。

已AEM使用ExtJS小部件庫開發。

**對話框** 對話框是特殊類型的小部件。

要編輯內容，請AEM使用應用程式開發人員定義的對話框。 這些元件組合了一系列小部件，以向用戶顯示編輯相關內容所需的所有欄位和操作。

對話框還用於編輯元資料和通過各種管理工具。

**元件** 軟體元件是提供預定義服務或事件的系統元件，並且能夠與其他元件通信。

在組AEM件內，通常用於呈現資源的內容。 當資源是頁面時，呈現該資源的元件稱為「頂級元件」或「分頁元件」。 但是，元件不必呈現內容，也不必連結到特定資源；例如，導航元件將顯示有關多個資源的資訊。

元件的定義包括：

* 用於呈現內容的代碼
* 一個對話框，用於用戶輸入和結果內容的配置。

**模板** 模板是特定類型頁面的基礎。 在「網站」頁籤中建立頁面時，用戶必須選擇模板。 然後，通過複製此模板建立新頁面。

模板是節點的層次結構，其結構與要建立的頁面相同，但沒有任何實際內容。

它定義用於呈現頁面的頁面元件和預設內容（主頂級內容）。 內容定義了如何將其呈現為以AEM內容為中心。

**頁面元件（頂層元件）** 用於呈現頁面的元件。

**頁面** 頁面是模板的「實例」。

頁面具有類型cq:Page的層次節點和類型cq:PageContent的內容節點。 內容節點的屬性sling:resourceType指向用於呈現頁面的頁面元件。

例如，要獲取當前頁的名稱，可以在指令碼中使用以下代碼：

S`tring pageName = currentPage.getName();`

當前頁面對象為currentPage。 有關處理頁面對象的詳細資訊，請參閱 [賈瓦多克](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html)。

**頁面管理器** 頁面管理器是一個介面，它提供頁面級操作的方法。

例如，要獲取資源的包含頁，可以在指令碼中使用以下代碼：

Page myPage = pageManager.getContainingPage(myResource);

將pageManager作為頁面管理器對象，將myResource作為資源對象。 有關頁面管理器提供的方法的詳細資訊，請參閱 [賈瓦多克](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html)。

## 儲存庫內的結構 {#structure-within-the-repository}

以下清單概述了在儲存庫中看到的結構。

>[!CAUTION]
>
>對此結構或其中的檔案進行更改時應謹慎。
>
>在開發時需要進行更改，但您應該注意，您完全瞭解所做任何更改的含義。

>[!CAUTION]
>
>不更改 `/libs` 路徑。 對於配置和其他更改，請從 `/libs` 至 `/apps` 在 `/apps`。

* `/apps`

   與申請相關；包括特定於您網站的元件定義。 開發的元件可基於以下位置提供的現成元件 `/libs/foundation/components`。

* `/content`

   為網站建立的內容。

* `/etc`

* `/home`

   用戶和組資訊。

* `/libs`

   屬於的核心的庫和定AEM義。 中的子資料夾 `/libs` 表示現成功能AEM，如搜索或複製。 中的內容 `/libs` 不應修改，因為它影響工作方AEM式。 您網站的特定功能應在 `/apps` （請參見） [定制元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

* `/tmp`

   臨時工作區。

* `/var`

   系統更改和更新的檔案；如審計日誌、統計、事件處理。

## 環境 {#environments}

生AEM產環境通常由兩種不同類型的實例組成：一個 [作者和發佈實例](/help/sites-deploying/deploy.md#author-and-publish-installs)。

## 調度員 {#the-dispatcher}

Dispatcher是Adobe的工具，用於快取和/或負載平衡。 有關詳細資訊，請參閱 [調度程式](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=zh-Hant)。

## FileVault（源修訂版系統） {#filevault-source-revision-system}

FileVault為JCR儲存庫提供檔案系統映射和版本控制。 它可用於管理開發項AEM目，並完全支援在標準版本控制系統（例如，Subversion）中儲存和版本化項目代碼、內容、配置等。

查看 [FileVault工具](/help/sites-developing/ht-vlttool.md) 文檔。

## 工作流程 {#workflows}

您的內容通常受組織流程的約束，包括由不同參與者批准和註銷等步驟。 這些進程可以表示為工作流， [定義及開發AEM](/help/sites-developing/workflows-models.md)，然後應用於 [適當的內容頁](/help/sites-administering/workflows.md) 或 [數字資產](/help/assets/assets-workflow.md) 按需要。

工作流引擎用於管理工作流及其後續應用程式對您的內容的實施。

## 多站點管理 {#multi-site-management}

多站點管理器(MSM)使您能夠輕鬆管理共用公共內容的多個網站。 MSM允許您定義站點之間的關係，以便在其他站點中自動複製一個站點中的內容更改。

例如，網站通常以多種語言為國際受眾提供。 當使用相同語言的站點數量較少（3到5個）時，可以手動執行跨站點同步內容的過程。 但是，當站點數量增加或涉及多種語言時，自動化該過程將變得更加高效。

* 有效地管理網站的不同語言版本。
* 基於源站點自動更新一個或多個站點：

   * 強制實施通用基礎結構並跨多個站點使用通用內容。
   * 最大限度地利用可用資源。
   * 保持一種共同的外觀和感覺。
   * 將精力集中在管理站點之間不同的內容上。

有關詳細資訊，請參見 [多站點管理器](/help/sites-administering/msm.md)。
