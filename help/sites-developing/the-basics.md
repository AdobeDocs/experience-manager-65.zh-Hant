---
title: AEM核心概念
description: 概述Adobe Experience Manager (AEM)如何建構的核心概念，以及如何在此基礎上開發，包括瞭解JCR、Sling、OSGi、Dispatcher、工作流程和MSM。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
exl-id: f6f32290-422e-4037-89d8-d9f414332e8e
source-git-commit: 3bcdbfc17efe1f4c6069fd97fd6a16ec41d0579e
workflow-type: tm+mt
source-wordcount: '3251'
ht-degree: 0%

---

# AEM核心概念 {#aem-core-concepts}

>[!NOTE]
>
>在開始瞭解Adobe Experience Manager (AEM)的核心概念之前，Adobe建議先完成中的WKND教學課程 [開始開發AEM Sites](/help/sites-developing/getting-started.md) 檔案。 內容包括AEM開發流程概述以及核心概念簡介。

## 在AEM上進行開發的先決條件 {#prerequisites-for-developing-on-aem}

您需要下列技能才能在AEM之上開發：

* 網頁應用程式技術的基本知識，包括：

   * request -response (XMLHttpRequest / XMLHttpResponse)循環
   * HTML
   * CSS
   * JavaScript

* Experience Server (CRX)的工作知識，包括Content Explorer
* 若要使用傳統UI進行開發，您也必須具備JSP (JavaServer Pages)的基本知識，包括瞭解及修改簡單JSP範例的能力。

也建議您閱讀並遵循 [准則與最佳實務](/help/sites-developing/dev-guidelines-bestpractices.md).

## Java™內容存放庫 {#java-content-repository}

Java™ Content Repository (JCR)標準、 [JSR 283](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/index.html)，會指定獨立於廠商和實作，以在內容存放庫內的精細層級上雙向存取內容。

規格領先者為Adobe Research （瑞士） AG。

此 [JCR API 2.0](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/index.html) 套件，javax.jcr。&amp;ast；用於直接存取及操控存放庫內容。

## Experience Server (CRX)和Jackrabbit {#experience-server-crx-and-jackrabbit}

Experience Server提供AEM以Experience Services為基礎、可用來建置自訂應用程式的Experience Services，並根據Jackrabbit嵌入內容存放庫。

[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) 是開放原始碼、完全符合JCR API 2.0的實作。

## Sling請求處理 {#sling-request-processing}

### Sling簡介 {#introduction-to-sling}

