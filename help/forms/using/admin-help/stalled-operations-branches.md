---
title: 處理操作和分支停頓
seo-title: Working with stalled operations and branches
description: 「已停止的操作」頁和「已停止的分支」頁顯示已停止的進程。
seo-description: The Stalled Operations page and the Stalled Branches page show the processes that have stalled.
uuid: 5f6202b0-79c2-4c3c-847a-236c0366e60b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8c2567f3-7220-436a-b9f2-2824a98c1ccc
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 處理操作和分支停頓 {#working-with-stalled-operations-and-branches}

「已停止的操作」頁和「已停止的分支」頁顯示已停止的進程。 當執行操作期間或之後發生錯誤，或由於過程中蓄意停頓操作而發生錯誤時，過程可能會停頓：

* 由於未預見的錯誤，操作可能會停止。 但是，進程中的「停頓分支」操作會故意阻止進程進一步運行，並要求管理員進行干預。
* 在評估規則期間，分支可能會停頓於操作之間。

當進程停止時，除非問題得到解決，並且操作或分支重新啟動，否則不會運行其他操作。

對於每個逾時的項目，清單會顯示下列資訊：

**操作名稱或分支名稱：** 操作或分支的名稱。

**狀態：** 對於已停頓的項目，一律停止。

**錯誤：** 問題的簡短說明。

**進程ID:** 當進程實例化時（即當用戶或自動步驟啟動進程時），形成工作流的正整數分配。 您可以使用此標識符跟蹤進程實例的整個生命週期。

**進程名稱 — 版本：** 在Workbench中指派的程式名稱。

**中止日期：** 操作或分支停止的日期和時間。

您可以在「已停止的操作」或「已停止的分支」頁面上執行下列工作：

* 選取錯誤以檢視其詳細資訊。 選擇錯誤時，將顯示「錯誤詳細資訊」頁。
* 終止或重試已中止的操作或重試已中止的分支。

## 終止或重試已停止的操作或分支 {#terminating-or-retrying-stalled-operations-or-branches}

在「停止的操作」頁上，您可以終止顯示的進程實例。

當您終止進程實例時，該實例將停止運行，並且不會執行任何進一步操作。 通常，僅當進程因錯誤而被阻止或無法使用且無法修復和重新啟動時才終止進程。

在「已停止的操作」頁或「已停止的分支」頁上，可以重試操作或分支。

當您重試操作時，會傳送Forms工作流程以請求重新啟動操作。 如果導致進程停頓的錯誤已經修正，並且重試請求成功，則進程從其停止的點開始再次運行，並且其狀態更改為「正在運行」。 如果無法重新啟動操作，操作將保持停止，您可能需要終止操作。

### 終止停止的操作 {#terminate-a-stalled-operation}

1. 在管理控制台中，按一下「服務>表單工作流程>操作逾時錯誤」。
1. 在「停止的操作」頁上，選擇要終止的項，然後按一下終止。

### 重試已中止的操作或分支 {#retry-a-stalled-operation-or-branch}

1. 在管理控制台中，按一下「服務」>「表單工作流程」，然後按一下「操作逾時」或「分支錯誤逾時」。
1. 在「已停止的操作」或「已停止的分支」頁上，選擇要重試的項目，然後按一下「重試」。

## 查看有關已停止操作或分支的錯誤詳細資訊 {#viewing-error-details-about-stalled-operations-or-branches}

如果從「已停止的操作」或「已停止的分支」頁面上的已停止項目清單中選擇錯誤，則會出現「錯誤詳細資訊」頁面，其中顯示有關錯誤的詳細資訊，可幫助您排解問題。

頁面底部的方塊包含錯誤資訊。

您也可以從「錯誤詳細資訊」頁終止或重試已停止的操作，並重試已停止的分支。

## 呈報使用者不存在時，程式不會停頓 {#process-does-not-stall-when-escalation-user-does-not-exist}

當在AEM Forms User Service中配置分配任務操作以在特定時段後將任務呈報給其他用戶，並且在分配任務操作執行之後但在升級發生之前刪除升級用戶時，將發生錯誤。

發生此情況時，進程和任務的狀態在配置的升級時間不會更改，升級不會發生，但進程不會停止。 伺服器日誌中顯示以下消息：

&quot;為升級指定的主體對taskID無效： *數字*，指定佇列： *數字*.&quot;

如果在生成任務之前（在「分配任務」操作執行之前）刪除了升級用戶，則進程會中止或引發InvalidPrincipal異常事件。

為避免此問題，在刪除用戶時，請搜索屬於該用戶的任務並相應處理這些任務。 (請參閱 [使用任務](/help/forms/using/admin-help/tasks.md#working-with-tasks).)
