---
title: We.Retail Reference實施
seo-title: We.Retail Reference Implementation
description: We.Retail是參考實施的技術預覽，它展示了通過We.Retail
seo-description: We.Retail is a technology preview of a reference implementation that illustrates the recommended way of setting up an online presence with AEM
uuid: d8833192-b592-4812-bf9b-bd882e8ee7f0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: f50150af-deff-4c29-bfe0-1cfc67b29d51
exl-id: 504c61c7-dcd3-412c-9239-d24a2b78e4b9
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 8%

---

# We.Retail Reference實施{#we-retail-reference-implementation}

## 簡介 {#introduction}

We.Retail是一個參考實施和示例內容，它展示了與Adobe Experience Manager建立線上聯繫的推薦方式。

We.Retail利用最新技術，AEM如HTL、響應式佈局、可編輯模板、核心元件等。

雖然它說明了零售垂直，但站點的設定方式可以應用於任何垂直，並且只有產品目錄和購物車功能是特定於零售的。

## 功能 {#features}

作AEM為標準參考實施，We.Retail展示了一些最強大的功AEM能。

| **功能** | **說明** | **有興趣嗎？** |
|---|---|---|
| [全球化網站結構](/help/sites-administering/tc-bp.md) | We.Retail包括即時複製到特定國家/地區站點的語言母版。 | [試試！](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [響應式佈局](/help/sites-authoring/responsive-layout.md) | 所有頁面都具有響應佈局以動態適應螢幕和設備大小。 | [試試！](/help/sites-developing/we-retail-responsive-layout.md) |
| [可編輯模板](/help/sites-developing/page-templates-editable.md) | 所有頁面都基於可編輯的模板，允許非開發人員調整和自定義模板。 | [試試！](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML 範本語言](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) | 所有元件均基於HTL |  |
| [電子商務能力](/help/commerce/cif-classic/developing/ecommerce.md) | 功能產品目錄 |  |
| [社區站點](/help/communities/overview.md) | 允許訪問者加入社區討論、閱讀部落格等 |  |
| [核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) | 所有元件都基於新的核心元件，而且更可用，用戶可配置的開箱即用 | [試試！](/help/sites-developing/we-retail-core-components.md) |
| [內容片段](/help/assets/content-fragments/content-fragments.md) | 「We.Retail Experiences」部分展示了通過內容片段重新使用內容的威力。 | [試試！](/help/sites-developing/we-retail-content-fragments.md) |
| [體驗片段](/help/sites-authoring/experience-fragments.md) | 體驗片段是由一個或多個元件組成的組，這些元件包括可在頁面中引用的內容和佈局。 | [試試！](/help/sites-developing/we-retail-experience-fragments.md) |

## 快速入門 {#getting-started}

We.Retail作為樣AEM本內容提供。 為了使用 [像AEM你平常一樣](/help/sites-deploying/deploy.md#getting-started)，確保未禁用示例內容。

>[!CAUTION]
>
>生產實例上不應安裝We.Retail。 應在中啟動生產實例 `nosamplecontent` [運行模式](/help/sites-deploying/configure-runmodes.md)。

>[!CAUTION]
>
>We.Retail基於最新技AEM術，因此不支援 [經典UI創作](/help/sites-classic-ui-authoring/home.md)。

### 最新版本 {#latest-version}

儘管We.Retail隨發行版一起AEM發佈，但內容及其功能的更新可能會在發佈後進行。 因此， [從GitHub下載最新版本](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) 然後 [上載](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) 和 [安裝](/help/sites-administering/package-manager.md#installing-packages) 作為實例上的AEM包。

### 第一步 {#first-steps}

1. 啟AEM動（和/或安裝We.Retail）後，站點 **We.Retail** 在 [站點控制台](/help/sites-authoring/basic-handling.md#global-navigation)。
1. 例如，可以開啟以下頁面，它應顯示為 [附錄](#appendix) 以下：

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## We.零售和Geometrixx {#we-retail-geometrixx}

Geometrixx及其許多化身在早期版本中充當樣AEM本。 自6.3版以來，We.Retail一直是隨附的示例內容，AEM並作為新的標準參考實施。

We.Retail在技術上更強大，利用最AEM新技術更靈活、更可擴展，同時還展示了產品的最新功能。

### 特徵比較 {#feature-comparison}

下表概述了We.Retail與Geometrixx相比的主要功能。

* **可用** 表示在示例內容中找到該功能的示例。
* **不可用** 表示該功能的示例在示例內容中不可用，但並不表示該功能本身不可用。

| **功能** | **We.Retail** | **Geometrixx** |
|---|---|---|
| 全球化網站結構 | 將語言大師即時複製到特定國家的站點 | 不可用 |
| 內容片段 | 可用 | 不可用 |
| 體驗片段 | 可用 | 不可用 |
| 回應式版面 | 所有頁面 | 僅Geometrixx Media |
| 可編輯的範本 | 所有頁面 | 不可用 |
| HTL | 所有元件 | 有限 |
| 定位 | 所有頁面 | 僅Geometrixx Outdoors |
| Screens | 可用 | 不可用 |
| 行動 | 不可用 | 可用 |
| 手稿 | 不可用 | 可用 |
| 旋轉木馬，下載，圖表元件 | 不可用 | 可用 |
| 列控制項 | 替換為佈局容器 | 可用 |
| Forms | 不可用 | 可用 |
| 行銷活動 | 沒有電子郵件示例 | 可用 |

>[!NOTE]
>
>這份清單力求完整，但不應被視為詳盡無遺。

## 貢獻 {#contribute}

We.Retail已作為開放原始碼項目發佈，最新版本的原始碼可從GitHub下載。

GITHUB代碼

可以在GitHub上找到此頁的代碼

* [在GitHub上開啟aem-sample-we-retail項目](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* 將項目下載為 [ZIP檔案](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/archive/master.zip)

最新版本也可以 [直接下載](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/latest) 作為可安裝的包。

如遇問題，請提交 [GitHub問題](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues)。

您可以隨意支付或與 [拉式請求](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)。

## 預覽 {#preview}

We.Retail歡迎頁面預覽：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
