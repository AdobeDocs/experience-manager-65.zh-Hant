---
title: 使用Apache Tika偵測MIME型別的資產
description: 啟用Apache Tika以協助[!DNL Experience Manager Assets]在上傳操作期間從內容資料流偵測到MIME型別的資產，而不是副檔名。
contentOwner: AG
role: Admin, Developer
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: ed6971a3-2c12-4fd2-81f4-ff329c416250
    internal-label: Metadata
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 4%
---
# 使用[!DNL Apache Tika]偵測MIME型別的資產 {#detecting-mime-type-of-assets-using-apache-tika}

通常，[!DNL Adobe Experience Manager Assets]會偵測您從副檔名上傳的MIME資產型別。

如果您使用[!DNL Apache Tika]上傳資產，[!DNL Assets]會在上傳作業期間從內容資料流偵測其MIME型別，而非副檔名。

此功能預設為停用。 若要啟用此功能，請從[!UICONTROL 設定管理員]設定&#x200B;**[!UICONTROL Day CQ DAM Mime Type]**&#x200B;服務。

>[!NOTE]
>
>使用[!DNL Apache Tika]程式庫偵測MIME型別是資源密集的作業。

1. 若要開啟Configuration Manager Web主控台，請存取`https://[aem_server]:[port]/system/console/configMgr`。

1. 從服務清單中，找到&#x200B;**[!UICONTROL Day CQ DAM Mime Type Service]**，然後按一下&#x200B;**[!UICONTROL 編輯]**。

1. 選取&#x200B;**[!UICONTROL 從內容偵測MIME]**&#x200B;選項，啟用已上傳資產的剖析，以決定其MIME型別，同時忽略副檔名。 依預設，此選項是取消選取的。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。
