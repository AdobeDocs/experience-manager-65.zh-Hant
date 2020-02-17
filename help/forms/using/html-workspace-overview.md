---
title: 使用AEM Forms工作區
seo-title: 使用AEM Forms工作區
description: 透過此流程工作流程的快速概觀，開始使用AEM Forms工作區。
seo-description: 透過此流程工作流程的快速概觀，開始使用AEM Forms工作區。
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 使用AEM Forms工作區{#working-with-aem-forms-workspace}

## 簡介 {#introduction}

AEM Forms工作區是AEM Forms的一部分。 工作區除了PDF表格外，還可協助轉譯HTML表格。 現在，您可以從行動介面和網頁應用程式參與商業程式。

此外，AEM Forms工作區也可使用標準HTML和JavaScript™開發方法進行高度自訂。 它是以元件為基礎的軟體，可輕鬆與您的其他Web應用程式整合。

如需詳細資訊，請參 [閱「AEM Forms工作區簡介」](/help/forms/using/introduction-html-workspace.md)。

## 熟悉 {#getting-familiar}

若要熟悉建立表單應用程式以自動化業務流程的端對端程式，請遵循逐步說明。 您可以使用Workbench、Designer和AEM Forms工作區，在進行逐步解說後建立、管理和測試應用程式。 如需實作詳細資訊，請 [參閱「建立您的第一個AEM Forms應用程式」](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)。

## 功能概述 {#functional-overview}

您可以使用AEM Forms工作區來執行下列工作：

**** 啟動業務流程：AEM Forms工作區可依您組織所設計和設定的程式分類。 您可以將常用類別設為我的最愛，以快速存取類別。 當您啟動流程時，通常會填寫表單，以啟動表單工作流程控制的業務流程。 如需詳細資訊，請參 [閱啟動程式](/help/forms/using/starting-processes.md)。

**** 檢視並處理工作：當您查看待辦事項清單時，您會看到業務流程中分配給您的任務，或者您所屬的任何組的任務，或者您是其他用戶的共用任務。 您可以視需要開啟、處理和完成工作。 通常，完成工作需要提供資訊、核准表格或拒絕表格。 如需詳細資訊，請 [參閱使用待辦事項清單](/help/forms/using/todo-lists.md)。

**追蹤工作**:若要追蹤您的工作，請使用AEM Forms工作區的「追蹤」標籤。 您可以搜尋您啟動或參與的作用中或已完成的程式。 您可以檢視屬於流程一部分的工作、指派和表單。 您也可以使用先前啟動之程式的表單資料來啟動新程式。 如需詳細資訊，請參閱 [追蹤程式](/help/forms/using/tracking-processes.md)。

## AEM Forms工作區的全新方案 {#new-offering-of-aem-forms-workspace}

**支援大量核准工作**:

您可以核准同一類型的多個工作。 在選擇一個要批准的任務後，將只啟用具有相同進程、具有相同任務名稱和相同路由選項的任務。 如需 [實作詳細資訊，請參閱使用待辦事項清單](/help/forms/using/todo-lists.md) 。

## 從Flex Workspace移轉至AEM Forms工作區 {#migrating-from-flex-workspace-to-aem-forms-workspace}

AEM Forms客戶不支援Flex Workspace。 所有使用Flex Workspace的客戶都應移至AEM Forms Workspace。

在AEM Forms工作區中，預設的演算和送出服務（在預設動作設定檔中）與XDP表單關聯已變更，並已引入新服務。 如需詳細資訊，請 [參閱「新增演算和送出服務」](/help/forms/using/new-render-submit-service.md)。 若要移轉與XDP表單搭配運作的現有程式，若要使用這些服務，您可以遵循下 [列步驟](/help/forms/using/new-render-submit-service.md#main-pars-faq)。

**將Flex工作區自訂與AEM Forms工作區對應**

這兩個工作區中各種類型的定製之間的映射如下。

<table>
 <tbody>
  <tr>
   <td><strong>自訂類型 </strong></td>
   <td><strong>涵蓋的自訂 </strong></td>
   <td><strong>對應的AEM Forms工作區自訂藍本</strong></td>
  </tr>
  <tr>
   <td>本地化自訂</td>
   <td>
    <ol>
     <li>變更工作區的地區設定</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">變更AEM Forms工作區地區設定</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>主題自訂</td>
   <td>
    <ol>
     <li>取代影像</li>
     <li>修改顏色</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">變更組織標誌</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">變更色彩配置</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>版面自訂</td>
   <td>
    <ol>
     <li>簡化工作區使用者介面<br /> </li>
     <li>建立新的登入畫面</li>
     <li>建立自訂核准容器</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">使用可重複使用的元件</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">建立新的登入畫面</a></li>
     <li>不建議使用「核准容器」。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

AEM Forms工作區中未提供的Flex Workspace功能包括：訊息與通知、歡迎頁面、核准容器，以及管理欄標題的選項。 如需完整清單，請參 [閱「AEM Forms工作區中不提供的Flex Workspace功能」](/help/forms/using/features-flex-workspace-available-html.md)。

## 使用AEM Forms工作區進行開發 {#developing-with-aem-forms-workspace}

### 建築 {#architecture}

AEM Forms工作區是以HTML和JavaScript™為基礎的網頁應用程式，代管於CRX™。 當在瀏覽器中開啟Workspace URL時，會存取CRX™資源，並在瀏覽器中將應用程式轉譯為HTML頁面。 JavaScript程式庫和自訂JavaScript程式碼可管理應用程式的內部和外部行為，例如使用者介面、使用者互動以及與AEM Forms伺服器的通訊。 如需詳細資訊，請參閱「AEM Forms工作區 [架構](/help/forms/using/html-workspace-architecture.md)」。

### AEM Forms工作區自訂 {#aem-forms-workspace-customization}

AEM Forms工作區支援多種自訂設定，以更新使用者介面的版面、外觀、功能等。 這些定制包括更新以下一個或多個內容：

* 使用者介面的外觀
* 使用語義定製的功能
* 在其他網頁應用程式中重複使用HTML元件

自訂 [文章](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-0) 會說明此類自訂的類型。

### 設定開發人員環境 {#set-up-the-developer-environment}

AEM Forms工作區交付項目包括部署在CRX上的CRX套件、包含完整原始碼的SDK封存、協力廠商JavaScript程式庫，以及建立AEM Forms工作區的指令碼。 使用這些設定來設定開發人員環境，以執行上述自訂設定。 如需詳細資訊，請參 [閱「建立AEM Forms工作區程式碼](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)」。

您可以自訂介面和核心功能的主要部分，例如字型、色彩配置、標誌、登入畫面、錯誤對話、與協力廠商應用程式整合，以及在協力廠商應用程式中重複使用元件。 您也可以增強「任務摘要」頁面上顯示的內容、顯示任務路由動作的影像，甚至修改建立AEM Forms工作區應用程式的低階骨幹模型和檢視。

### XDP表單的HTML轉換 {#html-rendering-of-xdp-forms}

依預設，在新程式中，XDP表格會在桌上型電腦上以PDF格式呈現，在平板電腦上則以HTML格式呈現。 您可以永遠以HTML格式來轉換XDP表格。 如需詳細資訊，請 [參閱「新增演算和送出服務」](/help/forms/using/new-render-submit-service.md)。

[Mobile Forms](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) (適用於描述檔 [)功能](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)，可啟用XDP表單的HTML轉譯。 依預設，「演算新HTML表單」會使用您可 `default.html` 以變更的描述檔。 您也可以新增在以HTML格式轉譯XDP表單之前發生的自訂變更。

## AEM Forms工作區應用程式 {#aem-forms-workspace-app}

若要在行動裝置上處理您的商業程式，您可以使用AEM Forms的AEM Forms工作區應用程式方案。 如需詳細資訊，請參閱「 [AEM Forms工作區應用程式總覽」](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
