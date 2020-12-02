---
title: AEM Communities概觀
seo-title: AEM Communities概觀
description: AEM Communities功能與設定概觀
seo-description: AEM Communities功能與設定概觀
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 4533fa42fa3fa9f157d5ca8fee1251005b1d587e
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---


# AEM Communities概觀{#aem-communities-overview}

Adobe Experience Manager(AEM)Communities提供快速建立內部部署社群網站的功能，可改善效能、改善網站管理，並鼓勵網站訪客轉換為有價值的社群成員。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## 社群功能{#communities-features}

AEM Communities可讓您與網站訪客建立關係，其中：

* **透** 過部落格、問答和活動日曆，
* 而&#x200B;**透過論壇、留言和其他社群內容獲得見解**，通常稱為使用者產生的內容(UGC)。
* 它允許發佈環境中受信任的成員&#x200B;**協調**,
* **社交** 登入Twitter和Facebook,
* **內嵌** 翻譯社群內容、
* **社群群群** 組從已發佈的社群網站建立，
* **** 獎章，
* **檔案共用**,
* **通** 知和 **活動流**,
* 允許&#x200B;**標籤**（@提及）用戶生成內容中其他已註冊成員，以引起他們的注意。
* 支援啟用元件（例如目錄和課程播放、作業、檔案庫）上的&#x200B;**鍵盤導覽**。

使用GitHub.com公開提供的[AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)或與新的We.Retail參考實作搭配使用，可展示社群功能。

## 社群網站 {#community-sites}

社群網站是使用簡單精靈建立的AEM網站，可產生網站，其中包含許多預先連線至網站的常用功能。

[站點建立嚮導](/help/communities/sites-console.md) :

