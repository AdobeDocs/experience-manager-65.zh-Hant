---
title: 在中創作時排除故AEM障
description: 使用時可能遇到的一些問AEM題。
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 8%

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

      * `http://localhost:4502/sites.html/content?`
      * 這將直接從Dispatcher請求AEM該頁並繞過該Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果複製隊列有問題，請與系統管理員聯繫。


## 工具欄上不可見的元件操作 {#component-actions-not-visible-on-toolbar}

* **問題**:

   * 在作者環境上編輯內容頁面時，所有適用的元件操作都不可見。

* **原因**:

   * 在少數情況下，先前的操作可能會影響工具欄。

* **解決方案**:

   * 刷新頁面。
