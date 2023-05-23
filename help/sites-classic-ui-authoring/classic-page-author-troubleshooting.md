---
title: 創作時AEM故障排除
description: 以下部分介紹在使用時可能遇到的一些問題AEM，以及有關如何解決這些問題的建議。
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

# 創作時AEM故障排除{#troubleshooting-aem-when-authoring}

以下部分介紹在使用時可能遇到的一些問題AEM，以及有關如何解決這些問題的建議。

>[!NOTE]
>
>當遇到問題時，也值得檢查 [已知問題](/help/release-notes/release-notes.md) 例如（發行版和服務包）。

>[!NOTE]
>
>具有管理員權限和想要解決問題的用戶AEM可以使用中介紹的故障排除方法 [故障排除AEM（適用於管理員）](/help/sites-administering/troubleshoot.md)。 如果您沒有足夠的權限，請與系統管理員聯繫以瞭解故障排AEM除。

## 舊頁面版本仍位於已發佈站點上 {#old-page-version-still-on-published-site}

* **問題**:

   * 您已對頁面進行了更改並將頁面複製到發佈站點，但 *老* 該頁面的版本仍顯示在發佈網站上。

* **原因**:

   * 這可能有幾種原因，最常是快取（本地瀏覽器或Dispatcher），但有時可能是複製隊列的問題。

* **解決方案**:

   * 這裡有各種可能：
   * 確認已正確複製該頁。 檢查頁狀態以及複製隊列的狀態（如有必要）。
   * 清除本地瀏覽器中的快取，然後再次訪問頁面。
   * 添加 `?` 到 例如：

      `http://localhost:4502/sites.html/content?`

      這將直接從Dispatcher請求AEM該頁並繞過該Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。

   * 如果複製隊列有問題，請與系統管理員聯繫。

## 旁踢不可見 {#sidekick-not-visible}

* **問題**:

   * 在作者環境中編輯內容頁面時，Sidekick不可見。

* **原因**:

   * 在少數情況下，您可能已將副腳的標題置於當前窗口範圍之外。 這表示您不能再將其重新定位。

* **解決方案**:

   * 從當前會話註銷並重新登錄。 Sidekick將返回預設位置。

## 查找和替換 — 並非所有實例都被替換 {#find-replace-not-all-instances-are-replaced}

* **問題:**

   * 使用 **查找和替換** 選項，並非所有實例 `find` 在頁面上替換術語。

* **原因**:

   * 功能 **查找和替換** 取決於內容的保存方式，以及是否可以搜索內容。 例如，日誌文本儲存在 `jcr:text` 未配置為搜索的屬性。 查找和替換servlet的預設範圍包括以下屬性：

      * `jcr:title`
      * `jcr:description`
      * `jcr:text`
      * `text`

* **解決方案**:

   * 這些定義可以與 **第CQ WCM天查找替換Servlet** 使用 **Web控制台**;例如，在

      `http://localhost:4502/system/console/configMgr`