AEM建置方式 [Sling](https://sling.apache.org/index.html)，此網頁應用程式架構以REST原則為基礎，可讓您輕鬆開發內容導向的應用程式。 Sling使用JCR存放庫（例如Apache Jackrabbit），或如果有AEM，則使用CRX內容存放庫作為其資料存放區。 Sling已對Apache Software Foundation有所貢獻 — 如需詳細資訊，請參閱Apache 。

使用Sling時，要呈現的內容型別不是第一個處理考量。 主要考量是URL是否解析為內容物件，然後可以找到指令碼以執行轉譯。 這為網頁內容作者提供了絕佳支援，協助他們建立可輕鬆根據需求自訂的頁面。

在包含各種不同內容元素的應用程式中，或是需要可輕鬆自訂的頁面時，這種彈性的優點顯而易見。 特別是在AEM解決方案中實作WCM之類的網頁內容管理系統時。

另請參閱 [15分鐘搞定Sling](https://sling.apache.org/documentation/getting-started/discover-sling-in-15-minutes.html) 開始使用Sling開發。

下圖說明Sling指令碼解析。 它說明如何從HTTP要求取得至內容節點、從內容節點取得至資源型別、從資源型別取得至指令碼，以及有哪些指令碼變數可用。

![瞭解Apache Sling指令碼解析](assets/sling-cheatsheet-01.png)

下圖說明在處理SlingPostServlet時可以使用的所有隱藏但強大的請求引數。 它包含所有POST請求的預設處理常式，為您提供在存放庫中建立、修改、刪除、複製和移動節點的無限選項。

![使用SlingPostServlet](assets/sling-cheatsheet-02.png)

### Sling以內容為中心 {#sling-is-content-centric}

Sling是 *以內容為中心*. 這表示處理著重於內容，因為每個(HTTP)請求都會對應至JCR資源（存放庫節點）形式的內容：

* 第一個目標是儲存內容的資源（JCR節點）
* 第二，表示或指令碼位於與請求某些部分（例如選取器和/或擴充功能）結合的資源屬性中

### RESTful Sling {#restful-sling}

由於以內容為中心的理念，Sling實作了REST導向的伺服器，因此在Web應用程式架構中引入了新概念。 優點包括：

* RESTful，而不只是曲面上的；資源和表示在伺服器內正確建模
* 移除一或多個資料模型

   * 之前需要下列專案：URL結構、業務物件、DB綱要；
   * 現在減少為： URL =資源= JCR結構

### URL分解 {#url-decomposition}

在Sling中，處理是由使用者請求的URL驅動。 這會定義適當的指令碼要顯示的內容。 為此，會從URL擷取資訊。

如果您分析下列URL：

```xml
https://myhost/tools/spy.printable.a4.html/a/b?x=12
```

您可以將它分解成其複合零件：

| 通訊協定 | 主機 | 內容路徑 | 選擇器 | 副檔名 |  | 尾碼 |  | 引數 |
|---|---|---|---|---|---|---|---|---|
| https:// | myhost | 工具/監視 | .printable.a4. | html | / | a/b | ? | x=12 |

**通訊協定** HTTP

**主機** 網站名稱。

**內容路徑** 指定要轉譯之內容的路徑。 用於擴充功能。 在此範例中，它們會轉譯為 `tools/spy.html`.

**選擇器** 用於轉譯內容的替代方法；在此範例中為A4格式的印表機友善版本。

**副檔名** 內容格式；也指定要用於轉譯的指令碼。

**尾碼** 可用來指定其他資訊。

**引數** 動態內容所需的任何引數。

#### 從URL到內容與指令碼 {#from-url-to-content-and-scripts}

使用下列原則：

* 對應會使用從請求中擷取的內容路徑來找出資源
* 找到適當的資源時，就會擷取sling資源型別，並用來找出要用於轉譯內容的指令碼

下圖說明了所使用的機制，以下各節將更詳細地討論該機制。

![chlimage_1-86](assets/chlimage_1-86a.png)

使用Sling，您可以指定哪一個指令碼會轉譯特定實體(透過設定 `sling:resourceType` 屬性)。 此機制比指令碼存取資料實體時的自由度更大（PHP指令碼中的SQL陳述式就是如此），因為資源可以有數個轉譯。

#### 將請求對應至資源 {#mapping-requests-to-resources}

系統會劃分請求並擷取必要資訊。 系統會搜尋存放庫中的請求資源（內容節點）：

* 首先Sling檢查請求中指定的位置是否存在節點；例如， `../content/corporate/jobs/developer.html`
* 如果找不到節點，則會捨棄擴充功能並重複搜尋；例如， `../content/corporate/jobs/developer`
* 如果找不到任何節點，則Sling會傳回http程式碼404 （找不到）。

Sling也可讓JCR節點以外的專案成為資源，但這是進階功能。

### 找到指令碼 {#locating-the-script}

找到適當的資源（內容節點）時， **sling資源型別** 「 」已擷取。 這是路徑，可找出要用於轉譯內容的指令碼。

指定的路徑 `sling:resourceType` 可以是下列其中一項：

* 絕對值
* 相對於設定引數

  由於相對路徑會增加可移植性，因此Adobe會建議使用相對路徑。

所有Sling指令碼都儲存在以下任一個的子資料夾中： `/apps` 或 `/libs`，會依此順序搜尋(請參閱 [自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

其他需要注意的要點包括：

* 當需要方法(GET、POST)時，會根據HTTP規格以大寫指定，例如jobs.POST.esp （請參閱下文）
* 支援各種指令碼引擎：

   * HTL (HTML範本語言 — Adobe Experience Manager偏好並建議的HTML伺服器端範本系統)： `.html`
   * ECMAScript (JavaScript)頁面（伺服器端執行）： `.esp, .ecma`
   * Java™ Server Pages （伺服器端執行）： `.jsp`
   * Java™ Servlet編譯器（伺服器端執行）： `.java`
   * JavaScript範本（使用者端執行）： `.jst`

Felix管理主控台會列出指定AEM執行個體支援的指令碼引擎清單( `http://<host>:<port>/system/console/slingscripting`)。

此外，Apache Sling也支援與其他熱門的指令碼引擎整合（例如Groovy、JRuby、Freemarker），並提供整合新指令碼引擎的方法。

使用上述範例，如果 `sling:resourceType` 是 `hr/jobs` 然後針對：

* GET/HEAD請求和以.html結尾的URL （預設請求型別、預設格式）

  指令碼為/apps/hr/jobs/jobs.esp；sling：resourceType的最後一個區段會形成檔案名稱。

* POST請求(除GET/HEAD以外的所有請求型別，方法名稱必須為大寫)

  POST用於指令碼名稱中。

  指令碼為 `/apps/hr/jobs/jobs.POST.esp`.

* 其他格式的URL，結尾不是.html

  例如 `../content/corporate/jobs/developer.pdf`

  指令碼為 `/apps/hr/jobs/jobs.pdf.esp`；尾碼會新增至指令碼名稱。

* 具有選取器的URL

  選取器可用來以替代格式顯示相同的內容。 例如，適合列印的版本、RSS摘要或摘要。

  如果您檢視適合列印的版本，其中選取器可能是 *列印*，如所示 `../content/corporate/jobs/developer.print.html`

  指令碼為 `/apps/hr/jobs/jobs.print.esp`；選取器會新增至指令碼名稱。

* 如果未定義sling：resourceType，則：

   * 內容路徑可用來搜尋適當的指令碼（如果路徑型ResourceTypeProvider為作用中）。

     例如，的指令碼 `../content/corporate/jobs/developer.html` 會在以下位置產生搜尋： `/apps/content/corporate/jobs/`.

   * 主要節點型別已使用。

* 如果找不到指令碼，則會使用預設指令碼。

  預設轉譯支援純文字(.txt)、HTML(.html)和JSON (.json)格式，所有這些格式都列出節點的屬性（格式適當）。 副檔名為.res或沒有要求副檔名的要求的預設轉譯為儘可能將資源多工緩衝處理。
* 如需http錯誤處理（程式碼403或404），Sling會在以下位置尋找指令碼：

   * /apps/sling/servlet/errorhandler的位置 [自訂指令碼](/help/sites-developing/customizing-errorhandler-pages.md)
   * 或標準指令碼/libs/sling/servlet/errorhandler/403.esp或404.esp的位置。

如果特定請求套用多個指令碼，則會選取最符合的指令碼。 相符專案越具體，越好；換言之，無論是否有任何相符的要求副檔名或方法名稱，選取器越符合越好。

例如，考慮存取資源的請求
`/content/corporate/jobs/developer.print.a4.html`
型別
`sling:resourceType="hr/jobs"`

假設您在正確位置有下列指令碼清單：

1. `GET.esp`
1. `jobs.esp`
1. `html.esp`
1. `print.esp`
1. `print.html.esp`
1. `print/a4.esp`
1. `print/a4/html.esp`
1. `print/a4.html.esp`

偏好設定順序為(8) - (7) - (6) - (5) - (4) - (3) - (2) - (1)。

除了資源型別(主要由 `sling:resourceType` 屬性)，還有資源超級型別。 這由以下指示 `sling:resourceSuperType` 屬性。 嘗試尋找指令碼時，也會考量這些超級型別。 資源超級型別的優點在於，它們可以形成資源階層，其中預設資源型別 `sling/servlet/default` （用於預設servlet）實際上是根。

資源的資源超級型別可透過兩種方式定義：

* 依據 `sling:resourceSuperType` 資源的屬性。
* 依據 `sling:resourceSuperType` 節點屬性，該節點的 `sling:resourceType` 點。

例如：

* /

   * a
   * b

      * sling：resourceSuperType = a

   * c

      * sling：resourceSuperType = b

   * x

      * sling：resourceType = c

   * y

      * sling：resourceType = c
      * sling：resourceSuperType = a

下列專案的型別階層：

* `/x`
   * 是 `[ c, b, a, <default>]`
* 而為 `/y`
   * 階層為 `[ c, a, <default>]`

這是因為 `/y` 具有 `sling:resourceSuperType` 屬性，而 `/x` 不會，因此其超型別會取自其資源型別。

#### 無法直接呼叫Sling指令碼 {#sling-scripts-cannot-be-called-directly}

在Sling中，無法直接呼叫指令碼，因為這會破壞REST伺服器的嚴格概念；您可以混合使用資源和表示法。

如果您直接呼叫表示（指令碼），會在指令碼內隱藏資源，讓框架(Sling)不知道該資源。 因此，您會遺失某些功能：

* 自動處理GET以外的http方法，包括：

   * 以Sling預設實作處理的POST、PUT、DELETE
   * 此 `POST.jsp` sling：resourceType位置中的指令碼

* 您的程式碼架構已不像原來那麼乾淨和結構清晰；這對於大規模開發至關重要

### Sling API {#sling-api}

這會使用Sling API套件org.apache.sling。&amp;ast；和標籤程式庫。

### 使用sling：include參照現有元素 {#referencing-existing-elements-using-sling-include}

最後考量是需要參考指令碼中的現有元素。

更複雜的指令碼（彙總指令碼）必須存取多個資源（例如導覽、側欄、頁尾、清單元素），並透過包含 *resource*.

若要這麼做，請使用sling：include(&quot;/&lt;path>/&lt;resource>「)命令。 這實際上包括參考資源的定義，如以下陳述式所示，該陳述式參考用於轉譯影像的現有定義：

```xml
%><sling:include resourceType="geometrixx/components/image/img"/><%
```

## OSGI {#osgi}

OSGi定義用於開發和部署模組化應用程式和程式庫的架構(也稱為Java™適用的動態模組系統)。 OSGi容器可讓您將應用程式分成個別模組（這些模組是含有其他中繼資訊的jar檔案，在OSGi術語中稱為套裝），並透過以下方式管理它們之間的交叉相依性：

* 在容器內實作的服務
* 容器與應用程式之間的合約

這些服務與合約提供的架構，可讓個別元素動態地互相探索，以便共同作業。

接著OSGi架構會提供這些套裝的動態載入/解除安裝、設定和控制，而不需要重新啟動。

>[!NOTE]
>
>有關OSGi技術的完整資訊，請參閱 [OSGi網站](https://www.osgi.org).
>
>特別值得一提的是，他們的「基礎教育」頁面包含一系列簡報和教學課程。

此架構可讓您使用應用程式特定模組來擴充Sling。 Sling和CQ5使用 [Apache Felix](https://felix.apache.org/documentation/index.html) OSGI （開放式服務閘道計畫）的實作，且以OSGi服務平台第4發行版本4.2規格為基礎。 兩者都是在OSGi架構中執行的OSGi套件組合集合。

這可讓您對安裝內的任何套裝軟體執行下列動作：

* 安裝
* 開始
* 停止
* 更新
* 解除安裝
* 檢視狀態
* 存取有關特定套裝的更詳細資訊（例如符號名稱、版本和位置）

另請參閱 [網頁主控台](/help/sites-deploying/web-console.md)， [OSGI設定](/help/sites-deploying/configuring-osgi.md)、和 [OSGi組態設定](/help/sites-deploying/osgi-configuration-settings.md) 以取得詳細資訊。

## AEM環境中的開發物件 {#development-objects-in-the-aem-environment}

下列專案符合開發需求：

**專案** 專案是節點或屬性。

如需有關操作Item物件的詳細資訊，請參閱 [Java™檔案](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html) 介面javax.jcr.Item的

**節點（及其屬性）** 節點及其屬性在JCR API 2.0規格(JSR 283)中定義。 它們儲存內容、物件定義、演算指令碼和其他資料。

節點會定義內容結構，其屬性會儲存實際內容和中繼資料。

內容節點會驅動轉譯。 Sling從傳入要求取得內容節點。 此節點的屬性sling：resourceType指向要使用的Sling演算元件。

在Sling環境中，JCR名稱節點也稱為資源。

例如，若要取得目前節點的屬性，您可以在指令碼中使用下列程式碼：

`PropertyIterator properties = currentNode.getProperties();`

currentNode是目前的節點物件。

如需有關操作Node物件的詳細資訊，請參閱 [Java™檔案](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html).

**Widget** 在AEM中，所有使用者輸入均由Widget管理。 這些通常用於控制內容的編輯。

對話方塊是藉由組合Widget所建置。

AEM是使用Widget的ExtJS資料庫開發的。

**對話方塊** 對話方塊是一種特殊型別的Widget。

若要編輯內容，AEM會使用應用程式開發人員定義的對話方塊。 這些功能結合一系列的Widget，向使用者呈現編輯相關內容所需的所有欄位和動作。

對話方塊也用於編輯中繼資料，以及各種管理工具。

**元件** 軟體元件是一種系統元素，提供預先定義的服務或事件，並能與其他元件通訊。

在AEM中，元件通常用於呈現資源的內容。 當資源為頁面時，轉譯該資源的元件稱為頂層元件或頁面元件。 不過，元件不需要呈現內容，也不需要連結至特定資源。 例如，導覽元件會顯示多個資源的相關資訊。

元件的定義包括下列各項：

* 用於呈現內容的程式碼
* 用於使用者輸入和結果內容配置的對話方塊。

**範本** 範本是特定頁面型別的基礎。 在網站標籤中建立頁面時，使用者必須選取範本。 然後複製此範本以建立新頁面。

範本是節點的階層，其結構與要建立的頁面相同，但沒有任何實際內容。

它會定義用於呈現頁面的頁面元件和預設內容（主要頂層內容）。 內容會定義其呈現方式，因為AEM是以內容為中心。

**頁面元件（最上層元件）** 要用來呈現頁面的元件。

**頁面** 頁面是範本的「例項」。

頁面具有cq：Page型別的階層節點和cq：PageContent型別的內容節點。 內容節點的屬性sling：resourceType指向用於轉譯頁面的頁面元件。

例如，若要取得目前頁面的名稱，您可以在指令碼中使用下列程式碼：

S`tring pageName = currentPage.getName();`

TcurrentPage為目前頁面物件。 如需有關操控頁面物件的詳細資訊，請參閱 [Java™檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/Page.html).

**頁面管理員** 頁面管理員是提供頁面層級作業方法的介面。

例如，若要取得資源的容納頁面，您可以在指令碼中使用下列程式碼：

頁面myPage = pageManager.getContainingPage(myResource)；

pageManager是頁面管理員物件，myResource是資源物件。 如需頁面管理員所提供方法的詳細資訊，請參閱 [Java™檔案](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/PageManager.html).

## 存放庫內的結構 {#structure-within-the-repository}

下列清單提供您在存放庫中看到的結構概覽。

>[!CAUTION]
>
>變更此結構或其中的檔案時，應務必謹慎。
>
>開發時需要變更，但應確保完全瞭解所做任何變更的影響。

>[!CAUTION]
>
>請勿變更中的任何專案 `/libs` 路徑。 如需設定及其他變更，請從複製專案 `/libs` 至 `/apps` 並在中進行任何變更 `/apps`.

* `/apps`

  與應用程式相關；包含您網站專用的元件定義。 您開發的元件可以依據以下位置提供的現成可用元件： `/libs/foundation/components`.

* `/content`

  為您的網站建立的內容。

* `/etc`

* `/home`

  使用者和群組資訊。

* `/libs`

  屬於AEM核心的程式庫和定義。 中的子資料夾 `/libs` 代表現成可用的AEM功能，例如搜尋或復寫。 中的內容 `/libs` 不應修改，因為它會影響AEM的運作方式。 您網站的特定功能應開發於 `/apps` (請參閱 [自訂元件和其他元素](/help/sites-developing/dev-guidelines-bestpractices.md#customizing-components-and-other-elements))。

* `/tmp`

  臨時工作區。

* `/var`

  變更並由系統更新的檔案；例如稽核記錄、統計資料、事件處理。

## 環境 {#environments}

使用AEM時，生產環境通常包含兩種不同型別的執行個體： [製作和發佈執行個體](/help/sites-deploying/deploy.md#author-and-publish-installs).

## 排程程式 {#the-dispatcher}

Dispatcher是Adobe的快取和/或負載平衡工具。 如需詳細資訊，請參閱 [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html).

## FileVault （來源修訂系統） {#filevault-source-revision-system}

FileVault為您的JCR存放庫提供檔案系統對應和版本控制。 透過對標準版本控制系統（例如Subversion）中專案計畫碼、內容、設定等的儲存和版本化提供完整支援，可用於管理AEM開發專案。

請參閱 [FileVault工具](/help/sites-developing/ht-vlttool.md) 詳細資訊的檔案。

## 工作流程 {#workflows}

您的內容通常受限於組織流程，包括各種參與者的核准和簽署等步驟。 這些程式可以表示為工作流程， [在AEM中定義和開發](/help/sites-developing/workflows-models.md)，然後套用至 [適當的內容頁面](/help/sites-administering/workflows.md) 或 [數位資產](/help/assets/assets-workflow.md) 視需要。

工作流程引擎是用來管理工作流程的實作，及其後續對您內容的應用程式。

## 多網站管理 {#multi-site-management}

多網站管理員(MSM)可讓您輕鬆管理共用相同內容的多個網站。 MSM可讓您定義網站之間的關係，如此一來，一個網站中的內容變更便會自動複製到其他網站。

例如，網站通常以多種語言提供給國際受眾。 若使用相同語言的網站數量偏低（三至五），則採用手動程式來同步跨網站的內容。 然而，當網站數量增加或涉及多種語言時，自動化程式會變得更有效率。

* 有效管理網站的不同語言版本。
* 根據來源網站自動更新一或多個網站：

   * 強制實施通用基礎結構，並在多個網站間使用通用內容。
   * 最大限度地利用可用資源。
   * 維持共同的外觀與風格。
   * 集中管理網站之間不同的內容。

如需詳細資訊，請參閱 [多站點管理員](/help/sites-administering/msm.md).
