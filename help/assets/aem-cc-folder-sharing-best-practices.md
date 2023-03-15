---
title: 資料夾共用至 [!DNL Adobe Creative Cloud] 最佳實務
description: 設定 [!DNL Adobe Experience Manager] 允許使用者 [!DNL Experience Manager Assets] 與Adobe Creative Cloud使用者交換資料夾。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] to [!DNL Adobe Creative Cloud] 資料夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>此 [!DNL Experience Manager] to [!DNL Creative Cloud] 已棄用資料夾共用功能。 Adobe強烈建議使用較新的功能，例如 [Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) 或 [Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). 深入了解 [Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] 可設定為允許 [!DNL Assets] 要與 [!DNL Adobe Creative Cloud] 應用程式，因此可在共用資料夾中使用 [!DNL Adobe Creative Cloud] 資產服務。 此功能可用於創意團隊和 [!DNL Assets] 使用者，尤其是當創意使用者無法存取 [!DNL Assets] 部署（不在企業網路上）。

這類整合可用於下列使用案例，尤其是與沒有直接存取權的使用者合作時 [!DNL Assets]:

* [!DNL Assets] 使用者與的使用者共用一組特定數位資產 [!DNL Adobe Creative Cloud] 檔案（例如，新行銷活動的設計作品創意簡報和一組已核准資產）。
* [!DNL Assets] 使用者會收到由 [!DNL Adobe Creative Cloud] 應用程式使用者。

>[!NOTE]
>
>閱讀本檔案之前，您可以檢閱整體 [Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md) 以取得整合的概觀。

## 概觀 {#overview}

[!DNL Experience Manager] to [!DNL Creative Cloud] 資料夾共用依賴於伺服器端在 [!DNL Assets] 和 [!DNL Creative Cloud] 帳戶。 創意專業人員，使用 [!DNL Creative Cloud] 案頭應用程式，可使用 [!DNL Adobe CreativeSync] 技術。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* **[!DNL Experience Manager Assets]** 部署在企業網路（受管服務或內部部署）中：資料夾共用會在此啟動。
* **[!DNL Adobe Marketing Cloud Assets]核心服務**:在 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 儲存服務。 使用整合之組織的管理員需要在Marketing Cloud組織與 [!DNL Assets] 部署。 它們也 [定義已核准的Creative Cloud共同作業人員清單](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), [!DNL Assets] 使用者也可以共用資料夾以提供額外安全性。

* **[!DNL Creative Cloud]Assets網站服務** (儲存和 [!DNL Creative Cloud] 檔案web UI):這是特定Creative Cloud應用程式使用者的位置，與 [!DNL Assets] 資料夾已共用，則可接受邀請並在其Creative Cloud帳戶儲存中查看資料夾。
* **Creative Cloud案頭應用程式**:（可選）可透過同步功能，從創意使用者的案頭直接存取共用資料夾/檔案 [!DNL Creative Cloud] 資產儲存。

## 特徵和限制 {#characteristics-and-limitations}

* **更改的單向傳播：** 檔案更改只傳播到一個方向 — 從系統([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])，即資產最初建立（上傳）的位置。 整合不提供兩個系統之間完全自動化的雙向同步。
* **版本設定:**

   * [!DNL Experience Manager] 只會在檔案源自於 [!DNL Experience Manager] 和已更新。
   * [!DNL Creative Cloud] 資產提供自己的 [版本化功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 此更新針對進行中工作更新（基本上，會儲存最多10天的更新）

* **空間限制：** 交換的檔案的大小和數量受特定 [Creative Cloud資產配額](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 對於創意使用者（視訂閱層級而定），且檔案大小上限為5 GB。 此外，組織在Adobe Marketing Cloud Assets核心服務中的資產配額，也限制了空間。

* **空間需求：** 共用資料夾中的檔案也需實際儲存在 [!DNL Experience Manager] 然後進入 [!DNL Creative Cloud] 帳戶，包含快取副本 [!DNL Marketing Cloud Assets] 核心服務。
* **網路和頻寬：** 共用資料夾中的檔案和所有更新需要通過網路在系統之間傳輸。 您應確保僅共用相關檔案和更新。
* **資料夾類型**:共用 [!DNL Assets] 類型的資料夾 `sling:OrderedFolder`，不支援在中共用的情境中 [!DNL Adobe Marketing Cloud]. 如果要共用資料夾，請在 [!DNL Assets]，不選取 [!UICONTROL 已訂購] 選項。

## 最佳實務 {#best-practices}

善用 [!DNL Experience Manager] to [!DNL Creative Cloud] 資料夾共用包括：

* **卷考量事項：** [!DNL Experience Manager] 和 [!DNL Creative Cloud] 資料夾共用應該用來共用較小數量的檔案，例如與特定促銷活動或活動相關的檔案。 若要共用較大的資產集（如組織中所有已核准的資產），請使用其他分送方法(例如 [!DNL Assets Brand Portal])或 [!DNL Experience Manager] 案頭應用程式。
* **避免共用深層階層：** 共用會遞回運作，不允許選擇性取消共用。 通常，只有沒有子資料夾的資料夾或層次結構非常淺的資料夾（如1個子資料夾級別）才應視為共用。
* **將資料夾分開以進行單向共用：** 應使用個別資料夾來共用最終資產，從 [!DNL Assets] to [!DNL Creative Cloud] 檔案，以及共用創意資產的 [!DNL Creative Cloud] 檔案 [!DNL Assets]. 此外，還能針對這些資料夾建立良好的命名慣例，為 [!DNL Assets] 和 [!DNL Creative Cloud] 使用者。
* **避免在共用資料夾中出現WIP:** 共用資料夾不應用於進行中的工作 — 在Creative Cloud檔案中使用單獨的資料夾來執行需要頻繁更改檔案的工作。
* **在共用資料夾之外開始新工作：** 新設計（創作檔案）應在「Creative Cloud檔案」中個別的WIP資料夾中啟動，且當它們準備好與共用時 [!DNL Assets] 使用者，應將其移動或儲存至共用資料夾。
* **簡化共用結構：** 要建立更易於管理的操作設定，請考慮簡化共用結構。 與其與所有創意使用者分享， [!DNL Assets] 資料夾只應與團隊代表共用，例如創意總監或團隊經理。 創意層的經理將接收最終資產、決定工作分配，然後讓設計師在自己的Creative Cloud帳戶中處理在製品資產。 他們可以使用Creative Cloud協作功能來協調工作，最後選擇並放回已準備好共用的資產 [!DNL Assets] 放入可供創意素材的共用資料夾。

下圖說明根據現有最終資產建立新設計的範例設定，來自 [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
