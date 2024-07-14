---
title: 疑難排解製作時的AEM
description: 下節涵蓋您在使用AEM時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# 疑難排解製作時的AEM{#troubleshooting-aem-when-authoring}

下節涵蓋您在使用AEM時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。

>[!NOTE]
>
>如果發生問題，也值得檢查您執行個體（發行版本和Service Pack）的[已知問題](/help/release-notes/release-notes.md)清單。

>[!NOTE]
>
>擁有管理員許可權且想要疑難排解AEM問題的使用者，可以使用[疑難排解AEM （適用於管理員）](/help/sites-administering/troubleshoot.md)中所述的疑難排解方法。 如果您沒有足夠的許可權，請聯絡您的系統管理員，瞭解如何疑難排解AEM。

## 發佈網站上仍顯示舊的頁面版本 {#old-page-version-still-on-published-site}

* **問題**：

   * 您已經變更頁面，並將頁面復寫至發佈網站，但發佈網站上仍顯示&#x200B;*舊*&#x200B;版本的頁面。

* **原因**：

   * 這可能有多種原因，通常是快取(本機瀏覽器或Dispatcher)，但有時復寫佇列可能會發生問題。

* **解決方案**：

   * 這裡有多種可能性：
   * 確認已正確復寫頁面。 檢查頁面狀態，並視需要檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，然後再次存取您的頁面。
   * 將`?`新增至頁面URL的結尾。 例如：

     `http://localhost:4502/sites.html/content?`

     這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果復寫佇列發生問題，請聯絡您的系統管理員。

## Sidekick不可見 {#sidekick-not-visible}

* **問題**：

   * 在作者環境中編輯內容頁面時，Sidekick不可見。

* **原因**：

   * 在極少數情況下，您可能會將sidekick的標題放在目前視窗的範圍之外。 這表示您無法再次重新調整其位置。

* **解決方案**：

   * 從目前的工作階段登出，然後重新登入。 Sidekick將返回預設位置。

## 尋找和取代 — 並非所有執行個體都會被取代 {#find-replace-not-all-instances-are-replaced}

* **問題：**

   * 使用&#x200B;**尋找和取代**&#x200B;選項時，可能會發生不是頁面上所有的`find`字詞執行個體都已被取代的情況。

* **原因**：

   * **尋找與取代**&#x200B;的功能取決於內容的儲存方式，以及是否可以搜尋內容。 例如，部落格文字儲存在`jcr:text`屬性中，但未設定搜尋該屬性。 尋找和取代servlet的預設範圍涵蓋下列屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**：

   * 可以使用&#x200B;**Day CQ WCM Find Replace Servlet**&#x200B;的設定，使用&#x200B;**網頁主控台**&#x200B;變更這些定義；例如，在

     `http://localhost:4502/system/console/configMgr`
