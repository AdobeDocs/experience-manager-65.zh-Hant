---
title: 新增附件
description: 新增像片和手寫筆記作為註解，以在AEM Forms應用程式中執行工作
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 新增附件{#adding-attachments}

## 在與AEM Forms工作流程伺服器(JEE上的AEM Forms)同步的表單中新增附件 {#adding-annotations}

AEM Forms應用程式可讓您將影像、手寫筆記和文字筆記附加至與AEM Forms JEE伺服器同步的表單。 如果您的表單是從AEM Forms Workflow伺服器載入，您的附件就會新增至表單。 您可以選取附件按鈕![attachments-app](assets/attachments-app.png)，一起檢視表單中的所有附件。 紅色通知會指定表單中的附件數量。 如果表單中沒有附件，您將看不到紅色通知按鈕。 如果表單中沒有附件，當您選取附件按鈕![attch](assets/attch.png)時，您會取得附加像片或塗鴉的選項。

您的選項有：

* **相簿**：讓您從裝置上儲存的圖片新增圖片。

* **攝影機**：讓您拍攝影片並將其新增至表單。

* **附註**：讓您新增草寫或文字附註。 使用![塗鴉](assets/scribble.png)新增塗鴉，並使用![鍵盤](assets/keyboard.png)新增文字備註。

>[!NOTE]
>
>其他AEM Forms應用程式使用者可以看到某個使用者新增的附件。 其他使用者無法刪除使用者新增的附件。
>

### 「附件」畫面 {#the-attachments-screen}

若要檢視某個位置的所有附件，請選取![attachments-app](assets/attachments-app.png)。 您可以在此新增、重新命名和刪除附件。

![一個位置中的所有附件](assets/attachments-screen.png)

您可以使用[附件]畫面中的&#x200B;**+**&#x200B;按鈕附加其他圖片、塗鴉或文字。

### 新增像片 {#adding-a-photograph}

您可以使用行動裝置的相機或裝置中已儲存的圖片，在表單中附加圖片。

1. 選取視窗底部的附件按鈕![attch](assets/attch.png)。
1. 在出現的快顯視窗中選取&#x200B;**相簿**&#x200B;或&#x200B;**攝影機**。
1. 根據您選取的選項，執行下列動作：

   1. 如果您選取&#x200B;**攝影機**。

      拍照。 然後選取&#x200B;**Use** ![use-pic](assets/use-pic.png)按鈕。

      或選取&#x200B;**重拍** ![重拍](assets/retake.png)按鈕以重拍像片。

   1. 如果您選取&#x200B;**相簿**。

      裝置的影像瀏覽器隨即彈出。 在裝置的圖片瀏覽器中，選取您要附加的圖片。

### 新增附註 {#adding-a-note}

**附註**&#x200B;選項可讓您在表單中新增手繪文字和文字附件。

1. 選取視窗底部的附件按鈕![attch](assets/attch.png)。
1. 在出現的快顯視窗中選取&#x200B;**附註**。
1. 在啟動的Notes使用者介面中，擷取手繪文字。

   ![手寫介面](assets/scribble-ui.png)

   塗鴉

   您可以在Scribble介面中使用下列選項：

   * **清除**：清除熒幕。
   * **完成按鈕**：附加目前的塗鴉。
   * **取消按鈕**：放棄目前的塗鴉並退出Scribble使用者介面。
   * ![鍵盤](assets/keyboard.png)：清除草寫並讓您新增文字備註。

   ![AEM Forms應用程式中的鍵盤塗鴉](assets/keyboard-inapp.png)

## 表單中的附件不使用AEM Forms Workflow (OSGi上的AEM Forms)與AEM Forms伺服器同步 {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

與AEM Forms OSGi伺服器同步的行動表單附件，其運作方式與AEM Forms JEE伺服器類似。

從AEM Forms OSGi伺服器載入應用程式的最適化表單不支援表單層級附件。 若要附加影像或文字附註，請在您編寫表單時啟用表單中的欄位層級附件。 從元件瀏覽器將檔案附件元件拖放到欄位上。

如果有最適化表單，您可以檢視記錄檔案(DoR)中的附加檔案。 請參閱[產生非XFA最適化表單的記錄檔案](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)。
