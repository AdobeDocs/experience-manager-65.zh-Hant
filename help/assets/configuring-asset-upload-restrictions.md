---
title: 設定資產上傳限制
description: '限制使用者可上傳的資產（檔案）類型 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 15%

---


# 設定資產上傳限制 {#configuring-asset-upload-restrictions}

您可以設 [!DNL Adobe Experience Manager Assets] 定以限制使用者可上傳的資產類型。 它有助於防止意外上傳不想要的格式和惡意檔案。 此服 `Day CQ DAM Asset Upload Restriction` 務可讓您控制使用者可上傳的檔案類型。 依預設，可 [!DNL Assets] 讓使用者上傳所有MIME類型的資產。 不過，您可以設定服務，限制使用者僅上傳特定MIME類型的檔案。

1. 開啟Configuration Manager Web控制台。 存取 `https://[aem_server]:[port]/system/console/configMgr`.
1. 在編輯模 **[!UICONTROL 式中開啟「日CQ DAM資產上傳限制]** 」服務。 依預設，會選 **取「允許所有MIME** 」選項，可讓使用者上傳所有MIME類型的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. To restrict users to upload files of certain MIME types only, unselect the **[!UICONTROL Allow all MIME]** option and specify allowed MIME types in the **[!UICONTROL Allowed Asset MIMEs (regex)]** fields using regular expressions.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Click **[!UICONTROL Save]** to save the changes. 如果您為允許的MIME類型指定MIME字串，則對於任何MIME類型不符合這些欄位中已設定之MIME字串的資產，上傳作業會失敗。
