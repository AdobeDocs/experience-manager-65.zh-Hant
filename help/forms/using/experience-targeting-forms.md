---
title: 在AEM Forms中建立鎖定目標的體驗
description: 在AEM Forms中使用Target來建立目標客戶的自訂體驗。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
exl-id: fdc91054-3f7e-4cbf-bdfa-7d7a621747f1
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# 在AEM Forms中建立鎖定目標的體驗 {#create-targeted-experiences-in-aem-forms}

## 將Adobe Target與AEM Forms整合 {#integrate-adobe-target-with-aem-forms}

Adobe Target與AEM整合，可讓您建立針對目標受眾自訂的體驗。 透過Adobe Target，您可以建立A/B測試、測量使用者回應，並為目標使用者產生自訂的網頁內容。 您可以整合Adobe Target與AEM Forms，以針對最適化表單和互動式通訊的影像元件進行定位。

在AEM中設定Adobe Target以搭配最適化表單和互動式通訊使用，請參閱[在AEM](/help/sites-administering/target.md)中建立Target設定和[新增架構](/help/sites-administering/target.md)。

>[!NOTE]
>
>使用主機名稱或IP位址轉譯最適化表單或互動式通訊時，Targeting就會運作。 使用localhost轉譯最適化表單或互動式通訊時，它會失敗。

## 建立Target活動 {#creating-a-target-activity}

1. 選取&#x200B;**Adobe Experience Manager > Personalization >活動**。

   `https://<hostname>:<port>/libs/cq/personalization/touch-ui/content/v2/activities.html`

1. 在「活動」頁面中，選取&#x200B;**建立>建立品牌**。
1. 系統會要求您選擇範本並輸入屬性。

   選取範本，選取[下一步] **。**&#x200B;在[內容]區段中輸入您品牌的標題，然後選取[建立]。****
您的品牌現在已列在活動頁面中。

1. 在「活動」頁面中選取您的品牌。
1. 在品牌的主版區域中，選取&#x200B;**建立** > **建立活動**。

   建立活動時，您可以指定其詳細資料、目標和設定。

   詳細資訊區段包含名稱、目標定位引擎和目標。 當您選取Adobe Target作為定位引擎時，您會啟用Target雲端設定選項。 選擇您的Target雲端設定、選擇活動型別、提供活動目標，然後選取&#x200B;**下一步**。 互動式通訊僅支援體驗鎖定活動型別。

   Target區段可讓您新增對象體驗並將其命名。 按一下「**新增體驗**」以啟用「**選取對象**」和「**命名體驗**」選項。 選取&#x200B;**選取對象**&#x200B;以檢視對象清單及其來源。 從「對象名稱」清單中選取對象。 選取&#x200B;**新增體驗**&#x200B;以命名體驗，並選取&#x200B;**下一步**。

   「目標與設定」區段可讓您排程活動並排定其優先順序。 設定活動的開始日期、結束日期和優先順序、目標量度、其他量度，並選取&#x200B;**儲存**。

   活動現在會列在您的品牌頁面中。

   >[!NOTE]
   >
   >您可以忽略錯誤「您的活動已儲存，但未同步至Target。 原因：在儲存活動時遇到以下體驗「沒有選件」。

1. 若要啟用Target，請編輯.jsp檔案以包含您的最適化表單範本所使用的使用者端資料庫。

   例如，在現成可用的實作中，按一下&#x200B;**工具** > **CRXDE Lite**。

   在CRXDE Lite位址列中，輸入/libs/fd/af/components/page/base/head.jsp以編輯head.jsp檔案。

   此實作使用simpleEnrollment範本。 在此實作中，請修改head.jsp檔案以包含下列使用者端程式庫：

   `<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>`

   `<cq:include path="clientcontext_optimized" resourceType="/libs/cq/personalization/components/clientcontext_optimized"/>`

   `<cq:include path="config" resourceType="cq/personalization/components/clientcontext_optimized/config"/>`

1. 若要啟用最適化表單的Target框架，請導覽至您的表單或互動式通訊，並以編輯模式開啟它。

   若要以編輯模式開啟表單或互動式通訊，請選取&#x200B;**選取**，然後選取&#x200B;**開啟**。

   或者，當您將指標移到表單或互動式通訊圖示上而不選取它時，會出現四個按鈕。 您可以選取顯示的&#x200B;**編輯**&#x200B;按鈕，以編輯模式開啟表單。

1. 在頁面工具列中，選取&#x200B;**頁面資訊** ![主題選項](assets/theme-options.png) > **開啟屬性**。
1. 在[一般]索引標籤中，選擇&#x200B;**Adobe Target**&#x200B;欄位的設定。 選取「**儲存並關閉**」。

## 將建立的活動套用至最適化表單影像或互動式通訊影像 {#applying-created-activity-to-an-adaptive-form-image-or-an-interactive-communication-image}

1. 開啟最適化表單和互動式通訊以進行編輯。 如果您要開啟互動式通訊，請開啟Web Channel。

1. 在互動式通訊或自適應表單的製作模式中，新增要定位的影像。

   >[!NOTE]
   >
   >AEM Forms僅支援鎖定影像元件目標。 確認裝載影像元件的面板未包含任何其他元件，且面板的欄數設為1。

1. 從&#x200B;**編輯**&#x200B;切換至&#x200B;**鎖定目標**&#x200B;模式。 切換模式的選項位於右上角附近。
1. 選取&#x200B;**品牌**、選取&#x200B;**活動**，然後選取&#x200B;**開始鎖定目標**。 **Audiences**&#x200B;功能表會出現在編輯器的右側。

   ![目標功能表](assets/targeting-menu.png)

1. 從&#x200B;**對象**&#x200B;功能表選取對象，然後選取要定位的影像。 選單出現。 在功能表中選取&#x200B;**目標**。 選取影像並選取&#x200B;**設定**。 在屬性視窗中，選取要針對所選對象顯示的影像。 對所有對象重複此步驟。 互動式通訊或調適型表單中的影像已啟用體驗鎖定目標。

## 檢查建立的活動是否與Target伺服器同步 {#check-if-the-created-activity-syncs-with-the-target-server}

用於鎖定與Target伺服器同步的活動。 若要檢查您的活動是否與目標伺服器同步，請在您的品牌頁面中檢查活動的狀態。

請確認活動的狀態為「已同步」。

## 驗證Target行為 {#validate-target-behavior}

驗證Target行為：

* 在作者模式下搭配`wcmmode preview`使用目標定位
* 在發佈模式中搭配`wcmmode preview`和`wcmmode disabled`使用目標定位

## 監視影像元件的鎖定目標 {#monitor-targeting-for-the-image-component}

若要監視表單上影像元件的目標定位，請發佈您的影像、活動和最適化表單。

## 未解決的問題 {#open-issues}

可見度運算式，針對調適型表單上的目標影像設定焦點失敗。
