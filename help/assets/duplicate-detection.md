---
title: 啟用重複資產的檢測
description: 瞭解如何啟用在Experience Manager中檢測重複資產。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 0%

---

# 啟用重複資產的檢測 {#enable-detection-of-duplicate-assets}

如果嘗試上載中存在的資產 [!DNL Adobe Experience Manager Assets]，重複檢測功能將其標識為重複。 預設情況下禁用重複檢測。 要啟用該功能，請執行以下步驟：

1. 開啟 [!DNL Experience Manager] 通過訪問 `https://[aem_server]:[port]/system/console/configMgr`。
1. 編輯Servlet的配置 **[!UICONTROL 第CQ天建立資產]**。
1. 選擇 **[!UICONTROL 檢測重複]** ，然後按一下 **[!UICONTROL 保存]**。

   ![在Servlet中選擇檢測重複選項](assets/chlimage_1-377.png)

   *圖：在servlet中選擇「檢測重複」選項。*

檢測重複功能現在在中啟用 [!DNL Assets]。 當用戶嘗試上載中存在的資產時 [!DNL Experience Manager]，系統檢查衝突並指示衝突。 使用儲存在以下位置的SHA-1散列來標識資產 `jcr:content/metadata/dam:sha1`，這意味著不管檔案名如何，都會檢測重複的資產。

>[!MORELIKETHIS]
>
>* [現有儲存庫中的重複資產（社區成員的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

