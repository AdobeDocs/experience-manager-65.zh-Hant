---
title: 疑難排解製作時的AEM
description: 下節涵蓋您在使用AEM時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 6%

---

# 疑難排解製作時的AEM{#troubleshooting-aem-when-authoring}

下節涵蓋您在使用AEM時可能會遇到的一些問題，以及有關如何疑難排解這些問題的建議。

>[!NOTE]
>
>遇到問題時，也值得檢查 [已知問題](/help/release-notes/release-notes.md) （發行版本和Service Pack）。

>[!NOTE]
>
>具有管理員許可權的使用者以及想要疑難排解AEM問題的使用者，可以使用中所述的疑難排解方法 [疑難排解AEM （適用於管理員）](/help/sites-administering/troubleshoot.md). 如果您沒有足夠的許可權，請向系統管理員洽詢AEM疑難排解的相關資訊。

## 發佈網站上仍顯示舊的頁面版本 {#old-page-version-still-on-published-site}

* **問題**:

   * 您已對頁面進行變更，並將頁面復寫至發佈站台，但 *舊* 頁面版本仍會顯示在發佈網站上。

* **原因**:

   * 這可能有多種原因，最常見的是快取（本機瀏覽器或Dispatcher），不過有時復寫佇列可能會出現問題。

* **解決方案**:

   * 這裡有多種可能性：
   * 確認頁面已正確復寫。 檢查頁面狀態，並視需要檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，然後再次存取您的頁面。
   * 新增 `?` 到頁面URL的結尾。 例如：

      `http://localhost:4502/sites.html/content?`

      這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果復寫佇列發生問題，請聯絡您的系統管理員。

## Sidekick不可見 {#sidekick-not-visible}

* **問題**:

   * 在作者環境中編輯內容頁面時看不到Sidekick。

* **原因**:

   * 在極少數的情況下，您可能會將sidekick的標題放在目前視窗的範圍之外。 這表示您無法再次重新調整其位置。

* **解決方案**:

   * 從目前的工作階段登出，然後重新登入。 Sidekick將返回預設位置。

## 尋找和取代 — 並非所有例項都會被取代 {#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 使用時 **尋找和取代** 選項，並非所有的 `find` 字詞會替換在頁面上。

* **原因**:

   * 的功能 **尋找和取代** 取決於內容的儲存方式以及是否可以搜尋內容。 例如，部落格文字儲存在 `jcr:text` 未設定為要搜尋的屬性。 尋找和取代servlet的預設範圍涵蓋下列屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**:

   * 這些定義可透過以下設定進行變更： **Day CQ WCM尋找取代Servlet** 使用 **網頁主控台**；例如，

      `http://localhost:4502/system/console/configMgr`
