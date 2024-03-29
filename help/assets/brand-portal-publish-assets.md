---
title: 將資產發佈至Brand Portal
description: 瞭解如何發佈和取消發佈資產到Brand Portal。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: brand-portal
content-type: reference
docset: aem65
feature: Brand Portal
role: User
exl-id: 76652a16-cad6-4e95-9e66-41efec452b03
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 41%

---

# 將資產發佈至Brand Portal {#publish-assets-to-brand-portal}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=zh-Hant) |
| AEM 6.5 | 本文章 |

身為Adobe Experience Manager (AEM) Assets管理員，您可以將資產和資料夾發佈到AEM Assets Brand Portal執行個體（或排程發佈工作流程在之後的日期/時間）。 不過，您必須先使用 Brand Portal 設定 AEM Assets。如需詳細資訊，請參閱[使用 Brand Portal 設定 AEM Assets](/help/assets/configure-aem-assets-with-brand-portal.md)。

複製成功後，您可以將資產、資料夾和集合發佈到Brand Portal。 若要將資產發佈至Brand Portal，請執行下列步驟：

>[!NOTE]
>
>Adobe 建議將發佈時間交錯開來，尤其建議選擇非尖峰時段，如此 AEM 作者才不會佔用過多資源。

1. 從「資產」控制檯選取您要發佈的資產/資料夾，然後按一下 **[!UICONTROL 快速發佈]** 工具列中的選項。

   或者，選取您要發佈至Brand Portal的資產。

   ![publish2bp-2](assets/publish2bp.png)

1. 若要將資產發佈至Brand Portal，可使用下列兩個選項：
   * [立即發佈資產](#publish-to-bp-now)
   * [稍後發佈資產](#publish-to-bp-now)

## 立即發佈資產 {#publish-to-bp-now}

若要將所選資產發佈至 Brand Portal，請執行下列其中一項操作：

* 在工具列中選取&#x200B;**[!UICONTROL 快速發佈]**。然後在功能表中選取 **[!UICONTROL 發佈至Brand Portal]**.

* 在工具列中選取&#x200B;**[!UICONTROL 管理出版物]**。

   1. 然後從 **[!UICONTROL 動作]** 選取 **[!UICONTROL 發佈至Brand Portal]**、和從 **[!UICONTROL 正在排程]** 選取 **[!UICONTROL 現在]**. 按一下「**[!UICONTROL 下一步]**」。

   2. 範圍 **[!UICONTROL 範圍]**，確認您的選取專案並按一下 **[!UICONTROL 發佈至Brand Portal]**.

系統會顯示訊息，指出資產已排入佇列，等候發佈至 Brand Portal。登入 Brand Portal 介面可查看已發佈的資產。

## 稍後發佈資產 {#publish-to-bp-later}

若要將資產發佈至 Brand Portal 的動作安排在之後的日期或時間：

1. 選取要發佈的資產/資料夾後，選取 **[!UICONTROL 管理發布]** 從頂端的工具列取得。

1. 開啟 **[!UICONTROL 管理發布]** 頁面，選取 **[!UICONTROL 發佈至Brand Portal]** 從 **[!UICONTROL 動作]** 並選取 **[!UICONTROL 稍後]** 從 **[!UICONTROL 正在排程]**.

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 選取&#x200B;**[!UICONTROL 啟用日期]**&#x200B;並指定時間。按一下&#x200B;**[!UICONTROL 下一步]**。

1. 選取&#x200B;**啟用日期**&#x200B;並指定時間。按一下&#x200B;**下一步**。

1. 在&#x200B;**[!UICONTROL 工作流程]**&#x200B;中指定&#x200B;**[!UICONTROL 工作流程標題]**。按一下&#x200B;**[!UICONTROL 稍後發佈]**。

   ![publishworkflow](assets/publishworkflow.png)

現在，請登入Brand Portal以檢視已發佈的資產在Brand Portal介面上是否可用。

![bp_landingpage](assets/bp_landingpage.png)
