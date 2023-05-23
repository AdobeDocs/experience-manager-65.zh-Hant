---
title: 建立新資料夾以對表單進行分類
seo-title: Create new folders to categorize forms
description: 使用資料夾來組織表單模板、PDF、資源和自適應表單。
seo-description: Use folders to organize your form templates, PDFs, resources, and adaptive forms.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Admin
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 建立新資料夾以對表單進行分類 {#create-new-folders-to-categorize-forms}

您可以更好地使用資料夾來組織資產。 由於AEM Forms支援多種類型的資產 — 表單模板、PDF、文檔、資源和自適應表單，以及各種元資料 — 因此，您可以使用資料夾根據所需的條件對表單進行分類。

AEM Forms允許您更改資料夾的標題。 標題與儲存庫中儲存資料夾的節點的名稱不同。 而是將標題作為資料夾的元資料進行維護。 如果更改資料夾的標題，則資料夾記憶體在的任何資產的路徑都不會受到影響。

## 建立資料夾 {#create-a-folder}

可以通過以下方式之一在AEM Forms建立資料夾：

* 上載包含所需資料夾結構中的資產的ZIP檔案(請參閱 [在AEM Forms獲取XDP和PDF文檔](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 新建空資料夾

1. 登錄AEM Forms用戶介面 `https://<server>:<port>/aem/forms.html`。
1. 導航到要在其下建立資料夾的位置。
1. 按一下 ![aem6forms_add](assets/aem6forms_add.png) 表徵圖，然後選擇 **[!UICONTROL 建立資料夾]**。

1. 輸入以下詳細資訊：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（強制）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >預設情況下，名稱欄位的值會自動從標題中填充。 名稱只能包含字母數字字元或連字元(-)和下划線(_)特殊字元。 在標題中輸入的任何其他特殊字元將自動替換為連字元，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱或進一步編輯它。

1. 按一下 **[!UICONTROL 提交]。**

   在資產清單的當前位置顯示具有您定義的標題的新資料夾。

   如果存在具有指定名稱的資料夾，則提交將失敗並出現錯誤。 通過懸停在錯誤上方，可以查看錯誤消息 ![aem6forms_error_alert](assets/aem6forms_error_alert.png) 表徵圖。

### 編輯資料夾標題 {#edit-the-folder-title-br}

1. 選擇要編輯其標題的資料夾。
1. 按一下編輯 ![aem6forms_edit](assets/aem6forms_edit.png) 的子菜單。
1. 輸入新標題。 文本欄位將預先填充資料夾標題的當前值。 可以將其更改為新值。
1. 按一下 **[!UICONTROL 提交]。**
