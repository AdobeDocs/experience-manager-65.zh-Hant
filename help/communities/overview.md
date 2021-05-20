---
title: AEM Communities概述
seo-title: AEM Communities概述
description: AEM Communities功能與設定的概觀
seo-description: AEM Communities功能與設定的概觀
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 1%

---

# AEM Communities概述{#aem-communities-overview}

Adobe Experience Manager(AEM)Communities可讓您快速建立內部部署社群網站，進而改善效能、改善網站管理，並鼓勵將網站訪客轉換為有價值的社群成員。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## 社區功能{#communities-features}

AEM Communities可讓您開發與網站訪客的關係，其可：

* **** 透過部落格、問答和事件日曆提供資訊，
* 而&#x200B;**透過論壇、留言和其他社群內容獲得**&#x200B;見解，通常稱為使用者產生的內容(UGC)。
* 它允許發佈環境中受信任的成員&#x200B;**協調**,
* **社交** 登入Twitter和Facebook,
* **內嵌** 翻譯社群內容，
* **從已發佈** 的社群網站建立社群群組，
* **** 獎章，
* **檔案共用**,
* **** 通知和 **活動流**、
* 允許&#x200B;**標籤**(@mention)用戶生成內容中的其他已註冊成員，以引起他們的注意。
* 在啟用元件（例如目錄和課程播放、工作總攬、檔案庫）上支援&#x200B;**鍵盤導覽** 。

可使用GitHub.com上公開提供的[AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)，或透過新的We.Retail參考實作來示範社群功能。

## 社群網站 {#community-sites}

社群網站是使用簡單精靈建立的AEM網站，可產生預先連線至網站的許多常見功能的網站。

[站點建立嚮導](/help/communities/sites-console.md):

