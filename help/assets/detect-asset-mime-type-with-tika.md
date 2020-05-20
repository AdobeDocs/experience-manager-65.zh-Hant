---
title: 使用Apache Tika偵測資產的MIME類型
description: 啟用Apache Tika可協助AEM Assets在上傳作業期間，從內容串流偵測MIME類型的資產，而非副檔名。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# 使用Apache Tika偵測資產的MIME類型 {#detecting-mime-type-of-assets-using-apache-tika}

通常，Adobe Experience Manager(AEM)Assets會偵測您從其副檔名上傳的MIME資產類型。

如果您使用Apache Tika上傳資產，AEM Assets會在上傳作業期間從內容串流偵測其MIME類型，而非副檔名。

此功能預設為停用。 若要啟用此功能，請從 **[!UICONTROL Configuration Manager設定Day CQ DAM Mime Type]**[!UICONTROL 服務]。

>[!NOTE]
>
>使用Apache Tika程式庫進行MIME類型偵測是一項耗用大量資源的作業。

1. 要開啟Configuration Manager Web控制台，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。

1. 從服務清單中，找到 **[!UICONTROL Day CQ DAM Mime Type Service]** ，然後單 **[!UICONTROL 擊Edit]**。

1. 選取「從 **[!UICONTROL 內容偵測MIME]** 」選項，啟用已上傳資產的剖析，以在忽略副檔名時判斷其MIME類型。 依預設，會取消選取此選項。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. Click **[!UICONTROL Save]** to save the changes.
