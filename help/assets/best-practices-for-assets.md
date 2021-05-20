---
title: ' [!DNL Assets]的最佳作法'
description: 通過確定和遵守取決於部署和配置的最佳做法，增強系統在負載下的穩定性和效能。
contentOwner: AG
feature: 資產管理
role: Architect, Administrator
exl-id: 6b50f1b3-9c1c-47c8-a43e-6f40c42a41cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# [!DNL Assets] {#best-practices-for-assets}的最佳作法

[!DNL Adobe Experience Manager Assets] 是提供高品質數位行銷體驗的重要環節，透過提升內容速度，有助於達成業務目標。如果您在[!DNL Experience Manager Assets]內處理大量資產，或定期/定期上傳許多資產，包括影片和Dynamic Media，則最佳化數位資產管理體驗對於提高系統效率至關重要。

根據您為組織放置[!DNL Assets]的方式，以及用於資產擷取、轉譯產生和中繼資料擷取的功能，識別並遵循不同區域的最佳實務，可大幅增強負載下的系統穩定性和效能。

檢閱下列指南後，您將擁有相關知識和工具，以建立和管理符合您需求的企業資產管理系統：

* [資產效能調整指南](/help/assets/performance-tuning-guidelines.md):本指南包含一組最佳實務，您可在實作的任何時間點依循這些作法，即使在上線後亦然，以確保充分運用您的系統。
* [資產規模調整指南](/help/assets/assets-sizing-guide.md) :在編製[!DNL Assets]實施的估計值時，務必確保在資產儲存、CPU、記憶體、IO和網路吞吐量方面有足夠的可用資源。 若要調整其中許多項目的大小，必須了解要將多少資產載入系統中。 本指南包括有助於確定用於估計[!DNL Assets]部署所需基礎架構和資源的有效度量的最佳實踐，以及規模調整工具。
* [資產移轉指南](/help/assets/assets-migration-guide.md):如果您想要將資產從舊版系統移轉至資產，請考慮執行數個步驟來簡化移轉程式。 移轉指南包含您執行之工作的相關最佳實務，以分階段方式將資產帶入[!DNL Experience Manager]。 這包括套用中繼資料、產生轉譯，以及啟動資產以發佈例項。
* [資產網路考量檔案](/help/assets/assets-network-considerations.md):在處理[!DNL Experience Manager]部署時，了解網路拓撲對於了解網路效能、識別中斷點和描述預期的用戶體驗非常重要。 [!DNL Assets]網路考量事項檔案會在設計資產部署時討論網路考量事項。
* [資產監控指南](/help/assets/assets-monitoring-best-practices.md):部署[!DNL Experience Manager]部署後，您應監視某些任務和一般系統，以確保系統的完整性和操作效率。 「監控」指南包含監控系統各個層面的最佳實務。
* [Experience Manager案頭應用程式最佳實務](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html): [!DNL Experience Manager] 案頭應用程式會將您的數位資產管理(DAM)解決方案與案頭連結，讓您可以直接在案頭開啟網頁使用者介 [!DNL Experience Manager] 面中可用的檔案。案頭應用程式的簡單易用工作流程，採用案頭作業系統提供的網路共用技術。 本指南說明[!DNL Experience Manager]案頭應用程式的主要功能和建議使用。
* [Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md):您可以透過多 [!DNL Experience Manager] 種方 [!DNL Creative Cloud] 式整合部署。遵循一些最佳實務來簡化您的整合和資產轉移工作流程，有助於實現最高效率。 本指南包含有關將[!DNL Assets]與[!DNL Adobe Creative Cloud]整合的最佳實務。
