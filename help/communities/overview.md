---
title: AEM Communities概述
seo-title: AEM Communities Overview
description: AEM Communities功能和設定概述
seo-description: An overview of AEM Communities features and setup
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: 9f9f80eb4cb74b687c7fadd41d0f8ea4ee967865
workflow-type: tm+mt
source-wordcount: '1273'
ht-degree: 1%

---

# AEM Communities概述 {#aem-communities-overview}

Adobe Experience Manager(AEM社區)提供了快速建立內部社區站點的能力，該站點改善了效能，改善了站點管理，並鼓勵站點訪問者轉化為有價值的社區成員。

## 社區功能 {#communities-features}

AEM Communities支援與網站訪問者建立關係，該關係：

* **通知** 通過部落格、問答和事件日曆，
* 同時 **洞察力** 通過論壇、評論和其他社區內容，通常稱為用戶生成內容(UGC)。
* 它允許 **緩和** 由發佈環境中的受信任成員執行，
* **社交登錄** twitter和Facebook,
* **內聯翻譯** 社區內容，
* **社區組建立** 從發佈的社區網站，
* **評分** 頒發徽章，
* **檔案共用**。
* **通知** 和 **活動流**。
* 允許 **標籤** (@mention)用戶生成內容中的其他註冊成員，以引起他們的注意。

可以使用 [演示AEM機](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) 在GitHub.com上公開提供，或與新的We.Retail參考實現一起提供。

## 社群網站 {#community-sites}

社區站點是使用簡AEM單嚮導建立的站點，該嚮導將生成一個網站，該網站預先連接到該站點，並具有許多常見功能。

的 [站點建立嚮導](/help/communities/sites-console.md):

