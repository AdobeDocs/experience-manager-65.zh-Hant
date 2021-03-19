---
title: 資料夾共用至 [!DNL Adobe Creative Cloud] 最佳實務
description: 配置 [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] 以與Adobe Creative Cloud(CC)用戶交換資料夾。
contentOwner: AG
role: 業務從業人員、管理員
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] 到檔案 [!DNL Adobe Creative Cloud] 夾共用  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>[!DNL Experience Manager]至[!DNL Creative Cloud]資料夾共用功能已過時。 Adobe強烈建議使用較新的功能，例如[Adobe資產連結](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html)或[Experience Manager案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)。 進一步瞭解[Experience Manager與Creative Cloud整合最佳實踐](/help/assets/aem-cc-integration-best-practices.md)。

[!DNL Adobe Experience Manager] 可設定為允許中的使 [!DNL Assets] 用者與應用程式的使用者共用資 [!DNL Adobe Creative Cloud] 料夾，以便在資產服務中以共用資料 [!DNL Adobe Creative Cloud] 夾的形式使用。此功能可用於創意團隊和[!DNL Assets]使用者之間交換檔案，尤其是當創意使用者無法存取[!DNL Assets]部署時（他們不在企業網路上）。

此類整合可用於下列使用案例，尤其是與沒有直接存取[!DNL Assets]的使用者合作時：

* [!DNL Assets] 使用者與檔案使用者共用一組特定數位資 [!DNL Adobe Creative Cloud] 產（例如，一組創意簡報和一組已核准的資產，以用於新的行銷活動的設計作品）。
* [!DNL Assets] 使用者會收到應用程式使用者建立 [!DNL Adobe Creative Cloud] 的新檔案。

>[!NOTE]
>
>在閱讀本檔案之前，您可以先閱讀整體[Experience Manager與Creative Cloud整合最佳範例](/help/assets/aem-cc-integration-best-practices.md)，以取得整合的概觀。

## 概覽 {#overview}

[!DNL Experience Manager] 到文 [!DNL Creative Cloud] 件夾共用依賴於資料夾和檔案在與帳戶之間的伺服器端 [!DNL Assets] 共用 [!DNL Creative Cloud] 。在桌上型電腦上使用[!DNL Creative Cloud]案頭應用程式的創意專業人員，也可以使用[!DNL Adobe CreativeSync]技術，將共用資料夾直接在光碟上使用。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* **[!DNL Experience Manager Assets]** 部署在企業網路（受管理服務或內部部署）中：資料夾共用會從這裡開始。
* **[!DNL Adobe Marketing Cloud Assets]核心服務**:充當儲存服務 [!DNL Experience Manager] 和存 [!DNL Creative Cloud] 儲服務。使用整合的組織的管理員需要在Marketing Cloud組織和[!DNL Assets]部署之間建立信任關係。 它們還[定義了已批准的Creative Cloud協作者清單](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html),[!DNL Assets]用戶也可以共用資料夾，以提高安全性。

* **[!DNL Creative Cloud]資產web services** (儲存和檔 [!DNL Creative Cloud] 案web UI):這是特定Creative Cloud應用程式使用者(與其共 [!DNL Assets] 用資料夾)可接受邀請並在其Creative Cloud帳戶儲存區中查看資料夾的地方。
* **Creative Cloud案頭應用程式**:（可選）允許透過與資產儲存空間同步，從創意使用者的案頭直接存取共用資料夾/ [!DNL Creative Cloud] 檔案。

## 特性和限制{#characteristics-and-limitations}

* **變更的單向傳播：** 檔案變更只會從原本建立（上傳）資產的系統([!DNL Experience Manager] 或 [!DNL Creative Cloud Assets])沿一個方向傳播。此整合無法提供兩個系統之間完全自動化的雙向同步。
* **版本設定:**

   * [!DNL Experience Manager] 只會在更新時建立資產版本(如果檔案是源自此處並 [!DNL Experience Manager] 在此處更新)。
   * [!DNL Creative Cloud] 資產提供其自 [己](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) 的版本控制功能，其目標為「進行中的工作」更新（基本上，可將更新儲存長達10天）

* **空間限制：** 檔案交換的大小和數量受創意使用者的特定 [Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) 資產配額（視訂閱層級而定）以及檔案大小上限5 GB的限制。此外，該組織在Adobe Marketing Cloud資產核心服務中的資產配額也限制了空間。

* **空間需求：** 共用資料夾中的檔案也必須實際儲存在帳戶中， [!DNL Experience Manager] 然後 [!DNL Creative Cloud] 在核心服務中使用快取 [!DNL Marketing Cloud Assets] 副本。
* **網路和頻寬：** 共用資料夾中的檔案和所有更新都必須透過網路在系統之間傳輸。您應確保僅共用相關檔案和更新。
* **資料夾類型**:共用 [!DNL Assets] 類型的資 `sling:OrderedFolder`料夾時，不支援在中共用的內容 [!DNL Adobe Marketing Cloud]。如果要共用資料夾，在[!DNL Assets]中建立資料夾時，不要選擇[!UICONTROL Ordered]選項。

## 最佳做法{#best-practices}

利用[!DNL Experience Manager]至[!DNL Creative Cloud]資料夾共用的最佳做法包括：

* **卷注意事項：** [!DNL Experience Manager] 和資 [!DNL Creative Cloud] 料夾共用應用於共用較少的檔案，例如與特定促銷活動或活動相關的檔案。若要共用較大的資產集（如組織中所有已核准的資產），請使用其他散發方法（例如[!DNL Assets Brand Portal]）或[!DNL Experience Manager]案頭應用程式。
* **避免共用深層次：** 共用會以遞歸方式運作，不允許選擇性取消共用。通常，只有沒有子資料夾或具有非常淺層層次的資料夾（如1個子資料夾級別）才應考慮共用。
* **單向共用的個別檔案夾：應使** 用個別檔案夾，將最終資產從檔案 [!DNL Assets] 共 [!DNL Creative Cloud] 用，並將創意可用的資產從檔案共 [!DNL Creative Cloud] 用到 [!DNL Assets]。結合這些資料夾的良好命名慣例，可為[!DNL Assets]和[!DNL Creative Cloud]使用者建立更容易瞭解的工作環境。
* **避免在共用資料夾中使用WIP：不應將共用資料夾用於「正在進行的工作」(Work in Progress)-在「Creative Cloud檔案」中使用單獨的資料夾執行需要頻繁更改檔案的工作。** 
* **在共用資料夾外開始新作品：新設計（創意檔案）應在「Creative Cloud檔案」中的個別WIP資料夾中啟動，當它們準備好與使用者共用時，應將它們移動或儲存至共用資料夾。**  [!DNL Assets] 
* **簡化共用結構：** 若要建立更易於管理的作業設定，請考慮簡化共用結構。[!DNL Assets]資料夾不應與所有創意使用者共用，而應僅與團隊代表共用，例如創意主管或團隊經理。 創意部門的經理會收到最終資產、決定工作指派，然後讓設計人員在WIP資產的Creative Cloud帳戶中工作。 他們可使用Creative Cloud協作功能來協調工作，最後選取並放回可共用至[!DNL Assets]的資產至其創意就緒共用資料夾。

下圖說明如何根據[!DNL Assets]的現有最終資產建立新設計的範例設定。

![chlimage_1-180](assets/chlimage_1-407.png)
