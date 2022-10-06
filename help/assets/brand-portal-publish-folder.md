---
title: 將資料夾發佈至 Brand Portal
seo-title: Publish folders to Brand Portal
description: 了解如何將資料夾發佈和取消發佈至Brand Portal。
seo-description: Learn how to publish and unpublish folders to Brand Portal.
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 38%

---

# 將資料夾發佈至 Brand Portal{#publish-folders-to-brand-portal}

身為Adobe Experience Manager(AEM)Assets管理員，您可以將資產和資料夾發佈至貴組織的AEM Assets Brand Portal例項（或將發佈工作流程排程至稍後的日期/時間）。 不過，您必須先整合AEM Assets與Brand Portal。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

發佈資產或資料夾後，Brand Portal的使用者就能使用它。

如果您後續修改了AEM Assets中的原始資產或資料夾，在您重新發佈資產或資料夾之前，這些變更不會反映在Brand Portal中。 這項功能可確保對進行中工作所作的變更不會出現在 Brand Portal 中。Brand Portal 僅提供管理員發佈的已核准變更。

## 將資料夾發佈至 Brand Portal {#publish-folders-to-brand-portal-1}

1. 在AEM Assets介面中，暫留在所需資料夾上並選取 **發佈** 選項。

   或者，選取所需的資料夾，然後依照進一步步驟操作。

   ![publish2bp](assets/publish2bp.png)

1. **現在發佈資料夾**

   若要將所選資料夾發佈至 Brand Portal，請執行下列其中一項操作：

   * 在工具列中選取&#x200B;**快速發佈**。然後，從功能表中選取 **發佈至Brand Portal**.

   * 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **動作** 選取 **發佈至Brand Portal**&#x200B;從 **排程** 選取 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**發佈至 Brand Portal**。

   系統會顯示訊息，指出資料夾已排入佇列，等候發佈至 Brand Portal。登入Brand Portal介面，查看已發佈的資料夾。

   **稍後發佈資料夾**

   若要將資產資料夾的發佈至Brand Portal工作流程排程至之後的日期或時間：

   1. 選取要發佈的資產/資料夾後，請選取 **管理出版物** 從頂端的工具列。
   1. 從 **動作** 選取 **發佈至Brand Portal**&#x200B;從 **排程** 選取 **稍後**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目。按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;底下指定「工作流程標題」。按一下&#x200B;**稍後發佈**。

      ![managerchedulepub](assets/manageschedulepub.png)



## 從 Brand Portal 取消發佈資料夾 {#unpublish-folders-from-brand-portal}

您可以從AEM Author例項中取消發佈，以移除任何已發佈至Brand Portal的資產資料夾。 取消發佈原始資料夾後，Brand Portal 使用者將無法再取用資料夾副本。

您可以選擇從Brand Portal快速取消發佈資料夾，或排程以後的日期和時間。 若要從 Brand Portal 取消發佈資產資料夾：

1. 從AEM Author例項的AEM Assets介面中，選取您要取消發佈的資料夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具列中，按一下 **管理出版物**.

1. **立即從Brand Portal取消發佈**

   若要從Brand Portal快速取消發佈所需的資料夾：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **動作** 選取 **從Brand Portal取消發佈**&#x200B;從 **排程** 選取 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**從 Brand Portal 取消發佈**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍後從Brand Portal取消發佈**

   若要將資料夾從Brand Portal發佈排程到之後的日期和時間：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **動作** 選取 **從Brand Portal取消發佈**，從 **排程** 選取 **稍後**.
   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;中指定&#x200B;**工作流程標題**。按一下 **稍後取消發佈。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>將資產發佈/取消發佈至Brand Portal/從資料夾的程式類似於對應的程式。
