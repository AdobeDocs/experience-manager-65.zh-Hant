---
title: 將資產發佈至 Brand Portal
seo-title: 將資產發佈至 Brand Portal
description: 了解如何將資產發佈和取消發佈至Brand Portal。
seo-description: 了解如何將資產發佈和取消發佈至Brand Portal。
uuid: 350beb85-c0fb-4a1c-8597-c03592c02d3d
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: 39b8cf9b-afec-4c9a-8a5d-7fc87e643f26
docset: aem65
feature: 品牌入口網站
role: Business Practitioner
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 44%

---

# 將資產發佈至 Brand Portal {#publish-assets-to-brand-portal}

身為Adobe Experience Manager(AEM)Assets管理員，您可以將資產和資料夾發佈至貴組織的AEM Assets Brand Portal例項（或將發佈工作流程排程至稍後的日期/時間）。 不過，您必須先使用 Brand Portal 設定 AEM Assets。如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

復寫成功後，您可以將資產、資料夾和集合發佈至Brand Portal。 若要將資產發佈至Brand Portal，請依照下列步驟操作：

>[!NOTE]
>
>Adobe 建議將發佈時間交錯開來，尤其建議選擇非尖峰時段，如此 AEM 作者才不會佔用過多資源。

1. 從Assets控制台選取您要發佈的資產/資料夾，然後從工具列按一下&#x200B;**[!UICONTROL 快速發佈]**&#x200B;選項。

   或者，選取您要發佈至Brand Portal的資產。

   ![publish2bp-2](assets/publish2bp.png)

1. 若要將資產發佈至Brand Portal，可使用下列兩個選項：
   * [立即發佈資產](#publish-to-bp-now)
   * [稍後發佈資產](#publish-to-bp-now)

## 現在發佈資產 {#publish-to-bp-now}

若要將所選資產發佈至 Brand Portal，請執行下列其中一項操作：

* 在工具列中選取&#x200B;**[!UICONTROL 快速發佈]**。然後，從功能表中選取&#x200B;**[!UICONTROL 發佈至Brand Portal]**。

* 在工具列中選取&#x200B;**[!UICONTROL 管理出版物]**。

   1. 然後，從&#x200B;**[!UICONTROL Action]**&#x200B;中選擇&#x200B;**[!UICONTROL 發佈到Brand Portal]**，從&#x200B;**[!UICONTROL Scheduling]**&#x200B;中選擇&#x200B;**[!UICONTROL Now]**。 按一下&#x200B;**[!UICONTROL 下一步]**。

   2. 在&#x200B;**[!UICONTROL 範圍]**&#x200B;中，確認您的選擇，然後按一下&#x200B;**[!UICONTROL 發佈至Brand Portal]**。

系統會顯示訊息，指出資產已排入佇列，等候發佈至 Brand Portal。登入 Brand Portal 介面可查看已發佈的資產。

## 稍後發佈資產 {#publish-to-bp-later}

若要將資產發佈至 Brand Portal 的動作安排在之後的日期或時間：

1. 選取要發佈的資產/資料夾後，請從頂端的工具列選取&#x200B;**[!UICONTROL 管理出版物]**。

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面上，從&#x200B;**[!UICONTROL Action]**&#x200B;中選擇&#x200B;**[!UICONTROL 發佈到Brand Portal]**，然後從&#x200B;**[!UICONTROL Scheduling]**&#x200B;中選擇&#x200B;**[!UICONTROL Later]**。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 選取&#x200B;**[!UICONTROL 啟用日期]**&#x200B;並指定時間。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。

1. 在&#x200B;**[!UICONTROL 工作流程]**&#x200B;中指定&#x200B;**[!UICONTROL 工作流程標題]**。按一下&#x200B;**[!UICONTROL 稍後發佈]**。

   ![publishworkflow](assets/publishworkflow.png)

現在，請登入Brand Portal ，查看已發佈的資產是否可在Brand Portal介面上使用。

![bp_landing_page](assets/bp_landing_page.png)
