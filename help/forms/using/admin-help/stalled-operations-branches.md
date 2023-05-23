---
title: 處理停止的操作和分支
seo-title: Working with stalled operations and branches
description: 「停止的操作」頁和「停止的分支」頁顯示已停止的進程。
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

# 處理停止的操作和分支 {#working-with-stalled-operations-and-branches}

「停止的操作」頁和「停止的分支」頁顯示已停止的進程。 當在執行操作期間或之後或由於進程中蓄意停止操作而出現錯誤時，進程可能會停止：

* 由於意外錯誤，操作可能會停止。 但是，進程中的「停止分支」操作會故意阻止進程進一步運行，並要求管理員進行干預。
* 在規則評估期間，分支可以在操作之間停止。

當進程停止時，在問題解決並重新啟動操作或分支之前，不會運行其他操作。

對於每個停止的項目，清單顯示以下資訊：

**操作名稱或分支名稱：** 操作或分支的名稱。

**狀態：** 對於已停止的項目，始終STALT。

**錯誤：** 問題的簡短描述。

**進程ID:** 在流程實例化時（即當用戶或自動步驟啟動流程時），工作流所分配的正整數。 您可以使用此標識符跟蹤進程實例的生命週期。

**進程名稱 — 版本：** 在Workbench中分配的流程的名稱。

**停止日期：** 操作或分支停止的日期和時間。

可以在「停止的操作」或「停止的分支」頁上執行以下任務：

* 選擇一個錯誤以查看有關它的詳細資訊。 選擇錯誤後，將顯示「錯誤詳細資訊」頁。
* 終止或重試停止的操作或重試停止的分支。

## 終止或重試停止的操作或分支 {#terminating-or-retrying-stalled-operations-or-branches}

在「停止的操作」(Stalted Operations)頁上，可以終止顯示的進程實例。

終止進程實例時，該實例將停止運行，並且不再執行其他操作。 通常，僅當進程因錯誤而被阻止或無法使用且無法修復和重新啟動時，才終止該進程。

在「停止的操作」頁或「停止的分支」頁上，可以重試該操作或分支。

當您重試操作時，會向Forms工作流發送請求以重新啟動該操作。 如果導致進程停止的錯誤已修復且重試請求成功，則進程從其停止的點開始再次運行，其狀態將更改為「正在運行」。 如果無法重新啟動該操作，則該操作將保持STALTED狀態，您可能需要終止它。

### 終止停止的操作 {#terminate-a-stalled-operation}

1. 在管理控制台中，按一下「服務」>「表單工作流」>「停止的操作錯誤」。
1. 在「停止的操作」頁上，選擇要終止的項，然後按一下終止。

### 重試停止的操作或分支 {#retry-a-stalled-operation-or-branch}

1. 在管理控制台中，按一下「服務」>「表單」工作流，然後按一下「停止的操作錯誤」或「停止的分支錯誤」。
1. 在「停止的操作」或「停止的分支」頁上，選擇要重試的項，然後按一下「重試」。

## 查看有關停止操作或分支的錯誤詳細資訊 {#viewing-error-details-about-stalled-operations-or-branches}

如果從「停止的操作」或「停止的分支」頁上的停止項清單中選擇錯誤，則將顯示「錯誤詳細資訊」頁，其中顯示有關有助於解決問題的錯誤的詳細資訊。

頁面底部的框包含錯誤資訊。

您還可以從「錯誤詳細資訊」頁終止或重試停止的操作，並重試停止的分支。

## 當升級用戶不存在時，進程不會停止 {#process-does-not-stall-when-escalation-user-does-not-exist}

當將表單用戶服務中的分配任務操作配置為在特定時間段後將任務升級給其他用戶，並且在分配任務操作執行後但在升級發生之前刪除升級用戶時，將發生錯誤。

出現這種情況時，流程和任務的狀態在配置的升級時間不會更改，並且升級不會發生，但流程不會停止。 伺服器日誌中顯示以下消息：

&quot;為升級指定的主體對taskID無效： *數*，已指定隊列： *數*&quot;

如果在生成任務之前（在「分配任務」操作執行之前）刪除升級用戶，則進程將停止或引發InvalidPrincipal異常事件。

為防止此問題，在刪除用戶時，請搜索屬於該用戶的任務並相應地處理它們。 (請參閱 [處理任務](/help/forms/using/admin-help/tasks.md#working-with-tasks)。)
