---
title: 製作時疑難排解AEM
seo-title: Troubleshooting AEM when Authoring
description: 使用AEM時可能會遇到的一些問題
seo-description: Some issues that you might encounter when using AEM
uuid: 99af51ea-8628-4811-83f2-ab3f88f0279e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: da0a5644-2e1d-4394-a6aa-11bb41406ba6
exl-id: 05586b17-35d4-496e-8f0e-293c755eb066
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 8%

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

      * `http://localhost:4502/sites.html/content?`
      * 這會直接向AEM要求頁面，並略過Dispatcher。 如果您收到更新的頁面，表示您應清除Dispatcher快取。
   * 如果複製隊列出現問題，請與系統管理員聯繫。


## 工具列上看不到元件動作 {#component-actions-not-visible-on-toolbar}

* **問題**:

   * 在製作環境上編輯內容頁面時，不會顯示完整的適用元件動作。

* **原因**:

   * 在少數情況下，先前的動作可能會影響工具列。

* **解決方案**:

   * 重新整理頁面。
