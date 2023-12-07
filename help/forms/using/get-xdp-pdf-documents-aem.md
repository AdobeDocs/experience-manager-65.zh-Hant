---
title: 在AEM Forms中取得XDP和PDF檔案
description: AEM Forms可讓您上傳要搭配最適化表單使用的表單和支援資產。 您也可以以ZIP格式大量上傳表單和相關資源。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin
exl-id: 9ecdc50a-31e3-46ae-948a-d1f6e6085734
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 0%

---

# 在AEM Forms中取得XDP和PDF檔案{#getting-xdp-and-pdf-documents-in-aem-forms}

## 概觀 {#overview}

您可以將表單上傳至AEM Forms，從本機檔案系統匯入至CRX存放庫。 下列資產型別支援上傳作業：

* 表單範本（XFA表單）
* PDF forms
* 檔案(平面PDF檔案)

您可以個別上傳支援的資產型別，或以ZIP封存檔的形式上傳。 您可以上傳該型別的資產 `Resource`，僅與ZIP封存中的XFA表單一起提供。

>[!NOTE]
>
>確定您是 `form-power-users` 群組以上傳XDP檔案。 請聯絡您的管理員以成為群組的成員。

## 正在上傳表單 {#uploading-forms}

1. 登入AEM Forms使用者介面，方法是存取 `https://'[server]:[port]'/aem/forms.html`.
1. 導覽至您要上傳表單的資料夾或包含表單的資料夾。
1. 在動作工具列中，選取 **建立>檔案上傳**.

   ![「建立」下的「來自本機儲存體的檔案」選項](assets/step.png)

1. 上傳表單或封裝對話方塊可讓您瀏覽並選擇您要上傳的檔案。 檔案瀏覽器只會顯示支援的檔案格式(ZIP、XDP和PDF)。

   >[!NOTE]
   >
   >檔案名稱只能包含英數字元、連字型大小或底線。

1. 選取檔案後按一下「上傳」可上傳檔案，或按一下「取消」取消上傳。 快顯視窗會列出在目前位置新增的資產和更新的資產。

   >[!NOTE]
   >
   >對於ZIP檔案，會顯示所有支援資產的相對路徑。 ZIP內不支援的資產會遭忽略，不會列出。 不過，如果ZIP封存僅包含不支援的資產，則會顯示錯誤訊息，而非快顯對話方塊。

   ![上傳XFA表單時上傳對話方塊](assets/upload-scr.png)

1. 如果一個或多個資產的檔案名稱無效，則會顯示錯誤。 修正以紅色反白顯示的檔案名稱，然後重新上傳。

   ![上傳XFA表單時出現錯誤訊息](assets/upload-scr-err.png)

上傳完成後，背景工作流程會根據資產預覽為每個資產產生縮圖。 較新版本的資產（如果上傳）會覆寫現有資產。

### 受保護模式 {#protected-mode}

AEM Forms伺服器可讓您執行JavaScript程式碼。 惡意的JavaScript程式碼可能會損害AEM Forms環境。 保護模式會限制AEM Forms僅從受信任的資產和位置執行XDP檔案。 AEM Forms UI中可用的所有XDP都視為受信任的資產。

受保護模式預設為開啟。 如有必要，您可以停用保護模式：

1. 以管理員身分登入AEM Web Console。 URL為https://&#39;[伺服器]：[連線埠]&#39;/system/console/configMgr
1. 開啟Mobile Forms設定以進行編輯。
1. 取消選取「受保護模式」選項，然後按一下 **儲存**. 受保護模式已停用。

## 更新參考的XFA表單 {#updating-referenced-xfa-forms}

在AEM Forms中，XFA表單範本可由最適化表單或其他XFA表單範本參照。 此外，範本可以參照資源或其他XFA範本。

參考XFA的最適化表單會有其欄位與XFA中可用的欄位繫結。 更新表單範本時，關聯的調適型表單會嘗試與XFA同步。 如需詳細資訊，請參閱 [將調適型表單與關聯的XFA同步](../../forms/using/synchronizing-adaptive-forms-xfa.md).

移除表單範本會損毀相依的最適化表單或表單範本。 這類最適化表單有時非正式地稱為「已變更表單」。 在AEM Forms使用者介面中，您可以透過以下兩種方式找到已變更的表單。

* 資產清單中的調適型表單縮圖上會顯示警告圖示，而當您將指標停留在警告圖示上時，會顯示下列訊息。\
  `Schema/Form Template for this adaptive form has been updated so go to Authoring mode and rebase it with new version.`

![更新相關XFA後出現不同步調適用性表單的警告](assets/dirtyaf.png)

系統會維持旗標，指出最適化表單是否已變更。 此資訊可與表單中繼資料一併顯示在表單屬性頁面上。 僅適用於已修改的最適化表單，中繼資料屬性 `Model Refresh` 顯示 `Recommended` 值。

![表示最適化表單與XFA模型不同步](assets/model-refresh.png)
