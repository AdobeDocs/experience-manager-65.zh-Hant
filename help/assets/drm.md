---
title: 數位版權管理 [!DNL Adobe Experience Manager Assets]。
description: 瞭解如何管理中授權資產的資產到期狀態和資訊 [!DNL Experience Manager]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 20f337ea2e4f369eb6eb760d312199fa39556513
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 6%

---


# Digital Rights Management for assets {#digital-rights-management-in-assets}

數位資產通常與指定使用條款和期限的授權相關聯。 由於 [!DNL Adobe Experience Manager Assets] 與平台完全整合，因此您可以 [!DNL Experience Manager] 有效管理資產到期資訊和資產狀態。 您也可以將授權資訊與資產建立關聯。

## 資產到期 {#asset-expiration}

資產到期是強制執行資產授權要求的有效方式。 它可確保發佈的資產在過期時未發佈，避免任何授權違規的可能。 不具管理員權限的使用者無法編輯、複製、移動、發佈及下載過期的資產。

您可以在資訊卡和清單檢視的主控台 [!DNL Assets] 中檢視資產的到期狀態。

![expired_flag_card](assets/expired_flag_card.png)

*圖： 在資訊卡檢視中，資訊卡上的標幟表示已到期的資產。*

![expired_flag_list](assets/expired_flag_list.png)

*圖： 在清單視圖中，「狀[!UICONTROL 態]」列顯示[!UICONTROL 「已到期]」橫幅。*

您可以在左側導軌的「時間軸」中檢視資 [!UICONTROL 產的] 「到期狀態」。

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>不同時區的使用者會以不同方式顯示資產的到期日。

您也可以在「參考」邊欄中檢視資產的 **[!UICONTROL 到期]** 狀態。 它可管理資產到期狀態以及複合資產與參考子資產、系列和專案之間的關係。

1. 導覽至您要檢視其參考網頁和複合資產的資產。
1. 選取資產，然後按一下標 [!DNL Experience Manager] 志。

