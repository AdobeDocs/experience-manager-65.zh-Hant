---
title: 設定資產上傳限制
description: 限制使用者可上傳的資產類型（檔案）
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 20%

---

# 設定資產上傳限制 {#configuring-asset-upload-restrictions}

您可以設定 [!DNL Adobe Experience Manager Assets] 以限制使用者可上傳的資產類型。 它有助於防止意外上傳不想要的格式和惡意檔案。 此 `Day CQ DAM Asset Upload Restriction` 服務可讓您控制使用者可上傳的檔案類型。 依預設， [!DNL Assets] 可讓使用者上傳所有MIME類型的資產。 不過，您可以設定服務，限制使用者僅上傳特定MIME類型的檔案。

1. 開啟Configuration Manager Web控制台。 存取 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL 日CQ DAM資產上傳限制]** 服務。 依預設， **允許所有MIME** 選項，允許用戶上載所有MIME類型的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 若要限制使用者僅上傳某些MIME類型的檔案，請取消選取 **[!UICONTROL 允許所有MIME]** 選項，並在 **[!UICONTROL 允許的資產MIME(regex)]** 欄位。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。 如果您為允許的MIME類型指定MIME字串，則對於任何MIME類型不符合這些欄位中已設定之MIME字串的資產，上傳作業會失敗。
