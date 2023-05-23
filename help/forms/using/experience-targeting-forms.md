---
title: 在AEM Forms創造有針對性的體驗
seo-title: Create targeted experiences in AEM Forms
description: 使用AEM Forms的Target為目標客戶建立定制體驗。
seo-description: Use Target in AEM Forms to create customized experiences for targeted customers.
uuid: 174b6054-8fe3-4ab2-8afd-435e5dff9044
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 6cf54a08-d429-4a58-8429-a1cb784448d1
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 0%

---

# 在AEM Forms創造有針對性的體驗 {#create-targeted-experiences-in-aem-forms}

## 整合Adobe Target與AEM Forms {#integrate-adobe-target-with-aem-forms}

Adobe Target與AEM整合，讓您為目標受眾建立定製的體驗。 使用Adobe Target，您可以建立A/Btest、測量用戶響應並為目標用戶生成自定義的Web內容。 您可以將Adobe Target與AEM Forms整合，以針對自適應形式和互動式通信的影像元件。

將Adobe Target配AEM置為與自適應表單和互動式通信一起使用，請參見 [在中建立目標配AEM置](/help/sites-administering/target.md) 和 [添加框架](/help/sites-administering/target.md)。

>[!NOTE]
>
>當使用主機名或IP地址呈現自適應表單或交互通信時，目標就會生效。 當使用localhost呈現自適應表單或互動式通信時，該命令將失敗。

## 建立目標活動 {#creating-a-target-activity}

1. 點擊 **Adobe Experience Manager>個性化>活動**。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 在「活動」頁中，按一下 **建立>建立品牌**。
1. 系統會要求您選擇模板並輸入屬性。

   選擇模板，點擊 **下一個。** 在「屬性」部分輸入品牌標題，然後點擊 **建立。**
您的品牌現在列在「活動」頁面中。

1. 在「活動」頁面中點擊您的品牌。
1. 在品牌的主區域中，點擊 **建立** > **建立活動**。

   建立活動時，可指定活動的詳細資訊、目標和設定。

   「詳細資訊」部分包括名稱、目標引擎和目標。 選擇Adobe Target作為目標引擎時，將啟用目標雲配置選項。 選擇目標雲配置，選擇活動類型，提供活動目標，然後點擊 **下一個**。 互動式通信僅支援「體驗目標」活動類型。

   「目標」部分允許您添加觀眾體驗並命名它。 按一下 **添加體驗** 啟用 **選擇受眾** 和 **名稱體驗** 頁籤 點擊 **選擇受眾** 查看觀眾及其來源的清單。 從「受眾名稱」清單中選擇受眾。 點擊 **添加體驗** 命名體驗，點擊 **下一個**。

   「目標和設定」部分允許您安排活動並排定活動的優先順序。 設定活動的開始日期、結束日期和優先順序、目標度量、附加度量和點擊 **保存**。

   此活動現在列在您的品牌頁面中。

   >[!NOTE]
   >
   >您可以忽略錯誤「您的活動已保存，但未與目標同步。 原因：如果在保存活動時遇到以下體驗沒有優惠」。

1. 要啟用目標，請編輯.jsp檔案，以包括您的自適應表單模板使用的客戶端庫。

   例如，在現成的實現中，按一下 **工具** >  **CRXDE Lite**。

   在CRXDE Lite地址欄中，鍵入/libs/fd/af/components/page/base/head.jsp以編輯head.jsp檔案。

   此實現使用simpleEnrollment模板。 在此實現中，修改head.jsp檔案以包括以下客戶端庫：

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 要為自適應表單啟用目標框架，請導航到您的表單或互動式通信，然後在編輯模式下開啟它。

   要在編輯模式下開啟窗體或互動式通信，請點擊 **選擇** 然後點擊 **開啟**。

   或者，當您將指針移動到表單或互動式通信表徵圖上而不選擇它時，將顯示四個按鈕。 可以點擊 **編輯** 的子菜單。

1. 在頁面工具欄中，點擊 **頁面資訊** ![主題選項](assets/theme-options.png) > **開啟屬性**。
1. 在「常規」頁籤中，為 **Adobe Target** 的子菜單。 點擊 **保存並關閉**。

## 將建立的活動應用於自適應表單影像或互動式通信影像 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 開啟自適應窗體和互動式通信進行編輯。 如果要開啟互動式通信，請開啟Web通道。

1. 在互動式通信或自適應表單的創作模式中，添加要目標的影像。

   >[!NOTE]
   >
   >AEM Forms只支援將目標鎖定在影像元件上。 確保承載影像元件的面板不包含任何其他元件，並且面板的列數設定為1。

1. 切換自 **編輯** 至 **目標** 的子菜單。 切換模式的選項靠近右上角。
1. 選擇 **品牌**&#x200B;選中 **活動**，然後點擊 **開始目標**。 的 **觀眾** 菜單開啟它。

   ![目標菜單](assets/targeting-menu.png)

1. 從 **觀眾** 菜單，然後點擊影像到目標。 出現菜單。 在菜單中，點擊 **目標**。 點擊影像並點擊 **配置**。 在「屬性」窗口中，選擇要為所選受眾顯示的影像。 對所有觀眾重複此步驟。 在互動式通信或自適應形式中為影像啟用體驗目標。

## 檢查建立的活動是否與目標伺服器同步 {#check-if-the-created-activity-syncs-with-the-target-server}

用於與目標伺服器進行同步的活動。 要檢查活動是否與目標伺服器同步，請在品牌頁面中檢查活動的狀態。

確保活動的狀態為「已同步」。

## 驗證目標行為 {#validate-target-behavior}

要驗證目標行為，請執行以下操作：

* 使用目標 `wcmmode preview` 在作者模式下
* 使用目標 `wcmmode preview` 和 `wcmmode disabled` 在發佈模式下

## 映像元件的監視器目標 {#monitor-targeting-for-the-image-component}

要監視窗體上影像元件的目標，請發佈您的影像、活動和自適應窗體。

## 未解決的問題 {#open-issues}

可見性表達式，針對自適應表單上的目標影像設定焦點失敗。
