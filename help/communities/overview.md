---
title: AEM Communities概觀
description: 瞭解Adobe Experience Manager Communities功能和設定的基礎知識。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 1%

---

# AEM Communities概觀 {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities可讓您快速建立內部部署社群網站，此網站已改善效能、改善網站管理，並鼓勵將網站訪客轉換為有價值的社群成員。

## Communities功能 {#communities-features}

AEM Communities可讓您發展與網站訪客的關係，這會：

* **透過部落格、問答和事件行事曆通知**，
* 同時&#x200B;**透過論壇、評論和其他社群內容獲得見解**，通常稱為使用者產生的內容(UGC)。
* 它允許Publish環境中受信任的成員進行&#x200B;**稽核**，
* 使用Twitter和Facebook的&#x200B;**社交登入**，
* **社群內容的內嵌翻譯**，
* 從發佈的社群網站建立&#x200B;**社群群組**，
* **得分**&#x200B;獎勵徽章，
* **檔案共用**，
* **通知**&#x200B;和&#x200B;**活動資料流**，
* 允許在使用者產生的內容中標籤&#x200B;**其他註冊成員** (@mention)，以引起他們的注意。

社群功能可以使用GitHub.com上公開的[AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki)或新的`We.Retail`參考實作來示範。

## 社群網站 {#community-sites}

社群網站是使用簡單精靈建立的AEM網站，該精靈會產生具有許多預先連線到網站中的常見功能的網站。

[網站建立精靈](/help/communities/sites-console.md)：

