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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Clientlibs for Communities元件{#clientlibs-for-communities-components}

## 簡介 {#introduction}

本檔案章節說明如何新增用戶端程式庫(clientlibs)至Communities元件的頁面。

如需基本資訊，請造訪：

* [使用用戶端程式庫](/help/sites-developing/clientlibs.md) ，提供使用詳細資訊以及除錯工具
* [用於SCF的Clientlibs](/help/communities/client-customize.md#clientlibs) ，它在定制SCF元件時提供有用的資訊
* [部落格：AEM Client Libraries（由範例說明）](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## 為何需要Clientlibs {#why-clientlibs-are-required}

Clientlibs是元件正確運作(JavaScript)和樣式(CSS)的必要條件。

當功能有社 [群功能](/help/communities/functions.md) ，所有必要的元件和組態（包括必要的clientlibs）都會出現在社群網站中。 只有當作者需要使用其他元件時，才需要新增其他clientlib。

當所需的clientlibs遺失時， [將Communities元件新增至頁面](/help/communities/author-communities.md) ，可能會導致javascript錯誤以及意外的外觀。

### 範例：未使用Clientlibs的置入審核 {#example-placed-reviews-without-clientlibs}

![chlimage_1-132](assets/chlimage_1-132.png)

### 範例：使用Clientlibs進行置入的審核 {#example-placed-reviews-with-clientlibs}

![chlimage_1-133](assets/chlimage_1-133.png)

## 識別所需的客戶端 {#identifying-required-clientlibs}

開發人員的基本功能資訊可識別所需的用戶端。

此外，從AEM例項瀏覽至「社群元件指南」 [](/help/communities/components-guide.md) ，可存取元件所需的clientlib類別清單。

例如，在「檢閱」頁面的最上 [方](https://localhost:4502/content/community-components/en/reviews.html) ，會列出必要的clientlib

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-134](assets/chlimage_1-134.png)

## 添加必需的客戶端 {#adding-required-clientlibs}

當需要將Communities元件新增至頁面時，如果元件尚未出現，則必須新增必要的clientlibs。

使 [用CRXDE|Lite](#using-crxde-lite) ，修改社群網站頁面的現有clientlibslist。

要使用 [CRXDE Lite為社區站點添加clientlib](/help/sites-developing/developing-with-crxde-lite.md) :

* 瀏覽 [至https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* 找到 `clientlibslist` 要在其中添加元件的頁面的節點

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 已選 `clientlibslist` 取節點

   * 查找String[] 屬性 `scg:requiredClientLibs`
   * 選擇其 `Value` 以訪問「字串陣列」對話框

      * 必要時向下捲動
      * 選擇+以輸入新的客戶端庫

         * 重複添加更多客戶端庫
      * 選擇**確定**
   * 選擇「 **全部保存」**



>[!NOTE]
>
>如果網站不是社群網站，則需要搜尋網站所用用戶端程式庫的存在或位置。

使用「 [AEM Communities快速入門](/help/communities/getting-started.md) 」範例(其中 `site-name` 為Engage **)，在新增審核元件時，clientliblist會以下列方式顯示：

![chlimage_1-135](assets/chlimage_1-135.png)

