---
title: AEM Forms工作區快速入門
seo-title: Getting started with AEM Forms workspace
description: 如何開始使用LiveCycleAEM Forms工作區來管理您的業務自動化流程。
seo-description: How to get started with using the LiveCycle AEM Forms workspace to manage your business automation processes.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# AEM Forms工作區快速入門 {#getting-started-with-aem-forms-workspace}

您可以使用AEM Forms工作區來執行下列工作：

* 啟動業務流程
* 查看分配給您的任務或您有權訪問的其他待辦事項清單
* 跟蹤您啟動或參與的流程中的任務

## 導覽AEM Forms工作區 {#navigating-html-workspace}

AEM Forms工作區使用者介面中會顯示不同項目，端視您所處理的程式和任務而定。 您可能會/不會看到「摘要」、「Forms」、「詳細資訊」、「歷史記錄」、「附件」或「附註」頁簽，或者所有在本「幫助」中描述的按鈕。

您可以使用下列任一方法，導覽AEM Forms工作區主要使用者介面：

* 按一下頂端導覽列中的項目以存取「開始程式」、「待辦事項」清單、「偏好設定」、「追蹤」、「說明」和「登出」選項。
* 按一下「開始流程」、「待辦事項」或「追蹤」標籤，以存取三個主要工作區。
* 在「開始進程」、「待辦事項」和「跟蹤」頁簽上，按一下左側面板清單中的項，以訪問收藏夾、進程類別、搜索模板、草稿或分配的任務。 使用捲軸可查看清單中的其他項目。
* 所有操作按鈕（批准、拒絕、轉發、協商、鎖定和共用）均顯示在文檔和所有權中。
* 按一下導航欄中位於頁面底部的「所有選項」表徵圖，將任務轉發給其他用戶、與其他用戶共用任務、與其他用戶協商任務或鎖定任務。
* 在「歷史記錄」頁簽上，選擇一個任務以顯示該任務的「附件」和「分配」頁簽。
* 使用Tab鍵、方向鍵和空格鍵，即可在AEM Forms工作區中導覽，而不需使用滑鼠。

## 搭配螢幕助讀程式使用AEM Forms工作區 {#using-html-workspace-with-screen-readers}

AEM Forms工作區是網頁型HTML應用程式，與螢幕助讀程式相容。 您可以使用鍵盤導覽AEM Forms工作區介面。

若要搭配螢幕助讀程式使用AEM Forms工作區，請記住以下幾點：

* AEM Forms工作區是符合任何標準螢幕助讀程式工具的標準HTML應用程式。 運行螢幕助讀程式工具不需要任何特定指令碼。
* AEM Forms工作區中的所有導覽都是透過錨點標籤，您可透過索引標籤輕鬆存取。
* Forms可能需要幾秒鐘的時間才能載入。 螢幕助讀程式無法聽見通知您表單已載入，您必須等候。

## 使用鍵盤導覽AEM Forms工作區 {#navigating-html-workspace-using-a-keyboard}

使用鍵盤導覽AEM Forms工作區時，導覽會符合HTML協助工具慣例。 在某些情況下，Tab鍵順序不遵循典型的常規順序。 下列提示可協助您導覽介面：

* 如果在瀏覽器頂部的工具欄外出現Tab鍵問題，請按Ctrl+Tab鍵以在瀏覽器窗口的內容中定位。
* AEM Forms工作區說明會在個別的瀏覽器視窗中開啟。 檢視說明後，焦點會回到包含AEM Forms工作區的瀏覽器視窗。 當焦點返回時，「幫助」菜單將保持焦點。
* 當您開啟表單以開始處理或完成工作時，焦點會保留在現有元素中，不會變更為表單。 使用頁簽將焦點移動到表單中並瀏覽。 在表單中切換順序取決於表單的類型和設計。

   若為PDF forms，當您點選至表單結尾或提交表單時，游標焦點會跳至瀏覽器位址列。 您必須再次在功能表（但不是整個表單）中勾選索引標籤，才能移至表單動作按鈕，例如「另存新檔」和「完成」。 如果表單仍處於開啟狀態，您也可以在按鈕之前定位並返回表單。

## 管理偏好設定 {#managing-preferences}

您可以透過下列類別來設定各種AEM Forms工作區偏好設定：

**外出：** 設定首選項以控制如何在您外出時將任務分配給其他人。 請參閱 [設定外出首選項](todo-lists.md#setting-out-of-office-preferences).

**隊列：** 設定與其他用戶共用待辦事項清單或請求訪問其他用戶清單的首選項。 請參閱 [從組和共用隊列處理任務](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**UI設定：** 設定您與AEM Forms工作區互動的偏好設定。 請參閱 [設定用戶介面首選項](#set-user-interface-preferences).

### 設定用戶介面首選項 {#set-user-interface-preferences}

在「首選項> UI設定」標籤中設定用戶介面首選項。 可使用下列偏好設定。

* **開始位置：** 指定登入AEM Forms工作區時顯示的頁面。 四個可用選項是「開始程式」、「待辦事項」、「追蹤」和「我的最愛」。
* **註銷提示：** 指定在按一下「註銷」後，是否提示您確認要註銷。
* **日期格式：** 指定在AEM Forms工作區中使用的日期顯示格式。
* **時間格式**:指定在AEM Forms工作區中使用的時間顯示格式。
* **通過電子郵件通知任務事件：** 指定您是否收到任務事件的電子郵件通知，包括「待辦事項」清單和您所屬的組「待辦事項」清單中的任務的任務分配、提醒和截止時間。
* **在電子郵件中附加Forms:** 指定表單副本是否附加至電子郵件通知訊息。 僅PDF和XDP表單支援附件。
* **定期保存草稿：** 指定是否定期自動保存表單草稿。 若要定期儲存草稿，請啟用此選項，並將自動儲存持續時間從1分鐘設為30分鐘。 啟用自動儲存且使用者正在處理草稿時，草稿會在指定的分鐘數後定期儲存。 僅當草稿自上次儲存或自動儲存後發生變更時，才會自動儲存草稿。 儲存草稿時，畫面上會顯示警報訊息。
