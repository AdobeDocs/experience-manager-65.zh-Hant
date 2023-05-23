---
title: 設定資產上傳限制
description: 限制用戶可以上載的資產（檔案）類型
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

您可以配置 [!DNL Adobe Experience Manager Assets] 限制用戶可以上載的資產類型。 它有助於防止意外上載不希望有的格式和惡意檔案。 的 `Day CQ DAM Asset Upload Restriction` 服務使您能夠控制用戶可以上載的檔案類型。 預設情況下， [!DNL Assets] 允許用戶上載所有MIME類型的資產。 但是，您可以配置服務，以限制用戶僅上載特定MIME類型的檔案。

1. 開啟Configuration Manager Web控制台。 存取 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL 第CQ DAM資產上載限制]** 服務。 預設情況下， **允許所有MIME** 選項，允許用戶上載所有MIME類型的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 要限制用戶僅上載某些MIME類型的檔案，請取消選擇 **[!UICONTROL 允許所有MIME]** 選項，並在 **[!UICONTROL 允許的資產MIME（規則運算式）]** 欄位。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 按一下 **[!UICONTROL 保存]** 的子菜單。 如果您為允許的MIME類型指定MIME字串，則對於任何MIME類型不符合這些欄位中已設定之MIME字串的資產，上傳作業會失敗。
