---
title: 網站管理
seo-title: Website Administration
description: 瞭解如何使用Adobe Experience Manager管理多語言網站。
seo-description: Learn how to manage multilingual websites in AEM.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 4%

---

# 網站管理{#website-administration}

下列管理工具可用來管理網站與頁面：

* 多網站管理員(MSM)可讓您在多個位置使用相同的網站內容，同時允許以下變化：

   * [重複使用內容：多網站管理員和 Live Copy](/help/sites-administering/msm.md)

* 翻譯可讓您自動翻譯頁面內容、資產和使用者產生的內容，以建立和維護多語言網站：

   * [翻譯多語言網站的內容](/help/sites-administering/translation.md)

* 這兩個功能可結合使用，以符合以下兩種情況的網站 [跨國及多語言](#multinational-and-multilingual-sites).

## 跨國及多語言網站 {#multinational-and-multilingual-sites}

您可以透過結合使用多網站管理員和翻譯工作流程，有效率地建立跨國和多語言網站的內容。 針對特定國家/地區，以一種語言建立主要網站，然後將該內容當作其他網站的基礎，並視需要使用翻譯：

* [Translate](/help/sites-administering/translation.md) 將主場地翻譯成不同的語言。

* 使用 [多站點管理員](/help/sites-administering/msm.md) 至：

   * 重複使用主要網站的內容和翻譯，為其他國家/地區和文化建立網站。
   * 請務必將「多網站管理員」的使用限製為使用一種語言的內容，例如，國家網站中的英文主版 — >英文分支，國家網站中的法文主版 — >法文分支。
   * 必要時，請分離即時副本的元素，以新增本地化詳細資訊。

下圖說明主要概念如何交集（但並未顯示所有相關層級/元素）：

![顯示MSM和翻譯主要概念的圖表](assets/chlimage_1-71a.png)

>[!NOTE]
>
>在此情況以及可供比較的情況下，MSM不會據此管理不同的語言版本。
>
>* [MSM](/help/sites-administering/msm.md) 管理語言範圍內從Blueprint （例如全域主版）到即時副本（例如本機站台）的翻譯內容部署。
>* 此 [翻譯](/help/sites-administering/translation.md) AEM的整合功能以及協力廠商翻譯管理服務，可管理語言，並將內容翻譯成這些不同的語言。
>
>如需更進階的使用案例，您也可以跨語言主版使用MSM。

>[!NOTE]
>
>對於所有使用案例，建議閱讀以下最佳實務：
>
>* [MSM的最佳作法](/help/sites-administering/msm-best-practices.md)；尤其是：
>
>   * [建立網站](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM和多語言網站](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [翻譯最佳實務](/help/sites-administering/tc-bp.md)
