---
title: 發佈和取消發佈表單和文檔
seo-title: Publishing and unpublishing forms and documents
description: 您可以計畫表單的發佈和取消發佈。 已發佈表單將複製到發佈實例上。
seo-description: You can schedule publishing and unpublishing of forms. Published forms are replicated on the publish instance.
uuid: 0bad5608-b7a8-4599-81cc-2cd0a3dc7dd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
content-strategy: max-2018
discoiquuid: 32a7a50c-74f4-49bc-a0bd-a9ec142527cb
docset: aem65
exl-id: f26c4268-7885-4e61-a258-219d98288548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# 發佈和取消發佈表單和文檔{#publishing-and-unpublishing-forms-and-documents}

AEM Forms允許您輕鬆建立、發佈和取消發佈表單。 有關AEM Forms的詳細資訊，請參見 [管理表單簡介](../../forms/using/introduction-managing-forms.md)。

AEM Forms伺服器提供兩個實例：作者和發佈。 作者實例用於建立和管理表單資產和資源。 發佈實例用於保留最終用戶可用的資產和相關資源。 可以在「作者」模式下導入XDP和PDF forms。 有關詳細資訊，請參見 [在AEM Forms獲取XDP和PDF文檔](../../forms/using/get-xdp-pdf-documents-aem.md)。

## 支援的資產   {#supported-assets-nbsp}

AEM Forms支援以下類型的資產：

* 調適型表單
* 自適應文檔
* 自適應形式片段
* 主題
* 表單模板（XFA表單）
* PDF forms
* 文檔(平面PDF文檔)
* 表單集
* 資源（映像、架構和樣式表）

最初，所有資產只在Author實例中可用。 管理員或表單作者可以發佈除資源之外的所有資產。

選擇並發佈表單時，還會發佈其相關資產和資源。 但是，不發佈從屬資產。 在此背景下，相關資產和資源是已發佈資產使用或引用的資產。 從屬資產是指引用已發佈資產的資產。

您的自適應Forms可能會使用一些未自動發佈的配置、設定和自定義。 建議在發佈自適應表單之前發佈或激活這些資源。

* 可編輯的自適應表單模板
* Cloud ServiceAdobe Sign、Typekit、reCAPTCHA和表單資料模型的配置
* 僅當用戶具有管理權限時，才激活其他雲服務配置。
* 自定義。 這些包括但不限於：

   * 自定義佈局
   * 自定義外觀
   * CSS檔案 — 在「自適應表單」容器屬性對話框中作為輸入
   * 客戶端庫類別 — 在「自適應表單」容器屬性對話框中作為輸入
   * 可以作為Adaptive Form模板的一部分包含的任何其他客戶端庫。
   * 設計路徑

## 資產狀態 {#asset-states}

資產可以具有以下狀態：

* **未發佈：** 從未發佈的資產(未發佈的狀態僅適用於Forms資產。 通信管理資產沒有未發佈狀態。)
* **已發佈**:已發佈且在「發佈」實例上可用的資產
* **已修改**:發佈後修改的資產

## 發佈資產 {#publish-an-asset}

1. 登錄到AEM Forms伺服器。
1. 使用以下選項之一選擇和發佈資產。

   1. 將指針移到資產上並點擊 **[!UICONTROL 發佈]** ![aem6forms_globe](assets/aem6forms_globe.pngasset.png)。
   1. 執行下列操作之一，然後按一下「發佈」：

      * 如果在卡視圖中，請點擊 **[!UICONTROL 輸入選擇]** ![aem6forms_check circle](assets/aem6forms_check-circle.png)，並點擊資產。 資產被選中。
      * 如果您在清單視圖中，請選中資產的複選框。 資產被選中。
      * 點擊資產以顯示其詳細資訊。
      * 按一下「查看屬性」顯示資產的屬性 ![視圖屬性](assets/viewproperties.png)。

      >[!NOTE]
      >
      >不要選擇多個資產。 不支援一次發佈多個資產。


1. 當「發佈」進程啟動時，將顯示一個確認對話框，列出所有相關資產和資源。 在包含相關資產的對話框中，點擊 **[!UICONTROL 發佈]**。 將發佈資產，並顯示「發佈資產成功」對話框。

   >[!NOTE]
   >
   >對於「自適應」表單以及相關資產，還顯示「自適應表單」頁名。

   ![與所有相關資產和資源進行確認對話](assets/p4.png)

   與所有相關資產和資源進行確認對話。

   >[!NOTE]
   >
   >對於Forms管理器，如果用戶無權發佈列出的資產，則「發佈」(Publish)操作將被禁用。 需要額外權限的資產以紅色顯示。

   發佈資產後，資產的元資料屬性將複製到「發佈」實例，資產的狀態將更改為「已發佈」。 已發佈的從屬資產的狀態也更改為「已發佈」。

   發佈資產後，您可以使用Forms門戶在網頁上顯示所有資產。 有關詳細資訊，請參見 [門戶上發佈表單簡介](../../forms/using/introduction-publishing-forms.md)。

## 發佈所有信件管理資產 {#publish-all-the-correspondence-management-assets}

AEM Forms允許您一次性在伺服器上發佈所有Tergement Management資產。 已發佈的資產包括所有Tergement Management資產和相關依存項。

完成以下步驟以在伺服器上發佈所有Tergement Management資產：

1. 登錄到AEM Forms伺服器。
1. 點擊 **Adobe Experience Manager** 的子菜單。
1. 點擊 ![工具](assets/tools.png)，然後按一下 **Forms**。
1. 點擊 **發佈信件管理資產**。

   ![發佈cmp資產](assets/publish-cmp-assets.png)

   此時將顯示「發佈所有通信管理資產」頁，並顯示上次嘗試發佈通信管理資產流程的相關資訊。

   ![發佈上次運行的詳細資訊](assets/publish-last-run-details.png)

