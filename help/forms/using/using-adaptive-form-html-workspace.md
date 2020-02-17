---
title: 在HTML工作區中使用最適化表單
seo-title: 在HTML工作區中使用最適化表單
description: 在HTML工作區中使用最適化表單
seo-description: 在HTML工作區中使用最適化表單
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931

---


# 在HTML工作區中使用最適化表單{#using-an-adaptive-form-in-html-workspace}

AEM Forms on JEE提供在HTML工作區中使用最適化表單的功能。

由於您可以在「流程設計」期間選取XDP，因此已新增從現有最適化表單AEM儲存庫瀏覽的功能。 此功能使流程設計人員能夠在起點和任務中配置自適應表單。

## 流程設計體驗 {#process-design-experience}

執行以下操作，以便在流程設計中使用自適應表單：

* 在分配任務和起始點中，可以在將表單資產分配給任務時瀏覽到CRX儲存庫中的自適應表單資產。
* 在「分配任務／起點工作台」屬性工作表中，您可以隱藏自適應表單的頂層／全局工具欄。
* 您可以在最適化表單中，為「演算」和「提交」動作使用新的動作設定檔。

### LiveCycle應用程式匯出和匯入 {#livecycle-application-export-and-import}

由於最適化表單位於AEM儲存庫中，因此LiveCycle應用程式匯出只包含使用最適化表單的參考。 因此，LiveCycle應用程式的匯出和匯入是兩個步驟。 LiveCycle應用程式包含程式定義等。 包含最適化表單的個別套件會從AEM匯出為ZIP檔案。 匯入時，LiveCycle應用程式會透過Workbench匯入，而最適化表單則會透過AEM匯入。

## HTML工作區中最適化表單的使用者體驗 {#user-experience-of-adaptive-form-in-html-workspace}

HTML工作區除了提供行動表單的控制項外，還提供一些最適化表單控制項。 當使用者開啟工作或起點時，使用者可以新增附件、儲存、簽署、提交及導覽HTML工作區中的最適化表單。 具體內容如下：

1. 若要附加檔案，請使用「工作附件」，就像Mobile Forms一樣。 任何最適化表單的「檔案附件類型」按鈕都會隱藏。

1. 若要儲存最適化表單，請按一 **下「儲存**」，就像Mobile Forms中一樣。 任何最適化表單的「儲存類型」按鈕都會隱藏。

1. 若要提交最適化表單，請使用「 **Submit** 」按鈕或路由可用動作，就像Mobile Forms中一樣。 任何最適化表單的「提交類型」按鈕都會隱藏。

1. **最適化表單全域工具列可見性**:如果流程設計人員隱藏全域／頂層工具列，則工具列和按鈕不會顯示在最適化表單上。

1. **最適化表單的工作區導覽控制項**:「HTML工作區」中最適化表單的「下一個／上一個」按鈕，以及「儲存」、「提交」和「路由」動作按鈕。 按一下「下一頁／上一頁」按鈕，以導覽HTML工作區中最適化表單的面板。 「下一個／上一個」按鈕提供深度導覽，類似於最適化表單的「行動」檢視中的導覽控制項。

1. **Adaptive Form的eSign services和摘要元件**:「摘要」元件在HTML工作區中無法運作。 換言之，如果最適化表單具有「摘要」元件，則工作區中不會顯示該元件。 工作區使用者會按一下「HTML工作區」中的「提交」或路由動作，而非「設計」元件中的「自動提交」。 簽署檔案後，檔案會顯示為平面簽署的檔案。 按一下 **提交** 或路由操作以關閉／完成任務或起始點。\
   簽署的檔案會從eSign Services伺服器收集，資料xml檔案會轉送至程式的下一個步驟。

## 在流程設計中使用自適應表單的步驟 {#steps-to-use-adaptive-forms-in-process-design}

1. 開啟Adobe Experience Manager Forms Workbench。

1. 前往「檔 **案>新增>應用程式** 」，或使用現有的應用程式來建立應用程式。

   ![建立新應用程式](assets/create_new_appl.png)

   建立新應用程式

1. 建立程式，或在應用程式中使用現有程式。

   ![建立新流程](assets/create_new_process.png)

   建立新流程

1. 建立「起始點」或「指定任務」，然後按兩下它。
1. 在「簡 **[!UICONTROL 報與資料]** 」區段下，選 **[!UICONTROL 取使用CRX資產]** ，然後按一下資產前面的省略號。

   ![使用CRX資產](assets/use_crx_asset.png)

   使用CRX資產

1. 選取透過「管理資產」使用者介面建立的最適化表單，然後按一下「 **[!UICONTROL 確定]**」。

   ![選擇最適化表單](assets/selecting_form.png)

   選擇最適化表單

   >[!NOTE]
   >
   >如需有關建立最適化表單的詳細資訊，請參 [閱建立最適化表單](../../forms/using/creating-adaptive-form.md)。
   >
   >
   >有關建立流程的詳細資訊，請參 [閱建立和管理流程](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html)。

