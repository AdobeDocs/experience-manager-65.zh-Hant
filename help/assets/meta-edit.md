---
title: 如何編輯或新增中繼資料
description: 瞭解AEM Assets中的資產中繼資料，以及編輯資產中繼資料的各種方式。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# 如何編輯或新增中繼資料 {#how-to-edit-or-add-metadata}

中繼資料是可搜尋之資產的其他資訊。 上傳影像時會自動擷取。 您可以編輯現有的中繼資料，或將新的中繼資料屬性新增至現有欄位（例如，中繼資料欄位空白時）。

由於公司需要可控且可靠的中繼資料辭彙，AEM Assets不允許臨機新增中繼資料屬性。 雖然作者無法為資產新增中繼資料欄位，但開發人員可以。 請參 [閱為資產建立新的中繼資料屬性](meta-edit.md#editing-metadata-schema)。

## 編輯資產的中繼資料 {#editing-metadata-for-an-asset}

若要編輯中繼資料：

1. 執行下列任一項作業：

   * 從「資產」UI中，選取資產，然後按一下／點選工具列 **[!UICONTROL 中的「檢視屬性]** 」圖示。
   * 從資產縮圖中，選取「檢視 **[!UICONTROL 屬性]** 」快速動作。
   * 在資產頁面中，按一下／點選工具 **[!UICONTROL 列中的「檢視屬性]** 」圖示。
      ![chlimage_1-168](assets/chlimage_1-168.png)
   *圖：屬性圖示*

   資產頁面會顯示資產的所有中繼資料。 此中繼資料在上傳（收錄）至AEM Assets時會自動擷取。

   ![選取資產屬性以檢視中繼資料](assets/asset-metadata.png)


   *圖：在資產屬性頁面上編輯或新增中繼資料*

1. 視需要對各種標籤下的中繼資料進行編輯，在完成時，按一下工具列中的「儲存 **** 」以儲存您所做的變更。按一下/點 **[!UICONTROL 選「關閉]** 」，返回「資產」網頁介面。

   >[!NOTE]
   >
   >如果文字欄位空白，則沒有現有的中繼資料集。 您可以在欄位中輸入值，並儲存它以新增該中繼資料屬性。

對資產中繼資料所做的任何變更都會寫入原始二進位檔，作為其XMP資料的一部分。 這是透過AEM中繼資料回寫工作流程來完成的。 對現有屬性所做的變更(如 `dc:title`)會被覆寫，而新建立的屬性(包括自訂屬性 `cq:tags`)會與架構一起新增。

支援並啟用XMP回寫功能，適用於技術需求中所述的平台 [和檔案格式。](/help/sites-deploying/technical-requirements.md)

## 編輯中繼資料結構 {#editing-metadata-schema}

如需如何編輯中繼資料結構的詳細資訊，請參閱「編 [輯中繼資料結構表單](metadata-schemas.md#edit-metadata-schema-forms)」。

## 在AEM中註冊自訂命名空間 {#registering-a-custom-namespace-within-aem}

您可以在AEM中新增自己的名稱空間。 就像有預先定義的名稱空間（例如cq、jcr和sling）一樣，您也可以擁有儲存庫中繼資料和xml處理的名稱空間。

1. 轉至節點類型管理頁 `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`。
1. 按一下或點 **[!UICONTROL 選頁面頂]** 端的「命名空間」。 命名空間管理頁面會顯示在視窗中。

1. 若要新增命名空間，請按一下或點選 **[!UICONTROL 底部的]** 「新增」。
1. 在XML命名空間約定中指定自訂命名空間（以URI的形式指定ID及ID的相關首碼），然後按一下或點選「儲 **[!UICONTROL 存」]**。
