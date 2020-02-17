---
title: 最佳實務
seo-title: 最佳實務
description: Adobe工程與諮詢團隊已針對AEM開發人員開發了一套完整的最佳實務
seo-description: Adobe工程與諮詢團隊已針對AEM開發人員開發了一套完整的最佳實務
uuid: f962c31f-8140-482f-b189-16376e23bfed
contentOwner: Justin Edelson
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 99678c1a-81f3-4fb3-bf73-98f0691c3fb6
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Best Practices{#best-practices}

## 開發人員的最佳實務——快速入門 {#best-practices-for-developers-getting-started}

Adobe工程與諮詢團隊已針對AEM開發人員開發了一套完整的最佳實務。 Adobe開發人員在開發適用於客戶實作的核心AEM產品更新和客戶程式碼時，會遵守這些最佳實務。

開始AEM開發專案之前，請先檢閱下列最佳實務：

* [開發實務](/help/sites-developing/development-practices.md)
* [內容架構](/help/sites-developing/content-architecture.md)
* [軟體架構](/help/sites-developing/software-architecture.md)
* [編碼提示](/help/sites-developing/coding-tips.md)
* [程式碼缺陷](/help/sites-developing/code-pitfalls.md)
* [JCR互動](/help/sites-developing/jcr-integration.md)
* [OSGi Bundles](/help/sites-developing/osgi-bundles.md)

### 其他最佳做法資訊 {#additional-best-practices-information}

以下區域提供了專門用於制定最佳做法的檔案：

* [網站](#sites)
* [社群](/help/sites-developing/best-practices.md#communities)
* [工具/HTL](/help/sites-developing/best-practices.md#tooling-htl)

在下表中說明並連結特定檔案。

如需管理、部署和維護或撰寫的最佳實務，請參閱下列其中一項：

* [管理最佳實務](/help/sites-administering/administer-best-practices.md)
* [編寫最佳實務](/help/sites-authoring/best-practices.md)
* [部署最佳實務](/help/sites-deploying/best-practices.md)

## 網站 {#sites}

管理和製作網站內容有下列最佳實務：

<table>
 <tbody>
  <tr>
   <td>標準觸控式UI背後的部分理論。</td>
   <td><p><a href="/help/sites-developing/touch-ui-concepts.md">啟用觸控的UI:概念</a></p> <p><a href="/help/sites-developing/touch-ui-structure.md">啟用觸控的UI:結構</a></p> </td>
   <td>這些檔案提供觸控式使用者介面的概念和結構概觀。</td>
  </tr>
  <tr>
   <td>啟用觸控的UI:自訂控制台 </td>
   <td><a href="/help/sites-developing/customizing-consoles-touch.md">自訂觸控式UI主控台</a></td>
   <td>本檔案說明擴充觸控式UI主控台的最佳方式。</td>
  </tr>
  <tr>
   <td>可觸控的UI:自訂頁面製作</td>
   <td><a href="/help/sites-developing/customizing-page-authoring-touch.md">自訂可觸控的UI頁面製作</a></td>
   <td>說明如何擴充觸控式UI的頁面製作。</td>
  </tr>
  <tr>
   <td>工作流程</td>
   <td><a href="/help/sites-developing/workflows-best-practices.md">開發和擴充工作流程</a></td>
   <td><p>工作流程可讓您自動化Adobe Experience Manager(AEM)活動，並可代表AEM環境中發生的大量處理，因此強烈建議您謹慎規劃工作流程實作。</p> </td>
  </tr>
 </tbody>
</table>

## 社群 {#communities}

[AEM Communities](/help/communities/overview.md) 可簡化內部部署社群的建立和管理。

以下說明社群的一些最佳實務：

|  |  |  |
|---|---|---|
| 使用使用者產生的內容(UGC)的最佳實務 | [編碼准則](/help/communities/code-guide.md) | 為社交元件架構(SCF)開發靈活、可 [攜式程式碼的指引](/help/communities/scf.md) 。 |
| Communities元件的範例使用 | [社群元件指南](/help/communities/components-guide.md) | 互動式開發工具。 |

## 工具/HTL {#tooling-htl}

HTML範本語言(HTL)是AEM 6.0中新推出的HTML範本系統。它取代JSP和ESP作為AEM的偏好範本系統。

|  |  |  |
|---|---|---|
| HTL概觀 | [HTL概觀與語法](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) | 本檔案說明HTL是什麼、如何移至HTL、範例專案、語法、運算式和陳述式 |
| 在java中使用API | [HTL Java Use-API](https://helpx.adobe.com/experience-manager/htl/using/use-api.html) | HTL Java Use-API可讓HTL檔案存取自訂Java類別中的輔助方法。 |

>[!NOTE]
>
>以下是設定新AEM專案的最佳實務，其中詳述核心元件、可編輯範本、用戶端程式庫和元件開發的多部份教學課程可能很有趣：
>[AEM Sites快速入門- WKND教學課程](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop.html)

