---
title: 在AEM Forms取得XDP和PDF檔案
seo-title: 在AEM Forms取得XDP和PDF檔案
description: AEM Forms可讓您上傳表格和支援的資產，以搭配最適化表格使用。 您也可以將表單和相關資源批量上傳為ZIP。
seo-description: AEM Forms可讓您上傳表格和支援的資產，以搭配最適化表格使用。 您也可以將表單和相關資源批量上傳為ZIP。
uuid: cd49b4a8-c282-4059-95a0-c98f6c92ab14
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 28b9f1d6-6a52-458f-a8ed-a206502eda0d
docset: aem65
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 0%

---


# 在AEM Forms取得XDP和PDF檔案{#getting-xdp-and-pdf-documents-in-aem-forms}

## 概覽 {#overview}

您可以上傳至AEM Forms，將表單從本機檔案系統匯入CRX儲存庫。 下列資產類型支援上傳作業：

* 表單範本（XFA表單）
* PDF forms
* 檔案（平面PDF檔案）

您可以個別上傳支援的資產類型，或以ZIP封存的形式上傳。 您只能在ZIP封存的XFA表單旁上傳`Resource`類型的資產。

>[!NOTE]
>
>請確定您是`form-power-users`群組的成員，才能上傳XDP檔案。 請連絡您的管理員以成為群組成員。

## 上傳表單{#uploading-forms}

1. 通過訪問`https://'[server]:[port]'/aem/forms.html`登錄到AEM Forms用戶介面。
1. 導覽至您要上傳表單的檔案夾，或包含表單的檔案夾。
1. 在動作工具列中，點選「建立>檔案上傳&#x200B;**」。**

   ![「建立」下的「從本地儲存的檔案」選項](assets/step.png)

1. 「上傳表單」或「封裝」對話方塊可讓您瀏覽並選擇要上傳的檔案。 檔案瀏覽器只會顯示支援的檔案格式（ZIP、XDP和PDF）。

   >[!NOTE]
   >
   >檔案名稱只能包含英數字元、連字型大小或底線。

1. 選取檔案後按一下「上傳」以上傳檔案，或按一下「取消」以取消上傳。 快顯視窗會列出新增的資產和目前位置更新的資產。

   >[!NOTE]
   >
   >對於ZIP檔案，會顯示所有支援資產的相對路徑。 ZIP中不支援的資產會被忽略，且不會列出。 不過，如果ZIP封存只包含不支援的資產，則會顯示錯誤訊息，而非快顯對話方塊。

   ![上傳XFA表單時的「上傳」對話方塊](assets/upload-scr.png)

1. 如果一或多個資產的檔案名稱無效，則會顯示錯誤。 修正以紅色反白標示的檔案名稱，然後重新上傳。

   ![上傳XFA表單時出現錯誤訊息](assets/upload-scr-err.png)

上傳完成後，背景工作流程會根據資產的預覽來產生每個資產的縮圖。 資產的較新版本（如果已上傳）會覆寫現有資產。

### 保護模式{#protected-mode}

AEM Forms伺服器可讓您執行JavaScript程式碼。 惡意JavaScript程式碼可能會危害AEM Forms環境。 保護模式限制AEM Forms僅從受信任的資產和位置執行XDP檔案。 AEM FormsUI中的所有可用XDP都被視為可信資產。

受保護模式預設為開啟。 如有必要，您可以禁用保護模式：

1. 以管理員AEM身分登入Web Console。 URL為https://&#39;[server]:[port]&#39;/system/console/configMgr
1. 開啟行動Forms組態進行編輯。
1. 取消選擇「保護模式」選項，然後按一下「保存」。 ****&#x200B;保護模式被禁用。

## 更新引用的XFA表單{#updating-referenced-xfa-forms}

在AEM Forms,XFA表單範本可以由最適化表單或其他XFA表單範本參考。 此外，範本可參照資源或其他XFA範本。

引用XFA的最適化表單的欄位與XFA中的欄位有界。 在更新表單範本時，相關的最適化表單會嘗試與XFA同步。 如需詳細資訊，請參閱「同步最適化表單與相關的XFA](../../forms/using/synchronizing-adaptive-forms-xfa.md)」。[

移除表單範本會破壞相依最適化表單或表單範本。 這種適應性表單有時被非正式地稱為臟表單。 在AEM Forms用戶介面中，您可以通過以下兩種方式找到臟表單。

* 資產清單中的最適化表單縮圖上會顯示警告圖示，當您將指標暫留在警告圖示上時，會顯示下列訊息。\
   `Schema/Form Template for this adaptive form has been updated so please go to Authoring mode and rebase it with new version.`

![更新關聯的XFA後，出現不同步自適應表單的警告](assets/dirtyaf.png)

保持標幟以指示適應性表單是否臟。 這些資訊可在表單屬性頁面上取得，表格中繼資料亦同。 只有臟兮兮的最適化表單，中繼資料屬性`Model Refresh`才會顯示`Recommended`值。

![指示自適應表單與XFA模型不同步](assets/model-refresh.png)

