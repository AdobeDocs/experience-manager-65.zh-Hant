---
title: 多語言資產和資產翻譯
description: 了解如何自動化工作流程，將資產（包括二進位檔、中繼資料和標籤）翻譯成多種語言。
contentOwner: AG
feature: Asset Management
role: Admin
exl-id: edccf23c-087e-4253-babb-dd4c6610517d
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 8%

---

# 多語言資產 {#multilingual-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/translate-assets.html?lang=en) |
| AEM 6.5 | 本文 |
| AEM 6.4 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-64/assets/using/multilingual-assets.html?lang=en) |

[!DNL Adobe Experience Manager Assets] 可讓您自動處理資產的翻譯工作流程（包括二進位檔、中繼資料和標籤），以產生其他語言的資產，以用於多語言專案。

為了自動化翻譯工作流，您整合了翻譯服務提供商與 [!DNL Experience Manager] 並建立專案，將資產翻譯成多種語言。 [!DNL Experience Manager] 支援人工和機器翻譯工作流程。

人類翻譯：翻譯的資產會退回並匯入 [!DNL Experience Manager]. 當翻譯提供者與 [!DNL Experience Manager]，資產會自動在 [!DNL Experience Manager] 和翻譯提供者。

機器翻譯：機器翻譯服務會立即轉譯資產的中繼資料和標籤。

換算資產包括下列各項：

1. [連接Experience Manager與翻譯服務提供程式](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [建立翻譯整合框架配置](/help/sites-administering/tc-tic.md)
1. [準備翻譯資產](preparing-assets-for-translation.md)
1. [將翻譯雲服務應用於資料夾](transition-cloud-services.md)
1. [建立翻譯專案](translation-projects.md)

如果您的翻譯服務提供者未提供要與 [!DNL Experience Manager]，請使用 [替代過程](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

另請參閱 [建立內容片段的翻譯專案](creating-translation-projects-for-content-fragments.md).
