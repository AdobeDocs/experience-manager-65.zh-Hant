---
title: 資料夾共用到 [!DNL Adobe Creative Cloud] 最佳做法
description: 配置 [!DNL Adobe Experience Manager] 允許用戶 [!DNL Experience Manager Assets] 與Adobe Creative Cloud用戶交換資料夾。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] 至 [!DNL Adobe Creative Cloud] 資料夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>的 [!DNL Experience Manager] 至 [!DNL Creative Cloud] 不建議使用資料夾共用功能。 Adobe強烈建議使用較新的功能，如 [Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) 或 [Experience Manager案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)。 瞭解詳情 [Experience Manager和Creative Cloud整合最佳做法](/help/assets/aem-cc-integration-best-practices.md)。

[!DNL Adobe Experience Manager] 可以配置為允許用戶 [!DNL Assets] 與 [!DNL Adobe Creative Cloud] 應用程式，因此它們可作為共用資料夾在 [!DNL Adobe Creative Cloud] 資產服務。 此功能可用於在創意團隊和 [!DNL Assets] 用戶，尤其是當創意用戶無法訪問 [!DNL Assets] 部署（它們不在企業網路中）。

此類整合可用於以下使用情形，特別是與沒有直接訪問權限的用戶協作時 [!DNL Assets]:

* [!DNL Assets] 用戶與 [!DNL Adobe Creative Cloud] 檔案（例如，為新的市場營銷活動設計工作提供的創作簡報和一組批准的資產）。
* [!DNL Assets] 用戶接收新檔案 [!DNL Adobe Creative Cloud] 應用程式用戶。

>[!NOTE]
>
>在閱讀此文檔之前，您可以查看 [Experience Manager和Creative Cloud整合最佳做法](/help/assets/aem-cc-integration-best-practices.md) 的子菜單。

## 概觀 {#overview}

[!DNL Experience Manager] 至 [!DNL Creative Cloud] 資料夾共用依賴於在以下位置之間對資料夾和檔案的伺服器端共用 [!DNL Assets] 和 [!DNL Creative Cloud] 帳戶。 有創意的專業人員， [!DNL Creative Cloud] 案頭上的案頭應用程式，還可以使用 [!DNL Adobe CreativeSync] 技術。

下圖提供了整合的概述。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包括以下元素：

* **[!DNL Experience Manager Assets]** 部署在企業網路（托管服務或內部部署）中：此處啟動資料夾共用。
* **[!DNL Adobe Marketing Cloud Assets]核心服務**:充當 [!DNL Experience Manager] 和 [!DNL Creative Cloud] 儲存服務。 使用整合的組織的管理員需要在Marketing Cloud組織和 [!DNL Assets] 部署。 也 [定義已批准的Creative Cloud協作者清單](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), [!DNL Assets] 用戶也可以共用資料夾以獲得更多安全性。

* **[!DNL Creative Cloud]資產Web服務** (儲存和 [!DNL Creative Cloud] 檔案Web UI):這是特定Creative Cloud應用用戶的位置， [!DNL Assets] 資料夾已共用，將能夠接受邀請並在其Creative Cloud帳戶儲存中查看該資料夾。
* **Creative Cloud案頭應用**:（可選）允許通過與同步從創意用戶案頭直接訪問共用資料夾/檔案 [!DNL Creative Cloud] 資產儲存。

## 特點和限制 {#characteristics-and-limitations}

* **更改的單向傳播：** 檔案更改僅沿一個方向傳播 — 從系統([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])，資產最初建立（上載）的位置。 該整合沒有提供兩個系統之間的完全自動化雙向同步。
* **版本設定:**

   * [!DNL Experience Manager] 僅在檔案源於 [!DNL Experience Manager] 並在那裡更新。
   * [!DNL Creative Cloud] 資產提供自己的 [版本控制功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 針對Work in Progress更新（基本上，儲存最多10天的更新）

* **空間限制：** 交換的檔案的大小和數量受特定 [Creative Cloud資產配額](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 對於創意用戶（取決於訂閱級別），最大檔案大小限制為5 GB。 此外，該組織在Adobe Marketing Cloud資產核心服務中的資產配額也限制了空間。

* **空間要求：** 共用資料夾中的檔案還需要物理儲存在 [!DNL Experience Manager] 然後 [!DNL Creative Cloud] 帳戶，其中包含快取副本 [!DNL Marketing Cloud Assets] 核心服務。
* **網路和頻寬：** 共用資料夾中的檔案和所有更新需要通過網路在系統之間傳輸。 您應確保僅共用相關檔案和更新。
* **資料夾類型**:共用 [!DNL Assets] 類型的資料夾 `sling:OrderedFolder`，在中共用的上下文中不受支援 [!DNL Adobe Marketing Cloud]。 如果要共用資料夾，則在中建立資料夾時 [!DNL Assets]，不選擇 [!UICONTROL 已訂購] 的雙曲餘切值。

## 最佳做法 {#best-practices}

利用 [!DNL Experience Manager] 至 [!DNL Creative Cloud] 資料夾共用包括：

* **卷注意事項：** [!DNL Experience Manager] 和 [!DNL Creative Cloud] 資料夾共用應用於共用較少的檔案，例如與特定市場活動或活動相關的檔案。 要共用較大的資產集，如組織中所有已批准的資產，請使用其他分配方法(例如， [!DNL Assets Brand Portal])或 [!DNL Experience Manager] 案頭應用。
* **避免共用深層次結構：** 共用是循環工作的，不允許有選擇地取消共用。 通常，只有沒有子資料夾或層次結構非常淺的資料夾（如1個子資料夾級別）才應考慮共用。
* **單向共用的單獨資料夾：** 應使用單獨的資料夾來共用最終資產 [!DNL Assets] 至 [!DNL Creative Cloud] 檔案，並用於從共用創意就緒資產 [!DNL Creative Cloud] 檔案 [!DNL Assets]。 再加上這些資料夾的良好命名約定，它為您建立了一個更易於理解的工作環境 [!DNL Assets] 和 [!DNL Creative Cloud] 用戶都一樣。
* **避免共用資料夾中的WIP:** 不應將共用資料夾用於「正在進行的工作」 — 在「Creative Cloud檔案」中使用單獨的資料夾執行需要頻繁更改檔案的工作。
* **在共用資料夾外啟動新工作：** 新設計（創作檔案）應在「Creative Cloud檔案」中的單獨WIP資料夾中啟動，並且當它們準備與共用時 [!DNL Assets] 將其移動或保存到共用資料夾。
* **簡化共用結構：** 要獲得更易於管理的操作設定，請考慮簡化共用結構。 與其與所有創意用戶分享， [!DNL Assets] 資料夾應僅與團隊代表共用，如創意總監或團隊經理。 創意方面的經理將接收最終資產，決定工作分配，然後讓設計師在自己的Creative Cloud賬戶中就WIP資產工作。 他們可以使用Creative Cloud協作功能來協調工作，最後選擇並放回準備共用的資產 [!DNL Assets] 進入他們的可創作共用資料夾。

下圖說明了一個示例配置，用於根據現有最終資產從 [!DNL Assets]。

![chlimage_1-180](assets/chlimage_1-407.png)
