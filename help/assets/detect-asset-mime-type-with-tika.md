---
title: 使用Apache Tika偵測資產的MIME類型
description: 啟用Apache Tika以協助 [!DNL Experience Manager Assets] 在上傳作業期間（而非檔案副檔名）從內容資料流偵測資產的MIME類型。
contentOwner: AG
role: Admin, Architect
feature: 中繼資料，開發人員工具，資產管理
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# 使用[!DNL Apache Tika]偵測資產的MIME類型 {#detecting-mime-type-of-assets-using-apache-tika}

通常， [!DNL Adobe Experience Manager Assets]會偵測您從其副檔名上傳的資產的MIME類型。

如果您使用[!DNL Apache Tika]來上傳資產， [!DNL Assets]會在上傳作業期間從內容資料流中偵測其MIME類型，而非副檔名。

此功能預設為停用。 若要啟用功能，請從[!UICONTROL Configuration Manager]設定&#x200B;**[!UICONTROL Day CQ DAM Mime Type]**&#x200B;服務。

>[!NOTE]
>
>使用[!DNL Apache Tika]庫的MIME類型檢測是一項耗用大量資源的操作。

1. 要開啟Configuration Manager Web控制台，請訪問`https://[aem_server]:[port]/system/console/configMgr`。

1. 從服務清單中，找到&#x200B;**[!UICONTROL Day CQ DAM Mime Type Service]** ，然後按一下&#x200B;**[!UICONTROL Edit]**。

1. 選取&#x200B;**[!UICONTROL 從內容偵測MIME]**&#x200B;選項，以啟用剖析已上傳資產以在忽略副檔名時判斷其MIME類型。 依預設，會取消選取此選項。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存變更。
