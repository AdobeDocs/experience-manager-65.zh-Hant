---
title: 製作時疑難排解AEM
seo-title: Troubleshooting AEM when Authoring
description: 以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。
seo-description: The following section covers some issues that you might encounter when using AEM, together with suggestions on how to troubleshoot them.
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 6%

---

# 製作時疑難排解AEM{#troubleshooting-aem-when-authoring}

以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。

>[!NOTE]
>
>遇到問題時，也值得檢查 [已知問題](/help/release-notes/release-notes.md) 適用於您的執行個體（發行和服務套件）。

>[!NOTE]
>
>擁有管理員權限且想要疑難排解AEM問題的使用者，可使用 [疑難排解AEM（適用於管理員）](/help/sites-administering/troubleshoot.md). 如果您沒有足夠的權限，請向系統管理員洽詢疑難排解AEM。

## 舊頁面版本仍在已發佈的網站上 {#old-page-version-still-on-published-site}

* **問題**:

   * 您已對頁面進行變更，並將頁面複製到發佈網站，但 *舊* 頁面的版本仍顯示在發佈網站上。

* **原因**:

   * 這可能有數個原因，通常是快取（您的本機瀏覽器或Dispatcher），但有時可能是復寫佇列的問題。

* **解決方案**:

   * 這裡有各種可能性：
   * 確認頁面已正確復寫。 檢查頁面狀態，並在必要時檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，並再次存取您的頁面。
   * 新增 `?` 到頁面URL的結尾。 例如：

      `http://localhost:4502/sites.html/content?`

      這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果複製隊列出現問題，請與系統管理員聯繫。

## Sidekick不可見 {#sidekick-not-visible}

* **問題**:

   * 在製作環境上編輯內容頁面時，Sidekick不可見。

* **原因**:

   * 在少數情況下，您可能會將側腳的標題置於當前窗口的範圍之外。 這表示您無法重新定位。

* **解決方案**:

   * 從您目前的工作階段登出，然後重新登入。 Sidekick將返回預設位置。

## 查找和替換 — 並非所有實例都被替換 {#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 使用 **查找和替換** 選項，並非所有例項 `find` 詞語會在頁面上取代。

* **原因**:

   * 功能 **查找和替換** 取決於內容的儲存方式，以及是否可加以搜尋。 例如，部落格文字會儲存在 `jcr:text` 未配置為搜索的屬性。 查找和替換servlet的預設範圍涵蓋以下屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**:

   * 這些定義可以透過 **Day CQ WCM尋找取代Servlet** 使用 **Web主控台**;例如，在

      `http://localhost:4502/system/console/configMgr`
