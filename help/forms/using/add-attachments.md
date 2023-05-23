---
title: 添加附件
seo-title: Adding attachments
description: 在AEM Forms應用中將照片和筆記添加為任務的注釋
seo-description: Add photographs and scribble notes as annotations to your task in the AEM Forms app
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# 添加附件{#adding-attachments}

## 在與AEM Forms工作流伺服器同步的表單中添加附件(JEE上的AEM Forms) {#adding-annotations}

AEM Forms應用允許您將影像、潦草筆記和文本筆記附加到與AEM FormsJEE伺服器同步的窗體中。 如果從AEM Forms工作流伺服器載入表單，則會將附件添加到表單中。 您可以點擊附件按鈕 ![附件 — 應用](assets/attachments-app.png) 查看窗體中的所有附件。 紅色通知指定表單中的附件數。 如果表單中沒有附件，則看不到紅色通知按鈕。 如果表單中沒有附件，則按一下「附件」按鈕 ![攻擊](assets/attch.png)，您可以選擇附加照片或手寫。

您的選項包括：

* **庫**:允許您從設備上保存的圖片中添加圖片。

* **相機**:允許您拍攝圖片並將其添加到窗體中。

* **注釋**:用於添加文字框或文本注釋。 使用 ![潦草](assets/scribble.png) 添加畫框， ![鍵盤](assets/keyboard.png) 的子菜單。

>[!NOTE]
>
>一個用戶添加的附件對其他AEM Forms應用用戶可見。 其他用戶無法刪除用戶添加的附件。

### 「附件」螢幕 {#the-attachments-screen}

要查看某個位置中的所有附件，請點擊 ![附件 — 應用](assets/attachments-app.png)。 您可以在此處添加、更名和刪除附件。

![某個位置中的所有附件](assets/attachments-screen.png)

您可以使用 **+** 按鈕以附加另一個圖片、文字或文字。

### 添加照片 {#adding-a-photograph}

您可以使用移動設備的攝像頭或設備中保存的圖片來附加表單中的圖片。

1. 點擊附件按鈕 ![攻擊](assets/attch.png) 在窗口底部。
1. 點擊 **庫** 或 **相機** 在彈出窗口中。
1. 根據您選擇的選項，執行以下操作：

   1. 如果選擇 **相機**。

      拍張照片。 然後點擊 **使用** ![使用 — pic](assets/use-pic.png) 按鈕

      或點擊 **重取** ![重](assets/retake.png) 按鈕以重拍照片。

   1. 如果選擇 **庫**。

      設備的影像瀏覽器彈出。 在設備的圖片瀏覽器中，點擊要附加的圖片。

### 添加附註 {#adding-a-note}

的 **注釋** 選項，您可以在窗體中添加手繪指令碼和文本附件。

1. 點擊附件按鈕 ![攻擊](assets/attch.png) 在窗口底部。
1. 點擊 **注釋** 在彈出窗口中。
1. 在啟動的Notes用戶介面中，捕獲手繪圖。

   ![Scribble介面](assets/scribble-ui.png)

   斯克里布爾

   可以在Scribble介面中使用以下選項：

   * **清除**:清除螢幕。
   * **「完成」按鈕**:附加當前的塗抹。
   * **「取消」按鈕**:放棄當前指令碼並退出Scribble用戶介面。
   * ![鍵盤](assets/keyboard.png):清除塗鴉，並允許您添加文本注釋。

   ![AEM Forms應用程式Scribble中的鍵盤](assets/keyboard-inapp.png)

## 與AEM Forms伺服器同步的表單中的附件，但不帶AEM Forms工作流(OSGi上的AEM Forms) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

與AEM FormsOSGi伺服器同步的移動表單的附件與AEM FormsJEE伺服器類似。

從AEM FormsOSGi伺服器載入到應用程式中的自適應表單不支援表單級別附件。 要附加影像或文本注釋，請在建立表單時啟用欄位級附件。 將檔案附件元件從欄位上的元件瀏覽器中拖放。

在自適應表單中，可以查看記錄文檔(DoR)中的附加檔案。 看， [為非XFA自適應表單生成記錄文檔](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)。
