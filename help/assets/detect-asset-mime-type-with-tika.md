---
title: 使用Apache Tika檢測MIME資產類型
description: 啟用Apache Tika以幫助 [!DNL Experience Manager Assets] 在上載操作期間檢測來自內容流的MIME類型的資產，而不是檔案副檔名。
contentOwner: AG
role: Admin, Architect
feature: Metadata,Developer Tools,Asset Management
exl-id: a312466d-8d84-4c94-af85-1549afc61aed
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 使用檢測MIME類型的資產 [!DNL Apache Tika] {#detecting-mime-type-of-assets-using-apache-tika}

通常， [!DNL Adobe Experience Manager Assets] 檢測您從其檔案副檔名上載的資產的MIME類型。

如果您使用 [!DNL Apache Tika] 上傳資產， [!DNL Assets] 在上載操作期間從內容流（而不是檔案副檔名）檢測其MIME類型。

預設情況下禁用此功能。 要啟用該功能，請配置 **[!UICONTROL 第CQ天DAM Mime類型]** 服務 [!UICONTROL 配置管理器]。

>[!NOTE]
>
>使用的MIME類型檢測 [!DNL Apache Tika] 庫是資源密集型操作。

1. 要開啟Configuration Manager Web控制台，請訪問 `https://[aem_server]:[port]/system/console/configMgr`。

1. 從服務清單中，找到 **[!UICONTROL 第CQ天DAM MIME類型服務]** 按一下 **[!UICONTROL 編輯]**。

1. 選擇 **[!UICONTROL 從內容中檢測MIME]** 選項，以啟用對上載的資產的分析，以在忽略檔案副檔名時確定其MIME類型。 預設情況下，此選項處於未選中狀態。

   ![chlimage_1-333](assets/chlimage_1-333.png)

1. 按一下 **[!UICONTROL 保存]** 的子菜單。
