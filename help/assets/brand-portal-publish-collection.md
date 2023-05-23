---
title: 將集合發佈至 Brand Portal
seo-title: Publish collections to Brand Portal
description: 瞭解如何向Brand Portal發佈和取消發佈收藏。
seo-description: Learn how to publish and unpublish collections to Brand Portal.
uuid: 7de58548-4cfa-4a94-bac7-9e914dee9042
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 90e3fd0e-9bc3-4aff-8c7b-7408f5b940e8
docset: aem65
feature: Brand Portal
role: User
exl-id: 8f426012-d9ec-418e-8ab6-78e4aeff7538
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 36%

---

# 將集合發佈至 Brand Portal {#publish-collections-to-brand-portal}

作為Adobe Experience Manager(AEM)資產管理員，您可以將收集發佈到組織的AEM Assets Brand Portal實例。 但是，你必須先把AEM Assets和Brand Portal融為一體。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

如果您隨後對AEM Assets的原始收藏進行了修改，則在您再次發佈該收藏之前，這些更改不會反映在Brand Portal。 這一特點確保在Brand Portal不能進行正在進行的變革。 Brand Portal 僅提供管理員發佈的已核准變更。

>[!NOTE]
>
>內容片段無法發佈至 Brand Portal。因此，如果在AEM作者上選擇內容片段，則 **發佈到Brand Portal** 操作不可用。
>
>如果包含內容片段的集合從AEM作者發佈到Brand Portal，則資料夾中除內容片段之外的所有內容都將複製到Brand Portal介面。

## 將收藏發佈到Brand Portal {#publish-a-collection-to-brand-portal}

1. 在 AEM Assets UI 中按一下 AEM 標誌。
1. 從&#x200B;**導覽**&#x200B;頁面，前往&#x200B;**資產 > 集合**。
1. 從「集合」控制台中，選擇要發佈到Brand Portal的集合。

   ![select_collection](assets/select_collection.png)

1. 從工具列中按一下&#x200B;**發佈至 Brand Portal**。
1. 在確認對話方塊中，按一下&#x200B;**發佈**。
1. 關閉確認訊息。
1. 以管理員身份登錄到Brand Portal。 已發佈的集合可在「集合」控制台中使用。

   ![已發佈的集合](assets/published_collection.png)

## 取消發佈集合 {#unpublish-collections}

你可以取消發佈從AEM Assets到Brand Portal的系列。 取消發佈原始收藏後，其副本將不再可供Brand Portal用戶使用。

1. 從AEM Assets實例的「集合」控制台中，選擇要取消發佈的集合。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具列中按一下&#x200B;**從 Brand Portal 移除**&#x200B;圖示。
1. 在對話方塊中，按一下&#x200B;**取消發佈**。
1. 關閉確認訊息。集合會從 Brand Portal 介面中移除。
