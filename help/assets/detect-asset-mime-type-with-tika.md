---
title: 使用Apache Tika偵測資產的MIME類型
description: 啟用Apache Tika可協助AEM Assets在上傳作業期間，從內容串流偵測MIME類型的資產，而非副檔名。
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# 使用Apache Tika偵測資產的MIME類型 {#detecting-mime-type-of-assets-using-apache-tika}

通常，Adobe Experience Manager(AEM)Assets會偵測您從其副檔名上傳的MIME資產類型。

如果您使用Apache Tika上傳資產，AEM Assets會在上傳作業期間從內容串流偵測其MIME類型，而非副檔名。

此功能預設為停用。 若要啟用此功能，請從 **[!UICONTROL Configuration manager設定Day CQ DAM Mime Type]**[!UICONTROL 服務]。

>[!NOTE]
>
>使用Apache Tika程式庫進行MIME類型偵測是一項耗用大量資源的作業。

1. 要開啟Configuration Manager web控制台，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 從服務清單中，找到 **[!UICONTROL Day CQ DAM Mime Type Service]** ，並點選 **[!UICONTROL Edit]** （編輯）以在「Edit（編輯）」模式中開啟它。

1. 選取「從 **[!UICONTROL 內容偵測MIME]** 」選項，啟用已上傳資產的剖析，以在忽略副檔名時判斷其MIME類型。 依預設，會取消選取此選項。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下／點選「 **[!UICONTROL 儲存]** 」以儲存變更。