1. 從菜 **[!UICONTROL 單中選擇]** 「參照」(References)。

   ![chlimage_1-146](assets/chlimage_1-146.png)

   對於過期資產，「參考」邊欄會在頂端顯示「 **[!UICONTROL 資產已到期]** 」的到期狀態。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   如果資產已過期子資產，「參考」邊欄會顯示「資 **[!UICONTROL 產已過期子資產」的狀態]**。

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 搜尋過期資產 {#search-expired-assets}

您可以在「搜尋」面板中搜尋過期的資產，包括過期的子資產。

1. 在控制 [!DNL Assets] 台中，按一下工具列 **[!UICONTROL 中的「搜尋]** 」，以顯示「Omnisearch」方塊。

1. 在「Omnisearch」（搜索）框中，按Enter鍵可顯示搜索結果頁。

   ![chlimage_1-150](assets/chlimage_1-150.png)

1. 按一 [!DNL Experience Manager] 下標誌以顯示搜尋面板。

   ![chlimage_1-151](assets/chlimage_1-151.png)

1. Click the **[!UICONTROL Expiry Status]** option to expand it.

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選擇「 **[!UICONTROL 過期]**」。 過期的資產會顯示在搜尋結果中。

   ![chlimage_1-153](assets/chlimage_1-153.png)

當您選擇「已過 **[!UICONTROL 期]** 」選項時，主控台 [!DNL Assets] 只會顯示複合資產所參照的已到期資產和子資產。 在子資產到期後，不會立即顯示參照已到期子資產的複合資產。 相反地，它們會在偵測到 [!DNL Experience Manager] 它們在下次排程器執行時參考過期子資產後顯示。

如果您將已發佈資產的到期日修改為早於目前排程器週期的日期，則排程仍會在下次執行時將此資產偵測為已到期資產，並據以反映狀態。

此外，如果故障或錯誤導致調度程式無法檢測當前週期中的過期資產，則調度程式會在下一個週期重新檢查這些資產並檢測其過期狀態。

To enable the [!DNL Assets] console to display the referencing compound assets along with the expired subassets, configure an **[!UICONTROL Adobe CQ DAM Expiry Notification]** workflow in [!DNL Experience Manager] Configuration Manager.

1. 開啟 [!DNL Experience Manager] 配置管理器。
1. 選擇 **[!UICONTROL Adobe CQ DAM到期通知]**。 依預設， **[!UICONTROL 會選取「時間型排程器]** 」，此排程器會將工作排程在特定時間檢查資產是否已過期子資產。 作業完成後，已過期子資產和參考資產的資產會在搜尋結果中顯示為過期。

   ![chlimage_1-154](assets/chlimage_1-154.png)

1. 要定期運行作業，請清除「基於時 **[!UICONTROL 間的調度程式規則]** 」欄位，並在「定期調度程式」欄位中以秒為單 **[!UICONTROL 位修改時間]** 。例如，示例表達式&#39;0 0 0 &amp;ast;&amp;ast;?&#39;會在00小時觸發工作。
1. 選擇 **[!UICONTROL 在資產過期]** 時傳送電子郵件以接收電子郵件。

   >[!NOTE]
   >
   >只有資產建立者(將特定資產上傳至的人員 [!DNL Assets])會在資產過期時收到電子郵件。 請參 [閱如何設定電子郵件通知](/help/sites-administering/notification.md) ，以取得在整體層級設定電子郵件通知的詳細 [!DNL Experience Manager] 資訊。

1. 在「先 **[!UICONTROL 前通知的秒數]** 」欄位中，指定當您想要收到有關過期的通知時，資產到期前的秒數。 如果您是管理員或資產建立者，在資產到期前會收到訊息，通知您資產將在指定時間後到期。

   資產過期後，您會收到另一則確認到期的通知。 此外，過期的資產會停用。

1. 按一下&#x200B;**[!UICONTROL 「儲存」]**。

## 資產狀態 {#asset-states}

主控 [!DNL Assets] 台可顯示資產的各種狀態。 根據特定資產的目前狀態，其卡片檢視會顯示描述其狀態的標籤，例如「已到期」、「已發佈」、「已核准」、「已拒絕」等。

1. 在使用者 [!DNL Assets] 介面中，選取資產。

   ![chlimage_1-155](assets/chlimage_1-155.png)

1. 從工具 **[!UICONTROL 列按一下]** 「發佈」。 如果您在工具列上未看 **到** 「發佈」，請按一下工具列上的「更多 **[!UICONTROL 」，然後找出「]** 發佈 **** 」選項。

   ![chlimage_1-156](assets/chlimage_1-156.png)

1. 從功 **[!UICONTROL 能表選擇]** 「發佈」，然後關閉確認對話框。
1. 退出選擇模式。 資產的出版物狀態會顯示在卡片檢視中資產縮圖的底部。 在清單檢視中，「已發佈」欄會顯示資產發佈的時間。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 若要顯示其資產詳細資訊頁面，請在介面 [!DNL Assets] 中選取資產，然後按一下「屬 **[!UICONTROL 性]**」。

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. 在「進階」索引標籤中，從「過期」欄位設定資產的到 **[!UICONTROL 期日]** 。

   ![在「過期」欄位中設定資產到期日期和時間](assets/asset-properties-advanced-tab.png)

   *圖：[!UICONTROL 資產]「屬性」頁面中[!UICONTROL 的「進階]」標籤，以設定資產到期日。*

1. 按一 **[!UICONTROL 下「儲存]** 」，然後按一 **[!UICONTROL 下「關閉]** 」以顯示「資產」主控台。
1. 資產的發佈狀態會指出卡片檢視中資產縮圖底部的過期狀態。 在清單檢視中，資產的狀態會顯示為「已 **[!UICONTROL 到期]**」。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 在控制 [!DNL Assets] 台中，選擇資料夾並在該資料夾上建立查看任務。
1. 複查並批准／拒絕複查任務中的資產，然後按一下「完 **[!UICONTROL 成]**」。
1. 導航至您為其建立審閱任務的資料夾。 您核准／拒絕的資產狀態會顯示在卡片檢視的底部。 在清單檢視中，核准和到期狀態會顯示在適當的欄中。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 若要根據資產狀態來搜尋資產，請按一 **[!UICONTROL 下「搜尋]** 」以顯示Omnisearch列。

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. 按return並按一下 [!DNL Experience Manager] 以顯示搜索面板。
1. In the search panel, click **[!UICONTROL Publish Status]** and select **[!UICONTROL Published]** to search for published assets in [!DNL Assets].

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Click **[!UICONTROL Approval Status]** and click the appropriate option to search for approved or rejected assets.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 若要根據資產的到期狀態來搜尋資產，請在「搜尋」面 **[!UICONTROL 板中選取「到期狀態]** 」，然後選擇適當的選項。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 您也可以根據各種搜尋刻面下的狀態組合來搜尋資產。 例如，您可以在搜尋Facet中選取適當的選項，以搜尋已在審核工作中核准但尚未過期的已發佈資產。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## 數位版權管理 [!DNL Assets] {#digital-rights-management-in-assets-1}

這項功能會強制您接受授權合約，您才能從下載授權資產 [!DNL Adobe Experience Manager Assets]。

如果您選取受保護的資產並按一下「 **[!UICONTROL 下載]**」，則會將您重新導向至授權頁面以接受授權合約。 如果您不接受授權合約，則無 **[!UICONTROL 法使用]** 「下載」選項。

如果選擇包含多個受保護的資產，請一次選取一個資產、接受授權合約，然後繼續下載資產。

如果符合下列任一條件，資產即視為受保護：

* 資產中繼資料屬 `xmpRights:WebStatement` 性指向包含資產授權合約之頁面的路徑。
* 資產中繼資料屬性的值 `adobe_dam:restrictions` 是指定授權合約的原始HTML。

>[!NOTE]
>
>舊版中 `/etc/dam/drm/licenses` 用來儲存授權的位置已不 [!DNL Experience Manager] 再使用。
>
>如果您建立或修改授權頁面，或從舊版匯出 [!DNL Experience Manager] 這些頁面，Adobe建議您將它們儲存在 `/apps/settings/dam/drm/licenses` 或下 `/conf/&ast;/settings/dam/drm/licenses`。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在資訊卡檢視中，選取您要下載的資產，然後按一下「下 **[!UICONTROL 載」]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在「授 [!UICONTROL 權] 」窗格中，選 **[!UICONTROL 擇「同意」]**。 資產旁會出現核取標籤。 按一下「 **[!UICONTROL 下載]** 」選項。

   >[!NOTE]
   >
   >The **[!UICONTROL Download]** option is enabled only when you choose to agree to the license agreement for a protected asset. However, if your selection comprises both protected and unprotected assets, only the protected assets are listed in the pane and the **[!UICONTROL Download]** option is enabled to download the unprotected assets. 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 在對話方塊中，按一 **[!UICONTROL 下「下載]** 」以下載資產或其轉譯。
