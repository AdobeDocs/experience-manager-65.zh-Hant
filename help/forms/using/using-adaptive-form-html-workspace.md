---
title: 在HTML Workspace中使用最適化表單
description: 瞭解如何在HTML Workspace中使用最適化表單，讓現場工作人員存取其裝置上的表單。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# 在HTML Workspace中使用最適化表單{#using-an-adaptive-form-in-html-workspace}

JEE上的AEM Forms提供在HTML Workspace中使用最適化表單的功能。

由於可以在流程設計期間選擇XDP，因此新增了從現有的最適化表單AEM存放庫瀏覽的功能。 此功能可讓流程設計人員在「起點」和「工作」中設定最適化表單。

## 流程設計體驗 {#process-design-experience}

執行以下動作來啟用流程設計中要使用的調適型表單：

* 在指派任務和起點中，將表單資產指派給任務時，您可以瀏覽至CRX存放庫中的最適化表單資產。
* 在「指派工作/起點維護作業」特性表中，您可以隱藏最適化表單的頂層/全域工具列。
* 您可以在適用性表單中使用新的動作設定檔來呈現和提交動作。

### LiveCycle應用程式匯出和匯入 {#livecycle-application-export-and-import}

由於調適型表單位於AEM存放庫中，因此LiveCycle應用程式匯出僅包含所用調適型表單的參考。 因此，匯出和匯入LiveCycle應用程式是兩個步驟的過程。 LiveCycle應用程式包括流程定義等。 包含調適型表單的個別套件會從AEM匯出為ZIP檔案。 匯入時，LiveCycle應用程式會透過Workbench匯入，而適用性表單會透過AEM匯入。

## HTML Workspace中最適化表單的使用者體驗 {#user-experience-of-adaptive-form-in-html-workspace}

除了行動表單可用的控制項外，HTML Workspace還提供一些最適化表單專用控制項。 當使用者開啟「任務」或「起點」時，使用者可以在HTML工作區中新增附件、儲存、簽署、提交和導覽最適化表單。 具體內容如下：

1. 若要附加檔案，請使用「工作」附件，如行動Forms中的情況。 最適化表單的任何檔案附件型別按鈕都會隱藏。

1. 若要儲存最適化表單，請按一下 **儲存**，行動版Forms即是如此。 最適化表單的任何「儲存型別」按鈕都會隱藏。

1. 若要提交最適化表單，請使用 **提交** 按鈕或路由動作可使用，就像行動Forms中的情況。 最適化表單的任何提交型別按鈕都會隱藏。

1. **最適化表單全域工具列可見性**：如果Process Designer隱藏全域/最上層工具列，工具列和按鈕不會顯示在調適型表單上。

1. **最適化Forms的工作區導覽控制項**：下一頁/上一頁按鈕與HTML Workspace中適用性表單的儲存、提交和路由動作按鈕一起提供。 按一下「下一步/上一個」按鈕，即可在HTML Workspace中導覽最適化表單的面板。 「下一個/上一個」按鈕提供深層導覽，類似於最適化表單之「行動」檢視中的導覽控制項。

1. **Adaptive Form的eSign Services和摘要元件**：摘要元件在HTML Workspace中無法運作。 換言之，如果最適化表單有摘要元件，則不會在工作區中顯示。 工作區使用者按一下HTML Workspace中的提交或路由動作，而不是電子簽章元件中的自動提交。 檔案簽署後，會顯示為平面簽署的檔案。 按一下 **提交** 或路由動作，讓您能夠關閉/完成任務或「起點」。\
   已簽署的檔案會從eSign服務伺服器收集，而資料xml檔案會轉送至程式中的下一個步驟。

## 在流程設計中使用調適型表單的步驟 {#steps-to-use-adaptive-forms-in-process-design}

1. 開啟Adobe Experience Manager Forms Workbench。

1. 前往 **檔案>新增>應用程式** 或使用現有的應用程式來建立應用程式。

   ![建立新的應用程式](assets/create_new_appl.png)

   建立應用程式

1. 建立程式，或使用應用程式中的現有程式。

   ![建立新程式](assets/create_new_process.png)

   建立程式

1. 建立「起點」或「指派任務」，然後按兩下它。
1. 在 **[!UICONTROL 簡報與資料]** 區段，選取 **[!UICONTROL 使用CRX資產]** 並按一下資產前的省略符號。

   ![使用CRX資產](assets/use_crx_asset.png)

   使用CRX資產

1. 選取透過管理資產UI建立的最適化表單，然後按一下 **[!UICONTROL 確定]**.

   ![選取最適化表單](assets/selecting_form.png)

   選取最適化表單

   >[!NOTE]
   >
   >如需建立最適化表單的詳細資訊，請參閱 [建立最適化表單](../../forms/using/creating-adaptive-form.md).
   >
   >
   >如需有關建立流程的詳細資訊，請參閱 [建立和管理流程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
