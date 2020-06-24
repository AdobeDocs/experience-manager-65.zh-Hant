---
title: Adobe Experience Manager轉Adobe Creative Cloud資料夾分享最佳實務
description: 設定Adobe Experience Manager，讓Experience Manager Assets中的使用者可與Adobe Creative Cloud(CC)使用者交換資料夾。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---


# Adobe Experience Manager到Adobe Creative Cloud資料夾共用 {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>Experience Manager到Creative Cloud資料夾共用功能已過時。 Adobe強烈建議使用較新的功能，例如 [Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)[或Experience Manager案頭應用程式](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html)。 進一步了 [解Experience Manager和Creative Cloud整合最佳實務](/help/assets/aem-cc-integration-best-practices.md)。

Adobe Experience Manager可設定為允許資產中的使用者與Adobe Creative Cloud應用程式的使用者共用資料夾，以便在Adobe Creative Cloud Assets服務中以共用資料夾的形式提供。 此功能可用於創意團隊和資產使用者之間交換檔案，尤其是當創意使用者無法存取資產例項（他們不在企業網路上）時。

此類整合可用於下列使用案例，尤其是與沒有直接存取資產的使用者合作時：

* 資產使用者與Adobe Creative Cloud檔案的使用者共用一組特定資產（例如一組創意簡報和一組經過核准的資產，用於新行銷活動的設計作品）
* 資產使用者會收到Adobe Creative Cloud應用程式使用者建立的新檔案。

>[!NOTE]
>
>在閱讀本檔案之前，您可以先閱讀整體 [Experience Manager和Creative Cloud整合的最佳實務](/help/assets/aem-cc-integration-best-practices.md) ，以取得主題的更高層次概述。

## 概覽 {#overview}

Experience Manager對Creative Cloud資料夾共用有賴於在資產和Creative Cloud帳戶之間對資料夾和檔案的伺服器端共用。 在桌上型電腦上使用Creative Cloud案頭應用程式的創意專業人員，可使用Adobe CreativeSync技術，將共用資料夾直接在光碟上取用。

下圖提供整合的概觀。

![chlimage_1-179](assets/chlimage_1-406.png)

整合包含下列元素：

* **部署在企業網路** （受管理服務或內部部署）中的Experience Manager Assets伺服器： 資料夾共用會從這裡開始。
* **Adobe Marketing Cloud資產核心服務**: 在Experience Manager和Creative Cloud儲存服務之間充當中介。 使用整合的公司管理員需要在Marketing Cloud組織和「資產」例項之間建立信任關係。 他們也 [會定義已核准的Creative Cloud共同作業人員清單](https://docs.adobe.com/content/help/en/core-services/interface/assets/t-admin-add-cc-user.html)，讓Assets使用者也可以共用資料夾，以提高安全性。

* **Creative Cloud資產網站服務** （儲存空間和Creative Cloud檔案網頁UI）: 這是特定Creative Cloud應用程式使用者（與他們共用「資產」檔案夾）可接受邀請並在其Creative Cloud帳戶儲存空間中查看該檔案夾的地方。
* **Creative Cloud案頭應用程式**: （可選）可讓創意使用者透過與Creative Cloud Assets儲存空間同步，從案頭直接存取共用資料夾／檔案。

## 特性與限制 {#characteristics-and-limitations}

* **更改的單向傳播：** 檔案變更僅會從系統（Experience Manager或Creative Cloud資產）傳播至單一方向，而系統原本是在此處建立（上傳）資產。 此整合無法提供兩個系統之間完全自動化的雙向同步。
* **版本設定:**

   * Experience Manager僅會在更新時建立資產版本（如果檔案源自Experience Manager，並在更新時更新）。
   * Creative Cloud Assets提供其自己的版 [本控制功能](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) ，其目標是「進行中的作品」更新（基本上，可將更新儲存至10天）

* **空間限制：** 交換的檔案大小和數量受創意使用者專屬的 [Creative Cloud Assets配額(視訂閱層級而定](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) )和最大檔案大小限制為5 GB。 此外，組織在Adobe Marketing Cloud Assets核心服務中的資產配額也限制了空間。

* **空間需求：** 共用資料夾中的檔案也必須實際儲存在Experience Manager中，然後儲存在Creative Cloud帳戶中，並在Marketing Cloud Assets核心服務中使用快取副本。
* **網路和頻寬：** 共用資料夾中的檔案和所有更新都需要通過網路在系統之間傳輸。 您應確保僅共用相關檔案和更新。
* **資料夾類型**: 在Adobe Marketing Cloud中共用的內 `sling:OrderedFolder`容中，不支援共用類型的「資產」檔案夾。 如果您想要共用資料夾，在「資產」中建立資料夾時，請勿選取「已訂購」選項。

## Best practices {#best-practices}

將Experience Manager運用至Creative Cloud資料夾共用的最佳實務包括：

* **卷注意事項：** Experience Manager/Creative Cloud資料夾共用應用程式來共用較少的檔案，例如與特定促銷活動或活動相關的檔案。 若要共用較大的資產集（如組織中所有已核准的資產），請使用其他分發方法（例如，資產品牌入口網站）或Experience Manager案頭應用程式。

* **避免共用深層次：** 分享會以遞歸方式運作，不允許選擇性取消分享。 通常，只有沒有子資料夾或具有非常淺層層次的資料夾（如1個子資料夾級別）才應考慮共用。
* **分開資料夾以進行單向共用：** 應使用個別資料夾，將最終資產從Assets共用至Creative Cloud檔案，並將創意就緒資產從Creative Cloud檔案共用至Assets。 再加上這些檔案夾的良好命名慣例，可為資產和Creative Cloud使用者建立更容易瞭解的工作環境。
* **避免在共用資料夾中執行WIP:** 共用資料夾不應用於「進行中的作品」-請在「Creative Cloud檔案」中使用個別資料夾來執行需要經常變更檔案的工作。
* **在共用資料夾之外開始新工作：** 新設計（創意檔案）應從Creative Cloud檔案的個別WIP檔案夾中啟動，當它們準備好與「資產」使用者共用時，應將它們移動或儲存至共用檔案夾。
* **簡化共用結構：** 若要建立更易於管理的作業設定，請考慮簡化共用結構。 資產資料夾不應與所有創意使用者共用，而應僅與團隊代表共用，例如創意主管或團隊經理。 創意部門的經理將會收到最終資產、決定工作指派，然後讓設計人員在自己的Creative Cloud帳戶中處理WIP資產。 他們可使用Creative Cloud協作功能來協調工作，最後選取並放回資產的資產，並放回其可立即使用創意的共用資料夾。

下圖說明如何根據資產的現有最終資產建立新設計的範例設定。

![chlimage_1-180](assets/chlimage_1-407.png)
