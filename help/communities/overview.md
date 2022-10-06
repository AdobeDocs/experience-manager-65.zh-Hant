---
title: AEM Communities概述
seo-title: AEM Communities Overview
description: AEM Communities功能與設定的概觀
seo-description: An overview of AEM Communities features and setup
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
source-wordcount: '1435'
ht-degree: 1%

---

# AEM Communities概述 {#aem-communities-overview}

Adobe Experience Manager(AEM)Communities可讓您快速建立內部部署社群網站，進而改善效能、改善網站管理，並鼓勵將網站訪客轉換為有價值的社群成員。

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## 社群功能 {#communities-features}

AEM Communities可讓您開發與網站訪客的關係，其可：

* **通知** 通過部落格、問答和事件日曆，
* 同時 **獲得深入分析** 透過論壇、留言和其他社群內容，通常稱為使用者產生的內容(UGC)。
* 它允許 **審核** 由發佈環境中的受信任成員，
* **社交登入** twitter和Facebook,
* **內嵌翻譯** 社區內容，
* **社群群組建立** 從發佈的社群網站，
* **分數** 頒發徽章，
* **檔案共用**,
* **通知** 和 **活動資料流**,
* 允許 **標籤** (@mention)使用者產生內容中其他已註冊成員，以吸引其注意。
* 支援 **鍵盤導覽** 啟用元件（例如目錄和課程播放、工作總攬、檔案庫）。

可使用 [AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) 可在GitHub.com上公開取得，或透過新的We.Retail參考實作取得。

## 社群網站 {#community-sites}

社群網站是使用簡單精靈建立的AEM網站，可產生預先連線至網站的許多常見功能的網站。

此 [網站建立精靈](/help/communities/sites-console.md):

