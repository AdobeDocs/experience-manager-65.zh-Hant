---
title: 社區元件的客戶端
seo-title: Clientlibs for Communities Components
description: 社區的客戶端庫
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

# 社區元件的客戶端 {#clientlibs-for-communities-components}

## 簡介 {#introduction}

文檔的本節介紹如何將客戶端庫（客戶端庫）添加到社區元件的頁面。

有關基本資訊，請訪問：

* [使用客戶端庫](/help/sites-developing/clientlibs.md) 提供使用詳細資訊以及調試工具
* [SCF的客戶端](/help/communities/client-customize.md#clientlibs) 在定制SCF元件時提供有用資訊


## 為什麼需要客戶端 {#why-clientlibs-are-required}

要正確運行元件(JavaScript)和樣式(CSS)，需要客戶端。

當存在 [社區功能](/help/communities/functions.md) 對於功能，所有必要的元件和配置（包括所需的客戶端）都將出現在社區站點中。 只有在作者可以使用其他元件時，才需要添加其他客戶端。

當缺少所需的客戶端時， [將社區元件添加到頁面](/help/communities/author-communities.md) 可能導致javascript錯誤和意外外觀。

### 示例：無客戶端的已置評 {#example-placed-reviews-without-clientlibs}

![置評](assets/placed-reviews.png)

### 示例：與客戶端一起進行的審閱 {#example-placed-reviews-with-clientlibs}

![審閱客戶端](assets/reviews-clientlibs.png)

## 確定所需的客戶端 {#identifying-required-clientlibs}

開發人員的基本功能資訊標識所需的客戶端。

此外，從實AEM例瀏覽到 [社區元件指南](/help/communities/components-guide.md) 提供對元件所需的客戶端庫類別清單的訪問。

例如，在 [「審閱」頁](https://localhost:4502/content/community-components/en/reviews.html) 列出的所需客戶端

* cq.ckeditor
* cq.social.hbs.reviews

![客戶端評論](assets/clientlibs-reviews.png)

## 添加所需客戶端 {#adding-required-clientlibs}

當需要將社區元件添加到頁面時，如果元件尚未出現，則需要為其添加所需的客戶端。

使用 [CRXDE|Lite](#using-crxde-lite) 修改社區網站頁的現有客戶端libslist。

為社區站點添加客戶端庫 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 瀏覽到 [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)。
* 查找 `clientlibslist` 要添加元件的頁面的節點：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* 與 `clientlibslist` 選定的節點：

   * 查找字串[] 屬性 `scg:requiredClientLibs`。
   * 選擇其 `Value` 訪問「字串陣列」對話框。

      * 如有必要，向下滾動。
      * 選擇+以輸入新的客戶端庫。

         * 重複以添加更多客戶端庫。

         * 選擇 **確定**。
   * 選擇 **全部保存**。


>[!NOTE]
>
>如果站點不是社區站點，則需要發現用於該站點的客戶端庫的存在或位置。

使用 [AEM Communities入門](/help/communities/getting-started.md) 示例，其中 `site-name` 是 *參與*，這是添加審閱元件時客戶端liblist的顯示方式：

![審閱元件](assets/review-component.png)
