---
title: 時間軸檢視中的數位資產活動資料流
description: 本文說明如何在時間軸上顯示資產的活動記錄。
contentOwner: AG
feature: Asset Management
role: User, Admin
exl-id: 28dc0aa5-f2be-4e27-b7d8-415569b7ecd4
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 21%

---

# 時間軸中的活動資料流 {#activity-stream-in-timeline}

此功能會在時間軸上顯示資產的活動記錄。 如果您在中執行下列任何資產相關作業 [!DNL Adobe Experience Manager Assets]，活動資料流功能會更新時間軸以反映活動。

活動資料流中會記錄下列作業：

* 建立
* 刪除
* 下載（包括轉譯）
* 發佈
* 未發佈
* 批准
* 拒絕
* 移動

將從儲存日誌檔案的CRX位置提取要在時 `/var/audit/com.day.cq.dam/content/dam` 間軸中顯示的活動日誌。此外，上傳新資產或修改現有資產並簽入時，會記錄時間軸活動 [!DNL Experience Manager] 透過 [Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-assets-using-adobe-asset-link.ug.html) 或 [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html).

>[!NOTE]
>
>暫時性工作流程不會顯示在時間軸中，因為沒有為這些工作流程儲存歷史記錄資訊。

若要檢視活動資料流，請在資產上執行一或多個作業、選取資產，然後選擇 **[!UICONTROL 時間表]** 從GlobalNav清單。

![時間軸–2](assets/timeline-2.png)

時間軸會顯示您對資產執行之作業的活動資料流。

![activity_stream](assets/activity_stream.png)

>[!NOTE]
>
>「發佈」和「取消發佈」任 **[!UICONTROL 務的預設日]** 志存 **[!UICONTROL 儲位置為]**`/var/audit/com.day.cq.replication/content`。對於 **[!UICONTROL 移動]** ，預設位置為 `/var/audit/com.day.cq.wcm.core.page`。
