---
title: 資料夾共用 [!DNL Adobe Creative Cloud] 至最佳實務
description: 設 [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 定以與Adobe Creative Cloud(CC)使用者交換資料夾。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 5069c2cd26e84866d72a61d36de085dadd556cdd
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 到檔案 [!DNL Adobe Creative Cloud] 夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>「至 [!DNL Experience Manager] 資料 [!DNL Creative Cloud] 夾共用」功能已過時。 Adobe強烈建議使用較新的功能，例如 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)[或Experience Manager案頭應用程式](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)。 進一步了 [解Experience Manager和Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)。

[!DNL Adobe Experience Manager] 可設定為允許中的使用者 [!DNL Assets] 與應用程式的使用者共用資料夾， [!DNL Adobe Creative Cloud] 以便在資產服務中以共用資料夾的形 [!DNL Adobe Creative Cloud] 式使用。 此功能可用於創意團隊和使用者之間交換檔案 [!DNL Assets] ，尤其是當創意使用者無法存取部署時(他們不在企業網 [!DNL Assets] 路上)。

此類整合可用於下列使用案例，尤其是與沒有直接存取權的使用者合作時 [!DNL Assets]:

* [!DNL Assets] 使用者與檔案使用者共用一組特定數位資產(例如 [!DNL Adobe Creative Cloud] 一組創意簡報和一組已核准的資產，以用於新的行銷活動的設計作品)。
* [!DNL Assets] 使用者會收到應用程式使用者建立的 [!DNL Adobe Creative Cloud] 新檔案。

>[!NOTE]
>
>在閱讀本檔案之前，您可以先閱讀整體 [Experience Manager和Creative Cloud整合的最佳實務](/help/assets/aem-cc-integration-best-practices.md) ，以瞭解整合的概觀。

## 概覽 {#overview}

[!DNL Experience Manager] 至資 [!DNL Creative Cloud] 料夾共用需仰賴伺服器端在與帳戶之間共用資料夾和 [!DNL Assets] 檔案 [!DNL Creative Cloud] 。 在桌上型電腦上使用案頭 [!DNL Creative Cloud] 應用程式的創意專業人員，也可以使用技術，將共用資料夾直接在光碟上 [!DNL Adobe CreativeSync] 使用。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* **[!DNL Experience Manager Assets]** 部署在企業網路（受管理服務或內部部署）中：資料夾共用會從這裡開始。
* **[!DNL Adobe Marketing Cloud Assets]核心服務**:充當儲存服務與儲存服 [!DNL Experience Manager] 務之 [!DNL Creative Cloud] 間的中介。 使用整合的組織管理員需要在Marketing Cloud組織與部署之間建立信任關 [!DNL Assets] 系。 他們也 [會定義已核准的Creative Cloud共同作業人員清單](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)，讓使 [!DNL Assets] 用者也可以共用資料夾，以提高安全性。

* **[!DNL Creative Cloud]資產web services** (儲存空間和檔 [!DNL Creative Cloud] 案web UI):這是特定Creative Cloud應用程式使用者(共用資料夾 [!DNL Assets] 的使用者)可接受邀請並在其Creative Cloud帳戶儲存空間中查看資料夾的地方。
* **Creative Cloud案頭應用程式**:（可選）允許透過與資產儲存空間同步，從創意使用者的案頭直接存取共用資料夾/ [!DNL Creative Cloud] 檔案。

## 特性與限制 {#characteristics-and-limitations}

* **更改的單向傳播：** 檔案變更只會傳播至一個方向——從系統([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])傳播，而系統（或）原本是建立（上傳）資產。 此整合無法提供兩個系統之間完全自動化的雙向同步。
* **版本設定:**

   * [!DNL Experience Manager] 只會在更新時建立資產版本(如果檔案是源自此處並 [!DNL Experience Manager] 在此處更新)。
   * [!DNL Creative Cloud] 資產提供其自 [己的版本](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 化功能，其目標是「進行中的作品」更新（基本上，可將更新儲存至10天）

* **空間限制：** 交換的檔案大小和數量受創意使用者專屬的 [Creative Cloud Assets配額(視訂閱層級而定](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) )和最大檔案大小限制為5 GB。 此外，組織在Adobe Marketing Cloud Assets核心服務中的資產配額也限制了空間。

* **空間需求：** 共用資料夾中的檔案也必須實際儲存在帳戶中， [!DNL Experience Manager] 然後在核 [!DNL Creative Cloud] 心服務中使用快取 [!DNL Marketing Cloud Assets] 的副本。
* **網路和頻寬：** 共用資料夾中的檔案和所有更新都需要通過網路在系統之間傳輸。 您應確保僅共用相關檔案和更新。
* **資料夾類型**:共用類 [!DNL Assets] 型的資料夾 `sling:OrderedFolder`時，不支援在中共用的內容 [!DNL Adobe Marketing Cloud]。 如果要共用資料夾，在中建立資料夾時，請 [!DNL Assets]不要選擇「已 [!UICONTROL 訂購] 」選項。

## Best practices {#best-practices}

利用資料夾共用的 [!DNL Experience Manager] 最佳 [!DNL Creative Cloud] 實務包括：

* **卷注意事項：**[!DNL Experience Manager] 資料 [!DNL Creative Cloud] 夾共用功能應用於共用較少的檔案，例如與特定促銷活動或活動相關的檔案。 若要共用較大的資產集（如組織中所有已核准的資產），請使用其他分發方法(例如 [!DNL Assets Brand Portal])或案頭應 [!DNL Experience Manager] 用程式。
* **避免共用深層次：** 分享會以遞歸方式運作，不允許選擇性取消分享。 通常，只有沒有子資料夾或具有非常淺層層次的資料夾（如1個子資料夾級別）才應考慮共用。
* **分開資料夾以進行單向共用：** 應使用個別資料夾，將最終資產從檔案共 [!DNL Assets] 用至 [!DNL Creative Cloud] 檔案，並將創意就緒資產從檔案共 [!DNL Creative Cloud] 用至檔案 [!DNL Assets]。 再加上這些資料夾的良好命名慣例，讓使用者都能更容易瞭解工作 [!DNL Assets] 環 [!DNL Creative Cloud] 境。
* **避免在共用資料夾中執行WIP:** 共用資料夾不應用於「進行中的作品」-請在「Creative Cloud檔案」中使用個別資料夾來執行需要經常變更檔案的工作。
* **在共用資料夾之外開始新工作：** 新設計（創意檔案）應從Creative Cloud檔案的個別WIP檔案夾中啟動，當它們準備好要與使用者共用時，應將它們移動或儲存至共用檔案夾。 [!DNL Assets]
* **簡化共用結構：** 若要建立更易於管理的作業設定，請考慮簡化共用結構。 資料夾不應與所有創意使用者共 [!DNL Assets] 用，而應僅與團隊代表共用，例如創意主管或團隊經理。 創意部門的經理將會收到最終資產、決定工作指派，然後讓設計人員在自己的Creative Cloud帳戶中處理WIP資產。 他們可使用Creative Cloud協作功能來協調工作，最後選擇並放回可供創意使用的共用資料 [!DNL Assets] 夾中的資產。

下圖說明如何根據現有最終資產建立新設計的範例設定 [!DNL Assets]。

![chlimage_1-180](assets/chlimage_1-407.png)
