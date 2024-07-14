---
title: 資料夾共用至 [!DNL Adobe Creative Cloud] 最佳實務
description: 設定 [!DNL Adobe Experience Manager] 以允許 [!DNL Experience Manager Assets] 中的使用者與Adobe Creative Cloud使用者交換資料夾。
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager]到[!DNL Adobe Creative Cloud]資料夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>已棄用[!DNL Experience Manager]到[!DNL Creative Cloud]資料夾共用功能。 Adobe建議使用較新的功能，例如[Adobe資產連結](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)或[Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)。 深入瞭解[Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)。

可以將[!DNL Adobe Experience Manager]設定為允許[!DNL Assets]中的使用者與[!DNL Adobe Creative Cloud]應用程式的使用者共用資料夾，以便在[!DNL Adobe Creative Cloud]資產服務中將這些資料夾作為共用資料夾使用。 此功能可用於在創意團隊和[!DNL Assets]使用者之間交換檔案，尤其是當創意使用者無權存取[!DNL Assets]部署（他們不在企業網路上）時。

此型別的整合可用於下列使用案例，特別是當使用無法直接存取[!DNL Assets]的使用者時：

* [!DNL Assets]使用者與[!DNL Adobe Creative Cloud]個檔案的使用者共用一組特定數位資產（例如，為新的行銷活動的設計工作提供創意簡報和一組已核准資產）。
* [!DNL Assets]使用者會收到[!DNL Adobe Creative Cloud]個應用程式使用者建立的新檔案。

>[!NOTE]
>
>閱讀本檔案之前，您可以檢閱整體[Experience Manager與Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)，以取得整合的概觀。

## 概觀 {#overview}

[!DNL Experience Manager]到[!DNL Creative Cloud]資料夾共用依賴伺服器端在[!DNL Assets]和[!DNL Creative Cloud]帳戶之間共用資料夾和檔案。 創意專業人士若在其案頭上使用[!DNL Creative Cloud]案頭應用程式，也可以使用[!DNL Adobe CreativeSync]技術直接在他們的磁碟上提供共用資料夾。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* 在企業網路(Managed Services或內部部署)中部署&#x200B;**[!DNL Experience Manager Assets]**：在這裡起始資料夾共用。
* **[!DNL Adobe Experience Cloud Assets]核心服務**：充當[!DNL Experience Manager]與[!DNL Creative Cloud]儲存服務之間的中介者。 使用整合之組織的管理員必須在Experience Cloud組織與[!DNL Assets]部署之間建立信任關係。 他們也[定義已核准的Creative Cloud共同作業人員清單](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html)，讓[!DNL Assets]使用者也能共用資料夾，以獲得額外的安全性。

* **[!DNL Creative Cloud]Assets Web服務** （儲存空間和[!DNL Creative Cloud]檔案Web UI）：這是共用了[!DNL Assets]資料夾的特定Creative Cloud應用程式使用者可以接受邀請並在其Creative Cloud帳戶儲存空間中檢視資料夾的位置。
* **Creative Cloud案頭應用程式**： （選擇性）允許透過與[!DNL Creative Cloud] Assets儲存空間的同步，從創意使用者的案頭直接存取共用資料夾/檔案。

## 特性與限制 {#characteristics-and-limitations}

* **變更的單向傳輸：**&#x200B;檔案變更只會以一個方向傳輸 — 從資產最初建立（上傳）的系統（[!DNL Experience Manager]或[!DNL Creative Cloud Assets]）。 整合不會提供兩個系統之間的完全自動化雙向同步。
* **版本設定：**

   * 如果檔案源自於[!DNL Experience Manager]並在其中更新，[!DNL Experience Manager]只會在更新時建立資產的版本。
   * [!DNL Creative Cloud] Assets提供自己的[版本設定功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html)，其目標為「進行中工作」更新（基本上會儲存最多10天的更新）

* **空間限制：**&#x200B;交換的檔案大小和磁碟區受到創意使用者特定[Creative CloudAssets配額](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html)的限制（視訂閱層級而定），以及5 GB最大檔案大小的限制。 空間也受到組織在Adobe Experience Cloud Assets核心服務中的資產配額限制。

* **空間需求：**&#x200B;共用資料夾中的檔案也必須實際儲存在[!DNL Experience Manager]中，然後儲存在[!DNL Creative Cloud]帳戶中，在[!DNL Experience Cloud Assets]核心服務中有快取復本。
* **網路與頻寬：**&#x200B;共用資料夾中的檔案與所有更新必須透過網路在系統之間傳輸。 確保僅共用相關的檔案和更新。
* **資料夾型別**：在[!DNL Adobe Experience Cloud]中的共用內容中不支援共用型別`sling:OrderedFolder`的[!DNL Assets]資料夾。 如果要共用資料夾，在[!DNL Assets]中建立資料夾時，請勿選取[!UICONTROL 已排序]選項。

## 最佳做法 {#best-practices}

使用[!DNL Experience Manager]到[!DNL Creative Cloud]資料夾共用的最佳實務包括：

* **磁碟區考量：** [!DNL Experience Manager]與[!DNL Creative Cloud]資料夾共用應該用於共用較少的檔案，例如，與特定行銷活動或活動相關的檔案。 若要共用較大的資產集，例如組織中所有已核准的資產，請使用其他發佈方法（例如，[!DNL Assets Brand Portal]）或[!DNL Experience Manager]案頭應用程式。
* **避免共用深層階層：**&#x200B;共用會遞回運作，不允許選擇性取消共用。 通常，只有沒有子資料夾或具有淺層階層（例如一個子資料夾層級）的資料夾才應該考慮進行共用。
* **單向共用的個別資料夾：**&#x200B;應使用個別資料夾從[!DNL Assets]到[!DNL Creative Cloud]個檔案共用最終資產，以及從[!DNL Creative Cloud]個檔案將[!DNL Assets]個創意就緒資產共用。 再加上這些資料夾的良好命名慣例，可為[!DNL Assets]和[!DNL Creative Cloud]使用者建立更易於瞭解的工作環境。
* **避免共用資料夾中的WIP：**&#x200B;請勿將共用資料夾用於進行中的工作 — 在Creative Cloud檔案中使用個別資料夾來執行需要經常變更檔案的工作。
* **在共用資料夾之外開始新工作：**&#x200B;新設計（創意檔案）應該在Creative Cloud檔案中的個別WIP資料夾中開始，當它們準備好與[!DNL Assets]使用者共用時，應該將其移動或儲存到共用資料夾。
* **簡化共用結構：**&#x200B;若要使用更易於管理的作業設定，請考慮簡化共用結構。 [!DNL Assets]資料夾不應與所有創意使用者共用，而應僅與團隊代表共用，例如創意總監或團隊經理。 創意部門的經理會收到最終資產、決定工作指派，然後讓設計人員處理自己在製品資產的Creative Cloud帳戶。 他們可以使用Creative Cloud共同作業功能來協調工作，最後選取並放置準備好要共用回[!DNL Assets]的資產到他們的創意就緒共用資料夾。

下圖說明根據來自[!DNL Assets]的現有最終資產建立設計的設定範例。

![chlimage_1-180](assets/chlimage_1-407.png)
