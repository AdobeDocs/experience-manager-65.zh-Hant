---
title: 最佳作法
seo-title: Best Practices
description: Adobe工程與諮詢團隊已為AEM開發人員開發了一套完整的最佳實務
seo-description: Adobe Engineering and Consulting teams have developed a comprehensive set of best practices for AEM developers
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
exl-id: 0a478e80-c1b2-46c1-a6be-794d78b85d69
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 10%

---

# 最佳作法{#best-practices}

## 開發人員最佳實務 — 快速入門 {#best-practices-for-developers-getting-started}

Adobe 工程和顧問團隊已經為 AEM 開發人員發展出一組完整的最佳做法。Adobe開發人員在開發核心AEM產品更新和客戶程式碼以進行客戶實作時，會遵循這些最佳實務。

開始AEM開發專案前，請先檢閱下列最佳實務：

* [開發實務](/help/sites-developing/development-practices.md)
* [內容架構](/help/sites-developing/content-architecture.md)
* [軟體體系結構](/help/sites-developing/software-architecture.md)
* [編碼提示](/help/sites-developing/coding-tips.md)
* [程式碼陷阱](/help/sites-developing/code-pitfalls.md)
* [JCR互動](/help/sites-developing/jcr-integration.md)
* [OSGi套件組合](/help/sites-developing/osgi-bundles.md)
* [Java API最佳作法](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/understand-java-api-best-practices.html)

### 其他最佳實務資訊 {#additional-best-practices-information}

以下幾方面提供開發最佳實務的專屬檔案：

* [Sites](#sites)
* [社群](/help/sites-developing/best-practices.md#communities)
* [工具/HTL](/help/sites-developing/best-practices.md#tooling-htl)

下面的表中描述了特定文檔並連結到這些文檔。

如需管理、部署和維護或編寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [製作最佳實務](/help/sites-authoring/best-practices.md)
* [部署最佳實務](/help/sites-deploying/best-practices.md)

## 網站 {#sites}

管理和編寫網站內容有一些最佳實務，概述如下：

<table>
 <tbody>
  <tr>
   <td>標準觸控式UI背後的部分理論。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">觸控式UI:概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">觸控式UI:結構</a></p> </td>
   <td>這些檔案提供觸控式UI的概念和結構概觀。</td>
  </tr>
  <tr>
   <td>觸控式UI:自訂主控台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自訂觸控式UI主控台</a></td>
   <td>本檔案說明擴充觸控式UI主控台的最佳方式。</td>
  </tr>
  <tr>
   <td>觸控式UI:自訂頁面編寫</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自訂觸控式UI頁面編寫</a></td>
   <td>說明如何延伸觸控式UI的頁面編寫。</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">開發和延伸工作流程</a></td>
   <td><p>工作流程可讓您自動化Adobe Experience Manager(AEM)活動，並可代表AEM環境中發生的大量處理，因此強烈建議您謹慎規劃工作流程實作。</p> </td>
  </tr>
 </tbody>
</table>

## 社群 {#communities}

[AEM Communities](/help/communities/overview.md) 可簡化內部部署社群的建立和管理。

以下說明Communities的一些最佳實務：

|  |  |  |
|---|---|---|
| 使用使用者產生的內容(UGC)的最佳作法 | [編碼准則](/help/communities/code-guide.md) | 為開發彈性的可攜式程式碼的指引 [社會構成框架](/help/communities/scf.md) (SCF)。 |
| Communities元件的範例使用 | [社群元件指南](/help/communities/components-guide.md) | 互動式開發工具。 |

## 工具/HTL {#tooling-htl}

HTML模板語言(HTL)是以AEM 6.0為基礎而推出的一種新型HTML模板系統，它取代了JSP和ESP作為AEM的首選模板系統。

|  |  |  |
|---|---|---|
| HTL 總覽 | [HTL概觀和語法](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html) | 本檔案說明HTL是什麼、如何改用HTL、範例專案、語法、運算式和陳述式 |
| 在java中使用API | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API可讓HTL檔案存取自訂Java類別中的Helper方法。 |

>[!NOTE]
>
>以下是設定新AEM專案的最佳實務，其中會詳細說明核心元件、可編輯範本、用戶端程式庫和元件開發，您可能最感興趣的多部分教學課程：
>[AEM Sites - WKND 教學課程快速入門](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)
