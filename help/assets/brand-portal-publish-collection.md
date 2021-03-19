---
title: 將集合發佈至 Brand Portal
seo-title: 將集合發佈至 Brand Portal
description: 瞭解如何將系列發佈及解除發佈至品牌入口網站。
seo-description: 瞭解如何將系列發佈及解除發佈至品牌入口網站。
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: 品牌入口網站
role: 業務從業人員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 36%

---


# 將集合發佈至 Brand Portal {#publish-collections-to-brand-portal}

身為Adobe Experience Manager(AEM)資產管理員，您可以發佈系列至貴組織的AEM Assets品牌入口網站例項。 不過，您必須先將AEM Assets與品牌入口網站整合。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

如果您在後續修改了AEM Assets的原始系列，在您再次發佈系列之前，這些變更不會反映在品牌入口網站中。 此特性可確保在品牌入口網站中無法使用進行中的變更。 Brand Portal 僅提供管理員發佈的已核准變更。

>[!NOTE]
>
>內容片段無法發佈至 Brand Portal。因此，如果您在AEM Author上選取內容片段，則無法使用「發佈至品牌入口網站」**動作。**
>
>如果包含內容片段的系列是從AEM Author發佈至品牌入口網站，則資料夾的所有內容（內容片段除外）都會複製至品牌入口網站介面。

## 將系列發佈至品牌入口網站{#publish-a-collection-to-brand-portal}

1. 在 AEM Assets UI 中按一下 AEM 標誌。
1. 從&#x200B;**導覽**&#x200B;頁面，前往&#x200B;**資產 > 集合**。
1. 從「系列」主控台中，選取您要發佈至品牌入口網站的系列。

   ![select_collection](assets/select_collection.png)

1. 從工具列中按一下&#x200B;**發佈至 Brand Portal**。
1. 在確認對話方塊中，按一下&#x200B;**發佈**。
1. 關閉確認訊息。
1. 以管理員身分登入品牌入口網站。 已發佈的集合可在「集合」控制台中使用。

   ![已發佈的集合](assets/published_collection.png)

## 取消發佈集合 {#unpublish-collections}

您可以解除發佈您從AEM Assets發佈至品牌入口網站的系列。 在您解除發佈原始系列後，品牌入口網站使用者將無法再使用其副本。

1. 從您的AEM Assets例項的「系列」主控台中，選取您要解除發佈的系列。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具列中按一下&#x200B;**從 Brand Portal 移除**&#x200B;圖示。
1. 在對話方塊中，按一下&#x200B;**取消發佈**。
1. 關閉確認訊息。集合會從 Brand Portal 介面中移除。

