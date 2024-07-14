---
title: 適用於社群元件的Clientlibs
description: 瞭解如何將使用者端程式庫(clientlibs)新增至頁面，以便收集使用情況詳細資訊，並將偵錯工具用於Communities元件。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# 適用於社群元件的Clientlibs {#clientlibs-for-communities-components}

## 簡介 {#introduction}

本檔案章節說明如何將使用者端程式庫(clientlibs)新增到Communities元件的頁面。

如需基本資訊，請參閱下列內容：

* [使用提供使用詳細資訊和偵錯工具的使用者端資料庫](/help/sites-developing/clientlibs.md)
* SCF的[Clientlibs](/help/communities/client-customize.md#clientlibs)提供自訂SCF元件時有用的資訊


## 為何需要Clientlibs {#why-clientlibs-are-required}

元件的正常功能(JavaScript)和樣式(CSS)需要Clientlibs。

當功能有[社群功能](/help/communities/functions.md)時，所有必要的元件和設定（包括必要的clientlibs）都會出現在社群網站中。 只有當作者可以使用其他元件時，才能新增其他clientlibs。

當缺少必要的clientlibs時，[將Communities元件新增至頁面](/help/communities/author-communities.md)可能會導致JavaScript錯誤和意外外觀。

### 範例：不含Clientlibs的置入稽核 {#example-placed-reviews-without-clientlibs}

![置入的評論](assets/placed-reviews.png)

### 範例：使用Clientlibs置入的評論 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 識別必要的Clientlibs {#identifying-required-clientlibs}

開發人員的基本功能資訊可識別所需的clientlibs。

此外，從AEM執行個體瀏覽至[社群元件指南](/help/communities/components-guide.md)可存取元件所需的clientlib類別清單。

例如，在[檢閱頁面](https://localhost:4502/content/community-components/en/reviews.html)頂端列出的必要clientlibs包括

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 新增必要的Clientlibs {#adding-required-clientlibs}

當想要將Communities元件新增至頁面時，必須為該元件新增必要的clientlibs （如果尚未存在）。

使用[CRXDE|Lite](#using-crxde-lite)修改社群網站頁面的現有clientlibslist。

若要使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)為社群網站新增clientlib：

* 瀏覽至[https://&lt;server>：&lt;port>/crx/de](https://localhost:4502/crx/de)。
* 找到您要新增元件的頁面的`clientlibslist`節點：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 已選取`clientlibslist`節點：

   * 找出字串[]屬性`scg:requiredClientLibs`。
   * 選取其`Value`，以便存取字串陣列對話方塊。

      * 如有需要，向下捲動。
      * 選取+以輸入新的使用者端資源庫。

         * 重複以上步驟以新增更多使用者端程式庫。

         * 選取&#x200B;**確定**。

   * 選取&#x200B;**全部儲存**。

>[!NOTE]
>
>如果網站不是社群網站，則必須探索網站所使用的使用者端程式庫的存在或位置。

使用[AEM Communities快速入門](/help/communities/getting-started.md)範例（其中`site-name`為&#x200B;*engage*），新增檢閱元件時會以此方式顯示clientliblist：

![檢閱元件](assets/review-component.png)
