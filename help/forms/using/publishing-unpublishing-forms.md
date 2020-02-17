---
title: 發佈和取消發佈表單和檔案
seo-title: 發佈和取消發佈表單和檔案
description: 您可以排程表單的發佈和取消發佈。 發佈表單會複製在發佈例項上。
seo-description: 您可以排程表單的發佈和取消發佈。 發佈表單會複製在發佈例項上。
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
translation-type: tm+mt
source-git-commit: f9ed171c188a4dfb71f12ae9c98105a4c1895542

---


# 發佈和取消發佈表單和檔案{#publishing-and-unpublishing-forms-and-documents}

AEM Forms可讓您輕鬆建立、發佈和解除發佈表單。 如需AEM Forms的詳細資訊，請參閱「管 [理表單的簡介」](../../forms/using/introduction-managing-forms.md)。

AEM Forms伺服器提供兩個例項：作者與發佈。 作者例項是用於建立和管理表單資產與資源。 發佈例項用於保留可供使用者使用的資產和相關資源。 您可以在「作者」模式下匯入XDP和PDF表格。 如需詳細資訊，請 [參閱「在AEM Forms中取得XDP和PDF檔案」](../../forms/using/get-xdp-pdf-documents-aem.md)。

## 支援的資產 {#supported-assets-nbsp}

AEM Forms支援下列資產類型：

* 最適化表單
* 最適化檔案
* 最適化表單片段
* 主題
* 表單範本（XFA表單）
* PDF表格
* 檔案（平面PDF檔案）
* 表單集
* 資源（映像、方案和樣式表）

一開始，所有資產只能在「作者」例項中使用。 管理員或表單作者可以發佈資源以外的所有資產。

當您選取並發佈表單時，也會發佈其相關資產和資源。 不過，不會發佈相依資產。 在此背景下，相關資產和資源是已發佈資產所使用或參考的資產。 相依資產是指指已發佈資產的資產。

您的最適化表單可能會利用一些未自動發佈的設定、設定和自訂。 建議您在發佈最適化表單之前，先發佈或啟動這些資源。

* 可編輯的最適化表單範本
* Adobe Sign、Typekit、reCAPTCHA和表單資料模型的雲端服務設定
* 其他雲端服務設定只有在使用者擁有管理權限時才會啟動。
* 自訂。 包括但不限於：

   * 自訂版面
   * 自訂外觀
   * CSS檔案——在「最適化表單」容器屬性對話方塊中當做輸入
   * 用戶端程式庫類別——在「最適化表單」容器屬性對話方塊中作為輸入
   * 任何其他可能包含在Adaptive Form模板中的客戶端庫。
   * 設計路徑

## 資產狀態 {#asset-states}

資產可以有下列狀態：

* **** 未發佈：從未發佈的資產(未發佈狀態僅適用於Forms資產。 「信件管理」資產沒有「未發佈」狀態。)
* **已發佈**:已發佈且可在「發佈」例項中使用的資產
* **已修改**:發佈後修改的資產

## 發佈資產 {#publish-an-asset}

1. 登入AEM Forms伺服器。
1. 使用下列其中一項來選擇和發佈資產。

   1. 將指標移至資產上方，並點選「 **[!UICONTROL Publish]** ![aem6forms_globe」](assets/aem6forms_globe.pngasset.png)。
   1. 執行下列任一項作業，然後點選「發佈」:

      * 如果您位於卡片檢視中，請點選「 **[!UICONTROL Enter Selection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)」，然後點選資產。 選取資產。
      * 如果您位於清單檢視中，請選取資產的核取方塊。 選取資產。
      * 點選資產以顯示其詳細資訊。
      * 點選「檢視屬性」檢視屬性，以顯示資產的 ![屬性](assets/viewproperties.png)。
      >[!NOTE]
      >
      >請勿選取多個資產。 不支援一次發佈多個資產。


1. 當「發佈」程式啟動時，會出現確認對話方塊，列出所有相關的資產和資源。 在包含相關資產的對話方塊中，點選「發 **[!UICONTROL 布」]**。 資產隨即發佈，並出現「發佈資產成功」對話方塊。

   >[!NOTE]
   >
   >對於最適化表單以及相關資產，也會顯示最適化表單頁面名稱。

   ![與所有相關資產和資源進行確認對話](assets/p4.png)

   與所有相關資產和資源的確認對話方塊。

   >[!NOTE]
   >
   >對於Forms Manager，如果使用者沒有發佈所列資產的權限，則會停用「發佈」動作。 需要額外權限的資產會以紅色顯示。

   發佈資產後，資產的中繼資料屬性會複製到「發佈」例項，資產的狀態會變更為「已發佈」。 已發佈的相依資產的狀態也會變更為「已發佈」。

   發佈資產後，您可以使用表單入口網站來顯示網頁上的所有資產。 如需詳細資訊，請 [參閱Portal上發佈表格簡介](../../forms/using/introduction-publishing-forms.md)。

## Publish all the Correspondence Management Assets {#publish-all-the-correspondence-management-assets}

AEM Forms可讓您一次在伺服器上發佈所有Correponsement Management資產。 發佈的資產包括所有Correponsement Management資產和相關依存關係。

完成下列步驟，在伺服器上發佈所有Correponsement Management資產：

