---
title: 將資料夾發佈至 Brand Portal
seo-title: Publish folders to Brand Portal
description: 瞭解如何向Brand Portal發佈和取消發佈資料夾。
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

作為Adobe Experience Manager(AEM)資產管理員，您可以將資產和資料夾發佈到AEM Assets Brand Portal實例（或將發佈工作流安排到以後的日期/時間）。 但是，你必須先把AEM Assets和Brand Portal融為一體。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

在發佈資產或資料夾後，它可供Brand Portal的用戶使用。

如果您隨後對AEM Assets的原始資產或資料夾進行了修改，則在您重新發佈資產或資料夾之前，這些更改不會反映在Brand Portal。 這項功能可確保對進行中工作所作的變更不會出現在 Brand Portal 中。Brand Portal 僅提供管理員發佈的已核准變更。

## 將資料夾發佈至 Brand Portal {#publish-folders-to-brand-portal-1}

1. 從AEM Assets介面，懸停在所需資料夾上，然後選擇 **發佈** 的子菜單。

   或者，選擇所需資料夾並執行後續步驟。

   ![publish2bp](assets/publish2bp.png)

1. **現在發佈資料夾**

   若要將所選資料夾發佈至 Brand Portal，請執行下列其中一項操作：

   * 在工具列中選取&#x200B;**快速發佈**。然後，從菜單中選擇 **發佈到Brand Portal**。

   * 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **操作** 選擇 **發佈到Brand Portal**&#x200B;從 **計畫** 選擇 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**發佈至 Brand Portal**。

   系統會顯示訊息，指出資料夾已排入佇列，等候發佈至 Brand Portal。登錄到Brand Portal介面以查看已發佈資料夾。

   **稍後發佈資料夾**

   要將資產資料夾的發佈到Brand Portal工作流計畫到以後的日期或時間，請執行以下操作：

   1. 選擇要發佈的資產/資料夾後，選擇 **管理發布** 的上界。
   1. 從 **操作** 選擇 **發佈到Brand Portal**&#x200B;從 **計畫** 選擇 **稍後**。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目。按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;底下指定「工作流程標題」。按一下&#x200B;**稍後發佈**。

      ![managerchedulepub](assets/manageschedulepub.png)



## 從 Brand Portal 取消發佈資料夾 {#unpublish-folders-from-brand-portal}

通過從AEM Author實例中取消發佈已發佈到Brand Portal的任何資產資料夾，可以將其刪除。 取消發佈原始資料夾後，Brand Portal 使用者將無法再取用資料夾副本。

您可以選擇快速取消從Brand Portal發佈資料夾，或將其安排在以後的日期和時間。 若要從 Brand Portal 取消發佈資產資料夾：

1. 從AEM Author實例的AEM Assets介面中，選擇要取消發佈的資料夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具欄中，按一下 **管理發布**。

1. **立即從Brand Portal取消發佈**

   要從Brand Portal快速取消發佈所需資料夾：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **操作** 選擇 **從Brand Portal取消出版**&#x200B;從 **計畫** 選擇 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**從 Brand Portal 取消發佈**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍後從Brand Portal取消發佈**

   要將資料夾從Brand Portal發佈到以後的日期和時間，請執行以下操作：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **操作** 選擇 **從Brand Portal取消出版**，從 **計畫** 選擇 **稍後**。
   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;中指定&#x200B;**工作流程標題**。按一下 **稍後取消發佈。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>向/從Brand Portal發佈/取消發佈資產的過程與資料夾的相應過程類似。
