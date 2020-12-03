---
title: 將資料夾發佈至 Brand Portal
seo-title: 將資料夾發佈至 Brand Portal
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
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 38%

---


# 將資料夾發佈至 Brand Portal{#publish-folders-to-brand-portal}

身為Adobe Experience Manager(AEM)Assets管理員，您可以發佈資產和檔案夾至組織的AEM Assets Brand Portal例項（或排程發佈工作流程至較晚的日期／時間）。 不過，您必須先將AEM Assets與品牌入口網站整合。 如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

發佈資產或資料夾後，品牌入口網站的使用者即可使用它。

如果您在AEM Assets中對原始資產或檔案夾進行後續修改，在您重新發佈資產或檔案夾之前，這些變更不會反映在品牌入口網站中。 這項功能可確保對進行中工作所作的變更不會出現在 Brand Portal 中。Brand Portal 僅提供管理員發佈的已核准變更。

## 將資料夾發佈至 Brand Portal {#publish-folders-to-brand-portal-1}

1. 從AEM Assets介面，將滑鼠指標暫留在所要的資料夾上，並從快速動作中選取「**發佈**」選項。

   或者，選取所要的檔案夾，然後依照進一步的步驟進行。

   ![publish2bp](assets/publish2bp.png)

1. **現在發佈資料夾**

   若要將所選資料夾發佈至 Brand Portal，請執行下列其中一項操作：

   * 在工具列中選取&#x200B;**快速發佈**。然後，從功能表中選擇「發佈至品牌入口網站」**。**

   * 在工具列中選取&#x200B;**管理出版物**。
   1. 從&#x200B;**Action**&#x200B;選擇「發佈至品牌入口網站」，從&#x200B;**Scheduling**&#x200B;選擇「Now」（現在），然後按一下「Next」（下一步）。************
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**發佈至 Brand Portal**。

   系統會顯示訊息，指出資料夾已排入佇列，等候發佈至 Brand Portal。登入品牌入口網站介面，查看已發佈的資料夾。

   **稍後發佈資料夾**

   若要排程資產檔案夾的發佈至品牌入口網站工作流程，請執行下列動作：

   1. 在您選取要發佈的資產／檔案夾後，請從頂端的工具列選取「管理出版物」(**Manage Publication)。**
   1. 從&#x200B;**Action**&#x200B;選擇&#x200B;**發佈至品牌入口網站**，從&#x200B;**Scheduling**&#x200B;選擇&#x200B;**Later**。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目。按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;底下指定「工作流程標題」。按一下&#x200B;**稍後發佈**。

      ![managerchedulepub](assets/manageschedulepub.png)



## 從 Brand Portal 取消發佈資料夾 {#unpublish-folders-from-brand-portal}

您可以從AEM Author例項中取消發佈任何已發佈至品牌入口網站的資產資料夾，以移除它。 取消發佈原始資料夾後，Brand Portal 使用者將無法再取用資料夾副本。

您可以選擇從品牌入口網站快速解除發佈資料夾，或排程檔案夾在稍後的日期和時間。 若要從 Brand Portal 取消發佈資產資料夾：

1. 從AEM Author例項中的AEM Assets介面，選取您要解除發佈的檔案夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具欄中，按一下「管理出版物」。****

1. **立即從品牌入口網站取消發佈**

   若要從品牌入口網站快速解除發佈所需的檔案夾：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從&#x200B;**Action**&#x200B;選擇「從品牌門戶取消發佈」，從&#x200B;**Scheduling**&#x200B;選擇「現在」，然後按一下「下一步」。************
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**從 Brand Portal 取消發佈**。

   ![confirm-unpublish](assets/confirm-unpublish.png)

   **稍後從品牌入口網站取消發佈**

   若要排程從品牌入口網站發佈資料夾至稍後的日期和時間：

   1. 在工具列中選取&#x200B;**管理出版物**。
   1. 從&#x200B;**Action**&#x200B;選擇「從品牌入口網站取消發佈」，從&#x200B;**Scheduling**&#x200B;選擇「**Later**」。****
   1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。
   1. 在&#x200B;**範圍**&#x200B;中確認您的選取項目，然後按一下&#x200B;**下一步**。
   1. 在&#x200B;**工作流程**&#x200B;中指定&#x200B;**工作流程標題**。按一下&#x200B;**稍後取消發佈。**

      ![unpublishworkflows](assets/unpublishworkflows.png)


>[!NOTE]
>
>將資產發佈／解除發佈至／從品牌入口網站的程式與資料夾的對應程式類似。

