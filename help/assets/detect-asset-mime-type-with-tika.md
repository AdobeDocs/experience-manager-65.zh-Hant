---
title: 使用Apache Tika偵測資產的MIME類型
description: 啟用Apache Tika可協助 [!DNL Experience Manager Assets] 在上傳作業期間偵測內容串流中的MIME類型資產，而非副檔名。
contentOwner: AG
role: 管理員、架構師
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---


# 使用[!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}偵測資產的MIME類型

通常，[!DNL Adobe Experience Manager Assets]會偵測您從其副檔名上傳的資產的MIME類型。

如果您使用[!DNL Apache Tika]來上傳資產， [!DNL Assets]會在上傳作業期間從內容串流中偵測其MIME類型，而非副檔名。

此功能預設為停用。 要啟用該功能，請從[!UICONTROL Configuration Manager]配置&#x200B;**[!UICONTROL Day CQ DAM Mime Type]**&#x200B;服務。

>[!NOTE]
>
>使用[!DNL Apache Tika]庫的MIME類型檢測是一項資源密集型操作。

1. 要開啟Configuration Manager Web控制台，請訪問`https://[aem_server]:[port]/system/console/configMgr`。

1. 從服務清單中，找到&#x200B;**[!UICONTROL Day CQ DAM Mime Type Service]** ，然後按一下&#x200B;**[!UICONTROL Edit]**。

1. 選取「從內容偵測MIME」選項，以啟用剖析已上傳資產，在忽略副檔名時判斷其MIME類型。 ****&#x200B;依預設，會取消選取此選項。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下&#x200B;**[!UICONTROL 保存]**&#x200B;保存更改。
