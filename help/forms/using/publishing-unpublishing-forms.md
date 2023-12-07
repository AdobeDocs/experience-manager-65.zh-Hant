---
title: 發佈和取消發佈表單和檔案
description: 您可以排程表單的發佈和取消發佈。 發佈的表單會在發佈執行個體上復寫。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# 發佈和取消發佈表單和檔案{#publishing-and-unpublishing-forms-and-documents}

AEM Forms可讓您輕鬆建立、發佈和取消發佈表單。 如需AEM Forms的詳細資訊，請參閱 [管理表單簡介](../../forms/using/introduction-managing-forms.md).

AEM Forms伺服器提供兩個例項：「作者」和「發佈」。 製作例項用於建立及管理表單資產和資源。 發佈執行個體用於保留可供一般使用者使用的資產和相關資源。 您可以在作者模式中匯入XDP和PDF forms。 如需詳細資訊，請參閱 [在AEM Forms中取得XDP和PDF檔案](../../forms/using/get-xdp-pdf-documents-aem.md).

## 支援的資產   {#supported-assets-nbsp}

AEM Forms支援下列資產型別：

* 調適型表單
* 最適化檔案
* 最適化表單片段
* 主題
* 表單範本（XFA表單）
* PDF forms
* 檔案(平面PDF檔案)
* 表單集
* 資源（影像、方案和樣式表）

最初，所有資產都只能在Author例項中使用。 管理員或表單作者可以發佈資源以外的所有資產。

當您選取表單並發佈時，也會發佈其相關資產和資源。 但是，相依資產不會發佈。 在此上下文中，相關資產和資源是已發佈資產使用或參照的資產。 相依資產是參考已發佈資產的資產。

您的Adaptive Forms可能會使用一些不會自動發佈的設定、設定和自訂。 建議您先發佈或啟用這些資源，再發佈最適化表單。

* 可編輯的最適化表單範本
* Adobe Sign、Typekit、reCAPTCHA和表單資料模型的Cloud Service設定
* 只有當使用者擁有管理員許可權時，才會啟用其他雲端服務設定。
* 自訂。 這些包括但不限於：

   * 自訂版面
   * 自訂外觀
   * CSS檔案 — 在調適型表單容器屬性對話方塊中作為輸入專案
   * 使用者端資料庫類別 — 在調適型表單容器屬性對話方塊中作為輸入內容
   * 任何其他使用者端程式庫，可能包含在調適型表單範本中。
   * 設計路徑

## 資產狀態 {#asset-states}

資產可以有下列狀態：

* **已取消發佈：** 從未發佈的資產(未發佈狀態僅適用於Forms資產)。 通訊管理資產沒有「未發佈」狀態。)
* **已發佈**：已發佈且可在發佈執行個體上使用的資產
* **已修改**：發佈後修改的資產

## 發佈資產 {#publish-an-asset}

1. 登入AEM Forms伺服器。
1. 使用下列其中一項，選取並發佈資產。

   1. 將指標移至資產上並選取 **[!UICONTROL 發佈]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png).
   1. 執行下列任一項作業，然後選取「發佈」：

      * 如果您在卡片檢視中，請選取 **[!UICONTROL 輸入選取範圍]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然後選取資產。 已選取資產。
      * 如果您在清單檢視中，請選取資產的核取方塊。 已選取資產。
      * 選取要顯示其詳細資訊的資產。
      * 點選「檢視屬性」以顯示資產屬性 ![viewproperties](assets/viewproperties.png).

      >[!NOTE]
      >
      >請勿選取多個資產。 不支援一次發佈多個資產。

1. 當發佈程式啟動時，確認對話方塊會出現，列出所有相關資產和資源。 在包含相關資產的對話方塊中，選取 **[!UICONTROL 發佈]**. 資產會發佈，且發佈資產成功對話方塊會出現。

   >[!NOTE]
   >
   >對於調適型表單及相關資產，也會顯示調適型表單頁面名稱。

   ![包含所有相關資產和資源的確認對話方塊](assets/p4.png)

   包含所有相關資產和資源的確認對話方塊。

   >[!NOTE]
   >
   >對於Forms Manager，如果使用者沒有發佈所列資產的許可權，則會停用發佈動作。 需要額外許可權的資產會以紅色顯示。

   發佈資產後，資產的中繼資料屬性會複製到發佈執行個體，而資產的狀態會變更為已發佈。 已發佈的相依資產狀態也會變更為「已發佈」。

   發佈資產後，您可以使用Forms入口網站在網頁上顯示所有資產。 如需詳細資訊，請參閱 [在入口網站上發佈表單簡介](../../forms/using/introduction-publishing-forms.md).

## 發佈所有對應管理資產 {#publish-all-the-correspondence-management-assets}

AEM Forms可讓您一次發佈伺服器上的所有Correspondence Management資產。 發佈的資產包含所有「對應管理」資產和相關相依性。

完成下列步驟，在伺服器上發佈所有Correspondence Management資產：

1. 登入AEM Forms伺服器。
1. 選取 **Adobe Experience Manager** 於全域導覽列中。
1. 選取 ![工具](assets/tools.png)，然後選取 **Forms**.
1. 選取 **發佈對應管理資產**.

   ![publish-cmp-assets](assets/publish-cmp-assets.png)

   便會顯示「發佈所有對應管理資產」頁面，並顯示上次嘗試「發佈對應管理資產」程式的相關資訊。

   ![publish-last-run-details](assets/publish-last-run-details.png)

