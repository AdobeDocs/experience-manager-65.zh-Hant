---
title: 將資料夾發佈至品牌入口網站
seo-title: 將資料夾發佈至品牌入口網站
description: 瞭解如何發佈及解除發佈資料夾至品牌入口網站。
seo-description: 瞭解如何發佈及解除發佈資料夾至品牌入口網站。
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
translation-type: tm+mt
source-git-commit: 9f923782d3d0a7bdf45b18e8025bd2d083acf77c

---


# Publish folders to Brand Portal{#publish-folders-to-brand-portal}

身為Adobe Experience Manager(AEM)Assets管理員，您可以發佈資產和檔案夾至組織的AEM Assets Brand Portal例項（或排程發佈工作流程至較晚的日期／時間）。 不過，您必須先將AEM Assets與品牌入口網站整合。 如需詳細資訊，請 [參閱「設定AEM資產與品牌入口網站](/help/assets/configure-aem-assets-with-brand-portal.md)」。

發佈資產或資料夾後，品牌入口網站的使用者即可使用它。

如果您在AEM Assets中對原始資產或檔案夾進行後續修改，在您重新發佈資產或檔案夾之前，這些變更不會反映在品牌入口網站中。 此功能可確保品牌入口網站中不提供進行中的變更。 品牌入口網站中僅提供管理員發佈的已核准變更。

## Publish folders to Brand Portal {#publish-folders-to-brand-portal-1}

1. 從AEM Assets介面，將滑鼠指標暫留在所要的檔案夾上，然後從快速動作中選 **取** 「發佈」選項。

   或者，選取所要的檔案夾，然後依照進一步的步驟進行。

   ![publish2bp](assets/publish2bp.png)

1. **立即發佈資料夾**

   若要將選取的檔案夾發佈至品牌入口網站，請執行下列其中一項作業：

   * 從工具列中選取「快 **速發佈」**。 然後，從功能表中選取「 **發佈至品牌入口網站」**。

   * 從工具列中，選擇「管 **理出版物」**。
   1. 從「 **From** **Action**」(從「Scheduling Select Now」（立即排程）中，選擇「Publish to Brand Portal **」（發佈至品牌門戶），從「Scheduling** and ******Click Next」（立即排程和下一個）中。**
   1. 在「範圍」中確認您 **的選擇** ，然後按 **一下「發佈至品牌入口網站」**。
   出現訊息，指出資料夾已排入發佈至品牌入口網站的佇列。 登入品牌入口網站介面，查看已發佈的資料夾。

   **稍後發佈資料夾**

   若要排程資產檔案夾的發佈至品牌入口網站工作流程，請執行下列動作：

   1. 在您選取要發佈的資產／檔案夾後，從頂端的工 **具列選取「管理出版物** 」。
   1. 從「 **動作** 」中，從「排程 **」選取「發佈至品牌入口網站」,**&#x200B;並選 **取「稍後******&#x200B;排程」。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 選擇啟 **動日期** ，並指定時間。 按一 **下「下一步**」。
   1. 在「範圍」中確認您 **的選擇**。 按一 **下「下一步**」。
   1. 在「工作流程」( **Workflows)下指定「工作流」(Workflows**)標題。 按一下「 **稍後發佈**」。

      ![managerchedulepub](assets/manageschedulepub.png)



## Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

您可以從AEM Author例項中取消發佈任何已發佈至品牌入口網站的資產資料夾，以移除它。 解除發佈原始資料夾後，品牌入口網站使用者將無法再使用其副本。

您可以選擇從品牌入口網站快速解除發佈資料夾，或排程檔案夾在稍後的日期和時間。 若要從品牌入口網站取消發佈資產資料夾：

1. 從AEM Author例項中的AEM Assets介面，選取您要解除發佈的檔案夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具列中，按一下「管 **理出版物」**。

1. **立即從品牌入口網站取消發佈**

   若要從品牌入口網站快速解除發佈所需的檔案夾：

   1. 從工具列中，選擇「管 **理出版物」**。
   1. 從「 **動作** 」中選 **擇「從品牌Portal取消發佈**」，從「計畫」 **中選擇「********Next Lick And Portal」。**
   1. 在「範圍」中確認您 **的選擇** ，然後按一 **下「從品牌入口網站取消發佈」**。
   ![確認——取消發佈](assets/confirm-unpublish.png)

   **稍後從品牌入口網站取消發佈**

   若要排程從品牌入口網站發佈資料夾至稍後的日期和時間：

   1. 從工具列中，選擇「管 **理出版物」**。
   1. 從「 **動作** 」中 **選取「從品牌入口網站取消發佈**」，並從「計畫」 **中選** 取「稍後 ****&#x200B;取消發佈」。
   1. 選擇啟 **動日期** ，並指定時間。 按一 **下「下一步**」。
   1. 在「範圍」中確認您 **的選擇** ，然後按一 **下「下一步」**。
   1. 在「工作流 **程」中指定** 「工 **作流」標題**。 按一下「 **稍後取消發佈」。**

      ![unpublish工作流程](assets/unpublishworkflows.png)


>[!NOTE]
>
>將資產發佈／解除發佈至／從品牌入口網站的程式與資料夾的對應程式類似。

