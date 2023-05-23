---
title: 使用AEM Forms工作區
seo-title: Working with AEM Forms workspace
description: 通過此流程工作流的快速概述，開始使用AEM Forms工作區。
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 0%

---

# 使用AEM Forms工作區{#working-with-aem-forms-workspace}

## 簡介 {#introduction}

AEM Forms工作區是AEM Forms的一部分。 Workspace可方便HTMLForms和PDF forms的再現。 現在，您可以從移動介面和Web應用程式中參與業務流程。

此外，AEM Forms工作區可使用標準HTML和JavaScript™開發方法進行高度定制。 它是基於元件的軟體，可輕鬆與您的其他Web應用程式整合。

有關詳細資訊，請參見 [AEM Forms工作區簡介](/help/forms/using/introduction-html-workspace.md)。

## 熟悉 {#getting-familiar}

要熟悉建立表單應用程式以自動化業務流程的端到端流程，請遵循步驟。 在完成步驟後，您可以使用Workbench、Designer和AEM Forms工作區建立、管理和test應用程式。 有關實施的詳細資訊，請參見 [建立第一個AEM Forms應用程式](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)。

## 功能概述 {#functional-overview}

可以使用AEM Forms工作區執行以下任務：

**啟動業務流程：** AEM Forms工作區按您的組織設計和設定的流程分類。 您可以收藏常用類別，以快速訪問類別。 在啟動流程時，通常會填寫表單以啟動工作流控制的業務流程。 有關詳細資訊，請參見 [啟動進程](/help/forms/using/starting-processes.md)。

**查看任務並對其執行操作：** 查看待辦事項清單時，您會看到業務流程中分配給您的任務，或您所屬的任何組的任務，或是其他用戶的共用任務。 您可以根據需要開啟、處理和完成任務。 通常，完成任務涉及提供資訊、批准表單或拒絕表單。 有關詳細資訊，請參見 [使用待辦事項清單](/help/forms/using/todo-lists.md)。

**跟蹤任務**:要跟蹤任務，請使用AEM Forms工作區的「跟蹤」頁籤。 您可以搜索您啟動或參與的活動或已完成進程。 您可以查看作為流程一部分的任務、分配和表單。 您還可以使用先前啟動的流程中的表單資料啟動新流程。 有關詳細資訊，請參見 [跟蹤進程](/help/forms/using/tracking-processes.md)。

## AEM Forms工作區新產品 {#new-offering-of-aem-forms-workspace}

**支援批量審批任務**:

您可以批准同一類型的多個任務。 選擇一個任務進行審批後，將只啟用具有相同進程、相同任務名稱和相同路由選項的任務。 請參閱 [使用待辦事項清單](/help/forms/using/todo-lists.md) 以獲取實施詳細資訊。

## 從Flex工作區遷移到AEM Forms工作區 {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex工作區不支援AEM Forms客戶。 所有使用Flex工作區的客戶都應移至AEM Forms工作區。

在AEM Forms工作區中，與XDP表單關聯的預設呈現和提交服務在預設操作配置檔案中已更改，並引入了新服務。 有關詳細資訊，請參閱 [新建呈現和提交服務](/help/forms/using/new-render-submit-service.md)。 要遷移與XDP表單配合使用的現有流程，要利用這些服務，您可以遵循 [這些步驟](new-render-submit-service.md)。

**將Flex工作區自定義項與AEM Forms工作區映射**

兩個工作區中各種類型的自定義之間的映射如下所示。

<table>
 <tbody>
  <tr>
   <td><strong>自定義類型 </strong></td>
   <td><strong>包含的自定義 </strong></td>
   <td><strong>相應的AEM Forms工作區自定義方案</strong></td>
  </tr>
  <tr>
   <td>本地化定製</td>
   <td>
    <ol>
     <li>更改工作區的區域設定</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">更改AEM Forms工作區區域設定</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>主題自定義</td>
   <td>
    <ol>
     <li>替換影像</li>
     <li>修改顏色</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">更改組織徽標</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">更改配色方案</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>佈局自定義</td>
   <td>
    <ol>
     <li>簡化工作區用戶介面<br /> </li>
     <li>建立新登錄螢幕</li>
     <li>建立自定義批准容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重用元件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">建立新的登錄螢幕</a></li>
     <li>不建議使用批准容器。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

在Flex工作區中不可用的AEM Forms工作區的某些功能包括：消息和通知、歡迎頁、批准容器和用於管理列標題的選項。 有關完整清單，請參見 [Flex工作區功能在AEM Forms工作區中不可用](/help/forms/using/features-flex-workspace-available-html.md)。

## 使用AEM Forms工作區開發 {#developing-with-aem-forms-workspace}

### 架構 {#architecture}

AEM Forms工作區是基於HTML和JavaScript™的Web應用程式，托管在CRX™上。 在瀏覽器中開啟Workspace URL時，會訪問CRX™資源，並在瀏覽器中將應用程式呈現為HTML頁。 JavaScript庫和自定義JavaScript代碼管理應用程式的內部和外部行為，如用戶介面、用戶交互以及與AEM Forms伺服器的通信。 有關詳細資訊，請參閱AEM Forms工作區 [體系結構](/help/forms/using/html-workspace-architecture.md)。

### AEM Forms工作區定制 {#aem-forms-workspace-customization}

AEM Forms工作區支援多種自定義以更新用戶介面的佈局、外觀、功能等。 這些自定義涉及更新以下一個或多個內容：

* 用戶介面的外觀
* 使用語義自定義功能
* 在其他Web應用程式中重新使用HTML元件

的 [定制](introduction-customizing-html-workspace.md#types-of-customizations) 文章將介紹此類自定義的類型。

### 設定開發人員環境 {#set-up-the-developer-environment}

AEM Forms工作區交付項包括部署在CRX上的CRX包、包含完整原始碼的SDK存檔、第三方JavaScript庫和AEM Forms工作區的生成指令碼。 使用這些設定可設定開發人員環境以執行上述自定義。 有關詳細資訊，請參閱 [正在生成AEM Forms工作區代碼](introduction-customizing-html-workspace.md#building-html-workspace-code)。

您可以自定義介面和核心功能的主要部分，如字型、配色方案、徽標、登錄螢幕、錯誤對話框、與第三方應用程式的整合，以及在第三方應用程式中重新使用元件。 您還可以增強「任務摘要」頁面上顯示的內容，顯示任務路由操作的影像，甚至修改建立AEM Forms工作區應用程式的低級主幹模型和視圖。

### XDPForms的HTML渲染 {#html-rendering-of-xdp-forms}

預設情況下，對於新進程，XDP表單以案頭上的PDF格式和平板電腦上的HTML格式呈現。 可以始終以HTML格式呈現XDP表單。 有關詳細資訊，請參閱 [新建呈現和提交服務](/help/forms/using/new-render-submit-service.md)。

[移動Forms](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 功能， [配置檔案](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)，啟用XDP表單的HTML格式副本。 預設情況下，「渲染新HTML表單」使用 `default.html` 資料，你可以更改。 您還可以添加在以HTML格式呈現XDP表單之前發生的自定義更改。

## AEM Forms工作區 {#aem-forms-workspace-app}

要在移動設備上處理業務流程，可以使用AEM Forms工作區應用程式AEM Forms。 有關詳細資訊，請參見 [AEM Forms工作區應用概述](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)。
