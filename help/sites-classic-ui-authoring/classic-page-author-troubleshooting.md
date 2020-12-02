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
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 5%

---


# 疑難排解編寫AEM{#troubleshooting-aem-when-authoring}

下節涵蓋您使用AEM時可能遇到的一些問題，以及如何疑難排解的建議。

>[!NOTE]
>
>當遇到問題時，也有必要檢查實例（發行和服務包）的[已知問題](/help/release-notes/known-issues.md)清單。

>[!NOTE]
>
>具有管理員權限且想要疑難排解AEM問題的使用者，可使用[疑難排解AEM（適用於管理員）](/help/sites-administering/troubleshoot.md)中所述的疑難排解方法。 如果您沒有足夠的權限，請洽詢您的系統管理員有關疑難排解AEM的資訊。

## 已發佈網站{#old-page-version-still-on-published-site}上仍有舊版頁面

* **問題**:

   * 您已對頁面進行變更，並將頁面複製至發佈網站，但是頁面的&#x200B;*old*&#x200B;版本仍會顯示在發佈網站上。

* **原因**:

   * 這可能有幾種原因，最常是快取（本地瀏覽器或Dispatcher），但有時可能是複製隊列的問題。

* **解決方案**:

   * 這裡有各種可能：
   * 確認頁面已正確複製。 檢查頁狀態以及複製隊列的狀態（如果需要）。
   * 清除本機瀏覽器中的快取，並再次存取您的頁面。
   * 將`?`新增至頁面URL的結尾。 例如：

      `http://localhost:4502/sites.html/content?`

      這會直接從AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果複製隊列存在問題，請與系統管理員聯繫。

## Sidekick not visible {#sidekick-not-visible}

* **問題**:

   * 在作者環境中編輯內容頁面時，Sidekick不可見。

* **原因**:

   * 在少數情況下，您可能會將側腳的標題定位在目前視窗的範圍之外。 這表示您不能再重新定位它。

* **解決方案**:

   * 從您目前的工作階段登出，然後重新登入。 Sidekick會返回預設位置。

## 查找和替換——並非所有實例都被替換{#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 使用&#x200B;**尋找與取代**&#x200B;選項時，並非頁面上所有`find`詞語的例項都會被取代。

* **原因**:

   * **尋找與取代**&#x200B;的功能取決於內容的儲存方式，以及是否可加以搜尋。 例如，部落格文字會儲存在`jcr:text`屬性中，而未設定為可供搜尋。 查找和替換servlet的預設範圍涵蓋以下屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**:

   * 這些定義可以使用&#x200B;**Web控制台**&#x200B;的&#x200B;**Day CQ WCM查找替換Servlet**&#x200B;的配置進行更改；例如，在

      `http://localhost:4502/system/console/configMgr`