* 根據所選項組合站點的功能 [社群網站範本](/help/communities/sites.md) 即：

   * 從 [社群功能](#community-functions)
   * 可選 [社群團體](#communitygroups) 功能

* 使用設定進行配置：

   * 審核
   * 登入
   * 轉換

* 提供基本功能：

   * 回應式設計：uses [TwitterBootstrap主題](https://getbootstrap.com)

   * 登入：自我註冊， [社交登入](/help/communities/social-login.md)，使用者設定檔

      * 通知：成員會看到與他們相關的事件，以及用戶生成的內容 [@mentioned](/help/communities/overview.md#mentionssupport).

      * 傳訊：成員可以在社區站點內發送或接收消息。
      * 搜尋：可在社群網站內搜尋。
      * 語言切換：為 [多語言網站](/help/sites-administering/translation.md).

      * 管理：授權成員的存取權，以協調和管理社群網站中的使用者。

* 消除了許多頁面層級的製作步驟：

   * 品牌推廣：選擇性上傳橫幅影像，以在社群網站的所有頁面上顯示
   * 導覽功能表：為社群網站範本中包含的功能提供導覽連結。

若要體驗快速建立新社群網站的便利性，請造訪 [開始使用AEM Communities](/help/communities/getting-started.md).

## 社群內容持續性 {#community-content-persistence}

為了改善社群內容的效能與同步，AEM Communities需要專門針對在所有AEM（製作和發佈）執行個體之間共用的使用者產生內容(UGC)的通用存放區。

通過儲存資源提供器(SRP)輕鬆訪問社區內容，該提供器提供一個層，以將訪問與基礎拓撲分開，並支援UGC的公共儲存。

若要進一步了解社群內容持續性和建議的部署，請參閱：

* [社群內容儲存](/help/communities/working-with-srp.md)，討論UGC可用的SRP儲存選項。
* [建議的拓撲](/help/communities/topologies.md)，根據使用案例和SRP選擇討論拓撲。
* [升級至AEM 6.5 Communities](/help/communities/upgrade.md)，在移至AEM 6.5時，可提供UGC的實用資訊。

## Communities主控台 {#communities-consoles}

在製作環境中，全域導覽主控台可讓您存取 [Communities主控台](/help/communities/consoles.md)，其中包含：

* [網站](/help/communities/sites-console.md) 主控台

   * 網站建立
   * 網站編輯
   * 網站管理
   * [社群群組](/help/communities/groups.md) 主控台

* [協調](/help/communities/moderation.md) 主控台

   * 適用於製作和發佈環境的常見大量協調UI。
   * 新篩選條件。

* [成員和組](/help/communities/members.md) 管理主控台

   * 提供從製作環境建立及管理發布端使用者（成員）的功能。
   * 提供禁止成員的能力。
   * 提供從製作環境建立及管理發布端使用者群組（成員群組）的功能。

* [報表](/help/communities/reports.md) 主控台

   * 提供產生工作分配、貼文和檢視報表的能力。

* [資源](/help/communities/resources.md) 主控台

   * 提供建立啟用資源和學習路徑的功能。
   * 提供啟用資源和學習路徑報表的存取權。

全局工具控制台提供對以下Communities工具的訪問：

* [網站範本](/help/communities/tools.md#sitetemplatesconsole) 主控台

   * 建立和管理社區站點模板。

* [群組範本](/help/communities/tools.md#grouptemplatesconsole) 主控台

   * 建立和管理社群群組範本。

* [社群功能](/help/communities/tools.md#communityfunctionsconsole) 主控台

   * 建立和管理社群功能。

* [儲存配置](/help/communities/tools.md#storageconfiguratonconsole) 主控台

   * 選取並設定 [公用商店](/help/communities/working-with-srp.md) 的URL區段。

* [元件指南](/help/communities/components-guide.md)

   * 範例網站， [社群元件](https://localhost:4502/editor.html/content/community-components/en.html)，提供所有Communities元件的範例，以及其預設設定和實驗功能。

## 社群網站範本 {#community-site-templates}

社群網站的建立是根據社區網站模板的選擇，以快速設定獨立於任何示例網站的社區網站。

由社區功能和社區組模板組成的社區站點模板提供了社區站點的結構，包括登錄、用戶配置檔案、消息、站點菜單、搜索、主題和品牌特徵。

請參閱 [網站範本主控台](/help/communities/sites.md).

## 社群功能 {#community-functions}

社群體驗預期的功能眾所周知。 透過AEM Communities，這些功能可作為建置組塊，稱為社群功能。

社群功能是一般的AEM頁面，其元件匯整在功能中，可輕鬆整合至社群網站範本中。

請參閱 [社群功能主控台](/help/communities/functions.md).

## 社群群組和群組範本 {#community-groups-and-group-templates}

社群群組功能是讓來自製作和發佈環境的授權使用者和社群成員在社群網站內動態建立子社群的能力。

當範本的結構包含 [組函式](/help/communities/functions.md#groups-function).

建立社群群組需要選取社群群組範本，以提供社群群組頁面的設計。 將「組」函式添加到模板結構時，該函式配置為指定一個組模板，或在建立新的社區組時提供模板選項。

另請參閱:

* [網站群組主控台](/help/communities/groups.md) ，以在製作環境中建立子社群。
* [群組範本主控台](/help/communities/tools-groups.md) ，為群組建立網站結構。
* [開始使用AEM Communities](/help/communities/getting-started.md) 快速建立包含巢狀群組的社群網站的教學課程。

## 社群元件 {#community-components}

此 [社群元件](/help/communities/author-communities.md) 建立社群網站時，可將社群功能新增至任何AEM網站。

此 [社群元件指南](/help/communities/components-guide.md) 可供互動式探索元件。

## 社群類型 {#types-of-communities}

### 參與社群 {#engagement-community}

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

若要體驗快速建立新參與社群的便利性，請造訪 [開始使用AEM Communities](/help/communities/getting-started.md).

### 培訓社群 {#enablement-community}

培訓社群是社群網站，包含線上學習功能。

啟用社群的功能可能包括：

* 的所有功能 [參與社群](#engagement-community).
* 指派內容和學習的能力。 資源給成員和成員組。
* 支援SCORM內容，例如測驗和測試。
* 跟蹤任務完成。
* 存取報告與分析。
* 能夠通過論壇、報文傳送、評論和評分就學習資源進行對話。

當 [已配置啟用附加元件](/help/communities/enablement.md)，而生產環境則需要額外的授權才能使用。 培訓社群網站將包含 [指派函式](#community-functions).

若要體驗建立新啟用社群的便利性，請造訪 [AEM Communities啟用快速入門](/help/communities/getting-started-enablement.md).

## AEM示範電腦 {#aem-demo-machine}

此 [AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) 管理和執行AEM的示範 [網站](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [資產](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [社群](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [應用程式](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) 和 [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)，這通常需要設定，而不只是啟動QuickStart實例。 AEM Demo Machine將設定其他 [基礎結構](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 例如MongoDB、Solr、MySQL、FFmpeg和電子郵件伺服器。

AEM Demo Machine包括：

* A [圖形用戶介面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* 具有可配置的Apache ANT指令碼 [屬性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 和 [目標](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line).

* 要安裝的軟體包。

在Windows、MacOS和Linux上，使用CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功測試了AEM示範電腦。

AEM Demo Machine需要有效的AEM授權。

>[!NOTE]
>
>檢視 [影片簡介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 到AEM Demo Machine (13:26)。

## AEM Communities檔案 {#aem-communities-documentation}

* 瀏覽 [部署社群](deploy-communities.md) 了解建議的部署。
* 瀏覽 [管理社群網站](administer-landing.md) 了解如何建立社群網站、新增社群群組、設定社群網站範本、協調社群內容、管理成員、標籤、通知、分數和徽章。
* 瀏覽 [開發社區](communities.md) 了解社交元件架構(SCF)和自訂社群元件和功能。
* 瀏覽 [編寫Communities元件](author-communities.md) 了解如何使用和設定Communities元件。
