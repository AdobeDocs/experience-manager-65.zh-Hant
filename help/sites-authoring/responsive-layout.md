---
title: 內容頁面的回應式佈局
description: Adobe Experience Manager可讓您為頁面實現回應式版面。
uuid: 4db45d78-9fca-4251-b504-ae3481fd9a8b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 668d1a8a-c757-4c9f-833f-e5dada4d0384
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
source-git-commit: cae9890cd61d6d894f34c7299e2e15ee70e14ac9
workflow-type: tm+mt
source-wordcount: '1805'
ht-degree: 7%

---

# 回應式版面{#responsive-layout}

AEM可讓您透過使用 **配置容器** 元件。

這提供了段落系統，可讓您在回應式格線中定位元件。 此格點可根據裝置/視窗大小和格式重新排列版面。 元件需與 [**版面** 模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)，可讓您根據裝置建立及編輯回應式版面。

配置容器：

* 提供水準對齊格點的功能，以及將元件並排放置到格點中並定義它們何時應摺疊/重排的功能。
* 使用預先定義的中斷點（例如用於手機、平板電腦等） 可讓您定義相關裝置/方向的必要內容行為。

   * 例如，您可以自訂元件大小，或是否在特定裝置上可看見元件。

* 可巢狀化以允許欄控制項。

之後，使用者便可使用模擬器檢視特定裝置的內容呈現方式。

>[!CAUTION]
>
>雖然「版面容器」元件可在傳統UI中使用，但其完整功能僅在觸控式UI中提供並支援。

AEM使用多種機制組合，為您的頁面實現回應式佈局：

* [**配置容器**](#adding-a-layout-container-and-its-content-edit-mode) 元件

  此元件位於 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser) 和提供了一個格點段落系統，可讓您在回應式格點內新增和定位元件。 它也可以設定為您的頁面上的預設段落系統。

