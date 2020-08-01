---
title: 使用Apache Tika偵測資產的MIME類型
description: 讓Apache Tika在上 [!DNL Experience Manager Assets] 傳作業期間（而非副檔名），協助偵測內容串流的MIME類型資產。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# 使用 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常 [!DNL Adobe Experience Manager Assets] 會偵測您從其副檔名上傳的MIME資產類型。

如果您使 [!DNL Apache Tika] 用上傳資產， [!DNL Assets] 請在上傳作業期間從內容串流中偵測其MIME類型，而非副檔名。

此功能預設為停用。 若要啟用此功能，請從 **[!UICONTROL Configuration Manager設定Day CQ DAM Mime Type]**[!UICONTROL 服務]。

>[!NOTE]
>
>使用程式庫的MIME類 [!DNL Apache Tika] 型偵測需要耗費大量資源。

1. 要開啟Configuration Manager Web控制台，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。

1. 從服務清單中，找到 **[!UICONTROL Day CQ DAM Mime Type Service]** ，然後單 **[!UICONTROL 擊Edit]**。

1. 選取「從 **[!UICONTROL 內容偵測MIME]** 」選項，啟用已上傳資產的剖析，以在忽略副檔名時判斷其MIME類型。 依預設，會取消選取此選項。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
