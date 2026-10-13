---
title: 啟用偵測重複資產
description: 瞭解如何在Experience Manager中啟用重複資產偵測功能。
contentOwner: AG
role: User, Admin
feature: Asset Management,Asset Reports
exl-id: a403d60e-2193-4835-8f37-4a40f2d01819
hide: true
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: c29e3a96-cd2b-4e21-b382-a8279aa04553
    internal-label: Asset reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%
---
# 啟用偵測重複資產 {#enable-detection-of-duplicate-assets}

如果您嘗試上傳[!DNL Adobe Experience Manager Assets]中存在的資產，重複資料偵測功能會將其識別為重複。 重複資料偵測預設為停用。 若要啟用此功能，請執行下列步驟：

1. 存取`https://[aem_server]:[port]/system/console/configMgr`以開啟[!DNL Experience Manager] Web主控台設定頁面。
1. 編輯Servlet **[!UICONTROL Day CQ DAM建立資產]**&#x200B;的設定。
1. 選取&#x200B;**[!UICONTROL 偵測重複]**&#x200B;選項，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   ![選取servlet中的偵測重複選項](assets/chlimage_1-377.png)

   *圖：選取servlet中的偵測重複選項。*

[!DNL Assets]中現在已啟用偵測重複功能。 當使用者嘗試上傳存在於[!DNL Experience Manager]中的資產時，系統會檢查衝突並加以指示。 資產識別使用儲存在`jcr:content/metadata/dam:sha1`的SHA-1雜湊，這表示不論檔案名稱為何，都會偵測到重複的資產。

>[!MORELIKETHIS]
>
>* [在現有存放庫中複製資產（來自社群成員的教學課程）](https://experience-aem.blogspot.com/2019/06/aem-65-find-duplicate-assets-binaries-in-existing-repository.html)
>* [在AEM as a Cloud Service中偵測重複的資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/detect-duplicate-assets.html?lang=zh-Hant)
