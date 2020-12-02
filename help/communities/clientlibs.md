---
title: Clientlibs for Communities元件
seo-title: Clientlibs for Communities元件
description: 社群的用戶端程式庫
seo-description: 社群的用戶端程式庫
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# Clientlibs for Communities Components {#clientlibs-for-communities-components}

## 簡介 {#introduction}

本檔案章節說明如何新增用戶端程式庫(clientlibs)至Communities元件的頁面。

如需基本資訊，請造訪：

* [使用用戶端程式](/help/sites-developing/clientlibs.md) 庫，提供使用詳細資訊以及除錯工具
* [SCF的Clientlib在定](/help/communities/client-customize.md#clientlibs) 制SCF元件時提供有用資訊
* [部落格：AEM Client Libraries（由範例說明）](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## 為何需要Clientlibs {#why-clientlibs-are-required}

Clientlibs是元件正確運作(JavaScript)和樣式(CSS)的必要條件。

當某個功能存在[社區函式](/help/communities/functions.md)時，所有必要的元件和配置（包括所需的clientlibs）都將出現在社區站點中。 只有當作者需要使用其他元件時，才需要新增其他clientlib。

當所需的clientlibs遺失時，[將Communities元件新增至頁面](/help/communities/author-communities.md)可能會導致javascript錯誤以及意外的外觀。

### 範例：未使用Clientlibs {#example-placed-reviews-without-clientlibs}的置入審核

![置入審核](assets/placed-reviews.png)

### 範例：Placed Reviews with Clientlibs {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 標識必需的Clientlibs {#identifying-required-clientlibs}

開發人員的基本功能資訊可識別所需的用戶端。

此外，從AEM例項瀏覽至[社群元件指南](/help/communities/components-guide.md)可存取元件所需的clientlib類別清單。

例如，在[「檢閱」頁面](https://localhost:4502/content/community-components/en/reviews.html)的最上方，會列出所需的clientlibs

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 添加必需的Clientlibs {#adding-required-clientlibs}

當需要將Communities元件新增至頁面時，如果元件尚未出現，則必須新增必要的clientlibs。

使用[CRXDE|Lite](#using-crxde-lite)修改社群網站頁面的現有clientlibslist。

要使用[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)為社區站點添加clientlib:

* 瀏覽至[https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)。
* 為要添加元件的頁找到`clientlibslist`節點：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 選擇`clientlibslist`節點後：

   * 找到String[]屬性`scg:requiredClientLibs`。
   * 選擇其`Value`以訪問「字串陣列」對話框。

      * 如有必要，向下捲動。
      * 選擇+以輸入新的客戶端庫。

         * 重複以新增更多用戶端程式庫。

         * 選擇&#x200B;**確定**。
   * 選擇&#x200B;**全部保存**。


>[!NOTE]
>
>如果網站不是社群網站，則需要搜尋網站所用用戶端程式庫的存在或位置。

使用[AEM Communities](/help/communities/getting-started.md)快速入門範例（其中`site-name`是&#x200B;*engage*），在新增審核元件時，clientliblist會以下列方式顯示：

![review-component](assets/review-component.png)

