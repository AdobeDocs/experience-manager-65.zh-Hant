---
title: 開發人員的最AEM佳做法
description: Adobe 工程和顧問團隊已經為 AEM 開發人員發展出一組完整的最佳做法。
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 13%

---

# 最佳做法{#best-practices}

## 開發人員的最佳做法 — 入門 {#best-practices-for-developers-getting-started}

Adobe 工程和顧問團隊已經為 AEM 開發人員發展出一組完整的最佳做法。Adobe開發人員在為客戶實施開發核心產品更新AEM和客戶代碼時遵守這些最佳做法。

在開始開發項AEM目之前，請首先檢查以下最佳做法：

* [開發實踐](/help/sites-developing/development-practices.md)
* [內容體系結構](/help/sites-developing/content-architecture.md)
* [軟體體系結構](/help/sites-developing/software-architecture.md)
* [編碼提示](/help/sites-developing/coding-tips.md)
* [代碼陷阱](/help/sites-developing/code-pitfalls.md)
* [JCR交互](/help/sites-developing/jcr-integration.md)
* [OSGi捆綁包](/help/sites-developing/osgi-bundles.md)
* [Java API最佳實踐](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### 其他最佳做法資訊 {#additional-best-practices-information}

以下領域提供了專門用於制定最佳做法的文檔：

* [Sites](#sites)
* [社群](/help/sites-developing/best-practices.md#communities)
* [工具/HTL](/help/sites-developing/best-practices.md#tooling-htl)

具體文檔將在隨後的表中進行描述和連結。

有關管理、部署和維護或創作的最佳做法，請參閱以下內容之一：

* [管理最佳做法](/help/sites-administering/administer-best-practices.md)
* [編寫最佳做法](/help/sites-authoring/best-practices.md)
* [部署最佳做法](/help/sites-deploying/best-practices.md)

## Sites {#sites}

管理和創作網站內容有一些最佳做法概述如下：

<table>
 <tbody>
  <tr>
   <td>標準、可觸摸的UI背後的一些理論。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">啟用觸摸的UI:概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">啟用觸摸的UI:結構</a></p> </td>
   <td>這些文檔概述了啟用觸摸的UI的概念和結構。</td>
  </tr>
  <tr>
   <td>啟用觸摸的UI:自定義控制台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自定義啟用觸摸的UI控制台</a></td>
   <td>本文檔介紹了擴展啟用觸摸的UI控制台的最佳方法。</td>
  </tr>
  <tr>
   <td>啟用觸摸的UI:自定義頁面創作</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自定義啟用觸摸的UI頁面創作</a></td>
   <td>介紹如何擴展啟用觸摸的UI的頁面創作。</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">開發和延伸工作流程</a></td>
   <td><p>工作流使您能夠自AEM動執行Adobe Experience Manager()活動，並可代表環境中發生的大量處理AEM，因此強烈建議仔細規劃您的工作流實施。</p> </td>
  </tr>
 </tbody>
</table>

## 社群 {#communities}

[AEM Communities](/help/communities/overview.md) 簡化了內部社區的建立和管理。

下面介紹了社區的一些最佳做法：

|  |  |  |
|---|---|---|
| 使用用戶生成的內容(UGC)的最佳做法 | [編碼准則](/help/communities/code-guide.md) | 開發靈活、便攜代碼的指南 [社會構成框架](/help/communities/scf.md) (SCF)。 |
| 社區元件的示例用法 | [社區元件指南](/help/communities/components-guide.md) | 一種互動式開發工具。 |

## 工具/HTL {#tooling-htl}

HTML模板語言(HTL)是一種新的HTML模板系統，它以6.AEM0為開發平台。將JSP和ESP取代為ESP的首選模板系AEM統。

|  |  |  |
|---|---|---|
| HTL 總覽 | [HTL概述和語法](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 本文檔介紹HTL是什麼、如何移動到HTL、示例項目、語法、表達式和語句 |
| 在java中使用API | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API使HTL檔案能夠訪問自定義Java類中的幫助程式方法。 |

>[!NOTE]
>
>下面的多部分教程可能是設定新項目的最佳實踐AEM，詳細介紹了核心元件、可編輯模板、客戶端庫和元件開發：
>[AEM Sites - WKND 教學課程快速入門](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
