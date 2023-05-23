---
title: Digital Rights Management資產
description: 瞭解如何管理中的授權資產的資產到期狀態和資訊 [!DNL Experience Manager]。
contentOwner: AG
role: User, Admin
feature: DRM,Asset Management
exl-id: a49cfd25-e8d9-492f-be5e-acab0cf67a28
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 7%

---

# 資產的 Digital Rights Management {#digital-rights-management-in-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/drm.html?lang=en) |
| AEM 6.5 | 本文 |

數字資產通常與指定使用條款和持續時間的許可證相關聯。 因為 [!DNL Adobe Experience Manager Assets] 與 [!DNL Experience Manager] 平台，您可以高效地管理資產到期資訊和資產狀態。 您還可以將許可資訊與資產相關聯。

## 資產到期 {#asset-expiration}

資產到期是強制執行資產許可證要求的有效方法。 它確保已發佈的資產在過期時未發佈，這避免了發生任何許可證違規的可能性。 沒有管理員權限的用戶無法編輯、複製、移動、發佈和下載過期資產。

您可以在 [!DNL Assets] 控制台。

![expired_flag_list](assets/expired_flag_list.png)

*圖：在清單視圖中， [!UICONTROL 狀態] 列顯示 [!UICONTROL 已過期] 橫幅。*

您可以在 [!UICONTROL 時間軸] 左欄。

![chlimage_1-144](assets/chlimage_1-144.png)

>[!NOTE]
>
>不同時區中的用戶不同地顯示資產的到期日期。

您還可以在 **[!UICONTROL 引用]** 鐵軌。 它管理複合資產與引用的子集、集合和項目之間的資產到期狀態和關係。

1. 導航到要查看其引用網頁和複合資產的資產。
1. 選擇資產並開啟 **[!UICONTROL 引用]** 左欄。 對於已到期資產， [!UICONTROL 引用] 軌道顯示到期狀態 **[!UICONTROL 資產已過期]** 頂端。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   如果資產已過期子組， [!UICONTROL 引用] 滑軌顯示狀態 **[!UICONTROL 資產已到期子資產]**。

   ![chlimage_1-148](assets/chlimage_1-148.png)

### 搜索過期資產 {#search-expired-assets}

您可以在「搜索」面板中搜索過期資產，包括過期的子組。

1. 在 [!DNL Assets] 控制台，按一下 **[!UICONTROL 搜索]** 的子菜單。

1. 在「搜索」框中，選擇 `Enter` 鍵以顯示搜索結果頁。
1. 開啟左滑軌中的搜索面板。 按一下 **[!UICONTROL 到期狀態]** 按鈕。

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選擇 **[!UICONTROL 已過期]**。 篩選搜索結果後，只顯示過期的資產。

選擇 **[!UICONTROL 已過期]** 頁籤 [!DNL Assets] console僅顯示複合資產引用的過期資產和子組。 引用過期子集的複合資產在子集到期後不會立即顯示。 相反，它們在 [!DNL Experience Manager] 檢測它們在下次運行調度程式時引用過期的子集。

如果您將已發佈資產的到期日期修改為早於當前計畫程式週期的日期，則計畫會在下次運行時將此資產檢測為到期資產，並相應地反映為狀態。

此外，如果出現故障或錯誤導致計畫程式無法在當前週期中檢測過期資產，則計畫程式將在下一個週期中重新檢查這些資產並檢測其過期狀態。

啟用 [!DNL Assets] 控制台：顯示引用複合資產以及過期的子集，配置 **[!UICONTROL Adobe CQ大壩期終通知]** 工作流 [!DNL Experience Manager] Configuration Manager。

1. 開啟 [!DNL Experience Manager] Configuration Manager。
1. 選擇 **[!UICONTROL Adobe CQ大壩期終通知]**。 預設情況下， **[!UICONTROL 基於時間的計畫程式]** 已選定，它將調度作業以在特定時間檢查資產是否已過期子集。 作業完成後，已過期子集和引用資產的資產在搜索結果中顯示為過期。

1. 要定期運行作業，請清除「基於時 **[!UICONTROL 間的調度程式規則]** 」欄位，並在「定期調度程式」欄位中以秒為單 **[!UICONTROL 位修改時間]** 。例如，示例表達式 `0 0 0 * * ?` 在00小時觸發作業。
1. 選擇 **[!UICONTROL 發送電子郵件]** 在資產過期時接收電子郵件。

   >[!NOTE]
   >
   >僅資產建立者（將特定資產上載到的人員） [!DNL Assets])在資產過期時收到電子郵件。 請參閱 [如何配置電子郵件通知](/help/sites-administering/notification.md) 有關在整體上配置電子郵件通知的詳細資訊 [!DNL Experience Manager] 級別。

1. 在 **[!UICONTROL 以秒為單位的前一通知]** 欄位中，指定資產到期前的時間（以秒為單位），以接收有關到期的通知。 資產建立者在資產到期前收到一條消息，通知您資產將在指定時間後到期。 資產到期後，您將收到確認到期的另一通知。 此外，失效的資產被停用。

1. 按一下「**[!UICONTROL 儲存]**」。

## 資產狀態 {#asset-states}

的 [!DNL Assets] 控制台可顯示資產的各種狀態。 根據特定資產的當前狀態，其卡視圖將顯示描述其狀態的標籤，例如「已到期」、「已發佈」、「已批准」、「已拒絕」等。

