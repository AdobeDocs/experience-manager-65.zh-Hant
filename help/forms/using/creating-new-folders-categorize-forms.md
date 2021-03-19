---
title: 建立新資料夾以分類表單
seo-title: 建立新資料夾以分類表單
description: 使用資料夾來組織表單範本、PDF、資源和最適化表單。
seo-description: 使用資料夾來組織表單範本、PDF、資源和最適化表單。
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: 管理員
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# 建立新資料夾，將表單{#create-new-folders-to-categorize-forms}分類

您可以使用資料夾更妥善地組織資產。 由於AEM Forms支援多種類型的資產——表單範本、PDF、檔案、資源和可調式表單，以及各種中繼資料——您可以使用資料夾，根據所需的准則來分類表單。

AEM Forms可讓您變更資料夾的標題。 標題與儲存庫中儲存資料夾的節點的名稱不同。 標題會保留為資料夾的中繼資料。 如果您變更資料夾的標題，資料夾內任何資產的路徑都不受影響。

## 建立資料夾{#create-a-folder}

您可以通過以下方式之一在AEM Forms建立資料夾：

* 上傳包含所需資料夾結構中資產的ZIP檔案(請參閱[取得AEM Forms的XDP和PDF檔案](/help/forms/using/get-xdp-pdf-documents-aem.md))

* 建立新的空資料夾

1. 登錄至`https://<server>:<port>/aem/forms.html`的AEM Forms用戶介面。
1. 導覽至您要建立資料夾的位置。
1. 按一下工具列中的![aem6forms_add](assets/aem6forms_add.png)圖示，然後選取「建立資料夾&#x200B;]**」。**[!UICONTROL 

1. 輸入以下詳細資訊：

   * **標題：** 資料夾的顯示名稱
   * **名稱：** *（必需）* 要在儲存庫中儲存資料夾的節點名稱

   >[!NOTE]
   >
   >依預設，名稱欄位的值會自動從標題填入。 名稱只能包含英數字元，或連字型大小(-)和底線(_)特殊字元。 在標題中輸入的任何其他特殊字元都會自動取代為連字型大小，並提示您確認新名稱。 您可以選擇繼續使用建議的名稱，或進一步編輯。

1. 按一下&#x200B;**[!UICONTROL 提交]。**

   資產清單中的目前位置會顯示含有您所定義標題的新資料夾。

   如果資料夾存在指定的名稱，則提交將失敗並出現錯誤。 您可以將滑鼠指標暫留在名稱欄位旁的錯誤![ aem6forms_error_alert](assets/aem6forms_error_alert.png)圖示上，以檢視錯誤訊息。

### 編輯資料夾標題{#edit-the-folder-title-br}

1. 選擇要編輯其標題的資料夾。
1. 按一下工具列中的編輯![aem6forms_edit](assets/aem6forms_edit.png)圖示。
1. 輸入新標題。 文字欄位會預先填入資料夾標題的目前值。 您可將其變更為新值。
1. 按一下&#x200B;**[!UICONTROL 提交]。**

