---
title: 資料夾共用至 [!DNL Adobe Creative Cloud] 最佳實務
description: 設定 [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 以與Adobe Creative Cloud使用者交換資料夾。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 到資 [!DNL Adobe Creative Cloud] 料夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>已棄用[!DNL Experience Manager]到[!DNL Creative Cloud]資料夾共用功能。 Adobe強烈建議使用較新的功能，例如[Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)或[Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)。 進一步了解[Experience Manager和Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)。

[!DNL Adobe Experience Manager] 可設定為允許中的使用者與 [!DNL Assets] 應用程式的使用者共用資料夾， [!DNL Adobe Creative Cloud] 以便在assets服務中以共用資料夾的形 [!DNL Adobe Creative Cloud] 式使用。此功能可用於創意團隊與[!DNL Assets]使用者之間交換檔案，尤其是當創意使用者無法存取[!DNL Assets]部署時（他們不在企業網路上）。

此類型的整合可用於下列使用案例，尤其是與沒有直接存取[!DNL Assets]之使用者合作時：

* [!DNL Assets] 使用者與檔案的使用者共用一組特 [!DNL Adobe Creative Cloud] 定數位資產（例如創意簡報和一組經過核准的資產，供新行銷活動的設計工作使用）。
* [!DNL Assets] 使用者會收到應用程式使用者建 [!DNL Adobe Creative Cloud] 立的新檔案。

>[!NOTE]
>
>閱讀本檔案前，您可以先檢閱整體[Experience Manager和Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)，以了解整合的概觀。

## 概覽 {#overview}

[!DNL Experience Manager] 資料 [!DNL Creative Cloud] 夾共用需仰賴伺服器端在和帳戶之間共用資料夾和 [!DNL Assets] 檔 [!DNL Creative Cloud] 案。在其案頭上使用[!DNL Creative Cloud]案頭應用程式的創意專業人員可使用[!DNL Adobe CreativeSync]技術，在其磁碟上直接使用共用資料夾。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* **[!DNL Experience Manager Assets]** 部署在企業網路（受管服務或內部部署）中：資料夾共用會在此啟動。
* **[!DNL Adobe Marketing Cloud Assets]核心服務**:充當和儲存服務 [!DNL Experience Manager] 之 [!DNL Creative Cloud] 間的中介。使用整合的組織的管理員需要在Marketing Cloud組織和[!DNL Assets]部署之間建立信任關係。 它們也[定義已核准Creative Cloud共同作業人員的清單](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html)，讓[!DNL Assets]使用者也可以共用資料夾以提供額外安全性。

* **[!DNL Creative Cloud]資產網站服務** (儲存和檔 [!DNL Creative Cloud] 案網頁UI):這是共用資料夾的特定Creative Cloud應用 [!DNL Assets] 程式使用者能夠接受邀請並在其Creative Cloud帳戶儲存體中查看資料夾的位置。
* **Creative Cloud案頭應用程式**:（可選）可透過與Assets儲存空間同步，從創意使用者的案頭直接存取共用資料夾/ [!DNL Creative Cloud] 檔案。

## 特徵和限制 {#characteristics-and-limitations}

* **變更的單向傳播：** 檔案變更只會傳播至一個方向 — 從資產最初建立（上傳）的系統([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])。整合不提供兩個系統之間完全自動化的雙向同步。
* **版本設定:**

   * [!DNL Experience Manager] 只有在檔案源自於且在該處更新時，才會在更新時建 [!DNL Experience Manager] 立資產的版本。
   * [!DNL Creative Cloud] 資產提供其專 [屬的](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 版本設定功能，目標為「進行中的工作」更新（基本上，可儲存最多10天的更新）

* **空間限制：** 檔案交換的大小和數量受創意使用者特 [定Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 資產配額（視訂閱層級而定）以及檔案大小上限為5 GB的限制。此外，組織在Adobe Marketing Cloud Assets核心服務中的資產配額，也限制了空間。

* **空間需求：** 共用資料夾中的檔案也需實際儲存在中， [!DNL Experience Manager] 然後儲 [!DNL Creative Cloud] 存在帳戶中，核心服務中需有 [!DNL Marketing Cloud Assets] 快取副本。
* **網路和頻寬：** 共用資料夾中的檔案和所有更新都需要通過網路在系統之間傳輸。您應確保僅共用相關檔案和更新。
* **資料夾類型**:共用 [!DNL Assets] 類型的資料 `sling:OrderedFolder`夾在中的共用內容不受支 [!DNL Adobe Marketing Cloud]援。如果要共用資料夾，在[!DNL Assets]中建立資料夾時，請勿選取[!UICONTROL Ordered]選項。

## 最佳實務 {#best-practices}

將[!DNL Experience Manager]運用於[!DNL Creative Cloud]資料夾共用的最佳實務包括：

* **數量考量：** [!DNL Experience Manager] 和資 [!DNL Creative Cloud] 料夾共用應該用來共用較少數量的檔案，例如與特定促銷活動或活動相關的檔案。若要共用較大的資產集（如組織中所有已核准的資產），請使用其他分送方法（例如[!DNL Assets Brand Portal]）或[!DNL Experience Manager]案頭應用程式。
* **避免共用深層階層：** 共用會遞回運作，不允許選擇性取消共用。通常，只有沒有子資料夾的資料夾或層次結構非常淺的資料夾（如1個子資料夾級別）才應視為共用。
* **分隔資料夾以進行單向共用：** 應使用個別資料夾來共用從到檔案的最終 [!DNL Assets] 資 [!DNL Creative Cloud] 產，以及將創意就緒的資產從檔案共用 [!DNL Creative Cloud] 回 [!DNL Assets]檔案。它再加上這些資料夾的良好命名慣例，為[!DNL Assets]和[!DNL Creative Cloud]使用者建立了一個更容易理解的工作環境。
* **避免在共用資料夾中進行WIP:** 不應將共用資料夾用於進行中的工作 — 在Creative Cloud檔案中使用個別資料夾來執行需要經常變更檔案的工作。
* **在共用資料夾之外開始新工作：** 新設計（創作檔案）應在「Creative Cloud檔案」的個別WIP資料夾中啟動，當它們準備好與使用者共用時，應將其 [!DNL Assets] 移動或儲存至共用資料夾。
* **簡化共用結構：** 為了提供更方便管理的作業設定，請考慮簡化共用結構。[!DNL Assets]資料夾不應與所有創意使用者共用，而應僅與團隊代表共用，例如創意總監或團隊經理。 創意層的經理將接收最終資產、決定工作分配，然後讓設計師在自己的Creative Cloud帳戶中處理在製品資產。 他們可以使用Creative Cloud協作功能來協調工作，最後選擇準備好共用回[!DNL Assets]的資產，並將其放入創意就緒的共用資料夾。

下圖說明根據[!DNL Assets]的現有最終資產建立新設計的範例設定。

![chlimage_1-180](assets/chlimage_1-407.png)