1. 點擊 **發佈** 在確認消息中，點擊 **確定**。

   批處理完成後，您可以查看上次運行的詳細資訊。 這包括管理員登錄以及批處理是否成功運行或失敗等資訊。

   >[!NOTE]
   >
   >一旦啟動，則無法取消發佈進程。 此外，在「發佈」操作進行過程中，請勿建立、刪除、修改或發佈任何資產或啟動「導出所有通信管理資產」操作。

## 自動發佈和取消發佈Forms和文檔 {#automate-publishing-and-unpublishing-for-forms-amp-documents}

AEM Forms允許您為Forms和文檔安排資產發佈和取消發佈。 可以在元資料編輯器中指定調度。 有關管理表單元資料的詳細資訊，請參見 [管理表單元資料。](../../forms/using/manage-form-metadata.md)

按照以下步驟安排發佈和取消發佈Forms和文檔資產的日期和時間：

1. 選擇資產並點擊 **[!UICONTROL 查看屬性]**。 將開啟「元資料屬性」頁。
1. 在「元資料屬性」頁中，按一下 **[!UICONTROL 高級]**，然後按一下 **[!UICONTROL 編輯]** ![illustratorcc_penciltool_cur_edit_2_17](assets/illustratorcc_penciltool_cur_edit_2_17.png)。
1. 在 **[!UICONTROL 按時發佈]** 和 **[!UICONTROL 發佈關閉時間]** 的子菜單。\
   點擊 **[!UICONTROL 完成]** ![aem6forms_check](assets/aem6forms_check.png)。

## 取消發佈資產 {#unpublish-an-asset}

1. 選擇已發佈的資產並點擊 **[!UICONTROL 取消發佈]** ![發佈](assets/unpublish.png)。
1. 使用以下選項之一選擇和取消發佈資產。

   1. 將指針移到資產上並點擊 **[!UICONTROL 取消發佈]** ![發佈](assets/unpublish.png)。
   1. 執行下列操作之一，然後點擊取消發佈：

      * 如果在卡視圖中，請點擊 **[!UICONTROL 輸入選擇]** ![aem6forms_check circle](assets/aem6forms_check-circle.png)，並點擊資產。 資產被選中。

      * 如果您在清單視圖中，將滑鼠懸停在資產上，然後點擊 ![選擇元件複選標籤](assets/selectassetcheckmark.png) 。 資產被選中。

      * 點擊資產以顯示其詳細資訊。
      * 按一下「查看屬性」顯示資產的屬性 ![視圖屬性](assets/viewproperties.png)。

1. 啟動「取消發佈」進程時，將顯示確認對話框。 點擊 **[!UICONTROL 取消發佈]**。

   >[!NOTE]
   >
   >只取消發佈所選資產，且其子項和引用資產（如果有）未取消發佈。

## 將資產或信件還原為以前發佈的版本 {#revert-an-asset-or-letter-to-the-previously-published-version}

每次編輯資產或信件後發佈該資產或信件時，都會建立該資產或信件的版本。 您可以將資產或信件還原為以前發佈的版本。 如果資產或文檔的當前版本出現問題，則可能需要執行此操作。

>[!NOTE]
>
>如果從系統中刪除了該已發佈信函中使用的任何相關資產，則不要將信件還原為上次發佈狀態。

1. 選擇資產並點擊 **[!UICONTROL 還原為以前發佈的版本]** ![RevertopreviyPublished版本](assets/reverttopreviouslypublishedversion.png)。
1. 在還原資產之前，將顯示確認對話框。 點擊 **[!UICONTROL 還原]**。

   資產或信件將回退到其先前發佈的版本。

## 刪除資產 {#delete-an-asset}

>[!NOTE]
>
>刪除資產會從發佈實例中刪除它。 刪除資產也會刪除其版本歷史記錄（基本版本除外）。

1. 選擇資產並點擊 **[!UICONTROL 刪除]** ![刪除](assets/delete.png)。

   >[!NOTE]
   >
   >當您通過點擊資產來顯示資產詳細資訊或通過點擊「查看屬性」來顯示資產的屬性時，「刪除」選項也可用 ![視圖屬性](assets/viewproperties.png)。

1. 在刪除資產之前，將顯示確認對話框。 點擊 **[!UICONTROL 刪除]**。

   >[!NOTE]
   >
   >只刪除所選資產，而不刪除相關資產。 要檢查資產的引用，請點擊 ![參照](assets/references.png) ，然後選擇資產。
   >
   >
   >如果您嘗試刪除的資產是另一個資產的子資產，則不會刪除它。 要刪除此資產，請從其他資產中刪除此資產的引用，然後重試。

## 受保護的自適應表單 {#protected-adaptive-forms}

您可以為希望選定用戶訪問的表單啟用身份驗證。 啟用表單身份驗證後，用戶在訪問表單之前會看到登錄螢幕。 只有具有授權憑據的用戶才能訪問表單。

要啟用表單的身份驗證，請執行以下操作：

1. 在瀏覽器中，在發佈實例中開啟configMgr。\
   URL: `https://<hostname>:<PublishPort>/system/console/configMgr`

1. 在Adobe Experience ManagerWeb控制台配置中，按一下 **Apache Sling身份驗證服務** 來配置它。
1. 在出現的「Apache Sling Authentication Service」對話框中，使用 **+** 按鈕以添加路徑。\
   添加路徑時，將為該路徑中的表單啟用身份驗證服務。
