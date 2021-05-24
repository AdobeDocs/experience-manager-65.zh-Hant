---
title: 製作時疑難排解AEM
seo-title: 製作時疑難排解AEM
description: 以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。
seo-description: 以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
exl-id: 27a6b012-576e-40bc-9b50-c310b3c56c9e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 5%

---

# 製作時疑難排解AEM{#troubleshooting-aem-when-authoring}

以下章節說明使用AEM時可能會遇到的一些問題，以及如何疑難排解的建議。

>[!NOTE]
>
>遇到問題時，也值得檢查您執行個體（發行版和服務套件）的[已知問題](/help/release-notes/known-issues.md)清單。

>[!NOTE]
>
>擁有管理員權限且想要疑難排解AEM問題的使用者，可使用[疑難排解AEM（管理員適用）](/help/sites-administering/troubleshoot.md)中所述的疑難排解方法。 如果您沒有足夠的權限，請向系統管理員洽詢疑難排解AEM。

## 已發佈網站上仍舊有的頁面版本{#old-page-version-still-on-published-site}

* **問題**:

   * 您已對頁面進行變更，並將頁面複製到發佈網站，但頁面的&#x200B;*old*&#x200B;版本仍顯示在發佈網站上。

* **原因**:

   * 這可能有數個原因，通常是快取（您的本機瀏覽器或Dispatcher），但有時可能是復寫佇列的問題。

* **解決方案**:

   * 這裡有各種可能性：
   * 確認頁面已正確復寫。 檢查頁面狀態，並在必要時檢查復寫佇列的狀態。
   * 清除本機瀏覽器中的快取，並再次存取您的頁面。
   * 將`?`新增至頁面URL的結尾。 例如：

      `http://localhost:4502/sites.html/content?`

      這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果複製隊列出現問題，請與系統管理員聯繫。

## Sidekick不可見{#sidekick-not-visible}

* **問題**:

   * 在製作環境上編輯內容頁面時，Sidekick不可見。

* **原因**:

   * 在少數情況下，您可能會將側腳的標題置於當前窗口的範圍之外。 這表示您無法重新定位。

* **解決方案**:

   * 從您目前的工作階段登出，然後重新登入。 Sidekick將返回預設位置。

## 查找和替換 — 並非所有實例都被替換{#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 使用&#x200B;**Find &amp; Replace**&#x200B;選項時，並非所有`find`詞語的例項都會在頁面上取代。

* **原因**:

   * **尋找和取代**&#x200B;的功能取決於內容的儲存方式，以及是否可以搜尋內容。 例如，部落格文本儲存在未配置為搜索的`jcr:text`屬性中。 查找和替換servlet的預設範圍涵蓋以下屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**:

   * 可使用&#x200B;**Web控制台**&#x200B;的&#x200B;**Day CQ WCM查找替換Servlet**&#x200B;配置更改這些定義；例如，在

      `http://localhost:4502/system/console/configMgr`
