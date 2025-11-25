---
title: 編輯頁面內容
description: 建立頁面後，您可以編輯內容以進行所需的更新。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '3015'
ht-degree: 4%

---

# 編輯頁面內容{#editing-page-content}

建立頁面後（新頁面或作為啟動項或即時副本的一部分），您可以編輯內容以進行所需的更新。

使用可拖曳至頁面的[元件](/help/sites-authoring/default-components-console.md) （適合內容型別）新增內容。 接著，您就可以就地編輯、移動或刪除這些專案。

>[!NOTE]
>
>您的帳戶需要[適當的存取權](/help/sites-administering/security.md)和[許可權](/help/sites-administering/security.md#permissions)才能編輯頁面。
>
>如果您遇到任何問題，Adobe建議您聯絡系統管理員。

>[!NOTE]
>
>如果您的頁面、範本，或兩者已適當設定，您可以在編輯時使用[回應式版面](/help/sites-authoring/responsive-layout.md)。

>[!NOTE]
>
>在&#x200B;**編輯**&#x200B;模式中，內容中的連結可見，但&#x200B;**無法存取**。 如果您想要使用內容中的連結進行導覽，請使用[預覽模式](#previewingpagestouchoptimizedui)。

## 頁面工具列 {#page-toolbar}

根據頁面設定，頁面工具列會提供適當功能的存取權。

![頁面工具列](assets/screen_shot_2018-03-22at111338.png)

工具列提供許多選項的存取權。 根據您目前的內容和組態，某些選項可能無法使用。

* **切換側面板**

  這會開啟/關閉側面板，其中包含[資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)、[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)和[內容樹狀結構](/help/sites-authoring/author-environment-tools.md#content-tree)。

  ![切換側面板](do-not-localize/screen_shot_2018-03-22at111425.png)

* **頁面資訊**

  它可讓您存取[頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information)功能表，包括頁面詳細資訊以及可在頁面上採取的動作，包括檢視及編輯頁面資訊、檢視頁面屬性以及發佈/取消發佈頁面。

  ![頁面資訊](do-not-localize/screen_shot_2018-03-22at111437.png)

* **模擬器**

  切換[模擬器工具列](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)，此工具列用於模擬其他裝置上的頁面外觀。 這會在版面模式中自動切換。

  ![模擬器](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

  開啟[內容中心](/help/sites-authoring/ch-previewing.md)。 僅適用於「預覽」模式。

  ![內容中心](assets/screen_shot_2018-03-22at111543.png)

* **頁面標題**

  這僅供參考。

  ![頁面標題](assets/screen_shot_2018-03-22at111554.png)

* **模式選擇器**

  它會顯示目前的[模式](/help/sites-authoring/author-environment-tools.md#page-modes)，並讓您選取其他模式，例如編輯、配置、時間扭曲或定位。

  ![模式選擇器](assets/chlimage_1-120.png)

* **預覽**

  啟用[預覽模式](/help/sites-authoring/editing-content.md#preview-mode)。 這會顯示發佈時所顯示的頁面。

  ![預覽模式](assets/chlimage_1-121.png)

* **註釋**

  它可讓您在檢閱頁面時新增[註解](/help/sites-authoring/annotations.md)至頁面。 在第一個註解後，圖示會切換為數字，指出頁面上的註解數量。

  ![註釋](do-not-localize/screen_shot_2018-03-22at111638.png)

### 狀態通知 {#status-notification}

如果頁面是[工作流程](/help/sites-authoring/workflows.md)或多個工作流程的一部分，則在編輯頁面時，此資訊會顯示在畫面頂端的通知列中。

![工作流程通知](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>狀態列只對具有適當許可權的使用者帳戶可見。

通知會列出針對頁面執行的工作流程。 如果使用者參與目前的工作流程步驟，則[的選項會影響工作流程狀態](/help/sites-authoring/workflows-participating.md)，並可取得更多有關工作流程的資訊，例如：

* **完成** — 開啟&#x200B;**完成工作專案**&#x200B;對話方塊

* **委派** — 開啟&#x200B;**完成工作專案**&#x200B;對話方塊

* **檢視詳細資料** — 開啟工作流程的&#x200B;**詳細資料**&#x200B;視窗

透過通知列完成及委派工作流程步驟，其運作方式與從[通知]收件匣參與[工作流程](/help/sites-authoring/workflows-participating.md)時的運作方式相同。

如果頁面受限於多個工作流程，則在通知的右端會顯示工作流程數量，並附上箭頭按鈕，讓您捲動瀏覽工作流程。

![工作流程數目通知](assets/chlimage_1-122.png)

## 元件預留位置 {#component-placeholder}

元件預留位置是一個指示器，可顯示將元件放置於何處 — 位於目前暫留的元件上方。

* 將元件新增至頁面時（從元件瀏覽器拖曳）：

  ![正在新增元件](assets/screen_shot_2018-03-22at111928.png)

* 移動現有元件時：

  ![移動現有元件](assets/screen_shot_2018-03-22at112445.png)

## 插入元件 {#inserting-a-component}

### 使用元件瀏覽器插入元件 {#inserting-a-component-from-the-components-browser}

您可以使用[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)來新增元件。 [元件預留位置](#component-placeholder)會顯示元件的位置：

1. 確定您的頁面處於&#x200B;[**編輯**&#x200B;模式](/help/sites-authoring/author-environment-tools.md#page-modes)。
1. 開啟[元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)。
1. 將必要的元件拖曳到[必要的位置](#component-placeholder)。

1. [編輯](#editmovecopypastedelete)元件。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填滿整個畫面。 開始拖曳元件後，瀏覽器會關閉以再次顯示頁面，讓您可以放置元件。

### 使用段落系統插入元件 {#inserting-a-component-from-the-paragraph-system}

您可以使用段落系統的&#x200B;**將元件拖曳到這裡**&#x200B;方塊來新增元件：

1. 確定您的頁面處於&#x200B;[**編輯**&#x200B;模式](/help/sites-authoring/author-environment-tools.md#page-modes)。
1. 有兩種方式可以從段落系統選取和新增元件：

   * 從現有元件的工具列或&#x200B;**拖曳元件到此處**&#x200B;方塊中選取&#x200B;**插入元件**&#x200B;選項(+)。

   ![插入元件選擇](assets/screen_shot_2018-03-22at112536.png)

   * 如果您使用案頭裝置，可以按兩下&#x200B;**將元件拖曳到這裡**&#x200B;方塊。

   **插入新元件**&#x200B;對話方塊會開啟，讓您選取所需的元件：

   ![插入新元件](assets/screen_shot_2018-03-22at112650.png)

1. 選取的元件會新增至頁面底部。 [視需要編輯](#editmovecopypastedelete)元件。

### 使用Assets瀏覽器插入元件 {#inserting-a-component-using-the-assets-browser}

您也可以從[資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)拖曳資產，將元件新增至頁面。 這會自動建立適當型別的元件（並包含資產）。

這適用於下列資產型別（部分取決於頁面/段落系統）：

<table>
 <tbody>
  <tr>
   <th><strong>資產類型</strong></th>
   <th><strong>產生的元件型別</strong></th>
  </tr>
  <tr>
   <td>影像</td>
   <td>影像</td>
  </tr>
  <tr>
   <td>文件</td>
   <td>下載</td>
  </tr>
  <tr>
   <td>產品</td>
   <td>產品</td>
  </tr>
  <tr>
   <td>影片</td>
   <td>閃光燈</td>
  </tr>
  <tr>
   <td>內容片段</td>
   <td>內容片段<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>您可針對您的安裝設定此行為。 如需詳細資訊，請參閱[設定段落系統，以便拖曳資產建立元件執行個體](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance)。

若要拖曳上述任一資產型別來建立元件：

1. 確定您的頁面處於&#x200B;[**編輯**&#x200B;模式](/help/sites-authoring/author-environment-tools.md#page-modes)。
1. 開啟[資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser)。
1. 將所需的資產拖曳至所需的位置。 [元件預留位置](#component-placeholder)會顯示元件的位置。

   適合資產型別的元件會在所需位置建立，其中包含所選資產。

1. 如有必要，請[編輯](#editmovecopypastedelete)元件。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個畫面。 當您開始拖曳資產時，瀏覽器會關閉以再次顯示頁面，讓您能夠放置資產。

瀏覽資產時，如果您發現必須快速變更資產，請按一下資產名稱旁的編輯圖示，以啟動[Asset Editor](/help/assets/manage-assets.md)。

![編輯圖示](assets/screen_shot_2018-03-22at112735.png)

## 編輯/設定/複製/剪下/刪除/貼上 {#edit-configure-copy-cut-delete-paste}

選取元件會開啟工具列。 這可讓您存取可在元件上執行的各種動作。

使用者可用的實際動作會視情況顯示，並非所有動作皆可在此處說明。

![元件工具列選項](assets/screen_shot_2018-03-22at112909.png)

* **編輯**

  [根據元件型別](/help/sites-authoring/default-components.md)，這可讓您[編輯元件的內容](#edit-content)。 通常會提供工具列。

  ![編輯](do-not-localize/screen_shot_2018-03-22at112936.png)

* **設定**

  [依存於元件型別](/help/sites-authoring/default-components.md)，這可以讓您編輯及設定元件的屬性。 通常會開啟一個對話方塊。

  ![設定](do-not-localize/screen_shot_2018-03-22at112955.png)

* **複製**

  這會將元件複製到剪貼簿。 貼上後，原始元件仍會保留。

  ![複製](do-not-localize/screen_shot_2018-03-22at113000.png)

* **剪下**

  這會將元件複製到剪貼簿。 貼上動作後，會移除原始元件。

  ![剪下](assets/screen_shot_2018-03-22at113007.png)

* **刪除**

  這會從含有您確認的頁面中刪除元件。

  ![刪除](do-not-localize/screen_shot_2018-03-22at113012.png)

* **插入元件**

  這會開啟對話方塊以[新增元件](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system)。

  ![插入元件](do-not-localize/screen_shot_2018-03-22at113017.png)

* **貼上**

  這會將元件從剪貼簿貼到頁面。 原始物件是否保留取決於您是使用複製還是剪下。

   * 您可以貼至相同頁面或不同頁面。
   * 貼上的專案會貼在您選取貼上動作的專案上方。
   * 僅當剪貼簿上有內容時，才會顯示「貼上」動作。

  ![貼上](assets/screen_shot_2018-03-22at113553.png)

  >[!NOTE]
  >
  >如果您在剪下/復製作業前將頁面貼到已開啟的其他頁面，則必須重新整理頁面以檢視貼上的內容。

* **群組**

  這可讓您一次選取多個元件。 透過&#x200B;**Control+Click**&#x200B;或&#x200B;**Command+Click**，桌上型電腦裝置也能達到相同效果。

  ![群組](do-not-localize/screen_shot_2018-03-22at113240.png)

* **父系**

  這可讓您選取所選元件的父元件。

  ![父系](assets/screen_shot_2018-03-22at113028.png)

* **配置**

  這可讓您修改所選元件的[配置](/help/sites-authoring/editing-content.md#edit-component-layout)。 這僅適用於選取的元件，而且不會啟動整個頁面的[配置模式](/help/sites-authoring/author-environment-tools.md#page-modes)。

  ![配置](do-not-localize/screen_shot_2018-03-22at113044.png)

* **轉換成體驗片段變數**

  這可讓您從選取的元件建立[體驗片段](/help/sites-authoring/experience-fragments.md)，或將其新增至現有的體驗片段。

  ![轉換成體驗片段變數](do-not-localize/screen_shot_2018-03-22at113033.png)

## 編輯（內容） {#edit-content}

在元件中新增或編輯內容的方法有兩種：

* 開啟[元件對話方塊以進行編輯](#component-edit-dialog)。
* [從資產瀏覽器拖放資產](#draganddropintocomponent)以直接新增內容。

### 元件編輯對話方塊 {#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#edit-configure-copy-cut-delete-paste)。

確切的編輯選項取決於元件。 對於某些元件，[所有動作僅可在全熒幕模式](#edit-content-full-screen-mode)下使用。 例如：

* [文字元件](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

  ![文字元件](assets/screen_shot_2018-03-22at120215.png)

* 影像元件

  ![影像元件](assets/screen_shot_2018-03-22at120252.png)

  >[!NOTE]
  >
  >無法編輯空白的影像元件。
  >
  >
  >[拖曳或上傳影像（使用[設定]）](/help/sites-authoring/default-components-foundation.md#image)，您才能開始編輯。

* 影像元件 — 全熒幕

  [進入影像元件的全熒幕模式](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)可讓您有更多空間編輯影像，並顯示額外的編輯選項，例如&#x200B;**啟動地圖**&#x200B;和&#x200B;**重設縮放**。 此外，全螢幕還允許選取裁切預設集。

  ![影像元件全熒幕](assets/screen_shot_2018-03-22at120529.png)

* 由多個基本元件所建構的元件，例如[Text &amp; Image基礎元件](/help/sites-authoring/default-components-foundation.md#text-image)，會先要求您確認所要的編輯選項集：

  ![元件編輯選項](assets/chlimage_1-123.png)

### 將Assets拖放至元件中 {#drag-and-drop-assets-into-component}

對於特定元件型別，您可以直接從資產瀏覽器將資產拖放至元件，以更新內容：

| **資產型別** | **元件型別** |
|---|---|
| 影像 | 影像 |
| 文件 | 下載 |
| 產品 | 產品 |
| 影片 | 閃光燈 |
| 內容片段 | 內容片段 |

## 編輯（內容）全熒幕模式 {#edit-content-full-screen-mode}

對於所有元件，可使用（和退出）存取全熒幕模式：

![編輯全熒幕模式](do-not-localize/chlimage_1-20.png)

例如，**Text**&#x200B;元件：

![文字編輯器](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>對於某些元件，全熒幕模式比基本就地編輯器有更多可用選項。

## 移動元件 {#moving-a-component}

若要移動段落元件：

1. 選取要以選取並按住或按住來移動的段落。
1. 將段落拖曳到新位置。 AEM會指出段落的存放位置。 將其拖曳至所需位置。

   ![移動段落元件](assets/screen_shot_2018-03-22at121821.png)

1. 此時會移動您的段落。

>[!NOTE]
>
>您也可以使用[剪下並貼上](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste)來移動元件。

## 編輯元件配置 {#edit-component-layout}

您可以選取元件的[配置](/help/sites-authoring/responsive-layout.md)動作，以變更該元件的配置，而不需重複從編輯切換到&#x200B;**配置模式**&#x200B;來調整元件。 不必離開編輯模式，即可節省時間。

1. 在網站主控台的&#x200B;**編輯**&#x200B;模式中，選取元件會顯示元件的工具列。

   ![在表單](assets/screen_shot_2018-03-22at133756.png)中編輯模式

   按一下&#x200B;**配置**&#x200B;動作，以便調整元件的配置。

   ![元件工具列](do-not-localize/chlimage_1-21.png)

1. 選取「配置」動作後：

   * 元件顯示的調整大小控點。
   * 模擬器工具列會顯示在畫面頂端。
   * 元件工具列上會顯示「配置」動作，而非標準編輯動作。

   ![多個裝置上的表單預覽](assets/screen_shot_2018-03-22at133843.png)

   您現在可以修改元件的配置，就像在[配置模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)中一樣。

1. 進行必要的配置變更後，按一下元件動作功能表中的&#x200B;**關閉**&#x200B;以停止修改元件的配置。 元件的工具列會回到其正常的編輯狀態。

   ![關閉](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>「配置」動作僅限於選定元件的範圍。 例如，如果您正在編輯一個元件的版面，然後選取另一個元件，則會為新選取的元件顯示標準編輯工具列（而非版面工具列）。 調整大小操作框和模擬器工具列消失。
>
>如果您必須編輯頁面的整體版面配置（會影響多個元件），請切換至[版面配置模式](/help/sites-authoring/responsive-layout.md)。

## 繼承元件 {#inherited-components}

繼承的元件可能是各種情況的產物，包括：

* [多網站管理](/help/sites-administering/msm.md)
* [啟動](/help/sites-authoring/launches.md) （當以即時副本為基礎時）。
* 特定元件，例如Geometrixx中的繼承段落系統。

您可以取消（然後重新啟用）繼承。 此功能可從以下來源取得（視元件而定）：

* **即時副本**

  元件工具列（如果元件位在屬於即時副本或啟動專案的頁面上，則根據即時副本）。 例如：

  ![即時副本](assets/screen_shot_2018-03-22at134339.png)

  取消繼承選項可供使用：

  ![取消繼承](do-not-localize/screen_shot_2018-03-22at134406.png)

  或者，如果已取消，則重新啟用繼承：

  ![重新啟用繼承](do-not-localize/screen_shot_2018-03-22at134417.png)

  「轉出」動作也適用於Blueprint或即時副本來源：

  ![推出](do-not-localize/screen_shot_2018-03-22at134516.png)

* **繼承的段落系統**

  組態對話方塊。 例如，與繼承的段落系統一樣：

  ![繼承的段落系統](assets/chlimage_1-124.png)

## 編輯頁面範本 {#editing-the-page-template}

如果頁面是以[可編輯的範本](/help/sites-authoring/templates.md#editable-and-static-templates)為基礎，您可以選取[頁面資訊功能表](/help/sites-authoring/templates.md#editing-templates-template-authors)中的&#x200B;**編輯範本**，輕鬆切換至[範本編輯器](/help/sites-authoring/author-environment-tools.md#page-information)。

如果頁面是以[靜態範本](/help/sites-authoring/templates.md#editable-and-static-templates)為基礎，您可以使用工具列上的[頁面模式選取器](/help/sites-authoring/default-components-designmode.md)切換至[設計模式](/help/sites-authoring/author-environment-tools.md#page-modes)，以啟用/停用頁面上使用的元件。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-authoring/basic-handling.md#column-view)[的範本](/help/sites-authoring/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

[即時副本狀態頁面模式](/help/sites-authoring/author-environment-tools.md#page-modes)可讓您快速總覽即時副本狀態，以及哪些元件是/不是繼承的：

* 綠色邊框：繼承
* 粉紅色邊框：繼承已取消

例如：

![即時副本繼承狀態](assets/screen_shot_2018-03-22at134820.png)

## 新增註解 {#adding-annotations}

[註解](/help/sites-authoring/annotations.md)可讓檢閱者和其他作者針對您的內容提供意見回饋。 它們通常用於稽核和驗證目的。

## 預覽頁面 {#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode) — 快速就地預覽

* [以發佈的形式檢視](#view-as-published) — 完整預覽可在新索引標籤中開啟頁面

>[!NOTE]
>
>* 內容中的連結可見，但在編輯模式中無法存取。
>* 如果您想要使用連結來導覽，請使用任一預覽選項。
>* 使用[鍵盤快速鍵](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M`，在預覽和上次選取的模式之間切換。
>

>[!NOTE]
>
>這兩個選項都會設定WCM模式Cookie。

### 預覽模式 {#preview-mode}

編輯內容時，您可以使用預覽[模式](/help/sites-authoring/author-environment-tools.md#page-modes)來預覽頁面。 此模式可讓您進行下列工作：

* 隱藏各種編輯機制，讓您能快速檢視頁面在發佈時的顯示方式。
* 使用連結進行導覽。
* 它&#x200B;**不會**&#x200B;重新整理頁面內容。

製作時，使用頁面編輯器右上角的圖示即可使用預覽模式：

![預覽](assets/chlimage_1-125.png)

### 以已發佈狀態檢視 {#view-as-published}

**以發佈的形式檢視**&#x200B;選項可從[頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information)功能表取得。 這會在新索引標籤中開啟頁面、重新整理內容，並會在發佈頁面時顯示該頁面。

## 鎖定頁面 {#locking-a-page}

AEM可讓您鎖定頁面，不讓其他人修改內容。 當您對某個特定頁面進行大量編輯，或必須凍結頁面一段時間時，此功能會很有用。

您可以透過下列任一方式鎖定頁面：

* **網站**&#x200B;主控台

   1. 選取具有[選取模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)的頁面。
   1. 選取鎖定圖示。

  ![鎖定圖示](assets/screen_shot_2018-03-22at134928.png)

* **頁面編輯器**

   1. 若要開啟功能表，請選取&#x200B;**頁面資訊**&#x200B;圖示。
   1. 選取&#x200B;**鎖定頁面**&#x200B;選項。

鎖定後，主控台檢視資訊會更新；編輯時，工具列會顯示鎖定符號。

![鎖定符號](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>當[模擬使用者](/help/sites-administering/security.md#impersonating-another-user)時，可以執行鎖定頁面。 然而，以這種方式鎖定的頁面只能由被模擬的使用者或管理員使用者解除鎖定。
>
>無法透過模擬鎖定頁面的使用者來解鎖頁面。

## 解鎖頁面 {#unlocking-a-page}

解除鎖定頁麵類似於[鎖定頁面](#locking-a-page)。 鎖定頁面時，鎖定選項會由解鎖動作取代。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![解除鎖定](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>當[模擬使用者](/help/sites-administering/security.md#impersonating-another-user)時，可以執行鎖定頁面。 然而，以這種方式鎖定的頁面只能由被模擬的使用者或管理員使用者解除鎖定。
>
>無法透過模擬鎖定頁面的使用者來解鎖頁面。

## 復原和重做頁面編輯 {#undoing-and-redoing-page-edits}

下列圖示可讓您還原或重做動作。 這些會在適當時顯示在工具列中：

![復原與重做](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>[鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z`也可用於復原頁面編輯動作。
>
>也可使用鍵盤快速鍵`Ctrl-Y`重做頁面編輯動作。

>[!NOTE]
>
>如需復原和重做頁面編輯時可行方法的完整詳細資訊，請參閱[復原和重做頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory)。

## 還原和重做頁面編輯 — 理論 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系統管理員可以根據您執行個體的需求[設定復原/重做功能的各個方面](/help/sites-administering/config-undo.md)。

AEM會儲存您執行動作的歷史記錄，以及您執行動作的順序。 此功能表示您可以依照執行順序復原多個動作，並視需要重做這些動作，以重新套用一或多個動作。

如果選取了內容頁面上的元素（例如文字元件），則復原和重做命令會套用至選取的專案。

復原和重做指令的行為與其他軟體程式中的類似。 在您決定內容時，請使用命令來還原網頁的最近狀態。 例如，如果您將文欄位落移至頁面上的不同位置，您可以使用復原指令將段落移回。 如果之後您認為前一個位置較好，請使用重做指令「復原復原」。

>[!NOTE]
>
>您可以：
>
>* 只要您使用復原後尚未進行頁面編輯，就可以重做動作。
>* 復原最多20個編輯動作（預設設定）。
>* 也使用[鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md)進行還原和重做。
>

您可以對下列型別的頁面變更使用「復原」和「重做」：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上專案

表單元件轉譯的表單欄位不應在編寫頁面時指定值。 因此，「復原」和「重做」指令不會影響您對這些元件型別值所做的變更。 例如，您無法還原在下拉式清單中選取值的作業。

>[!NOTE]
>
>需要特殊許可權才能復原和重做檔案與影像的變更。

>[!NOTE]
>
>檔案和影像的變更記錄至少會持續10小時。 然而，在這段時間之後，變更的逆轉則無法保證。 您的管理員可以變更十小時的預設時間。
