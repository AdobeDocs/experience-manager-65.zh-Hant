---
title: 使用Edge Delivery Services
description: 使用Edge Delivery Services
source-git-commit: 0c0e14ec3d022b7e9efd17edf2997990f5ac3dc2
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# 使用Edge Delivery Services {#usingedge}

有了Edge Delivery，您可以建立快速開發環境，讓作者能夠快速更新及發佈內容，並快速啟動新網站。 為此，您可以在相同網站上使用多個內容來源，無論您選擇什麼來源，發佈作業都會順暢且有效簡化。 因此，從編輯到在網際網路上即時檢視內容，只需要幾秒鐘的時間。

## 編寫 {#authoring-edge}

有了Edge Delivery，製作過程便捷、快速、靈活。 您可以在Edge Delivery Services的上下文中採用兩個不同的編寫路徑：

* 檔案式撰寫(例如Microsoft Word或Google Docs) - [如需詳細資訊，請參閱此連結](https://www.hlx.live/docs/authoring).
* 頁面編輯器/通用編輯器 — 請聯絡您的Adobe銷售代表。

若是檔案式撰寫，您可以使用各種來源，例如Microsoft Word和Google Docs。 來自這些來源的檔案會成為您網站上的頁面。 標題、清單、影像、字型元素和視訊都可從初始來源傳輸至您的網站。 您可以新增中繼資料以用於SEO目的，或使用區塊來搭配結構化內容並新增功能。

## 發佈 {#publishing-edge}

有了Edge Delivery，無論內容來源為何，發佈內容都能順暢無礙。 程式如下：您使用 [sidekick延伸模組](#using-sidekick) 以觸發發佈機制，您的內容將於數秒後於您的網站上線。

## Edge Delivery Services和GitHub {#github-edge}

Edge Delivery運用GitHub，讓客戶可直接從GitHub存放庫管理和部署程式碼。 例如，您可以在Google檔案或Microsoft Word中撰寫內容，並在GitHub中使用CSS和JavaScript開發網站功能。 系統會自動為您從內容預覽到生產環境的每個分支建立網站。 您放入GitHub存放庫中的每個資源都可在您的網站上取得，無需建置程式。

## 使用Sidekick {#using-sidekick}

AEM Sidekick提供上下文感知選項的工具列，讓您可輕鬆編輯、預覽和發佈內容。 晚於 [安裝](https://www.hlx.live/docs/sidekick-extension) AEM sidekick擴充功能可用於專案環境或編輯內容時(例如，在Google檔案中)。 視環境而定，它有數個可用的動作，例如：預覽、重新載入、編輯和發佈。 在使用Sidekick時，您也可以將環境從預覽切換到生產，反之亦然。

**若要發佈**，在預覽頁面上開啟Sidekick並使用Publish動作。 在您按一下「發佈」後，即可在即時和生產環境中使用頁面的目前預覽版本。

## 將AEM Assets與檔案式製作整合 {#integrate-assets-edge}

「邊緣傳送」可讓您在Microsoft Word或Google檔案中編寫檔案時，使用AEM Assets存放庫中的可用影像。

若要在檔案中使用影像，必須滿足以下條件 [設定AEM Assets sidekick外掛程式](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin).

適用於AEM Assets的sidekick外掛程式支援對以下專案的存取：

* AEM Assets as a Cloud Service 

* AEM Assets Essentials

設定AEM Assets Sidekick外掛程式後，您可以 [開始在Google檔案或Microsoft Word檔案中使用影像](https://www.hlx.live/docs/aem-assets-sidekick-plugin).

## 進一步閱讀 {#further-reading}

如需詳細資訊，請參閱下列頁面：

* 如需開始使用Edge Delivery的詳細資訊，請參閱 [建置](https://www.hlx.live/docs/#build) Edge傳遞檔案的區段。
* 若要瞭解如何使用Edge Delivery製作和發佈內容，請參閱 [發佈區段](https://www.hlx.live/docs/authoring).
* 若要瞭解如何使用sidekick擴充功能，請參閱 [使用sidekick](https://www.hlx.live/docs/sidekick) 頁面。
* 如需AEM編寫的相關資訊，請參閱 [製作概念頁面](/help/sites-authoring/author.md))
