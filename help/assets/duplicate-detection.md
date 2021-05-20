---
title: 啟用重複資產的偵測
description: 了解如何啟用偵測Experience Manager中的重複資產。
contentOwner: AG
role: Business Practitioner, Administrator
feature: 資產管理，資產報表
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 啟用重複資產的偵測{#enable-detection-of-duplicate-assets}

如果您嘗試上傳[!DNL Adobe Experience Manager Assets]中存在的資產，重複偵測功能會將其識別為重複。 預設會停用重複偵測。 要啟用該功能，請執行以下步驟：

1. 通過訪問`https://[aem_server]:[port]/system/console/configMgr`開啟[!DNL Experience Manager] Web控制台配置頁。
1. 編輯Servlet **[!UICONTROL Day CQ DAM Create Asset]**&#x200B;的設定。
1. 選擇&#x200B;**[!UICONTROL 檢測重複]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL 保存]**。

   ![在servlet中選擇檢測重複選項](assets/chlimage_1-377.png)

   *圖：在servlet中選擇檢測重複選項。*

現在在[!DNL Assets]中啟用了檢測重複功能。 當使用者嘗試上傳[!DNL Experience Manager]中存在的資產時，系統會檢查衝突並指出衝突。 系統會使用儲存在`jcr:content/metadata/dam:sha1`的SHA-1雜湊來識別資產，這表示系統會無論檔案名稱為何都偵測到重複資產。

>[!MORELIKETHIS]
>
>* [在現有存放庫中複製資產（社群成員的教學課程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

