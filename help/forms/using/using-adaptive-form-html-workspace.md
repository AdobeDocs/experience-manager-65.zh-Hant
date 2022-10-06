---
title: 在HTML工作區中使用最適化表單
seo-title: Using an adaptive form in HTML Workspace
description: 在HTML工作區中使用最適化表單
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# 在HTML工作區中使用最適化表單{#using-an-adaptive-form-in-html-workspace}

AEM Forms on JEE提供在HTML工作區中使用最適化表單的功能。

由於您可以在程式設計期間選取XDP，因此已新增從現有最適化表單AEM存放庫瀏覽的功能。 此功能使流程設計人員能夠在起始點和任務中配置最適化表單。

## 流程設計體驗 {#process-design-experience}

執行以下操作，以便在流程設計中使用最適化表單：

* 在「指派任務」和「起始點」中，將表單資產指派至任務時，您可以瀏覽至CRX存放庫中的最適化表單資產。
* 在「分配任務/起始點工作台」屬性工作表中，您可以隱藏最適化表單的頂層/全局工具欄。
* 您可以在最適化表單中使用新的「演算」和「提交」動作設定檔。

### LiveCycle應用程式導出和導入 {#livecycle-application-export-and-import}

由於適用性表單位於AEM存放庫中，因此LiveCycle應用程式匯出僅包含所使用適用性表單的參考。 因此，LiveCycle應用程式的匯出和匯入是兩步驟的過程。 LiveCycle應用程式包含程式定義等。 包含適用性表單的個別套件會從AEM匯出為ZIP檔案。 匯入時，LiveCycle應用程式會透過Workbench匯入，而適用性表單則會透過AEM匯入。

## HTML工作區中最適化表單的使用者體驗 {#user-experience-of-adaptive-form-in-html-workspace}

HTML工作區除了提供行動表單可用的控制項外，還提供一些最適化表單專用控制項。 當使用者開啟工作或起始點時，使用者可以在HTML工作區中新增附件、儲存、簽署、提交及導覽最適化表單。 具體如下：

1. 若要附加檔案，請使用「工作」附件，如同Mobile Forms。 任何最適化表單的「檔案附件」類型按鈕都會隱藏。

1. 若要儲存最適化表單，請按一下 **儲存**，如行動Forms。 任何最適化表單的「儲存類型」按鈕都會隱藏。

1. 若要提交最適化表單，請使用 **提交** 按鈕或路由動作可用，如行動Forms。 任何最適化表單的「提交類型」按鈕都會隱藏。

1. **適用性表單全域工具列可見性**:如果流程設計器隱藏了全局/頂級工具欄，則工具欄和按鈕不會顯示在適用性表單上。

1. **適用性Forms的工作區導覽控制項**:「HTML工作區」中適用性表單的「下一個/上一個」按鈕以及「儲存」、「提交」和「路由操作」按鈕均可用。 按一下下一步/上一步按鈕，導覽HTML工作區中最適化表單的面板。 「下一個/上一個」按鈕提供深層導覽，類似於適用性表單的「行動」檢視中的導覽控制項。

1. **電子簽名服務與最適化表單的摘要元件**:摘要元件在HTML工作區中無法運作。 換言之，如果適用性表單有「摘要」元件，則工作區中不會顯示該元件。 工作區使用者在「設計」元件中按一下「提交」或「HTML工作區」中的「路由」動作，而不是「自動提交」。 文檔簽名後，它將顯示為平面簽名文檔。 按一下 **提交** 或關閉/完成任務或起始點的路由操作。\
   從eSign Services伺服器收集已簽名的文檔，並將資料xml檔案轉發到該過程的下一步。

## 流程設計中使用最適化表單的步驟 {#steps-to-use-adaptive-forms-in-process-design}

1. 開啟Adobe Experience Manager Forms Workbench。

1. 前往 **檔案>新建>應用程式** 或使用現有應用程式建立應用程式。

   ![建立新應用程式](assets/create_new_appl.png)

   建立新應用程式

1. 建立流程，或在應用程式中使用現有流程。

   ![建立新流程](assets/create_new_process.png)

   建立新流程

1. 建立起始點或分配任務，然後按兩下它。
1. 在 **[!UICONTROL 簡報與資料]** 部分，選擇 **[!UICONTROL 使用CRX資產]** 然後按一下資產前的點。

   ![使用CRX資產](assets/use_crx_asset.png)

   使用CRX資產

1. 選取透過「管理資產」UI建立的最適化表單，然後按一下 **[!UICONTROL 確定]**.

   ![選取最適化表單](assets/selecting_form.png)

   選取最適化表單

   >[!NOTE]
   >
   >如需建立最適化表單的詳細資訊，請參閱 [建立最適化表單](../../forms/using/creating-adaptive-form.md).
   >
   >
   >如需建立程式的詳細資訊，請參閱 [建立和管理流程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
