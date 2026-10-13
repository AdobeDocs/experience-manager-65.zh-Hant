---
title: 設定資產上傳限制
description: 限制使用者可上傳的資產型別（檔案）
contentOwner: AG
role: Developer, Admin
feature: Asset Management,Upload
exl-id: 0e009b9a-54c4-4715-98ee-0207839f90f6
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: cda65036-5305-4f01-89da-9b3506ae8c50
    internal-label: Administration
subfeature_v2:
  - id: f1dc0c96-022d-4003-afbe-47bd40173c4a
    internal-label: Upload assets
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 9%
---
# 設定資產上傳限制 {#configuring-asset-upload-restrictions}

您可以設定[!DNL Adobe Experience Manager Assets]以限制使用者可以上傳的資產型別。 它有助於防止意外上傳不需要的格式和惡意檔案。 `Day CQ DAM Asset Upload Restriction`服務可讓您控制使用者可以上傳的檔案型別。 依預設，[!DNL Assets]允許使用者上傳所有MIME型別的資產。 不過，您可以將服務設定為限制使用者只上傳特定MIME型別的檔案。

1. 開啟Configuration Manager Web主控台。 存取`https://[aem_server]:[port]/system/console/configMgr`。
1. 在編輯模式中開啟&#x200B;**[!UICONTROL Day CQ DAM Asset上傳限制]**&#x200B;服務。 依預設，**允許所有MIME**&#x200B;選項已選取，可讓使用者上傳所有MIME型別的檔案。

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. 若要限制使用者僅上傳特定MIME型別的檔案，請取消選取&#x200B;**[!UICONTROL 允許所有MIME]**&#x200B;選項，並使用規則運算式在&#x200B;**[!UICONTROL 允許的資產MIME (regex)]**&#x200B;欄位中指定允許的MIME型別。

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。 如果您為允許的MIME型別指定MIME字串，則對於任何MIME型別不符合這些欄位中已設定之MIME字串的資產，上傳作業都會失敗。
