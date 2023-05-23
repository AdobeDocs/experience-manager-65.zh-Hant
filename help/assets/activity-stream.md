---
title: 時間軸視圖中數字資產的活動流
description: 本文介紹如何在時間線上顯示資產的活動日誌。
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 21%

---

# 時間軸中的活動流 {#activity-stream-in-timeline}

此功能顯示時間線上資產的活動日誌。 如果在中執行以下與資產相關的任何操作 [!DNL Adobe Experience Manager Assets]，活動流功能將更新時間軸以反映活動。

活動流中記錄了以下操作：

* 建立
* 刪除
* 下載（包括格式副本）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，當上載新資產或修改現有資產並將其檢入時，將記錄時間線活動 [!DNL Experience Manager] 通過 [Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 或 [Experience Manager案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)。

>[!NOTE]
>
>臨時工作流不會顯示在時間軸中，因為未保存這些工作流的歷史記錄資訊。

要查看活動流，請對資產執行一個或多個操作，選擇資產，然後選擇 **[!UICONTROL 時間軸]** 清單中。

![時間軸2](assets/timeline-2.png)

時間軸顯示您對資產執行的操作的活動流。

![活動流](assets/activity_stream.png)

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。
