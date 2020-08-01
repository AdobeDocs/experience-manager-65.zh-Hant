---
title: 可偵測重複資產
description: 瞭解如何在Experience Manager中啟用重複資產的偵測。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---


# 可偵測重複資產 {#enable-detection-of-duplicate-assets}

如果您嘗試上傳中存在的資產，重複 [!DNL Adobe Experience Manager Assets]的偵測功能會將其識別為重複。 預設會停用重複偵測。 要啟用該功能，請執行以下步驟：

1. 通過訪 [!DNL Experience Manager] 問開啟Web控制台配置頁 `https://[aem_server]:[port]/system/console/configMgr`。
1. 編輯servlet日CQ DAM創 **[!UICONTROL 建資產的配置]**。
1. 選擇「檢 **[!UICONTROL 測重複]** 」選項，然後單 **[!UICONTROL 擊「保存」]**。

   ![在servlet中選擇檢測重複選項](assets/chlimage_1-377.png)

   *圖： 在servlet中選擇「檢測重複」選項。*

現在已在中啟用檢測重複功能 [!DNL Assets]。 當使用者嘗試上傳中存在的資產時， [!DNL Experience Manager]系統會檢查衝突並指出衝突。 資產使用儲存於的SHA-1雜湊來識別，這表 `jcr:content/metadata/dam:sha1`示不論檔案名稱為何，都會偵測到重複資產。

>[!MORELIKETHIS]
>
>* [現有儲存庫中重複的資產（社區成員的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

