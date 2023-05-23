---
title: 在AEM Forms獲取XDP和PDF文檔
seo-title: Getting XDP and PDF documents in AEM Forms
description: AEM Forms允許您上傳表單和支援的資產，以便與自適應表單一起使用。 您還可以將表單和相關資源批量上載為ZIP。
seo-description: AEM Forms allows you to upload forms and supported assets to use with adaptive forms. You can also bulk upload forms and related resources as a ZIP.
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
role: Admin
exl-id: 9ecdc50a-31e3-46ae-948a-d1f6e6085734
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# 在AEM Forms獲取XDP和PDF文檔{#getting-xdp-and-pdf-documents-in-aem-forms}

## 概觀 {#overview}

您可以將表單從本地檔案系統導入到CRX儲存庫，方法是將表單上載到AEM Forms。 以下資產類型支援上載操作：

* 表單模板（XFA表單）
* PDF forms
* 文檔(平面PDF文檔)

您可以單獨或作為ZIP存檔上載受支援的資產類型。 您可以上載類型的資產 `Resource`，僅與ZIP存檔中的XFA窗體一起使用。

>[!NOTE]
>
>確保您是 `form-power-users` 組以能夠上載XDP檔案。 請與管理員聯繫以成為組的成員。

## 正在上載表單 {#uploading-forms}

1. 通過訪問 `https://'[server]:[port]'/aem/forms.html`。
1. 導航到要上載表單的資料夾或包含表單的資料夾。
1. 在操作工具欄中，按一下 **建立>檔案上載**。

   ![「建立」下的「本地儲存檔案」選項](assets/step.png)

1. 通過「上載表單」或「包」對話框，可以瀏覽並選擇要上載的檔案。 檔案瀏覽器只顯示支援的檔案格式(ZIP、XDP和PDF)。

   >[!NOTE]
   >
   >檔案名只能包含字母數字字元、連字元或下划線。

1. 選擇檔案後按一下「上載」以上載檔案，或按一下「取消」取消上載。 彈出窗口列出了添加的資產和在當前位置更新的資產。

   >[!NOTE]
   >
   >對於ZIP檔案，將顯示所有受支援資產的相對路徑。 ZIP中不支援的資產將被忽略，且未列出。 但是，如果ZIP存檔中只包含不受支援的資產，則會顯示一條錯誤消息，而不是彈出對話框。

   ![上載XFA表單時的「上載」對話框](assets/upload-scr.png)

1. 如果一個或多個資產的檔案名無效，則顯示錯誤。 更正以紅色突出顯示的檔案名並重新上載。

   ![上載XFA表單時出現錯誤消息](assets/upload-scr-err.png)

上載完成後，後台工作流將根據資產的預覽為每個資產生成縮略圖。 較新版本的資產（如果上載）將覆蓋現有資產。

### 保護模式 {#protected-mode}

AEM Forms伺服器允許您運行JavaScript代碼。 惡意的JavaScript代碼可能會危害AEM Forms環境。 受保護模式限制AEM Forms僅從受信任的資產和位置運行XDP檔案。 AEM FormsUI中提供的所有XDP都被視為可信資產。

預設情況下，受保護模式處於開啟狀態。 如有必要，可以禁用受保護模式：

1. 以管理員身AEM份登錄到Web控制台。 URL為https://&#39;[伺服器]:[埠]「/system/console/configMgr
1. 開啟移動Forms配置進行編輯。
1. 取消選擇「受保護模式」選項，然後按一下 **保存**。 已禁用受保護模式。

## 更新引用的XFA表單 {#updating-referenced-xfa-forms}

在AEM Forms,XFA表單模板可以由自適應表單或另一個XFA表單模板引用。 此外，模板可以引用資源或其他XFA模板。

引用XFA的自適應表單的欄位與XFA中可用的欄位綁定。 在更新表單模板時，關聯的自適應表單會嘗試與XFA同步。 有關詳細資訊，請參閱 [將自適應表單與關聯的XFA同步](../../forms/using/synchronizing-adaptive-forms-xfa.md)。

刪除表單模板會損壞從屬自適應表單或表單模板。 這種自適應形式有時被非正式地稱為臟形式。 在AEM Forms用戶介面中，您可以通過以下兩種方式查找臟表單。

* 在資產清單中的自適應表單縮略圖上顯示一個警告表徵圖，當將指針懸停在警告表徵圖上時，將顯示以下消息。\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![更新關聯的XFA後出現不同步自適應表單的警告](assets/dirtyaf.png)

保持標誌以指示自適應形式是否臟。 此資訊可在表單屬性頁和表單元資料上找到。 僅對臟自適應表單，元資料屬性 `Model Refresh` 顯示 `Recommended` 值。

![表示自適應形式與XFA模型不同步](assets/model-refresh.png)
