---
title: 使用Apache Tika偵測資產的MIME類型
description: 啟用Apache Tika以提供說明 [!DNL Experience Manager Assets] 在上傳作業期間（而非檔案副檔名）從內容資料流偵測MIME類型的資產。
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 偵測資產的MIME類型，使用 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常， [!DNL Adobe Experience Manager Assets] 會偵測您從其副檔名上傳的資產的MIME類型。

如果您使用 [!DNL Apache Tika] 上傳資產， [!DNL Assets] 在上傳作業期間會從內容資料流中偵測其MIME類型，而非檔案副檔名。

此功能預設為停用。 若要啟用功能，請設定 **[!UICONTROL Day CQ DAM Mime類型]** 服務 [!UICONTROL Configuration Manager].

>[!NOTE]
>
>MIME類型檢測，使用 [!DNL Apache Tika] 程式庫是耗用大量資源的作業。

1. 若要開啟Configuration Manager Web控制台，請訪問 `https://[aem_server]:[port]/system/console/configMgr`.

1. 從服務清單中，找到 **[!UICONTROL Day CQ DAM Mime類型服務]** 按一下 **[!UICONTROL 編輯]**.

1. 選取 **[!UICONTROL 從內容中檢測MIME]** 選項，啟用已上傳資產的剖析，以在忽略副檔名時判斷其MIME類型。 依預設，會取消選取此選項。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。
