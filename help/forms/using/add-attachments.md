---
title: 新增附件
description: 新增像片和手寫筆記作為註解，以在AEM Forms應用程式中執行工作
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 新增附件{#adding-attachments}

## 在與AEM Forms工作流程伺服器(JEE上的AEM Forms)同步的表單中新增附件 {#adding-annotations}

AEM Forms應用程式可讓您將影像、手寫筆記和文字筆記附加至與AEM Forms JEE伺服器同步的表單。 如果您的表單是從AEM Forms Workflow伺服器載入，您的附件就會新增至表單。 您可以選取附件按鈕 ![attachments-app](assets/attachments-app.png) 以一起檢視表單中的所有附件。 紅色通知會指定表單中的附件數量。 如果表單中沒有附件，您將看不到紅色通知按鈕。 如果表單中沒有附件，當您選取附件按鈕時 ![附加](assets/attch.png)，您就可以選擇附加像片或塗鴉。

您的選項有：

* **相簿**：可讓您從裝置上儲存的圖片新增圖片。

* **相機**：可讓您拍攝圖片並將其新增至表單。

* **附註**：讓您新增草寫或文字註記。 使用 ![塗鴉](assets/scribble.png) 以新增塗鴉，並且 ![鍵盤](assets/keyboard.png) 以新增文字註記。

>[!NOTE]
>
>其他AEM Forms應用程式使用者可以看到某個使用者新增的附件。 其他使用者無法刪除使用者新增的附件。
>

### 「附件」畫面 {#the-attachments-screen}

若要檢視某個位置的所有附件，請選取 ![attachments-app](assets/attachments-app.png). 您可以在此新增、重新命名和刪除附件。

![一個位置中的所有附件](assets/attachments-screen.png)

您可以使用 **+** 「附件」畫面中的按鈕，以附加其他圖片、塗鴉或文字。

### 新增像片 {#adding-a-photograph}

您可以使用行動裝置的相機或裝置中已儲存的圖片，在表單中附加圖片。

1. 選取附件按鈕 ![附加](assets/attch.png) 在視窗底部。
1. 選取 **相簿** 或 **相機** 在出現的快顯視窗中。
1. 根據您選取的選項，執行下列動作：

   1. 如果您選取 **相機**.

      拍照。 然後選取 **使用** ![use-pic](assets/use-pic.png) 按鈕。

      或選取 **重拍** ![重拍](assets/retake.png) 按鈕以重拍像片。

   1. 如果您選取 **相簿**.

      裝置的影像瀏覽器隨即彈出。 在裝置的圖片瀏覽器中，選取您要附加的圖片。

### 新增附註 {#adding-a-note}

此 **附註** 選項可讓您在表單中新增手繪文字和文字附件。

1. 選取附件按鈕 ![附加](assets/attch.png) 在視窗底部。
1. 選取 **附註** 在出現的快顯視窗中。
1. 在啟動的Notes使用者介面中，擷取手繪文字。

   ![塗鴉介面](assets/scribble-ui.png)

   塗鴉

   您可以在Scribble介面中使用下列選項：

   * **清除**：清除畫面。
   * **完成按鈕**：附加目前的塗鴉。
   * **取消按鈕**：捨棄目前的草寫並退出草寫使用者介面。
   * ![鍵盤](assets/keyboard.png)：清除草稿，並讓您新增文字註記。

   ![AEM Forms應用程式中的鍵盤塗鴉](assets/keyboard-inapp.png)

## 表單中的附件不使用AEM Forms Workflow (OSGi上的AEM Forms)與AEM Forms伺服器同步 {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

與AEM Forms OSGi伺服器同步的行動表單附件，其運作方式與AEM Forms JEE伺服器類似。

從AEM Forms OSGi伺服器載入應用程式的最適化表單不支援表單層級附件。 若要附加影像或文字附註，請在您編寫表單時啟用表單中的欄位層級附件。 從元件瀏覽器將檔案附件元件拖放到欄位上。

如果有最適化表單，您可以檢視記錄檔案(DoR)中的附加檔案。 請參閱， [產生非XFA最適化表單的記錄檔案](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
