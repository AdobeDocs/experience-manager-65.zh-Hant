---
title: 使用Apache Tika偵測MIME型別的資產
description: 啟用Apache Tika以協助 [!DNL Experience Manager Assets] 在上傳作業期間從內容資料流偵測資產的MIME型別，而非副檔名。
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 1%

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

1. 按一下[儲存]儲存變更。****