1. 在 [!DNL Assets] 用戶介面，選擇資產。
1. 按一下 **[!UICONTROL 發佈]** 的子菜單。 如果你看不到 **發佈** 在工具欄上，按一下 **[!UICONTROL 更多]** 在工具欄上，然後 **[!UICONTROL 發佈]** ![發佈選項](assets/do-not-localize/publish-globe.png) 的雙曲餘切值。
1. 選擇 **[!UICONTROL 發佈]** ，然後關閉確認對話框。
1. 退出選擇模式。 資產的發佈狀態顯示在卡視圖中資產縮略圖的底部。 在清單視圖中，「已發佈」列顯示資產發佈的時間。

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. 要顯示其資產詳細資訊頁面，請在 [!DNL Assets] 介面，選擇資產並按一下 **[!UICONTROL 屬性]** ![查看屬性](assets/do-not-localize/info-circle-icon.png)。

1. 在 [!UICONTROL 高級] 頁籤中，設定 **[!UICONTROL 過期]** 的子菜單。

   ![設定資產到期日期和到期時間欄位](assets/asset-properties-advanced-tab.png)

   *圖： [!UICONTROL 高級] 頁籤 [!UICONTROL 屬性] 的子菜單。*

1. 按一下 **[!UICONTROL 保存]** 然後按一下 **[!UICONTROL 關閉]** 顯示資產控制台。
1. 資產的發佈狀態在卡視圖中資產縮略圖底部指示過期狀態。 在清單視圖中，資產的狀態顯示為 **[!UICONTROL 已過期]**。

   ![chlimage_1-160](assets/chlimage_1-160.png)

1. 在 [!DNL Assets] 控制台，選擇一個資料夾並在該資料夾上建立查看任務。
1. 審閱和批准/拒絕審閱任務中的資產，然後按一下 **[!UICONTROL 完成]**。
1. 導航到為其建立審閱任務的資料夾。 您批准/拒絕的資產的狀態顯示在卡視圖的底部。 在清單視圖中，審批和到期狀態將顯示在相應的列中。

   ![chlimage_1-161](assets/chlimage_1-161.png)

1. 要根據資產的狀態搜索資產，請按一下 **[!UICONTROL 搜索]** ![搜索選項](assets/do-not-localize/search_icon.png) 按鈕。
1. 選擇 `Return` 按一下 [!DNL Experience Manager] 的子菜單。
1. 在搜索面板中，按一下 **[!UICONTROL 發佈狀態]** 選擇 **[!UICONTROL 已發佈]** 要在中搜索已發佈的資產 [!DNL Assets]。

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. 按一下 **[!UICONTROL 審批狀態]** 並按一下相應的選項以搜索已批准或拒絕的資產。

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. 若要根據資產的到期狀態來搜尋資產，請在「搜尋」面 **[!UICONTROL 板中選取「到期狀態]** 」，然後選擇適當的選項。

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. 您還可以根據各種搜索方面下的狀態組合來搜索資產。 例如，您可以通過在搜索方面選擇相應的選項來搜索已在審閱任務中批准但尚未過期的已發佈資產。

   ![chlimage_1-166](assets/chlimage_1-166.png)

## Digital Rights Management [!DNL Assets] {#digital-rights-management-in-assets-1}

此功能強制您接受許可協定，然後您才能從下載許可資產 [!DNL Adobe Experience Manager Assets]。

如果選擇受保護的資產並按一下 **[!UICONTROL 下載]**，您將被重定向到許可證頁面以接受許可證協定。 如果您不接受許可協定， **[!UICONTROL 下載]** 頁籤

如果所選內容包含多個受保護資產，則一次選擇一個資產，接受許可協定，然後繼續下載該資產。

如滿足以下任一條件，則資產被視為受保護：

* 資產元資料屬性 `xmpRights:WebStatement` 指向包含資產的許可協定的頁面路徑。
* 資產元資料屬性的值 `adobe_dam:restrictions` 是指定許可協定的原始HTML。

>[!NOTE]
>
>位置 `/etc/dam/drm/licenses` 用於將許可證儲存在早期版本中 [!DNL Experience Manager] 已棄用。
>
>如果您建立或修改許可證頁面，或將其從上一頁埠 [!DNL Experience Manager] 版本，Adobe建議您將其儲存在 `/apps/settings/dam/drm/licenses` 或 `/conf/&ast;/settings/dam/drm/licenses`。

### 下載受DRM保護的資產 {#downloading-drm-assets}

1. 在卡視圖中，選擇要下載的資產，然後按一下 **[!UICONTROL 下載]**。
1. 在「版 **[!UICONTROL 權管理]** 」頁面中，從清單中選取您要下載的資產。
1. 在 [!UICONTROL 許可證] 框，選擇 **[!UICONTROL 同意]**。 資產旁邊將顯示複選標籤。 按一下 **[!UICONTROL 下載]** 的雙曲餘切值。

   >[!NOTE]
   >
   >的 **[!UICONTROL 下載]** 選項僅在您選擇同意受保護資產的許可協定時啟用。 但是，如果您的選擇同時包含受保護和未受保護的資產，則窗格和 **[!UICONTROL 下載]** 選項可下載未受保護的資產。 若要同時接受多個受保護資產的授權合約，請從清單中選取資產，然後選擇「同 **[!UICONTROL 意」]**。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 在對話框中，按一下 **[!UICONTROL 下載]** 下載資產或其格式副本。
