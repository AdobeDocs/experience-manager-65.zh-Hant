---
title: 網站管理
seo-title: Website Administration
description: 瞭解如何在中管理多語言網AEM站。
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 4%

---

# 網站管理{#website-administration}

以下管理工具可用於管理網站和頁面：

* 多站點管理器(MSM)使您能夠在多個位置使用相同的站點內容，同時允許變化：

   * [重複使用內容：多網站管理員和 Live Copy](/help/sites-administering/msm.md)

* 翻譯允許您自動翻譯頁面內容、資產和用戶生成的內容，以建立和維護多語言網站：

   * [翻譯多語言網站的內容](/help/sites-administering/translation.md)

* 這兩個功能可以結合起來，以滿足同時兼有這兩個功能的網站 [多語種](#multinational-and-multilingual-sites)。

## 跨國和多語言站點 {#multinational-and-multilingual-sites}

您可以通過「多站點管理器」和翻譯工作流的組合使用，高效地為跨國和多語言站點建立內容。 以一種語言為特定國家（地區）建立主體站點，然後根據需要使用翻譯將該內容用作其他站點的基礎：

* [翻譯](/help/sites-administering/translation.md) 把主體網站翻譯成不同的語言。

* 使用 [多站點管理器](/help/sites-administering/msm.md) 至：

   * 重新使用主站點的內容和翻譯，為其他國家和文化建立站點。
   * 確保將多站點管理器的使用限制為使用一種語言的內容，例如，在國家/地區站點中使用英語母版 — >英語分支，在國家/地區站點使用法語母版 — >法語分支。
   * 如果需要，分離即時副本的元素以添加本地化詳細資訊。

下圖說明了主要概念如何相交（但不顯示涉及的所有級別/元素）:

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>在這種情況下，以及可比較的情況下，MSM不會管理這樣的不同語言版本。
>
>* [MSM](/help/sites-administering/msm.md) 管理在語言邊界內將已翻譯內容從藍圖（例如全局母版）部署到即時拷貝（例如本地站點）。
>* 的 [翻譯](/help/sites-administering/translation.md) 與第AEM三方翻譯管理服務一起管理這些語言並將內容翻譯成這些不同語言的整合能力。
>
>對於更高級的使用情形，MSM也可跨語言母版使用。

>[!NOTE]
>
>對於所有使用情形，建議閱讀以下最佳做法：
>
>* [MSM的最佳做法](/help/sites-administering/msm-best-practices.md);特別是：
   >
   >   * [建立網站](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM和多語言網站](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻譯最佳做法](/help/sites-administering/tc-bp.md)