1. 選取 **發佈** 然後，在確認訊息中，選取 **確定**.

   批次處理完成後，您可以檢視上次執行的詳細資訊。 這包括管理員登入以及批次是否成功執行的資訊。

   >[!NOTE]
   >
   >發佈程式一經啟動便無法取消。 此外，在發佈作業進行時，請勿建立、刪除、修改或發佈任何資產，或啟動「匯出所有對應管理資產」作業。

## 自動發佈和取消發佈Forms和檔案 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms可讓您為Forms和檔案排程資產發佈和取消發佈。 您可以在中繼資料編輯器中指定排程。 如需有關管理表單中繼資料的詳細資訊，請參閱 [管理表單中繼資料。](../../forms/using/manage-form-metadata.md)

請依照下列步驟，排程發佈和取消發佈Forms &amp; Documents資產的日期和時間：

1. 選取資產並選取 **[!UICONTROL 檢視屬性]**. 「中繼資料屬性」頁面隨即開啟。
1. 在「中繼資料屬性」頁面中，選取 **[!UICONTROL 進階]**，然後選取 **[!UICONTROL 編輯]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png).
1. 在 **[!UICONTROL 準時發佈]** 和 **[!UICONTROL 發佈關閉時間]** 欄位中，選取日期和時間。\
   選取 **[!UICONTROL 完成]** ![aem6forms_check](assets/aem6forms_check.png).

## 取消發佈資產 {#unpublish-an-asset}

1. 選取已發佈的資產，然後選取 **[!UICONTROL 取消發佈]** ![取消發佈](assets/unpublish.png).
1. 使用下列其中一項，選取並取消發佈資產。

   1. 將指標移至資產上並選取 **[!UICONTROL 取消發佈]** ![取消發佈](assets/unpublish.png).
   1. 執行下列任一項作業，然後選取取消發佈：

      * 如果您在卡片檢視中，請選取 **[!UICONTROL 輸入選取範圍]** ![aem6forms_check-circle](assets/aem6forms_check-circle.png)，然後選取資產。 已選取資產。

      * 如果您在清單檢視中，將滑鼠指標暫留在資產上並選取「 」 ![selectassetcheckmark](assets/selectassetcheckmark.png) . 已選取資產。

      * 選取要顯示其詳細資訊的資產。
      * 點選「檢視屬性」以顯示資產屬性 ![viewproperties](assets/viewproperties.png).

1. 取消發佈程式啟動時，會顯示確認對話方塊。 選取 **[!UICONTROL 取消發佈]**.

   >[!NOTE]
   >
   >只會取消發佈選取的資產，不會取消發佈其子項和參照的資產（如果有的話）。

## 將資產或字母回覆至先前發佈的版本 {#revert-an-asset-or-letter-to-the-previously-published-version}

每當您在編輯資產或信函後發佈資產或信函時，就會建立資產或信函的版本。 您可以將資產或信函回覆至先前發佈的版本。 如果資產或檔案的目前版本發生問題，您可能需要這麼做。

>[!NOTE]
>
>如果系統中刪除了發佈信函中使用的任何相依資產，請勿將信函還原為上次發佈狀態。

1. 選取資產並選取 **[!UICONTROL 回覆至先前發佈的版本]** ![reverttopreviouslypublishedversion](assets/reverttopreviouslypublishedversion.png).
1. 在回覆資產之前，會顯示確認對話方塊。 選取 **[!UICONTROL 回覆]**.

   資產或信函會復原至其先前發佈的版本。

## 刪除資產 {#delete-an-asset}

>[!NOTE]
>
>刪除資產會將其從發佈執行個體中移除。 刪除資產也會移除其版本記錄（基礎版本除外）。

1. 選取資產並選取 **[!UICONTROL 刪除]** ![刪除](assets/delete.png).

   >[!NOTE]
   >
   >點選資產以顯示資產詳細資訊，或點選檢視屬性以顯示資產屬性時，也可以使用「刪除」選項 ![viewproperties](assets/viewproperties.png).

1. 刪除資產之前，會顯示確認對話方塊。 選取&#x200B;**[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >只會刪除選取的資產，不會刪除相依的資產和。 若要檢查資產的引用，請選取 ![引用](assets/references.png) 然後選取資產。
   >
   >
   >如果您嘗試刪除的資產是另一個資產的子資產，則不會刪除它。 若要刪除這類資產，請從其他資產中移除此資產的參考資料，然後重試。

## 受保護的最適化表單 {#protected-adaptive-forms}

您可以啟用您希望所選使用者存取之表單的驗證。 當您啟用表單驗證時，使用者在存取表單之前會先看到登入畫面。 只有擁有授權憑證的使用者才能存取表單。

若要啟用表單的驗證：

1. 在瀏覽器中，開啟發佈執行個體中的configMgr 。\
   URL： `https://<hostname>:<PublishPort>/system/console/configMgr`

1. 在Adobe Experience Manager Web主控台設定中，按一下 **Apache Sling驗證服務** 以進行設定。
1. 在出現的Apache Sling Authentication Service對話方塊中，使用 **+** 按鈕以新增路徑。\
   當您新增路徑時，會針對該路徑中的表單啟用驗證服務。