* [**佈局模式**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

  將版面容器放置到頁面上後，您就可以使用 **版面** 在回應式格線中定位內容的模式。

* [**模擬器**](#selecting-a-device-to-emulate)
這可讓您建立並編輯回應式網站，這些網站可透過以互動方式調整元件大小，根據裝置/視窗大小重新安排版面。 之後，使用者便可使用模擬器檢視內容的呈現方式。

透過這些回應式格點機制，您可以：

* 根據裝置寬度（與裝置型別和方向相關），使用中斷點來定義不同的內容配置。
* 使用這些相同的中斷點和內容版面配置來確保您的內容會回應案頭瀏覽器視窗的大小。
* 使用水準對齊格點，可讓您在格點中放置元件、視需要調整大小，以及定義它們何時應摺疊/重排成並排或上下對齊/重排。
* 隱藏特定裝置配置的元件。
* 實現欄控制。

根據您的專案，版面容器可能會用作頁面的預設段落系統，或用作可透過元件瀏覽器新增到頁面的元件（或兩者）。

>[!NOTE]
>
>Adobe提供 [GitHub檔案](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) 回應式佈局的參考資料，前端開發人員可參考該參考資料，以便在AEM之外使用AEM格線，例如在為未來的AEM網站建立靜態HTML模型時。

>[!NOTE]
>
>在範本上設定即可使用上述機制。 另請參閱 [設定回應式佈局](/help/sites-administering/configuring-responsive-layout.md) 以取得進一步資訊。

## 配置定義、裝置模擬和中斷點 {#layout-definitions-device-emulation-and-breakpoints}

當您建立網站內容時，您想要確保內容的顯示方式適合用來檢視內容的裝置。

AEM可讓您根據裝置的寬度來定義版面：

* 模擬器可讓您在一系列裝置上模擬這些版面。 除了裝置型別外，還選取了方向 **旋轉裝置** 選項時，可隨著寬度變更而影響選取的中斷點。
* 中斷點是區分配置定義的分隔點。

   * 它們實際上會定義使用特定版面之任何裝置的最大寬度（以畫素為單位）。
   * 中斷點通常適用於一系列選取的裝置，具體取決於其顯示器的寬度。
   * 中斷點的範圍會向左延伸，直到下一個中斷點為止。
   * 您無法明確地選取中斷點，選取裝置和方向會自動選取適當的中斷點。

裝置 **案頭**&#x200B;沒有特定寬度的中斷點會與預設中斷點相關（亦即高於上次設定中斷點的所有內容）。

>[!NOTE]
>
>您可以為每個個別裝置定義中斷點，但這會大幅增加定義和維護版面配置所需的工作。

使用模擬器時，您會選取特定裝置來模擬和定義版面，相關的中斷點也會反白顯示。 您所做的任何配置變更都將適用於中斷點套用的其他裝置，亦即位於使用中中斷點標籤左側、但下一個中斷點標籤前的任何裝置。

例如，當您選取裝置時 **iPhone 6 Plus** （定義為540畫素的寬度）用於模擬和配置、中斷點 **電話** （定義為768畫素）也會啟動。 您對版面所做的任何變更 **IPHONE 6** 將適用於下的其他裝置 **電話** 中斷點，例如 **IPHONE 5** （定義為320畫素）。

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## 選取要模擬的裝置 {#selecting-a-device-to-emulate}

1. 開啟必要頁面以進行編輯。 例如：

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. 選取 **模擬器** 圖示從上方工具列選取：

   ![模擬器](do-not-localize/screen_shot_2018-03-23at084256.png)

1. 模擬器工具列將會開啟。

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   模擬器工具列會顯示其他版面選項：

   * **旋轉裝置**  — 可讓您將裝置從垂直（縱向）方向旋轉至水準（橫向）方向，反之亦然。

     ![旋轉裝置](do-not-localize/screen_shot_2018-03-23at084612.png) ![旋轉裝置](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **選取裝置**  — 從清單定義要模擬的特定裝置（請參閱下一步以瞭解詳細資訊）

     ![選取裝置](do-not-localize/screen_shot_2018-03-23at084743.png)

1. 若要選取要模擬的特定裝置，您可以：

   * 使用「選取裝置」圖示，並從下拉式選擇器中選取。
   * 在模擬器工具列中，點選/按一下裝置指示器。

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. 選取特定裝置後，您可以：

   * 檢視所選裝置的作用中標籤，例如 **iPad。**
   * 檢視作用中的標籤以取得適當的 [中斷點](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) 例如 **平板電腦。**

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * 藍色虛線代表 *摺頁* 針對選取的裝置(此處為 **IPHONE 6**)。

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * 摺頁也可以視為分頁符號(不要與 [中斷點](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints))以取得詳細資訊。 為方便起見，此畫面會顯示在捲動前，使用者在裝置上看到的內容部分。
   * 如果模擬的裝置高度高於熒幕大小，則不會顯示折線。
   * 顯示摺頁是為了方便作者，不會顯示在已發佈的頁面上。

## 新增版面容器及其內容 (編輯模式) {#adding-a-layout-container-and-its-content-edit-mode}

A **配置容器** 是段落系統，具備以下功能：

* 包含其他元件。
* 定義版面。
* 回應變更。

>[!NOTE]
>
>如果尚未提供，請 **配置容器** 必須明確 [已為段落系統/頁面啟動](/help/sites-administering/configuring-responsive-layout.md) (例如，使用 [**設計** 模式](/help/sites-authoring/default-components-designmode.md))。

1. 「配 **置容器** 」是元件瀏覽器中的標準 [元件](/help/sites-authoring/author-environment-tools.md#components-browser)。從這裡，您可以將其拖曳至頁面上的必要位置，之後您將看到「拖曳元件至此處 **** 」預留位置。
1. 然後，您可以將元件新增至版面容器。 這些元件將儲存實際內容：

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## 選取版面容器並對其執行動作（編輯模式） {#selecting-and-taking-action-on-a-layout-container-edit-mode}

與其他元件一樣，您可以選取版面容器，然後對其採取剪下、複製、刪除等動作(當在 **編輯** 模式)：

>[!CAUTION]
>
>由於版面容器是段落系統，刪除元件將會同時刪除版面格線以及容器內容納的所有元件（及其內容）。

1. 如果您將滑鼠移到格點預留位置上或點選格點，則會顯示動作選單。

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   您需要選取 **父級** 選項。

   ![父選項](do-not-localize/screen_shot_2018-03-23at085417.png)

1. 如果配置元件為巢狀，請選取 **父級** 選項會顯示下拉式選取專案，讓您選取巢狀配置容器或其父項。

   當您將滑鼠移至下拉式清單中的容器名稱上時，其外框將顯示在頁面上。

   * 最低的巢狀配置容器將以黑色外框。
   * 下一個最低的巢狀配置容器將以深灰色顯示。
   * 每個後續容器都會以較淺的灰色陰影顯示。

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. 這將會反白顯示整個格線及其內容。 動作工具列隨即顯示，您可從中選取動作，例如 **刪除。**

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## 定義版面（版面模式） {#defining-layouts-layout-mode}

>[!NOTE]
>
>您可以為每一個專案定義個別的配置 [中斷點](#layout-definitions-device-emulation-and-breakpoints) （由模擬的裝置型別和方向所決定）。

若要設定以版面容器實作的回應式格線的版面，您需要使用 **版面** 模式。

**版面** 啟動模式的方式有兩種。

* 使用工具列 [中的模式選單](/help/sites-authoring/author-environment-tools.md#page-modes) ，然後選擇「 **版面模式」**

   * 選取「 **版面** 」模式，就像切換至「編輯 **」模式或「** 定位 **** 」模式。
   * **配置模式** (Layout **mode)會維持持續性，而且您必須先透過模式選取器** 選取其他模式，才能離開「配置」模式。

* 時間 [編輯個別元件。](/help/sites-authoring/editing-content.md#edit-component-layout)

   * 藉由使用 **版面** 元件快速動作選單中的選項，您可以切換至 **版面** 模式。
   * **版面** 編輯元件時模式會持續存在並恢復為 **編輯** 模式，此時焦點會變更為另一個元件。

在版面配置模式中，您可以對格線執行各種動作：

* 使用藍點調整內容元件的大小。 調整大小一律靠齊格點。 當調整背景格點大小時，將顯示以協助對齊：

  ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

  >[!NOTE]
  >
  >當元件(例如 **影像** 都會重新調整大小。

* 按一下/點選內容元件，工具列可讓您：

   * **父級**

     可讓您選取整個版面容器元件，以便對整體執行動作。

   * **浮動至新行**

     元件將會移至新的一行，視格線內的可用空間而定。

   * **隱藏元件**

     元件將變得不可見（可以從版面配置容器的工具列恢復）。

  ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* 在 **版面** 模式：您可以點選/按一下 **將元件拖曳到這裡** 以選取整個元件。 這將會顯示此模式的工具列。

  根據版面配置元件和屬於它的元件的狀態，工具列會有不同的選項。 例如：

   * **父級**  — 選取父元件。

     ![父級](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **顯示隱藏的元件**  — 顯示所有或個別元件。 數字表示目前有多少個隱藏的元件。計數器顯示隱藏的元件數目。

     ![顯示隱藏的元件](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **還原中斷點配置**  — 還原至預設版面。 這表示不會強制使用自訂版面。

     ![反向中斷點配置](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **浮動至新行**  — 如果間距允許，將元件向上移動一個位置。

     ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **隱藏元件**  — 隱藏目前的元件。

     ![隱藏元件](do-not-localize/screen_shot_2018-03-23at090834.png)

     >[!NOTE]
     >
     >在上述範例中，浮動和隱藏動作可供使用，因為此配置容器巢狀內嵌於上層配置容器中。

   * **取消隱藏元件**
選取父元件以顯示包含「 」的動作工具列 **顯示隱藏的元件** 選項。 在此示例中，隱藏了兩個元件。

     ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

  選取「顯 **示隱藏的元件** 」(Show hidden components)選項，會以藍色顯示目前隱藏在原始位置的元件。

  ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

  選取 **全部還原** 將取消隱藏所有隱藏的元件。
