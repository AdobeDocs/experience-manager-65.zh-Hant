---
title: 使用Apache Tika偵測MIME型別的資產
description: 啟用Apache Tika以協助 [!DNL Experience Manager Assets] 在上傳操作期間，從內容串流中偵測資產的MIME型別，而不是副檔名。
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

# 使用以下專案偵測MIME型別的資產 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

一般而言， [!DNL Adobe Experience Manager Assets] 會偵測您從副檔名上傳的資產的MIME型別。

如果您使用 [!DNL Apache Tika] 若要上傳資產， [!DNL Assets] 會在上傳作業期間從內容串流中偵測其MIME型別，而不是透過副檔名。

此功能預設為停用。 若要啟用此功能，請設定 **[!UICONTROL Day CQ DAM Mime型別]** 服務來源 [!UICONTROL 組態管理員].

>[!NOTE]
>
>使用MIME型別偵測 [!DNL Apache Tika] 程式庫是耗用大量資源的作業。

1. 若要開啟Configuration Manager Web主控台，請存取 `https://[aem_server]:[port]/system/console/configMgr`.

1. 從服務清單中，找出 **[!UICONTROL Day CQ DAM Mime型別服務]** 並按一下 **[!UICONTROL 編輯]**.

1. 選取 **[!UICONTROL 從內容中偵測MIME]** 可啟用上傳資產剖析的選項，以在忽略副檔名時判斷其MIME型別。 依預設，此選項是取消選取的。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。
