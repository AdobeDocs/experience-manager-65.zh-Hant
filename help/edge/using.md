---
title: 使用 Edge Delivery Services
description: 使用 Edge Delivery Services
exl-id: 6c9178b0-c8f3-4fc7-8614-8e71ffc2f0b8
solution: Experience Manager, Experience Manager Assets
feature: Edge Delivery Services
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 95%

---

# 使用 Edge Delivery Services {#usingedge}

Edge Delivery 能讓您建立快速開發的環境，作者可以在其中快速更新和發佈內容，並且可以快速啟動新網站。為此，您可以在同一網站上使用多個內容來源，並且無論您選擇何種來源，都可採用無縫且簡化的方式來發佈。因此，從編輯到在網路上查看內容只需幾秒鐘。

## 編寫 {#authoring-edge}

透過 Edge Delivery，編寫變得簡單、快速且靈活。您可以在 Edge Delivery Services 的環境中採用兩種不同的路徑進行編寫：

* 以文件為主的編寫 (例如 Microsoft Word 或 Google Docs) - [請參考此連結以了解更多詳情](https://www.hlx.live/docs/authoring)。
* 頁面編輯器/Universal Editor - 請聯絡您的 Adobe 銷售代表。

如果有檔案式撰寫，您可以使用各種來源，例如Microsoft Word和Google Docs。 來自這些來源的文件會成為您網站上的頁面。標題、清單、影像、字體元素、影片都可以從初始來源傳輸到您的網站。您可以為 SEO 目的新增中繼資料，或者使用塊處理結構化內容並新增功能。

## 發佈 {#publishing-edge}

使用 Edge Delivery 時，無論內容來源為何，都可以無縫發佈內容。程序如下：您使用 [Sidekick 擴充功能](#using-sidekick)來觸發發佈機制，您的內容幾秒鐘內將出現在您的網站上。

## Edge Delivery Services 和 GitHub {#github-edge}

Edge Delivery 使用 GitHub，因此客戶可以直接從其 GitHub 存放庫管理和部署程式碼。例如，您可以在 Google Docs 或 Microsoft Word 中編寫內容，並使用 GitHub 中的 CSS 和 JavaScript 開發網站功能。系統會自動為您的每個分部建立網站，從內容預覽到生產都包括在內。您放入 GitHub 存放庫的每個資源都可以在您的網站上使用，無需任何建置程序。

## 使用 Sidekick {#using-sidekick}

AEM sidekick 提供一個有感知選項的工具列，讓您可以輕鬆編輯、預覽和發佈內容。[安裝](https://www.hlx.live/docs/sidekick-extension) AEM sidekick 擴充功能後，可以在專案環境中或編輯內容時使用 (例如，在 Google Docs 中)。根據環境的不同，此工具有多種可用操作，例如：預覽、重新載入、編輯和發佈。您也可以在使用 Sidekick 時切換環境，從預覽切換到生產，反之亦然。

**若要發佈**，在預覽頁面上開啟 Sidekick 並使用「發佈」操作。按一下「發佈」後，目前的頁面預覽版本將可供您在即時和生產環境中使用。

## 將 AEM Assets 與文件型撰寫整合 {#integrate-assets-edge}

當您在 Microsoft Word 或 Google Docs 中編寫文件時，Edge Delivery 可讓您使用 AEM Assets 存放庫內的可用影像。

只有在[設定 AEM Assets Sidekick 外掛程式](https://www.hlx.live/developer/configuring-aem-assets-sidekick-plugin)後，系統才會提供使用文件中影像的選項。

AEM Assets 的 Sidekick 外掛程式支援存取：

* AEM Assets as a Cloud Service 

* AEM Assets Essentials

設定 AEM Assets Sidekick 插件後，您可以[開始在 Google Docs 或 Microsoft Word 文件中使用影像](https://www.hlx.live/docs/aem-assets-sidekick-plugin)。

## 延伸閱讀： {#further-reading}

有關更多詳細資訊，請參閱以下頁面：

* 有關如何開始使用 Edge Delivery 詳細資訊，請參閱 Edge Delivery 文件中的「[建置](https://www.hlx.live/docs/#build)」部份。 
* 若要了解如何使用 Edge Delivery 編寫和發佈內容，請參閱[「發佈」部份](https://www.hlx.live/docs/authoring)。
* 若要了解如何使用 Sidekick 擴充功能，請參閱「[使用 Sidekick](https://www.hlx.live/docs/sidekick)」頁面。
* 如需AEM編寫的相關資訊，請參閱 [製作概念頁面](/help/sites-authoring/author.md))
