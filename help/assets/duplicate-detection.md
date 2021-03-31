---
title: 可偵測重複資產
description: 瞭解如何啟用偵測Experience Manager中的重複資產。
contentOwner: AG
role: 業務從業人員、管理員
feature: 資產管理，資產報表
translation-type: tm+mt
source-git-commit: aec4530fa93eacd151ca069c2da5d1bc92408e10
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# 啟用重複資產{#enable-detection-of-duplicate-assets}的偵測

如果您嘗試上傳存在於[!DNL Adobe Experience Manager Assets]中的資產，重複偵測功能會將其識別為重複。 預設會停用重複偵測。 要啟用該功能，請執行以下步驟：

1. 通過訪問`https://[aem_server]:[port]/system/console/configMgr`開啟[!DNL Experience Manager] Web控制台配置頁。
1. 編輯servlet **[!UICONTROL Day CQ DAM Create Asset]**&#x200B;的配置。
1. 選擇&#x200B;**[!UICONTROL detect duplicate]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL Save]**。

   ![在servlet中選擇檢測重複選項](assets/chlimage_1-377.png)

   *圖：在servlet中選擇「檢測重複」選項。*

現在[!DNL Assets]中已啟用偵測重複功能。 當使用者嘗試上傳存在於[!DNL Experience Manager]中的資產時，系統會檢查衝突並指出衝突。 資產使用儲存在`jcr:content/metadata/dam:sha1`的SHA-1雜湊來識別，這表示不論檔案名稱為何，都會偵測到重複資產。

>[!MORELIKETHIS]
>
>* [現有儲存庫中重複的資產（社區成員的教程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)

