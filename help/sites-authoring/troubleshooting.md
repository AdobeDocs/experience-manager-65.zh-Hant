---
title: 編寫時疑難排解AEM
seo-title: 編寫時疑難排解AEM
description: 使用AEM時可能會遇到的一些問題
seo-description: 使用AEM時可能會遇到的一些問題
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
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

      * `http://localhost:4502/sites.html/content?`
      * 這會直接從AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果複製隊列存在問題，請與系統管理員聯繫。


## 工具欄上不顯示元件操作 {#component-actions-not-visible-on-toolbar}

* **問題**:

   * 在作者環境中編輯內容頁面時，不會顯示完整的適用元件動作。

* **原因**:

   * 在少數情況下，先前的動作可能會影響工具列。

* **解決方案**:

   * 重新整理頁面。