1. 登入AEM Forms伺服器。
1. 在全 **域導覽列中點選** 「Adobe Experience Manager」。
1. 點選 ![工具](assets/tools.png)，然後點選 **表單**。
1. Tap **Publish Correspondence Management Assets**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   此時將顯示「發佈所有對應管理資產」頁，並顯示上次嘗試發佈對應管理資產流程的相關資訊。

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 點選「 **發佈** 」，然後在確認訊息中點選「 **確定」**。

   批處理完成後，您可以查看上次運行的詳細資訊。 這包括管理員登錄以及批處理是否成功運行或失敗等資訊。

   >[!NOTE]
   >
   >一旦啟動發佈程式，就無法取消。 此外，在「發佈」操作進行中時，請勿建立、刪除、修改或發佈任何資產，或啟動「導出所有對應管理資產」操作。

## 將表單與檔案的發佈與取消發佈作業自動化 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms可讓您排程「表單與檔案」的資產發佈和取消發佈。 您可以在中繼資料編輯器中指定排程。 如需管理表單中繼資料的詳細資訊，請參閱 [管理表單中繼資料。](../../forms/using/manage-form-metadata.md)

請依照下列步驟，排程發佈和取消發佈表單與檔案資產的日期和時間：

1. 選取資產，然後點選「檢 **[!UICONTROL 視屬性」]**。 此時將開啟「元資料屬性」頁。
1. 在「中繼資料屬性」頁面中，點選「 **[!UICONTROL 進階]**」，然後點選「 **[!UICONTROL Edit]** ![illustratorcc_penciltool_cur_edit_2_17」](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
1. 在「按 **[!UICONTROL 時發佈]** 」和「 **[!UICONTROL 按時發佈]** 」欄位中，選取日期和時間。\
   點選 **[!UICONTROL 「Done]** ![aem6forms_check」](assets/aem6forms_check.png)。

## 取消發佈資產 {#unpublish-an-asset}

1. 選取已發佈的資產，然後點選「取 **[!UICONTROL 消發佈]**![取消發佈](assets/unpublish.png)」。
1. 使用下列其中一項來選取及取消發佈資產。

   1. 將指標移至資產上方，然後點選「取 **[!UICONTROL 消發佈]**![取消發佈](assets/unpublish.png)」。
   1. 執行下列任一項作業，然後點選取取消發佈：

      * 如果您位於卡片檢視中，請點選「 **[!UICONTROL Enter Selection]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)」，然後點選資產。 選取資產。

      * 如果您位於清單檢視中，請將滑鼠指標暫留在資產上，然後點選「 ![selectassettcheckmark](assets/selectassetcheckmark.png) 」。 選取資產。

      * 點選資產以顯示其詳細資訊。
      * 點選「檢視屬性」檢視屬性，以顯示資產的 ![屬性](assets/viewproperties.png)。

1. 當「解除發佈」程式啟動時，會出現確認對話框。 點選「 **[!UICONTROL 解除發佈]**」。

   >[!NOTE]
   >
   >只有選取的資產未發佈，且其子資產和參考資產（如果有）未發佈。

## 將資產或信件回復為先前發佈的版本 {#revert-an-asset-or-letter-to-the-previously-published-version}

每次您編輯資產或信件後發佈資產或信件，都會建立資產或信件的版本。 您可以將資產或信件回復為先前發佈的版本。 如果資產或檔案的目前版本發生問題，您可能需要這麼做。

>[!NOTE]
>
>如果已發佈信件中使用的任何從屬資產已從系統刪除，請勿將信件回復為上次發佈狀態。

1. 選取資產，然後點選「 **[!UICONTROL 回復為先前發佈的版本]**![」(Revert to Previouslypublished version](assets/reverttopreviouslypublishedversion.png))。
1. 在還原資產之前，會顯示確認對話方塊。 點選「 **[!UICONTROL 回復]**」。

   資產或信件會回滾至先前發佈的版本。

## 刪除資產 {#delete-an-asset}

>[!NOTE]
>
>刪除資產會從發佈例項中移除資產。 刪除資產也會移除其版本記錄（基本版本除外）。

1. 選取資產並點選「刪 **[!UICONTROL 除]**![」](assets/delete.png)。

   >[!NOTE]
   >
   >當您點選資產以顯示資產詳細資料，或點選「檢視屬性」檢視屬性以顯示資產屬性時，也可使用「刪除」 ![選項](assets/viewproperties.png)。

1. 刪除資產之前，會出現確認對話方塊。 點選 **[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >只會刪除所選資產，且不會刪除相依資產。 若要檢查資產的參考，請點選 ![參考](assets/references.png) ，然後選取資產。
   >
   >
   >如果您嘗試刪除的資產是另一個資產的子資產，則不會刪除該資產。 若要刪除此資產，請從其他資產移除此資產的參考，然後重試。

## 受保護的調適性表單 {#protected-adaptive-forms}

您可以為希望選定用戶訪問的表單啟用驗證。 當您啟用表單驗證時，使用者會在存取表單之前先看到登入畫面。 只有擁有授權認證的使用者才能存取表單。

若要啟用表單的驗證：

1. 在瀏覽器中，在發佈例項中開啟configMgr。\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. 在Adobe Experience Manager Web Console Configuration中，按一下 **Apache Sling Authentication Service** 以進行設定。
1. 在出現的Apache Sling Authentication Service對話方塊中，使用 **+** button新增路徑。\
   添加路徑時，該路徑中的表單將啟用驗證服務。