* 根據選定的[社區站點模板](/help/communities/sites.md)組合站點的功能，即：

   * 由[社區函式](#community-functions)構建
   * 可選[社區組](#communitygroups)功能

* 使用設定來設定：

   * 協調
   * 登錄
   * 轉換

* 提供基本功能：

   * 自適應設計：使用[Twitter引導主題](https://getbootstrap.com)

   * 登入：自我註冊， [社交登入](/help/communities/social-login.md)，使用者設定檔

      * 通知：
成員會看到與其相關的事件，而使用者產生的內容則位於[@intected](/help/communities/overview.md#mentionssupport)的位置。

      * 訊息：成員可以在社區站點內發送或接收消息。
      * 搜尋：能夠在社群網站中搜尋。
      * 語言切換：能夠為[多語言站點](/help/sites-administering/translation.md)選擇語言。

      * 管理：存取權，讓授權成員協調和管理社群網站中的使用者。

* 免除許多頁面層級的製作步驟：

   * 品牌：可選上傳橫幅影像，以顯示在社群網站的所有頁面上
   * 導覽功能表：為社群網站範本所包含的功能提供導覽連結。

若要體驗快速建立新社群網站的便利性，請造訪[AEM Communities](/help/communities/getting-started.md)快速入門。

## 社群內容永續性{#community-content-persistence}

為改善社群內容的效能與同步化，AEM Communities需要專為所有AEM（作者和發佈）例項之間共用的使用者產生內容(UGC)而設定的公用儲存。

社區內容可通過儲存資源提供器(SRP)輕鬆訪問，該提供器提供一個層，用於將訪問與底層拓撲分開，並支援UGC的公共儲存。

若要進一步瞭解社群內容永續性和建議的部署，請參閱：

* [社群內容儲存](/help/communities/working-with-srp.md)，討論UGC的可用SRP儲存選項。
* [推薦的拓撲](/help/communities/topologies.md)，它根據使用案例和SRP選擇討論拓撲。
* [升級至AEM 6.5 Communities](/help/communities/upgrade.md)，當您移至AEM 6.5時，這可提供有關UGC的有用資訊。

## Communities Console {#communities-consoles}

在作者環境中，全域導覽主控台提供對[Communities主控台](/help/communities/consoles.md)的存取，其中包含：

* [Sitesconsole](/help/communities/sites-console.md) 

   * 網站建立
   * 網站編輯
   * 網站管理
   * [社群群群組](/help/communities/groups.md) 主控台

* [協調控](/help/communities/moderation.md) 制台

   * 作者和發佈環境的常見大量協調UI。
   * 新的篩選條件。

* [成員和組管](/help/communities/members.md) 理控制台

   * 提供從作者環境建立和管理發布端使用者（成員）的能力。
   * 提供禁止成員的能力。
   * 提供從作者環境建立和管理發布端使用者群組（成員群組）的能力。

* [Reportsconsole(報](/help/communities/reports.md) 告控制台)

   * 提供產生指派、貼文和檢視報告的能力。

* [資源](/help/communities/resources.md) 控制台

   * 提供建立啟用資源和學習路徑的能力。
   * 提供對啟用資源和學習路徑報告的存取。

全域工具主控台可存取下列社群工具：

* [網站範本控](/help/communities/tools.md#sitetemplatesconsole) 制台

   * 建立和管理社群網站範本。

* [群組範本控](/help/communities/tools.md#grouptemplatesconsole) 制台

   * 建立和管理社群群組範本。

* [社群功能](/help/communities/tools.md#communityfunctionsconsole) 主控台

   * 建立和管理社群功能。

* [儲存配置](/help/communities/tools.md#storageconfiguratonconsole) 控制台

   * 選擇並配置站點的[公共儲存](/help/communities/working-with-srp.md)。

* [元件指南](/help/communities/components-guide.md)

   * 一個示例站點[社區元件](https://localhost:4502/editor.html/content/community-components/en.html)，它提供了所有社區元件的示例，包括其預設配置和實驗能力。

## 社群網站範本 {#community-site-templates}

社群網站的建立是以選擇社群網站範本為基礎，以快速設定獨立於任何範例網站的社群網站。

社群網站範本由社群功能和社群群組範本組成，提供社群網站的結構，包括登入、使用者設定檔、傳訊、網站選單、搜尋、主題和品牌功能。

請參閱[網站範本主控台](/help/communities/sites.md)。

## 社群功能 {#community-functions}

社群體驗預期的功能眾所周知。 有了AEM Communities，這些功能即可做為建置區塊，稱為社群功能。

社群功能是一般的AEM頁面，其中包含連結在功能中的元件，可輕鬆整合在社群網站範本中。

請參閱[社群功能控制台](/help/communities/functions.md)。

## 社群群組和群組範本{#community-groups-and-group-templates}

社群群組功能是讓來自作者和發佈環境的授權使用者和社群成員在社群網站中動態建立子社群的能力。

當模板的結構包含[組函式](/help/communities/functions.md#groups-function)時，可從作者環境在現有社區站點中建立社區組（子社區）或在現有組內嵌套。

建立社區組需要選擇提供社區組頁面設計的社區組模板。 將「群組」功能新增至範本結構時，其設定為指定一個群組範本，或在建立新社群群組時提供範本選擇。

另請參閱:

* [網站群組](/help/communities/groups.md) 控制台，可在作者環境中建立子社群。
* [群組範本](/help/communities/tools-groups.md) 控制台，以建立群組的網站結構。
* [AEM社群快速入門](/help/communities/getting-started.md) 教學課程，以快速建立包含巢狀群組的社群網站。

## 社群元件{#community-components}

建立社群網站的[社群元件](/help/communities/author-communities.md)可用於將社群功能新增至任何AEM網站。

[社群元件指南](/help/communities/components-guide.md)可供互動探索元件。

## 社區類型{#types-of-communities}

### 參與社群{#engagement-community}

參與社群是社群網站，主要吸引客戶提供資訊、徵求意見，並讓客戶以社群成員的身分互動。

參與社群的功能可能包括：

* 登入
* 傳送訊息
* 論壇
* 評論
* 評論
* 評等
* 投票
* 部落格
* 群組
* 日曆
* 轉換
* 審核
* 通知
* 計分和徽章
* Analytics報表

若要體驗快速建立新參與社群的簡易性，請造訪[AEM Communities](/help/communities/getting-started.md)快速入門。

### 啟用社群{#enablement-community}

啟用社群是包含線上學習功能的社群網站。

啟用社群的功能可能包括：

* [參與社群](#engagement-community)的所有功能。
* 指派內容與學習的能力。 資源。
* 支援SCORM內容，例如隨堂測驗和測試。
* 跟蹤任務完成。
* 存取報告與分析。
* 透過論壇、訊息、留言和評分進行學習資源相關對話的能力。

當配置[啟用附加元件](/help/communities/enablement.md)時，可建立啟用社區，該附加元件需要額外的許可以用於生產環境。 啟用社群網站將包含[指派函式](#community-functions)。

若要體驗建立新啟用社群的便利性，請造訪[AEM Communities for Enablement](/help/communities/getting-started-enablement.md)快速入門。

## AEM Demo Machine {#aem-demo-machine}

[AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)管理並執行AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)和[Forms&lt;a111/>的示範程式，這通常需要更多的設定，而不只是啟動QuickStart實例。 ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)AEM Demo Machine將設定額外的[基礎架構](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)，例如MongoDB、Solr、MySQL、FFmpeg和電子郵件伺服器。

AEM Demo Machine包含：

* A [圖形用戶介面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置[屬性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)和[目標](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)的Apache ANT指令碼。

* 要安裝的軟體包。

AEM Demo Machine已在Windows、MacOS和Linux上成功測試CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4。

AEM Demo Machine需要有效的AEM授權。

>[!NOTE]
>
>檢視AEM Demo Machine(13:26)的[影片簡介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be)。

## AEM Communities Documentation {#aem-communities-documentation}

* 請造訪[部署社群](deploy-communities.md)以瞭解建議的部署。
* 請造訪[管理社群網站](administer-landing.md)，以瞭解如何建立社群網站、新增社群群組、設定社群網站範本、協調社群內容、管理成員、標籤、通知、計分和標章。
* 請造訪[開發社群](communities.md)以瞭解社交元件架構(SCF)和自訂社群元件和功能。
* 請造訪[編寫社群元件](author-communities.md)，以瞭解如何編寫和設定社群元件。

