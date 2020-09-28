---
title: 時間軸檢視中數位資產的活動串流
description: 本文說明如何在時間軸上顯示資產的活動記錄檔。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 27%

---


# 時間軸中的活動串流 {#activity-stream-in-timeline}

此功能會在時間軸上顯示資產的活動記錄。 如果您在中執行下列任何資產相關作業， [!DNL Adobe Experience Manager Assets]活動串流功能會更新時間軸以反映活動。

活動流中記錄了以下操作：

* 建立
* 刪除
* 下載（包括轉譯）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。In addition, timeline activity is logged when new assets are uploaded or existing asses are modified and checked into [!DNL Experience Manager] via [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/manage-assets-using-adobe-asset-link.html) or [Experience Manager desktop app](https://docs.adobe.com/content/help/zh-Hant/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>暫時性工作流程不會顯示在時間軸中，因為不會儲存這些工作流程的歷史記錄資訊。

若要檢視活動串流，請對資產執行一或多個作業，選取資產，然後從GlobalNav清單中選 **[!UICONTROL 擇]** 「時間軸」。

![timeline-2](assets/timeline-2.png)

時間軸會顯示您對資產執行之作業的活動資料流。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。
