---
title: Communities元件的Clientlibs
seo-title: Communities元件的Clientlibs
description: 社群的用戶端程式庫
seo-description: 社群的用戶端程式庫
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Communities元件的Clientlibs {#clientlibs-for-communities-components}

## 簡介 {#introduction}

本檔案的本節說明如何將用戶端程式庫(clientlibs)新增至Communities元件的頁面。

如需基本資訊，請造訪：

* [使用用戶端程式](/help/sites-developing/clientlibs.md) 庫（提供使用情況詳細資訊及除錯工具）
* [SCF的客戶端](/help/communities/client-customize.md#clientlibs) 庫，在定制SCF元件時提供有用的資訊


## 為何需要Clientlibs {#why-clientlibs-are-required}

元件的正常運作(JavaScript)和樣式(CSS)需要Clientlibs。

當功能有[社群函式](/help/communities/functions.md)時，所有必要的元件和設定（包括必要的clientlib）都會出現在社群網站中。 只有當作者能使用其他元件時，才需要新增其他clientlib。

當缺少所需的clientlib時，[將Communities元件新增至頁面](/help/communities/author-communities.md)可能會導致javascript錯誤以及意外的外觀。

### 範例：未使用Clientlibs的置入評論 {#example-placed-reviews-without-clientlibs}

![置入審核](assets/placed-reviews.png)

### 範例：使用Clientlibs進行置入的審核 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 識別所需的Clientlib {#identifying-required-clientlibs}

開發人員的基本功能資訊可識別所需的用戶端。

此外，從AEM實例瀏覽到[Community Components Guide](/help/communities/components-guide.md)，可以訪問元件所需的clientlib類別清單。

例如，在[「檢閱」頁面](https://localhost:4502/content/community-components/en/reviews.html)的最上方，列出必要的clientlib

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 新增必要的Clientlib {#adding-required-clientlibs}

需要將Communities元件新增至頁面時，必須為元件新增所需的clientlib（如果尚未出現）。

使用[CRXDE|Lite](#using-crxde-lite)修改社群網站頁面的現有clientlibslist。

要使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)為社區站點添加clientlib，請執行以下操作：

* 瀏覽至[https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)。
* 找出您要新增元件之頁面的`clientlibslist`節點：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 已選擇`clientlibslist`節點：

   * 找到String[]屬性`scg:requiredClientLibs`。
   * 選擇其`Value`以訪問字串陣列對話框。

      * 如有必要，向下捲動。
      * 選擇+以輸入新的客戶端庫。

         * 重複以新增更多用戶端程式庫。

         * 選擇&#x200B;**OK**。
   * 選擇&#x200B;**保存全部**。


>[!NOTE]
>
>如果網站不是社群網站，則需要探索用於網站的用戶端程式庫的存在或位置。

使用[AEM Communities](/help/communities/getting-started.md)快速入門範例（其中`site-name`為&#x200B;*engage*），新增審核元件時，clientliblist會如下所示：

![檢閱元件](assets/review-component.png)
