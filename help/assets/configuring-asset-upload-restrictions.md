---
title: 設定資產上傳限制
description: 限制使用者可上傳的資產型別（檔案）
contentOwner: AG
role: Developer, Admin, Architect
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 20%

---

# 設定資產上傳限制 {#configuring-asset-upload-restrictions}

您可以設定 [!DNL Adobe Experience Manager Assets] 以限制使用者可上傳的資產型別。 它有助於防止意外上傳不需要的格式和惡意檔案。 此 `Day CQ DAM Asset Upload Restriction` 服務可讓您控制使用者可上傳的檔案型別。 根據預設， [!DNL Assets] 可讓使用者上傳所有MIME型別的資產。 不過，您可以將服務設定為限制使用者只上傳特定MIME型別的檔案。

1. 開啟Configuration Manager Web主控台。 存取 `https://[aem_server]:[port]/system/console/configMgr`.
1. 開啟 **[!UICONTROL Day CQ DAM資產上傳限制]** 編輯模式下的服務。 根據預設， **允許所有MIME** 選項已選取，可讓使用者上傳所有MIME型別的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 若要限制使用者僅上傳特定MIME型別的檔案，請取消選取 **[!UICONTROL 允許所有MIME]** 選項，並在以下位置指定允許的MIME型別： **[!UICONTROL 允許的資產MIME （規則運算式）]** 使用規則運算式的欄位。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。 如果您為允許的MIME類型指定MIME字串，則對於任何MIME類型不符合這些欄位中已設定之MIME字串的資產，上傳作業會失敗。
