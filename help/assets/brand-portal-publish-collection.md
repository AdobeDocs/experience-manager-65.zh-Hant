---
title: 將集合發佈至 Brand Portal
seo-title: Publish collections to Brand Portal
description: 了解如何將集合發佈和取消發佈至Brand Portal。
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

身為Adobe Experience Manager(AEM)Assets管理員，您可以將集合發佈至貴組織的AEM Assets Brand Portal例項。 不過，您必須先整合AEM Assets與Brand Portal。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

如果您後續修改了AEM Assets中的原始系列，在您再次發佈系列之前，Brand Portal不會反映這些變更。 此特性可確保Brand Portal中無法使用進行中的變更。 Brand Portal 僅提供管理員發佈的已核准變更。

>[!NOTE]
>
>內容片段無法發佈至 Brand Portal。因此，如果您在AEM作者上選取內容片段，則 **發佈至Brand Portal** 無法使用動作。
>
>如果從AEM Author將包含內容片段的集合發佈至Brand Portal，則除了內容片段以外，資料夾的所有內容都會複製到Brand Portal介面。

## 將集合發佈至Brand Portal {#publish-a-collection-to-brand-portal}

1. 在 AEM Assets UI 中按一下 AEM 標誌。
1. 從&#x200B;**導覽**&#x200B;頁面，前往&#x200B;**資產 > 集合**。
1. 在集合控制台中，選取您要發佈至Brand Portal的集合。

   ![select_collection](assets/select_collection.png)

1. 從工具列中按一下&#x200B;**發佈至 Brand Portal**。
1. 在確認對話方塊中，按一下&#x200B;**發佈**。
1. 關閉確認訊息。
1. 以管理員身分登入Brand Portal。 已發佈的集合可在「集合」控制台中使用。

   ![已發佈的集合](assets/published_collection.png)

## 取消發佈集合 {#unpublish-collections}

您可以取消發佈從AEM Assets發佈至Brand Portal的集合。 取消發佈原始集合後，Brand Portal使用者將無法再使用集合的副本。

1. 在AEM Assets例項的集合控制台中，選取您要取消發佈的集合。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具列中按一下&#x200B;**從 Brand Portal 移除**&#x200B;圖示。
1. 在對話方塊中，按一下&#x200B;**取消發佈**。
1. 關閉確認訊息。集合會從 Brand Portal 介面中移除。