* 根據選取的[社群網站範本](/help/communities/sites.md)來組合網站的功能，該範本為：

   * 由[社群功能](#community-functions)建置
   * 選用的[社群群組](#communitygroups)功能

* 使用設定進行配置：

   * 稽核
   * 登入
   * 轉換

* 提供基本功能：

   * 回應式設計：使用[TwitterBootstrap主題](https://getbootstrap.com)

   * 登入：自我註冊，[社交登入](/help/communities/social-login.md)，使用者設定檔

      * 通知：
成員會看到與其相關的事件，以及使用者產生的內容，其中他們是[@mentioned](/help/communities/overview.md#mentionssupport)。

      * 傳送訊息：成員可在社群網站內傳送或接收訊息。
      * 搜尋：可在社群網站內搜尋。
      * 語言切換：可為[多語言網站](/help/sites-administering/translation.md)選取語言。

      * 管理：授權成員的存取權，以便稽核和管理社群網站內的使用者。

* 省去許多頁面層級的編寫步驟：

   * 品牌推廣：可選擇上傳橫幅影像以在社群網站的所有頁面上顯示
   * 導覽功能表：社群網站範本中包含的功能提供導覽連結。

若要體驗快速建立社群網站的簡易性，請造訪[AEM Communities快速入門](/help/communities/getting-started.md)。

## 社群內容持續性 {#community-content-persistence}

為了改善社群內容的效能和同步化，AEM Communities需要專門針對在所有AEM （製作和發佈）執行個體之間共用的使用者產生內容(UGC)的共同存放區。

可透過儲存資源提供者(SRP)輕鬆存取社群內容，SRP提供將存取與基礎拓撲分隔開的圖層，並支援UGC的共同存放區。

若要進一步瞭解社群內容持續性和建議的部署，請參閱：

* [社群內容儲存](/help/communities/working-with-srp.md) — 討論UGC的可用的SRP儲存選項。
* [建議的拓撲](/help/communities/topologies.md) — 根據使用案例和SRP選擇討論拓撲。
* [升級至AEM 6.5 Communities](/help/communities/upgrade.md) — 在移至AEM 6.5時，提供有關UGC的實用資訊。

## 社群主控台 {#communities-consoles}

在作者環境中，全域導覽主控台提供對[社群主控台](/help/communities/consoles.md)的存取權，其中包含：

* [網站](/help/communities/sites-console.md)主控台

   * 網站建立
   * 網站編輯
   * 網站管理
   * [社群群組](/help/communities/groups.md)主控台

* [稽核](/help/communities/moderation.md)主控台

   * 適用於作者和Publish環境的通用大量稽核UI。
   * 新增篩選條件。

* [成員和群組](/help/communities/members.md)管理主控台

   * 可讓您從製作環境建立和管理發布端使用者（成員）。
   * 可讓您禁止成員。
   * 可讓您從製作環境建立和管理發布端使用者群組（成員群組）。

* [報表](/help/communities/reports.md)主控台

   * 可讓您產生指派、貼文和檢視報表。

全域工具主控台提供下列Communities工具的存取權：

* [網站範本](/help/communities/tools.md#sitetemplatesconsole)主控台

   * 建立及管理社群網站範本。

* [群組範本](/help/communities/tools.md#grouptemplatesconsole)主控台

   * 建立及管理社群群組範本。

* [社群功能](/help/communities/tools.md#communityfunctionsconsole)主控台

   * 建立及管理社群功能。

* [儲存設定](/help/communities/tools.md#storageconfiguratonconsole)主控台

   * 選取並設定網站的[公用存放區](/help/communities/working-with-srp.md)。

* [元件指南](/help/communities/components-guide.md)

   * 範例網站[Community Components](https://localhost:4502/editor.html/content/community-components/en.html)提供所有Community元件的範例以及其預設設定和實驗能力。

## 社群網站範本 {#community-site-templates}

社群網站建立是以選取社群網站範本為基礎，以快速設定獨立於任何範例網站的社群網站。

由社群功能和社群群組範本組成的社群網站範本，可提供社群網站的結構。 其中包含登入、使用者設定檔、訊息、網站功能表、搜尋、主題設定和品牌功能。

檢視[網站範本主控台](/help/communities/sites.md)。

## 社群功能 {#community-functions}

社群體驗的預期功能是眾所周知的。 透過AEM Communities，這些功能可作為基礎要素使用，稱為社群功能。

社群功能是一般的AEM頁面，其中包含以有線方式連線在一起的元件，可輕鬆整合至社群網站範本中。

檢視[社群功能主控台](/help/communities/functions.md)。

## 社群群組和群組範本 {#community-groups-and-group-templates}

社群群組功能可讓作者和發佈環境中的授權使用者和社群成員，在社群網站中動態建立子社群。

當範本的結構包含[群組函式](/help/communities/functions.md#groups-function)時，在作者環境中，可以在現有的社群網站中建立社群群組（子社群），或巢狀內嵌於現有的群組中。

建立社群群組需要選擇社群群組範本，以提供社群群組頁面的設計。 將「群組」功能新增至範本結構時，會將其設定為指定一個群組範本，或在建立新社群群組時提供範本選擇。

另請參閱：

* [網站群組主控台](/help/communities/groups.md)，用於在作者環境中建立子社群。
* [群組範本主控台](/help/communities/tools-groups.md)，用來建立群組的站台結構。
* [AEM Communities快速入門](/help/communities/getting-started.md)快速建立社群網站（包括巢狀群組）的教學課程。

## 社群元件 {#community-components}

建立社群網站的[社群元件](/help/communities/author-communities.md)可用來將社群功能新增至任何AEM網站。

[社群元件指南](/help/communities/components-guide.md)可供互動式探索元件。

## 參與社群 {#engagement-community}

參與社群是社群網站，著重於吸引客戶以資訊、徵求意見以及允許客戶作為社群成員互動。

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
* 行事曆
* 轉換
* 審核
* 通知
* 評分和徽章
* Analytics報表

若要體驗快速建立參與社群的簡易性，請造訪[AEM Communities快速入門](/help/communities/getting-started.md)。

## AEM示範電腦 {#aem-demo-machine}

[AEM示範電腦](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine)管理並執行AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)、[Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)、[社群](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)、[應用程式](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)和[Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)的示範，這些通常需要比啟動QuickStart執行個體更多的設定。 AEM示範機器會設定其他[基礎架構](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure)，例如MongoDB、Solr、MySQL、FFmpeg及電子郵件伺服器。

AEM示範機器包括：

* [圖形使用者介面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可設定的[屬性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties)和[目標](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)的Apache ANT指令碼。

* 要安裝的套件。

AEM Demo Machine已在Windows、macOS和Linux®上透過CQ 5.5、CQ 5.6.1、AEM 6.0、AEM 6.1、AEM 6.2、AEM 6.3和AEM 6.4成功進行測試。

AEM示範機器需要有效的AEM授權。

>[!NOTE]
>
>檢視AEM示範機器的[影片簡介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) (13:26)。

## AEM Communities檔案 {#aem-communities-documentation}

* 請造訪[部署社群](deploy-communities.md)，瞭解建議的部署。
* 造訪[管理社群網站](administer-landing.md)，瞭解如何建立社群網站、新增社群群組、設定社群網站範本、管理社群內容、管理成員、標籤、通知、評分和徽章。
* 造訪[開發Communities](communities.md)，瞭解社交元件架構(SCF)和自訂Communities元件和功能。
* 造訪[Authoring Communities Components](author-communities.md)，瞭解如何使用及設定Communities元件進行創作。
