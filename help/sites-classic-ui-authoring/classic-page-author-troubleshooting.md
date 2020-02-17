---
title: 編寫時疑難排解AEM
seo-title: 編寫時疑難排解AEM
description: 下節涵蓋您使用AEM時可能遇到的一些問題，以及如何疑難排解的建議。
seo-description: 下節涵蓋您使用AEM時可能遇到的一些問題，以及如何疑難排解的建議。
uuid: eb95e5ba-1eed-4ffb-80c1-9b8468820c22
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 9b492b17-9029-46ae-9dc0-bb21e6b484df
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 編寫時疑難排解AEM{#troubleshooting-aem-when-authoring}

下節涵蓋您使用AEM時可能遇到的一些問題，以及如何疑難排解的建議。

>[!NOTE]
>
>當遇到問題時，也有必要檢查實例( [發行版和服務包](/help/release-notes/known-issues.md) )的已知問題清單。

>[!NOTE]
>
>具有管理員權限且想要疑難排解AEM問題的使用者，可以使用疑難排解AEM（適用於管理員）中 [所述的疑難排解方法](/help/sites-administering/troubleshoot.md)。 如果您沒有足夠的權限，請洽詢您的系統管理員有關疑難排解AEM的資訊。

## 舊頁面版本仍在發佈網站上 {#old-page-version-still-on-published-site}

* **問題**:

   * 您已變更頁面並將頁面複製至發佈網站，但 *舊版* 「頁面」仍會顯示在發佈網站上。

* **原因**:

   * 這可能有幾種原因，最常是快取（本地瀏覽器或Dispatcher），但有時可能是複製隊列的問題。

* **解決方案**:

   * 這裡有各種可能：
   * 確認頁面已正確複製。 檢查頁狀態以及複製隊列的狀態（如果需要）。
   * 清除本機瀏覽器中的快取，並再次存取您的頁面。
   * 新 `?` 增至頁面URL的結尾。 例如：

      `http://localhost:4502/sites.html/content?`

      這會直接從AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果複製隊列存在問題，請與系統管理員聯繫。

## Sidekick不可見 {#sidekick-not-visible}

* **問題**:

   * 在作者環境中編輯內容頁面時，Sidekick不可見。

* **原因**:

   * 在少數情況下，您可能會將側腳的標題定位在目前視窗的範圍之外。 這表示您不能再重新定位它。

* **解決方案**:

   * 從您目前的工作階段登出，然後重新登入。 Sidekick會返回預設位置。

## 查找和替換——並非所有實例都被替換 {#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 使用「尋 **找與取代** 」選項時，並非頁面上所有的 `find` 詞語例項都會被取代。

* **原因**:

   * 「尋找與取 **代」的功能** ，取決於內容的儲存方式，以及是否可加以搜尋。 例如，部落格文字會儲存在屬 `jcr:text` 性中，該屬性未設定為可供搜尋。 查找和替換servlet的預設範圍涵蓋以下屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**:

   * 這些定義可以通過Day CQ WCM的配 **置進行更改，Find Replace Servlet** using **Web Console**;例如，在

      `http://localhost:4502/system/console/configMgr`

