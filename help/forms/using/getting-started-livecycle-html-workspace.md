---
title: AEM Forms工作區入門
seo-title: Getting started with AEM Forms workspace
description: 如何開始使用LiveCycleAEM Forms工作區來管理業務自動化流程。
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

# AEM Forms工作區入門 {#getting-started-with-aem-forms-workspace}

可以使用AEM Forms工作區執行以下任務：

* 啟動業務流程
* 查看分配給您或您有權訪問的其它待辦事項清單的任務，並對其執行操作
* 跟蹤您啟動或參與的流程的一部分任務

## 導航AEM Forms工作區 {#navigating-html-workspace}

AEM Forms工作區用戶介面中的不同項目將根據您正在處理的流程和任務顯示。 您可能看不到「摘要」、「Forms」、「詳細資訊」、「歷史記錄」、「附件」或「附註」頁籤，或者所有在本幫助中描述的按鈕。

可以使用以下任何方法瀏覽AEM Forms主工作區用戶介面：

* 按一下頂部導航欄中的項以訪問「開始流程」、「待辦事項」清單、「首選項」、「跟蹤」、「幫助」和「註銷」選項。
* 按一下「開始進程」(Start Process)、「待辦事項」(To-do)或「跟蹤」(Tracking)頁籤，訪問三個主要工作區。
* 在「開始流程」、「待辦事項」和「跟蹤」頁籤上，按一下左面板清單中的項，以訪問收藏夾、流程類別、搜索模板、草稿或分配的任務。 使用捲動條查看清單中的其他項。
* 所有操作按鈕（批准、拒絕、轉發、咨詢、鎖定和共用）都顯示在文檔和所有權中。
* 按一下頁面底部導航欄中的「所有選項」表徵圖，將任務轉發給其他用戶，與其他用戶共用任務，與其他用戶協商任務，或鎖定任務。
* 在「歷史記錄」頁籤上，選擇一個任務以顯示該任務的「附件」和「工作總攬」頁籤。
* 使用Tab鍵、箭頭鍵和空格鍵在AEM Forms工作區中導航，而不使用滑鼠。

## 使用AEM Forms工作區和螢幕閱讀器 {#using-html-workspace-with-screen-readers}

AEM Forms工作區是基於Web的HTML應用程式，與螢幕閱讀器相容。 可使用鍵盤在AEM Forms工作區介面中導航。

要將AEM Forms工作區與螢幕閱讀器一起使用，請記住以下幾點：

* AEM Forms工作區是符合任何標準螢幕閱讀器工具的標準HTML應用程式。 運行螢幕閱讀器工具不需要任何特定的指令碼。
* AEM Forms工作區中的所有導航都通過錨點標籤進行，這些標籤可以通過頁籤輕鬆訪問。
* Forms需要幾秒鐘才能裝載。 螢幕閱讀器無法聽到表單正在載入，您必須等待。

## 使用鍵盤導航AEM Forms工作區 {#navigating-html-workspace-using-a-keyboard}

使用鍵盤導航AEM Forms工作區時，導航符合HTML輔助功能約定。 在某些情況下，Tabbing命令不遵循典型的常規順序。 以下提示可幫助您導航介面：

* 如果在瀏覽器頂部的工具欄外的標籤上出現問題，請按Ctrl+Tab鍵以在瀏覽器窗口的內容中制表。
* AEM Forms工作區「幫助」(Help)將在單獨的瀏覽器窗口中開啟。 查看「幫助」後，焦點將返回包含AEM Forms工作區的瀏覽器窗口。 當焦點返回時，「幫助」菜單仍然聚焦。
* 當您開啟表單以啟動流程或完成任務時，焦點將保留在現有元素中，不會更改為表單。 使用頁籤將焦點移到窗體並瀏覽。 在表單中按順序排列取決於表單的類型和設計。

   對於PDF forms，當您制表到表單末尾或提交表單時，游標焦點會跳轉到瀏覽器地址欄。 必須再次在菜單中開啟標籤（但不是整個表單），才能轉到表單操作按鈕，如「另存為草稿」和「完成」。 如果表單仍然開啟，您還可以在按鈕之後制表並返回表單。

## 管理首選項 {#managing-preferences}

可以在以下類別中設定各種AEM Forms工作區首選項：

**外出：** 設定首選項以控制在您外出時如何將任務分配給其他人。 請參閱 [設定外出首選項](todo-lists.md#setting-out-of-office-preferences)。

**隊列：** 設定首選項，以便與其他用戶共用待辦事項清單或請求訪問其他用戶的清單。 請參閱 [處理來自組和共用隊列的任務](todo-lists.md#working-with-tasks-from-group-and-shared-queues)。

**UI設定：** 設定與AEM Forms工作區交互方式的首選項。 請參閱 [設定用戶介面首選項](#set-user-interface-preferences)。

### 設定用戶介面首選項 {#set-user-interface-preferences}

在「首選項」>「UI設定」頁籤中設定用戶介面首選項。 以下首選項可用。

* **起始位置：** 指定登錄到AEM Forms工作區時顯示的頁面。 可用的四個選項是「啟動流程」、「待辦事項」、「跟蹤」和「收藏夾」。
* **註銷提示：** 指定在按一下「註銷」後是否提示您確認要註銷。
* **日期格式：** 指定在AEM Forms工作區中使用的日期顯示格式。
* **時間格式**:指定在AEM Forms工作區中使用的時間顯示格式。
* **通過電子郵件通知任務事件：** 指定您是否收到任務事件的電子郵件通知，包括任務分配、提醒和任務的截止時間，這些任務位於您的待辦事項清單和您所屬的組待辦事項清單中。
* **以電子郵件方式附加Forms:** 指定表單的副本是否附加到電子郵件通知消息。 僅支援PDF和XDP表單的附件。
* **定期保存草稿：** 指定是否定期自動保存表單草稿。 要定期保存草稿，請啟用此選項，並將自動保存持續時間設定為1到30分鐘。 啟用自動保存後，當用戶正在處理草稿時，草稿將在指定的分鐘數後定期保存。 僅當自上次保存或自動保存後草圖發生更改時，草圖才自動保存。 保存草稿後，螢幕上將顯示一條警報消息。