* 根據所選的 [社區網站模板](/help/communities/sites.md) 即：

   * 由 [社區功能](#community-functions)
   * 可選 [社區組](#communitygroups) 特徵

* 使用設定配置：

   * 緩和
   * 登錄
   * 轉換

* 提供基本功能：

   * 響應性設計：使用 [TwitterBootstrap主題](https://getbootstrap.com)

   * 登錄：自我註冊， [社交登錄](/help/communities/social-login.md)，用戶配置檔案

      * 通知：成員可查看與其相關的事件，以及用戶生成的內容所在的位置 [@mentioned](/help/communities/overview.md#mentionssupport)。

      * 消息：成員可以在社區站點內發送或接收消息。
      * 搜索：能夠在社區站點內搜索。
      * 語言轉換：能夠為 [多語言站點](/help/sites-administering/translation.md)。

      * 管理：允許授權成員對社區站點中的用戶進行中和管理。

* 消除了許多頁面級創作步驟：

   * 品牌推廣：可選上載標題影像以在社區網站的所有頁面上顯示
   * 導航菜單：為包含在社區站點模板中的功能提供導航連結。

要體驗快速建立新社區站點的輕鬆性，請訪問 [AEM Communities入門](/help/communities/getting-started.md)。

## 社區內容持久性 {#community-content-persistence}

為提高社區內容的效能和同步性，AEM Communities要求專門為所有（作者和發佈）實例之間共用的用戶生成內容(UGC)AEM提供公共儲存。

通過儲存資源提供商(SRP)可方便地訪問社區內容，該提供商提供一個層來將訪問與底層拓撲分離，並支援UGC的公共儲存。

要瞭解有關社區內容持久性和建議部署的更多資訊，請參閱：

* [社區內容儲存](/help/communities/working-with-srp.md)，討論UGC的可用SRP儲存選項。
* [推薦的拓撲](/help/communities/topologies.md)討論了基於用例和SRP選擇的拓撲。
* [升級AEM到6.5個社區](/help/communities/upgrade.md)，它提供了在移動到6.5時有關UGCAEM的有用資訊。

## 社區控制台 {#communities-consoles}

在作者環境中，全局導航控制台提供對 [社區控制台](/help/communities/consoles.md)，其中包含：

* [站點](/help/communities/sites-console.md) 控制台

   * 網站建立
   * 網站編輯
   * 站點管理
   * [社區組](/help/communities/groups.md) 控制台

* [審核](/help/communities/moderation.md) 控制台

   * 用於作者和發佈環境的通用批量審核UI。
   * 新建篩選條件。

* [成員和組](/help/communities/members.md) 管理控制台

   * 提供從作者環境建立和管理發布端用戶（成員）的能力。
   * 提供禁止成員的能力。
   * 提供從作者環境建立和管理發布端用戶組（成員組）的能力。

* [報告](/help/communities/reports.md) 控制台

   * 提供生成有關分配、帖子和視圖的報告的能力。

全局工具控制台提供對以下社區工具的訪問：

* [站點模板](/help/communities/tools.md#sitetemplatesconsole) 控制台

   * 建立和管理社區網站模板。

* [組模板](/help/communities/tools.md#grouptemplatesconsole) 控制台

   * 建立和管理社區組模板。

* [社區功能](/help/communities/tools.md#communityfunctionsconsole) 控制台

   * 建立和管理社區功能。

* [儲存配置](/help/communities/tools.md#storageconfiguratonconsole) 控制台

   * 選擇並配置 [普通商店](/help/communities/working-with-srp.md) 地址欄。

* [元件指南](/help/communities/components-guide.md)

   * 一個樣本網站， [社區元件](https://localhost:4502/editor.html/content/community-components/en.html)，它提供了所有社區元件的示例，其預設配置以及對它們進行實驗的能力。

## 社群網站範本 {#community-site-templates}

社區站點建立基於對社區站點模板的選擇，以快速設定獨立於任何示例站點的社區站點。

社區網站模板由社區功能和社區組模板組成，提供社區網站的結構，包括登錄、用戶配置檔案、消息、站點菜單、搜索、主題和品牌特徵。

查看 [站點模板控制台](/help/communities/sites.md)。

## 社群功能 {#community-functions}

社區體驗的預期功能眾所周知。 對於AEM Communities，這些功能可以作為構建模組，稱為社區功能。

社區功能是AEM普通頁面，包括匯編到功能中的元件，該功能易於併入社區站點模板。

查看 [社區功能控制台](/help/communities/functions.md)。

## 社區組和組模板 {#community-groups-and-group-templates}

社區組功能是使子社區能夠由來自作者和發佈環境的授權用戶和社區成員在社區站點內動態建立。

當模板的結構包含 [組函式](/help/communities/functions.md#groups-function)。

建立社區組需要選擇提供社區組頁面設計的社區組模板。 將「組」功能添加到模板結構時，它配置為指定一個組模板或在建立新社區組時提供模板選項。

另請參閱:

* [站點組控制台](/help/communities/groups.md) 在作者環境中建立子社區。
* [組模板控制台](/help/communities/tools-groups.md) 建立組的站點結構。
* [AEM Communities入門](/help/communities/getting-started.md) 有關快速建立包含嵌套組的社區網站的教程。

## 社區元件 {#community-components}

的 [社區元件](/help/communities/author-communities.md) 可以使用構建社區站點的社區功能將社區功能添加到任何AEM站點。

的 [社區元件指南](/help/communities/components-guide.md) 可用於元件的互動式探索。

## 參與社區 {#engagement-community}

項目社區是一個社區站點，其重點是讓客戶向其通報、徵求反饋，並允許客戶作為社區成員進行交互。

項目社區的功能可能包括：

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
* 記分和徽章
* 分析報告

要體驗快速建立新的參與社區的輕鬆性，請訪問 [AEM Communities入門](/help/communities/getting-started.md)。

## 演示AEM機 {#aem-demo-machine}

的 [演示AEM機](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) 管理和運行演示AEM [站點](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)。 [資產](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)。 [社區](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)。 [應用](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) 和 [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms)，這通常需要的設定比啟動QuickStart實例更多。 演示AEM機將設定其他 [基礎](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) 例如MongoDB、Solr、MySQL、FFmpeg和電子郵件伺服器。

演示AEM機包括：

* A [圖形用戶介面](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)。
* 具有可配置的Apache ANT指令碼 [屬性](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) 和 [目標](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)。

* 要安裝的包。

在AEMWindows、MacOS和LinuxAEM上，使用CQ 5.5 、 CQ 5.6.1 、 AEM6.0 、AEM 6.1 、 AEM 6.2 、 AEM 6.3 、 6.4和6.4 Demo Machine成功測試了該電腦。

演示AEM機需要有效的AEM許可證。

>[!NOTE]
>
>查看 [視頻簡介](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) 演示AEM機(13:26)。

## AEM Communities文檔 {#aem-communities-documentation}

* 訪問 [部署社區](deploy-communities.md) 瞭解建議的部署。
* 訪問 [管理社區站點](administer-landing.md) 瞭解如何建立社區站點、添加社區組、配置社區站點模板、調節社區內容、管理成員、標籤、通知、評分和徽章。
* 訪問 [發展中社區](communities.md) 瞭解社會元件框架(SCF)和自定義社區元件和功能。
* 訪問 [創作社區元件](author-communities.md) 瞭解如何使用和配置社區元件。
