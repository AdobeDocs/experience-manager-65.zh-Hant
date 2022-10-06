---
title: Communities元件的Clientlibs
seo-title: Clientlibs for Communities Components
description: 社群的用戶端程式庫
seo-description: Client-side libraries for Communities
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
source-wordcount: '382'
ht-degree: 0%

---

# Communities元件的Clientlibs {#clientlibs-for-communities-components}

## 簡介 {#introduction}

本檔案的本節說明如何將用戶端程式庫(clientlibs)新增至Communities元件的頁面。

如需基本資訊，請造訪：

* [使用用戶端程式庫](/help/sites-developing/clientlibs.md) 提供使用詳情和調試工具
* [SCF的Clientlibs](/help/communities/client-customize.md#clientlibs) 在定制SCF元件時提供有用資訊


## 為何需要Clientlibs {#why-clientlibs-are-required}

元件的正常運作(JavaScript)和樣式(CSS)需要Clientlibs。

當存在 [社群功能](/help/communities/functions.md) 針對功能，所有必要的元件和設定（包括必要的clientlib）都會顯示在社群網站中。 只有當作者能使用其他元件時，才需要新增其他clientlib。

缺少所需的clientlib時， [將社群元件新增至頁面](/help/communities/author-communities.md) 可能會導致javascript錯誤和意外的外觀。

### 範例：未使用Clientlibs的置入評論 {#example-placed-reviews-without-clientlibs}

![置入審核](assets/placed-reviews.png)

### 範例：使用Clientlibs進行置入的審核 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 識別所需的Clientlib {#identifying-required-clientlibs}

開發人員的基本功能資訊可識別所需的用戶端。

此外，從AEM例項瀏覽至 [社群元件指南](/help/communities/components-guide.md) 提供對元件所需的clientlib類別清單的訪問。

例如，在 [審核頁面](https://localhost:4502/content/community-components/en/reviews.html) 列出的必要clientlib為

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 新增必要的Clientlib {#adding-required-clientlibs}

需要將Communities元件新增至頁面時，必須為元件新增所需的clientlib（如果尚未出現）。

使用 [CRXDE|Lite](#using-crxde-lite) 修改社區站點頁的現有clientlibslist。

為社區站點添加clientlib：使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 瀏覽至 [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* 找出 `clientlibslist` 節點，用於要添加元件的頁面：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 使用 `clientlibslist` 已選節點：

   * 找出字串[] 屬性 `scg:requiredClientLibs`.
   * 選取其 `Value` 以訪問「字串陣列」對話框。

      * 如有必要，向下捲動。
      * 選擇+以輸入新的客戶端庫。

         * 重複以新增更多用戶端程式庫。

         * 選擇 **確定**.
   * 選擇 **全部儲存**.


>[!NOTE]
>
>如果網站不是社群網站，則需要探索用於網站的用戶端程式庫的存在或位置。

使用 [開始使用AEM Communities](/help/communities/getting-started.md) 範例，其中 `site-name` is *參與*，新增reviews元件時，此為clientliblist的顯示方式：

![檢閱元件](assets/review-component.png)
