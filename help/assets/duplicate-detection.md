---
title: 啟用重複資產的偵測
description: 了解如何啟用偵測Experience Manager中的重複資產。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 啟用重複資產的偵測 {#enable-detection-of-duplicate-assets}

如果您嘗試上傳中存在的資產 [!DNL Adobe Experience Manager Assets]，重複偵測功能會將其識別為重複。 預設會停用重複偵測。 要啟用該功能，請執行以下步驟：

1. 開啟 [!DNL Experience Manager] Web控制台配置頁，方法是訪問 `https://[aem_server]:[port]/system/console/configMgr`.
1. 編輯servlet的配置 **[!UICONTROL 日CQ DAM建立資產]**.
1. 選取 **[!UICONTROL 偵測重複]** ，然後按一下 **[!UICONTROL 儲存]**.

   ![在servlet中選擇檢測重複選項](assets/chlimage_1-377.png)

   *圖：在servlet中選擇檢測重複選項。*

現在已在 [!DNL Assets]. 當使用者嘗試上傳中存在的資產時 [!DNL Experience Manager]，系統會檢查衝突並指出衝突。 會使用儲存於的SHA-1雜湊來識別資產 `jcr:content/metadata/dam:sha1`，表示系統會在檔案名稱無關的情況下偵測重複資產。

>[!MORELIKETHIS]
>
>* [在現有存放庫中複製資產（社群成員的教學課程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

