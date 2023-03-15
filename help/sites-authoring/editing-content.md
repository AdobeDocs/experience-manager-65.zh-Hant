---
title: 編輯頁面內容
seo-title: Editing Page Content
description: 建立頁面後，您可以編輯內容以進行所需的更新
seo-description: Once your page is created you can edit the content to make the updates you require
uuid: 5b4f0a8f-5196-42ea-8413-203783a0b77b
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: f92ed674-5865-4a53-8c3a-369536861f14
docset: aem65
exl-id: d5cf4478-51e4-4ca8-b3f8-6d7caed7d515
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3045'
ht-degree: 7%

---

# 編輯頁面內容{#editing-page-content}

建立頁面後（新頁面或作為啟動或即時副本的一部分），您可以編輯內容以進行所需的更新。

使用 [元件](/help/sites-authoring/default-components-console.md) （適合內容類型）拖曳至頁面上。 接著，您就可以就地編輯、移動或刪除這些項目。

>[!NOTE]
>
>您的帳戶需要 [適當的訪問權限](/help/sites-administering/security.md) 和 [權限](/help/sites-administering/security.md#permissions) 來編輯頁面。
>
>如果您遇到任何問題，建議您與系統管理員聯繫。

>[!NOTE]
>
>如果頁面和/或範本已適當設定，則您可以使用 [回應式版面](/help/sites-authoring/responsive-layout.md) 編輯。

>[!NOTE]
>
>登入時 **編輯** 模式，則內容中的連結是可見的，但 **無法存取**. 使用 [預覽模式](#previewingpagestouchoptimizedui) 如果您想使用內容中的連結進行導覽。

## 頁面工具列 {#page-toolbar}

頁面工具列提供對適當功能的存取，視頁面設定而定。

![screen_shot_2018-03-22at111338](assets/screen_shot_2018-03-22at111338.png)

工具列提供許多選項的存取權。 視您目前的內容和設定而定，某些選項可能無法使用。

* **切換側面板**

   這會開啟/關閉保持 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser), [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser)，和 [內容樹](/help/sites-authoring/author-environment-tools.md#content-tree).

   ![](do-not-localize/screen_shot_2018-03-22at111425.png)

* **頁面資訊**

   提供 [頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information) 功能表，包括頁面詳細資訊和可在頁面上採取的動作，包括檢視和編輯頁面資訊、檢視頁面屬性，以及發佈/取消發佈頁面。

   ![](do-not-localize/screen_shot_2018-03-22at111437.png)

* **模擬器**

   切換 [模擬器工具列](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)，可用來模擬其他裝置上頁面的外觀與風格。 這會在版面模式中自動切換。

   ![](do-not-localize/screen_shot_2018-03-22at111442.png)

* **ContextHub**

   開啟 [內容中心](/help/sites-authoring/ch-previewing.md). 僅在「預覽」模式中可用。

   ![screen_shot_2018-03-22at111543](assets/screen_shot_2018-03-22at111543.png)

* **頁面標題**

   這純粹是資訊。

   ![screen_shot_2018-03-22at111554](assets/screen_shot_2018-03-22at111554.png)

* **模式選擇器**

   顯示當前 [模式](/help/sites-authoring/author-environment-tools.md#page-modes) 和可讓您選取其他模式，例如編輯、版面、時間扭曲或鎖定目標。

   ![chlimage_1-120](assets/chlimage_1-120.png)

* **預覽**

   啟用 [預覽模式](/help/sites-authoring/editing-content.md#preview-mode). 這會以發佈時的顯示方式顯示頁面。

   ![chlimage_1-121](assets/chlimage_1-121.png)

* **注釋**

   可讓您新增 [註解](/help/sites-authoring/annotations.md) 檢視頁面時傳回至該頁面。 在第一個批注之後，表徵圖將切換到指示頁面上批注數的數字。

   ![](do-not-localize/screen_shot_2018-03-22at111638.png)

### 狀態通知 {#status-notification}

如果頁面是 [工作流程](/help/sites-authoring/workflows.md) 或多個工作流程時，此資訊會在編輯頁面時顯示在畫面頂端的通知列中。

![screen_shot_2018-03-22at111739](assets/screen_shot_2018-03-22at111739.png)

>[!NOTE]
>
>狀態欄僅對具有適當權限的使用者帳戶可見。

通知會列出針對頁面執行的工作流程。 如果使用者參與目前的工作流程步驟，則選項為 [影響工作流狀態](/help/sites-authoring/workflows-participating.md) 以及取得工作流程的詳細資訊，例如：

* **完成**  — 開啟 **完成工作項目** 對話

* **委派**  — 開啟 **完成工作項目** 對話

* **查看詳細資訊**  — 開啟 **詳細資料** 工作流窗口

透過通知列完成和委派工作流程步驟的運作方式與 [參與工作流程](/help/sites-authoring/workflows-participating.md) 從通知收件匣。

如果頁面受多個工作流程的規範，則通知的右端會顯示工作流程數，並附上箭頭按鈕，讓您捲動工作流程。

![chlimage_1-122](assets/chlimage_1-122.png)

## 元件預留位置 {#component-placeholder}

元件預留位置是一個指標，可在您放置元件時顯示元件的位置 — 位於目前暫留在的元件上方。

* 將新元件新增至頁面時（從元件瀏覽器拖曳）:

   ![screen_shot_2018-03-22at111928](assets/screen_shot_2018-03-22at111928.png)

* 移動現有元件時：

   ![screen_shot_2018-03-22at112445](assets/screen_shot_2018-03-22at112445.png)

## 插入元件 {#inserting-a-component}

### 從元件瀏覽器插入元件 {#inserting-a-component-from-the-components-browser}

您可以使用 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser). 此 [元件預留位置](#component-placeholder) 顯示元件的位置：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-authoring/author-environment-tools.md#page-modes).
1. 開啟 [元件瀏覽器](/help/sites-authoring/author-environment-tools.md#components-browser).
1. 將所需元件拖曳至 [必填職位](#component-placeholder).

1. [編輯](#editmovecopypastedelete) 元件。

>[!NOTE]
>
>在行動裝置上，元件瀏覽器會填入整個畫面。 開始拖曳元件後，瀏覽器會關閉再次顯示頁面，讓您放置元件。

### 從段落系統插入元件 {#inserting-a-component-from-the-paragraph-system}

您可以使用 **拖曳元件至此** 框：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-authoring/author-environment-tools.md#page-modes).
1. 從段落系統中選擇和添加新元件有兩種方式：

   * 選取 **插入元件** 選項(+)，可在現有元件的工具列或 **拖曳元件至此** 框。

   ![screen_shot_2018-03-22at112536](assets/screen_shot_2018-03-22at112536.png)

   * 如果您位於桌上型電腦裝置上，可以連按兩下 **拖曳元件至此** 框。

   此 **插入新元件** 對話方塊將會開啟，供您選取所需元件：

   ![screen_shot_2018-03-22at112650](assets/screen_shot_2018-03-22at112650.png)

1. 選取的元件將新增至頁面底部。 [編輯](#editmovecopypastedelete) 元件（視需要）。

### 使用資產瀏覽器插入元件 {#inserting-a-component-using-the-assets-browser}

您也可以從 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser). 這會自動建立適當類型的新元件（並包含資產）。

這對下列資產類型有效（有些將取決於頁面/段落系統）:

<table>
 <tbody>
  <tr>
   <th><strong>資產類型</strong></th>
   <th><strong>合成元件類型</strong></th>
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
>您可以針對安裝設定此行為。 請參閱 [配置段落系統以便拖動資產可建立元件實例](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 以取得詳細資訊。

若要借由拖曳上述其中一個資產類型來建立元件：

1. 確定您的頁面位於 [**編輯** 模式](/help/sites-authoring/author-environment-tools.md#page-modes).
1. 開啟 [資產瀏覽器](/help/sites-authoring/author-environment-tools.md#assets-browser).
1. 將所需資產拖曳至所需位置。 此 [元件預留位置](#component-placeholder) 顯示元件的位置。

   在所需位置建立與資產類型相適用的元件，其中會包含選取的資產。

1. [編輯](#editmovecopypastedelete) 元件（如有需要）。

>[!NOTE]
>
>在行動裝置上，資產瀏覽器會填滿整個畫面。 開始拖曳資產後，瀏覽器會關閉以再次顯示頁面，讓您放置資產。

如果瀏覽資產時發現您需要快速變更資產，可以啟動 [資產編輯器](/help/assets/manage-assets.md) 按一下資產名稱旁的編輯圖示，即可直接從瀏覽器存取。

![screen_shot_2018-03-22at112735](assets/screen_shot_2018-03-22at112735.png)

## 編輯/設定/複製/剪下/刪除/貼上 {#edit-configure-copy-cut-delete-paste}

選取元件會開啟工具列。 這可讓您存取可在元件上執行的各種動作。

使用者可用的實際動作會視情況顯示，並非此處會說明所有動作。

![screen_shot_2018-03-22at112909](assets/screen_shot_2018-03-22at112909.png)

* **編輯**

   [取決於元件類型](/help/sites-authoring/default-components.md) 這可讓您 [編輯元件的內容](#edit-content). 通常會提供工具列。

   ![](do-not-localize/screen_shot_2018-03-22at112936.png)

* **設定**

   [取決於元件類型](/help/sites-authoring/default-components.md) 這可讓您編輯和設定元件的屬性。 通常會開啟對話。

   ![](do-not-localize/screen_shot_2018-03-22at112955.png)

* **複製**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將會保留。

   ![](do-not-localize/screen_shot_2018-03-22at113000.png)

* **剪下**

   這會將元件複製到剪貼簿。 貼上動作後，原始元件將會移除。

   ![screen_shot_2018-03-22at113007](assets/screen_shot_2018-03-22at113007.png)

* **刪除**

   這會從含有您確認的頁面中刪除元件。

   ![](do-not-localize/screen_shot_2018-03-22at113012.png)

* **插入元件**

   這會開啟對話方塊 [新增元件](/help/sites-authoring/editing-content.md#inserting-a-component-from-the-paragraph-system).

   ![](do-not-localize/screen_shot_2018-03-22at113017.png)

* **貼上**

   這會將剪貼簿中的元件貼到頁面。 原始檔案是否保留，取決於您是使用複製還是剪切。

   * 您可以貼到相同的頁面或不同的頁面。
   * 貼上的項目會貼到您選取貼上動作的項目上方。
   * 只有剪貼簿上有內容時，才會顯示「貼上」動作。

   ![screen_shot_2018-03-22at113553](assets/screen_shot_2018-03-22at113553.png)

   >[!NOTE]
   >
   >如果您貼到剪下/復製作業前已開啟的其他頁面，則必須重新整理頁面才能查看貼上的內容。

* **群組**

   這可讓您一次選取多個元件。 在案頭裝置上，可透過 **按住Ctrl鍵並按一下** 或 **按住Command鍵並按一下**.

   ![](do-not-localize/screen_shot_2018-03-22at113240.png)

* **父級**

   可讓您選取所選元件的父元件。

   ![screen_shot_2018-03-22at113028](assets/screen_shot_2018-03-22at113028.png)

* **配置**

   這可讓您修改 [配置](/help/sites-authoring/editing-content.md#edit-component-layout) 的子句。 這只會套用至選取的元件，不會啟動 [版面模式](/help/sites-authoring/author-environment-tools.md#page-modes) 的URL。

   ![](do-not-localize/screen_shot_2018-03-22at113044.png)

* **轉換為體驗片段變數**

   這可讓您建立新 [體驗片段](/help/sites-authoring/experience-fragments.md) 從選取的元件，或將其新增至現有的體驗片段。

   ![](do-not-localize/screen_shot_2018-03-22at113033.png)

## 編輯（內容） {#edit-content}

在元件中新增和/或編輯內容有兩種方法：

* 開啟 [編輯元件對話方塊](#component-edit-dialog).
* [拖放資產](#draganddropintocomponent) 從「資產」瀏覽器直接新增內容。

### 元件編輯對話方塊 {#component-edit-dialog}

您可以使用元件工具列的「編輯 (鉛筆) 」圖示， [開啟元件以編輯內容](#edit-configure-copy-cut-delete-paste)。

確切的編輯選項取決於元件。 某些元件 [所有動作將僅可在全螢幕模式中使用](#edit-content-full-screen-mode). 例如：

* [文字元件](/help/sites-authoring/rich-text-editor.md#main-pars-title-24)

   ![screen_shot_2018-03-22at120215](assets/screen_shot_2018-03-22at120215.png)

* 影像元件

   ![screen_shot_2018-03-22at120252](assets/screen_shot_2018-03-22at120252.png)

   >[!NOTE]
   >
   >編輯在空白的影像元件上無法運作。
   >
   >
   >您必須 [拖曳或上傳影像（使用設定）](/help/sites-authoring/default-components-foundation.md#image) 開始編輯它之前。

* 影像元件 — 全螢幕

   [進入影像元件的全螢幕模式](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode) ，可讓您有更多空間編輯影像，並顯示額外的編輯選項，例如「啟動地圖」和「重設縮放」 ********。此外，全螢幕還允許選取裁切預設集。

   ![screen_shot_2018-03-22at120529](assets/screen_shot_2018-03-22at120529.png)

* 由多個基本元件(如 [文字與影像基礎元件](/help/sites-authoring/default-components-foundation.md#text-image)，首先請您確認您要的編輯選項集：

   ![chlimage_1-123](assets/chlimage_1-123.png)

### 將資產拖放至元件 {#drag-and-drop-assets-into-component}

對於特定元件類型，您可以將資產從資產瀏覽器直接拖放至元件中，以更新內容：

| **資產類型** | **元件類型** |
|---|---|
| 影像 | 影像 |
| 文件 | 下載 |
| 產品 | 產品 |
| 影片 | 閃光燈 |
| 內容片段 | 內容片段 |

## 編輯（內容）全螢幕模式 {#edit-content-full-screen-mode}

對於所有元件，可使用（並從中退出）存取全螢幕模式：

![](do-not-localize/chlimage_1-20.png)

例如， **文字** 元件：

![screen_shot_2018-03-22at121616](assets/screen_shot_2018-03-22at121616.png)

>[!NOTE]
>
>對於某些元件，全螢幕模式比基本就地編輯器有更多可用選項。

## 移動元件 {#moving-a-component}

要移動段落元件，請執行以下操作：

1. 選擇要用點選並按住或按住移動的段落。
1. 將段落拖動到新位置。 AEM表示可以將段落保存的位置。 將其放置在您想要的位置。

   ![screen_shot_2018-03-22at121821](assets/screen_shot_2018-03-22at121821.png)

1. 您的段落被移動。

>[!NOTE]
>
>您也可以使用 [剪下並貼上](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) 來移動元件。

## 編輯元件配置 {#edit-component-layout}

您可以選取元件的 [Layout](/help/sites-authoring/responsive-layout.md)****  (配置) 動作，以變更元件的配置，並節省時間，而不需離開編輯模式，而不需重複從編輯切換到配置模式來調整元件。

1. 登入時 **編輯** 在sites控制台的模式下，選擇元件會顯示元件的工具欄。

   ![screen_shot_2018-03-22at133756](assets/screen_shot_2018-03-22at133756.png)

   按一下或點選 **版面** 動作來調整元件的版面。

   ![](do-not-localize/chlimage_1-21.png)

1. 選取「配置」動作後：

   * 元件顯示的調整手柄大小。
   * 模擬器工具欄顯示在螢幕頂部。
   * 配置操作（而不是標準編輯操作）將顯示在元件工具欄上。

   ![screen_shot_2018-03-22at133843](assets/screen_shot_2018-03-22at133843.png)

   您現在可以修改元件的版面，如同在 [配置模式](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

1. 進行必要的配置變更後，按一下 **關閉** 按鈕，停止修改元件的佈局。 元件的工具列會恢復為正常編輯狀態。

   ![](do-not-localize/screen_shot_2018-03-22at133920.png)

>[!NOTE]
>
>「佈局」(Layout)操作的範圍僅限於所選元件。 例如，如果編輯一個元件的佈局，然後按一下另一個元件，則新選元件的標準編輯工具欄（而不是佈局工具欄）將顯示，重新調整控制滑塊和模擬器工具欄將消失。
>
>如果您需要編輯頁面的整體版面，並影響到多個元件，請切換至 [配置模式](/help/sites-authoring/responsive-layout.md).

## 繼承的元件 {#inherited-components}

繼承的元件可以是各種情況的產品，包括：

* [多網站管理](/help/sites-administering/msm.md)
* [啟動](/help/sites-authoring/launches.md) （根據即時副本時）。
* 特定元件，如Geometrixx內的繼承段落系統。

您可以取消（然後重新啟用）繼承。 視元件而定，這可從下列位置取得：

* **Live Copy**

   元件工具列（如果元件位於屬於即時副本或啟動的頁面上）。 例如：

   ![screen_shot_2018-03-22at134339](assets/screen_shot_2018-03-22at134339.png)

   取消繼承選項可用：

   ![](do-not-localize/screen_shot_2018-03-22at134406.png)

   或者，如果已取消，則重新啟用繼承：

   ![](do-not-localize/screen_shot_2018-03-22at134417.png)

   Blueprint或Live Copy來源中也提供「轉出」動作：

   ![](do-not-localize/screen_shot_2018-03-22at134516.png)

* **繼承的段落制度**

   配置對話框。 例如，與繼承段落系統一樣：

   ![chlimage_1-124](assets/chlimage_1-124.png)

## 編輯頁面範本 {#editing-the-page-template}

如果頁面是根據 [可編輯的範本](/help/sites-authoring/templates.md#editable-and-static-templates)，您可以輕鬆切換至 [範本編輯器](/help/sites-authoring/templates.md#editing-templates-template-authors) 選取 **編輯範本** 在 [頁面資訊功能表](/help/sites-authoring/author-environment-tools.md#page-information).

如果頁面是根據 [靜態範本](/help/sites-authoring/templates.md#editable-and-static-templates)，您可以 [設計模式](/help/sites-authoring/default-components-designmode.md) 使用 [頁面模式選取器](/help/sites-authoring/author-environment-tools.md#page-modes) 啟用/停用要在頁面上使用的元件。

在「欄檢視」或「清單檢視」中選取頁面時，您可輕鬆查看該頁 [面所依據](/help/sites-authoring/basic-handling.md#column-view)[的範本](/help/sites-authoring/basic-handling.md#list-view)。

## 即時副本狀態 {#live-copy-status}

此 [「即時副本狀態」頁面模式](/help/sites-authoring/author-environment-tools.md#page-modes) 可讓您快速概述即時副本狀態，以及繼承/不繼承哪些元件：

* 綠色邊框：繼承
* 粉紅色邊框：已取消繼承

例如：

![screen_shot_2018-03-22at134820](assets/screen_shot_2018-03-22at134820.png)

## 新增註解 {#adding-annotations}

[註解](/help/sites-authoring/annotations.md) 可讓審核者和其他作者提供您內容的意見反應。 它們通常用於審核和驗證目的。

## 預覽頁面 {#previewing-pages}

預覽頁面有兩個選項：

* [預覽模式](#preview-mode)  — 快速就地預覽

* [檢視為已發佈](#view-as-published)  — 在新索引標籤中開啟頁面的完整預覽

>[!NOTE]
>
>* 內容中的連結是可見的，但在「編輯」模式中無法存取。
>* 如果您想使用連結來導覽，請使用其中一個預覽選項。
>* 使用 [鍵盤快捷鍵](/help/sites-authoring/keyboard-shortcuts.md) `Ctrl-Shift-M` 在預覽模式和上次選取模式之間切換。
>


>[!NOTE]
>
>已針對這兩個選項設定WCM模式Cookie。

### 預覽模式 {#preview-mode}

編輯內容時，您可以使用預覽來預覽頁面 [模式](/help/sites-authoring/author-environment-tools.md#page-modes). 此模式：

* 隱藏各種編輯機制，讓您快速檢視頁面在發佈時的顯示方式。
* 可讓您使用連結進行導覽。
* 是 **not** 重新整理頁面內容。

編寫時，可使用頁面編輯器右上角的圖示來使用預覽模式：

![chlimage_1-125](assets/chlimage_1-125.png)

### 以已發佈狀態檢視 {#view-as-published}

此 **檢視為已發佈** 選項 [頁面資訊](/help/sites-authoring/author-environment-tools.md#page-information) 功能表。 這會在新索引標籤中開啟頁面，重新整理內容，並依照發佈環境中的顯示方式顯示頁面。

## 鎖定頁面 {#locking-a-page}

AEM可讓您鎖定頁面，讓其他人都無法修改內容。 當您對特定頁面進行許多編輯，或需要將頁面凍結一段時間時，這個功能會很實用。

可從以下任一位置鎖定頁面：

* **網站** 主控台

   1. 選擇具有 [選擇模式](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources).
   1. 選取鎖定圖示。

   ![screen_shot_2018-03-22at134928](assets/screen_shot_2018-03-22at134928.png)

* **頁面編輯器**

   1. 選取 **頁面資訊** 圖示以開啟功能表。
   1. 選取 **鎖定頁面** 選項。

鎖定後，控制台視圖資訊會更新，編輯鎖定符號時，工具欄中會顯示。

![screen_shot_2018-03-22at135010](assets/screen_shot_2018-03-22at135010.png)

>[!CAUTION]
>
>鎖定頁面時， [模擬使用者](/help/sites-administering/security.md#impersonating-another-user). 不過，以此方式鎖定的頁面，只能由模擬的使用者或管理員使用者解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。

## 解鎖頁面 {#unlocking-a-page}

解鎖頁面非常類似 [鎖定頁面](#locking-a-page). 鎖定頁面後，鎖定選項會由解除鎖定動作取代。

「頁面資訊」功能表 **會列出** 「解除鎖定」為選項，而網站主控台中的「鎖定」圖示會以「解除鎖定」圖示 **** 取代。

![screen_shot_2018-03-22at134942](assets/screen_shot_2018-03-22at134942.png)

>[!CAUTION]
>
>鎖定頁面時， [模擬使用者](/help/sites-administering/security.md#impersonating-another-user). 不過，以此方式鎖定的頁面，只能由模擬的使用者或管理員使用者解除鎖定。
>
>無法通過模擬鎖定頁面的用戶來解除鎖定頁面。

## 撤消和重新執行頁面編輯 {#undoing-and-redoing-page-edits}

下列圖示可讓您還原或重做動作。 這些在適當時會顯示在工具列中：

![](do-not-localize/screen_shot_2018-03-23at093614.png)

>[!NOTE]
>
>此 [鍵盤快捷鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) `Ctrl-Z` 也可用來還原頁面編輯動作。
>
>鍵盤快速鍵 `Ctrl-Y` 也可用於重做頁面編輯動作。

>[!NOTE]
>
>請參閱 [還原和重做頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory) 以取得還原和重新執行頁面編輯時可能進行的完整詳細資訊。

## 還原和重做頁面編輯 — 理論 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系統管理員可以 [設定還原/重做功能的各個方面](/help/sites-administering/config-undo.md) 根據您執行個體的需求。

AEM會儲存您所執行動作的歷史記錄，以及執行動作的順序，讓您可以依照執行動作的順序還原多個動作，並視需要重做以重新套用一或多個動作。

如果選取了內容頁面上的元素（例如文字元件），則還原和重做命令會套用至選取的項目。

撤消和重做命令的行為與其他軟體程式中的行為類似。 在您決定內容時，可使用命令還原網頁的最近狀態。 例如，如果將文本段落移動到頁面上的其他位置，則可以使用撤消命令將段落移回。 如果您接著決定上一個位置較好，請使用重做命令來「還原」。

>[!NOTE]
>
>您可以：
>
>* 只要您自使用還原功能後未進行頁面編輯，就重做動作。
>* 最多可還原20個編輯動作（預設設定）。
>* 也使用 [鍵盤快速鍵](/help/sites-authoring/page-authoring-keyboard-shortcuts.md) 以還原和重做。
>


您可以對下列類型的頁面變更使用還原和重做：

* 添加、編輯、刪除和移動段落
* 就地編輯段落內容
* 複製、剪下和貼上頁面中的項目

表單元件轉譯的表單欄位在編寫頁面時無法指定值。 因此，撤消和重做命令不會影響您對這些類型元件的值所做的更改。 例如，您無法還原下拉式清單中選取值的作業。

>[!NOTE]
>
>若要還原和重做檔案和影像的變更，需要特殊權限。

>[!NOTE]
>
>檔案和影像的變更記錄至少會持續10小時。 但是，在此之後，變更的還是無法保證。 管理員可以更改10小時的預設時間。
