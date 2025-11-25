---
title: 設定資產上傳限制
description: 限制使用者可上傳的資產型別（檔案）
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---

# 設定資產上傳限制 {#configuring-asset-upload-restrictions}

您可以設定[!DNL Adobe Experience Manager Assets]以限制使用者可以上傳的資產型別。 它有助於防止意外上傳不需要的格式和惡意檔案。 `Day CQ DAM Asset Upload Restriction`服務可讓您控制使用者可以上傳的檔案型別。 依預設，[!DNL Assets]允許使用者上傳所有MIME型別的資產。 不過，您可以將服務設定為限制使用者只上傳特定MIME型別的檔案。

1. 開啟Configuration Manager Web主控台。 存取`https://[aem_server]:[port]/system/console/configMgr`。
1. 在編輯模式中開啟&#x200B;**[!UICONTROL Day CQ DAM Asset上傳限制]**&#x200B;服務。 依預設，**允許所有MIME**&#x200B;選項已選取，可讓使用者上傳所有MIME型別的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 若要限制使用者僅上傳特定MIME型別的檔案，請取消選取&#x200B;**[!UICONTROL 允許所有MIME]**&#x200B;選項，並使用規則運算式在&#x200B;**[!UICONTROL 允許的資產MIME (regex)]**&#x200B;欄位中指定允許的MIME型別。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 按一下[儲存]儲存變更。 ****&#x200B;如果您為允許的MIME型別指定MIME字串，則對於任何MIME型別不符合這些欄位中已設定之MIME字串的資產，上傳作業都會失敗。
