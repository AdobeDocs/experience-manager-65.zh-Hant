---
title: 在HTML工作區中使用自適應窗體
seo-title: Using an adaptive form in HTML Workspace
description: 在HTML工作區中使用自適應窗體
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

# 在HTML工作區中使用自適應窗體{#using-an-adaptive-form-in-html-workspace}

AEM FormsJEE提供了在HTML工作區中使用自適應表單的功能。

由於可以在流程設計期間選擇XDP，因此添加了從現有自適應表單儲存庫AEM進行瀏覽的功能。 該功能使流程設計人員能夠在起點和任務中配置自適應表單。

## 流程設計經驗 {#process-design-experience}

執行以下操作以啟用在流程設計中使用自適應表單：

* 在分配任務和起始點中，在將表單資產分配給任務時，可以瀏覽到CRX儲存庫中的自適應表單資產。
* 在「分配任務/起點工作台」屬性工作表中，可以隱藏自適應表單的頂層/全局工具欄。
* 您可以在自適應表單中為「呈現」和「提交」操作使用新的「操作」配置檔案。

### LiveCycle應用程式導出和導入 {#livecycle-application-export-and-import}

由於自適應表單位AEM於儲存庫中，因此LiveCycle應用程式導出僅包含使用的自適應表單的引用。 因此，LiveCycle申請的進出口是一個兩步走的過程。 LiveCycle應用程式套件括進程定義等。 包含自適應表單的單獨包會作為ZIP檔案從中導AEM出。 導入時，LiveCycle應用程式通過Workbench導入，自適應表單通過導AEM入。

## HTML工作區中自適應表單的用戶體驗 {#user-experience-of-adaptive-form-in-html-workspace}

HTML工作區除了提供適用於移動表單的控制項外，還提供了一些自適應表單特定控制項。 當用戶開啟任務或起點時，用戶可以添加附件、保存、簽名、提交和導航HTML工作區中的自適應表單。 具體如下：

1. 要附加檔案，請使用任務附件，如移動Forms。 自適應表單的任何「檔案附件」類型按鈕都被隱藏。

1. 要保存自適應表單，請按一下 **保存**，莫比爾Forms就是如此。 自適應表單的任何「保存類型」按鈕都被隱藏。

1. 要提交自適應表單，請使用 **提交** 按鈕或路由操作可用，移動Forms就是如此。 任何自適應表單的「提交」類型按鈕都隱藏。

1. **自適應表單全局工具欄可見性**:如果流程設計器隱藏了全局/頂級工具欄，則工具欄和按鈕不會顯示在自適應表單上。

1. **適應性Forms的工作區導航控制項**:「下一個/上一個」按鈕以及「HTML工作區」中自適應表單的「保存」、「提交」和「路由操作」按鈕可用。 按一下「下一步」/「上一步」按鈕，在「HTML工作區」中導航自適應表單的面板。 「下一個/上一個」按鈕提供深度導航，類似於自適應表單的「移動」視圖中的導航控制項。

1. **自適應表單的eSign Services和摘要元件**:「摘要」元件在「HTML工作區」中不可操作。 換句話說，如果自適應表單具有「摘要」元件，則它在工作區中不可見。 工作區用戶在「設計」元件中按一下「提交」(Submit)或「HTML工作區」(Workspace)中的「路由」(Route)操作，而不是「自動提交」(Auto Submit)。 文檔簽名後，它將顯示為平面簽名文檔。 按一下 **提交** 或關閉/完成任務或起點的路由操作。\
   從eSign服務伺服器收集簽名文檔，並將資料xml檔案轉發到進程的下一步。

## 在工藝設計中使用自適應表單的步驟 {#steps-to-use-adaptive-forms-in-process-design}

1. 開啟Adobe Experience Manager Forms工作台。

1. 轉到 **檔案>新建>應用程式** 或使用現有應用程式建立應用程式。

   ![建立新應用程式](assets/create_new_appl.png)

   建立新應用程式

1. 建立進程，或在應用程式中使用現有進程。

   ![建立新流程](assets/create_new_process.png)

   建立新流程

1. 建立起點或分配任務，然後按兩下它。
1. 在 **[!UICONTROL 演示和資料]** 選擇 **[!UICONTROL 使用CRX資產]** 並按一下資產前的橢圓。

   ![使用CRX資產](assets/use_crx_asset.png)

   使用CRX資產

1. 選擇通過「管理資產」UI建立的自適應表單，然後按一下 **[!UICONTROL 確定]**。

   ![選擇自適應窗體](assets/selecting_form.png)

   選擇自適應窗體

   >[!NOTE]
   >
   >有關建立自適應表單的詳細資訊，請參見 [建立自適應窗體](../../forms/using/creating-adaptive-form.md)。
   >
   >
   >有關建立流程的詳細資訊，請參閱 [建立和管理流程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)。