* 根據所選[社區站點模板](/help/communities/sites.md)組合站點的功能，其為：

   * 從[community函式](#community-functions)建立
   * 可選[社區組](#communitygroups)功能

* 使用設定進行配置：

   * 審核
   * 登入
   * 轉換

* 提供基本功能：

   * 回應式設計：使用[TwitterBootstrap主題](https://getbootstrap.com)

   * 登入：自行註冊， [社交登入](/help/communities/social-login.md)，使用者設定檔

      * 通知：
成員會看到與其相關的事件，以及使用者產生的內容，其為[@mentioned](/help/communities/overview.md#mentionssupport)。

      * 傳訊：成員可以在社區站點內發送或接收消息。
      * 搜尋：可在社群網站內搜尋。
      * 語言切換：為[多語言網站](/help/sites-administering/translation.md)選擇語言的能力。

      * 管理：授權成員的存取權，以協調和管理社群網站中的使用者。

* 消除了許多頁面層級的製作步驟：

   * 品牌推廣：選擇性上傳橫幅影像，以在社群網站的所有頁面上顯示
   * 導覽功能表：為社群網站範本中包含的功能提供導覽連結。

若要快速建立新社群網站的便利性，請造訪[AEM Communities快速入門](/help/communities/getting-started.md)。

## 社群內容持續性{#community-content-persistence}

為了改善社群內容的效能與同步，AEM Communities需要專門針對在所有AEM（製作和發佈）執行個體之間共用的使用者產生內容(UGC)的通用存放區。

通過儲存資源提供器(SRP)輕鬆訪問社區內容，該提供器提供一個層，以將訪問與基礎拓撲分開，並支援UGC的公共儲存。

若要進一步了解社群內容持續性和建議的部署，請參閱：

* [社群內容儲存](/help/communities/working-with-srp.md)，討論UGC可用的SRP儲存選項。
* [建議的拓撲](/help/communities/topologies.md)，根據使用案例和SRP選擇討論拓撲。
* [升級至AEM 6.5 Communities](/help/communities/upgrade.md)，在移至AEM 6.5時，可提供有關UGC的實用資訊。

## Communities控制台{#communities-consoles}

在製作環境中，全域導覽主控台提供對[Communities主控台](/help/communities/consoles.md)的存取，其中包含：

* [](/help/communities/sites-console.md) Siteconsole

   * 網站建立
   * 網站編輯
   * 網站管理
   * [社群群](/help/communities/groups.md) 組主控台

* [](/help/communities/moderation.md) Moderationconsole

   * 適用於製作和發佈環境的常見大量協調UI。
   * 新篩選條件。

* [成員和群](/help/communities/members.md) 組管理控制台

   * 提供從製作環境建立及管理發布端使用者（成員）的功能。
   * 提供禁止成員的能力。
   * 提供從製作環境建立及管理發布端使用者群組（成員群組）的功能。

* [](/help/communities/reports.md) Reportsconsole

   * 提供產生工作分配、貼文和檢視報表的能力。

* [](/help/communities/resources.md) Resourcesconsole

   * 提供建立啟用資源和學習路徑的功能。
   * 提供啟用資源和學習路徑報表的存取權。

全局工具控制台提供對以下Communities工具的訪問：

* [網站范](/help/communities/tools.md#sitetemplatesconsole) 本

   * 建立和管理社區站點模板。

* [群組範本](/help/communities/tools.md#grouptemplatesconsole) 控制台

   * 建立和管理社群群組範本。

* [社群功能](/help/communities/tools.md#communityfunctionsconsole) 主控台

   * 建立和管理社群功能。

* [儲存配](/help/communities/tools.md#storageconfiguratonconsole) 置控制台

   * 選擇並配置站點的[公用儲存](/help/communities/working-with-srp.md)。

* [元件指南](/help/communities/components-guide.md)

   * 一個示例站點[社區元件](https://localhost:4502/editor.html/content/community-components/en.html)，提供所有社區元件的示例，以及其預設配置和實驗功能。

## 社群網站範本 {#community-site-templates}

社群網站的建立是根據社區網站模板的選擇，以快速設定獨立於任何示例網站的社區網站。

由社區功能和社區組模板組成的社區站點模板提供了社區站點的結構，包括登錄、用戶配置檔案、消息、站點菜單、搜索、主題和品牌特徵。

請參閱[網站範本主控台](/help/communities/sites.md)。

## 社群功能 {#community-functions}

社群體驗預期的功能眾所周知。 透過AEM Communities，這些功能可作為建置組塊，稱為社群功能。

社群功能是一般的AEM頁面，其元件匯整在功能中，可輕鬆整合至社群網站範本中。

請參閱[社群函式控制台](/help/communities/functions.md)。

## 社區組和組模板{#community-groups-and-group-templates}

社群群組功能是讓來自製作和發佈環境的授權使用者和社群成員在社群網站內動態建立子社群的能力。

當範本的結構包含[群組函式](/help/communities/functions.md#groups-function)時，可從製作環境中，在現有社群網站內建立或巢狀內建立社群群組（子社群）。

建立社群群組需要選取社群群組範本，以提供社群群組頁面的設計。 將「組」函式添加到模板結構時，該函式配置為指定一個組模板，或在建立新的社區組時提供模板選項。

另請參閱:

* [網站群](/help/communities/groups.md) 組主控台可在製作環境中建立子社群。
* [群組範本](/help/communities/tools-groups.md) 主控台，用於建立群組的網站結構。
* [AEM社群快速入](/help/communities/getting-started.md) 門教學課程，以快速建立包含巢狀群組的社群網站。

## 社區元件{#community-components}

建立社群網站的[社群元件](/help/communities/author-communities.md)可用於將社群功能新增至任何AEM網站。

[社群元件指南](/help/communities/components-guide.md)可供互動探索各元件。

## 社區類型{#types-of-communities}

### 參與社群{#engagement-community}

參與社群是社群網站，主要讓客戶提供相關資訊、徵求意見，並允許客戶以社群成員的身分互動。

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

若要快速建立新參與社群的便利性，請造訪[AEM Communities快速入門](/help/communities/getting-started.md)。

### 啟用社群{#enablement-community}

培訓社群是社群網站，包含線上學習功能。

啟用社群的功能可能包括：

* [參與社群](#engagement-community)的所有功能。
* 指派內容和學習的能力。 資源給成員和成員組。
* 支援SCORM內容，例如測驗和測試。
* 跟蹤任務完成。
* 存取報告與分析。
* 能夠通過論壇、報文傳送、評論和評分就學習資源進行對話。

當[啟用附加元件設定](/help/communities/enablement.md)時，可建立啟用社群，這需要額外的授權才能在生產環境中使用。 啟用社群網站將包含[指派函式](#community-functions)。

若要輕鬆建立新的啟用社群，請造訪[啟用AEM Communities快速入門](/help/communities/getting-started-enablement.md)。

## AEM示範電腦{#aem-demo-machine}

[AEM演示電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)管理並運行AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)和[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)的演示，這通常比啟動快速啟動實例更需要設定。 AEM演示電腦將設定其他[基礎架構](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)，如MongoDB、Solr、MySQL、FFmpeg和電子郵件伺服器。

AEM Demo Machine包括：

* [圖形用戶介面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置[properties](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)和[targets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)的Apache ANT指令碼。

* 要安裝的軟體包。

已在Windows、MacOS和Linux上，使用CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功測試AEM示範電腦。

AEM Demo Machine需要有效的AEM授權。

>[!NOTE]
>
>查看AEM演示電腦的[視頻簡介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) (13:26)。

## AEM Communities檔案{#aem-communities-documentation}

* 請造訪[部署Communities](deploy-communities.md)以了解建議的部署。
* 請訪問[管理社群網站](administer-landing.md)以了解如何建立社群網站、新增社群群組、設定社群網站範本、協調社群內容、管理成員、標籤、通知、評分和徽章。
* 請造訪[開發社群](communities.md)以了解社交元件架構(SCF)和自訂社群元件和功能。
* 請造訪[編寫社群元件](author-communities.md)，了解如何使用和設定社群元件。
