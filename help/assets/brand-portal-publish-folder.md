---
title: 將資料夾發佈至Brand Portal
description: 瞭解如何發佈和取消發佈資料夾到Brand Portal。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 92a156f0-ce2a-4c83-bd57-0c29efbf784f
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 34%

---

# 將資料夾發佈至Brand Portal{#publish-folders-to-brand-portal}

身為Adobe Experience Manager (AEM) Assets管理員，您可以將資產和資料夾發佈到AEM Assets Brand Portal執行個體（或排程發佈工作流程在之後的日期/時間）。 不過，您必須先整合AEM Assets與Brand Portal。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

發佈資產或資料夾後，Brand Portal的使用者即可使用該資產或資料夾。

如果您對AEM Assets中的原始資產或資料夾進行後續修改，則在您重新發佈資產或資料夾之前，這些變更不會反映在Brand Portal中。 這項功能可確保對進行中工作所作的變更不會出現在 Brand Portal 中。Brand Portal 僅提供管理員發佈的已核准變更。

## 將資料夾發佈至Brand Portal {#publish-folders-to-brand-portal-1}

1. 在AEM Assets介面中，暫留在所需的資料夾上，然後選取 **發佈** 快速操作中的選項。

   或者，選取所需的資料夾，然後遵循進一步的步驟。

   ![publish2bp](assets/publish2bp.png)

1. **現在發佈資料夾**

   若要將所選資料夾發佈至 Brand Portal，請執行下列其中一項操作：

   * 在工具列中選取&#x200B;**快速發佈**。然後在功能表中選取 **發佈至Brand Portal**.

   * 在工具列中選取&#x200B;**管理出版物**。

   1. 從 **動作** 選取 **發佈至Brand Portal**，從 **正在排程** 選取 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**發佈至 Brand Portal**。

   系統會顯示訊息，指出資料夾已排入佇列，等候發佈至 Brand Portal。登入Brand Portal介面可檢視已發佈的資料夾。

   **稍後發佈資料夾**

   若要將資產資料夾的發佈至Brand Portal工作流程安排在之後的日期或時間：

   1. 選取要發佈的資產/資料夾後，選取 **管理發布** 從頂端的工具列取得。
   1. 從 **動作** 選取 **發佈至Brand Portal**，從 **正在排程** 選取 **稍後**.

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目。按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;底下指定「工作流程標題」。按一下&#x200B;**稍後發佈**。

      ![managerchedulepub](assets/manageschedulepub.png)

## 從Brand Portal取消發佈資料夾 {#unpublish-folders-from-brand-portal}

您可以從AEM Author例項中透過取消發佈來移除任何已發佈至Brand Portal的資產資料夾。 取消發佈原始資料夾後，Brand Portal 使用者將無法再取用資料夾副本。

您可以選擇快速從Brand Portal中取消發佈資料夾，或將其排程在之後的日期和時間。 若要從 Brand Portal 取消發佈資產資料夾：

1. 從AEM Author例項的AEM Assets介面中，選取您要取消發佈的資料夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具列中按一下 **管理發布**.

1. **立即從Brand Portal取消發佈**

   若要從Brand Portal快速取消發佈所需的資料夾：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **動作** 選取 **從Brand Portal取消發佈**，從 **正在排程** 選取 **現在**，然後按一下 **下一個。**
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**從 Brand Portal 取消發佈**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍後從Brand Portal取消發佈**

   若要將資料夾從Brand Portal發佈到更晚的日期和時間，請執行下列動作：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從 **動作** 選取 **從Brand Portal取消發佈**、和從 **正在排程** 選取 **稍後**.
   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;中指定&#x200B;**工作流程標題**。按一下 **稍後取消發佈。**

      ![unpublishworkflows](assets/unpublishworkflows.png)

>[!NOTE]
>
>向Brand Portal發佈/取消發佈資產的程式與資料夾的對應程式類似。
