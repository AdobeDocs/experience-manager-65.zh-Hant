---
title: 編輯頁面內容
description: 使用可拖曳至頁面的元件來新增內容。 接著，您就可以就地編輯、移動或刪除這些專案。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 2%

---

# 編輯頁面內容{#editing-page-content}

建立頁面後（新頁面或作為啟動項或即時副本的一部分），您可以編輯內容以進行所需的更新。

使用可拖曳至頁面的[元件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md) （適合內容型別）新增內容。 接著，您就可以就地編輯、移動或刪除這些專案。

>[!NOTE]
>
>您的帳戶需要[適當的存取權](/help/sites-administering/security.md)和[許可權](/help/sites-administering/security.md#permissions)才能編輯頁面；例如，新增、編輯或刪除元件、加上註解、解除鎖定。
>
>如果您遇到任何問題，我們建議您連絡系統管理員。

## Sidekick {#sidekick}

sidekick是編寫頁面時的關鍵工具。 它會在編寫頁面時浮動，所以一律可見。

有數個索引標籤和圖示可供使用，包括：

* 元件
* 頁面
* 資訊
* 版本設定
* 工作流程
* 模式
* 支架
* ClientContext
* 網站

![chlimage_1-71](assets/chlimage_1-71.png)

這些模組可讓您存取廣泛的功能選擇；包括：

* [選取元件](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [顯示引用](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [存取稽核記錄](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [切換模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [正在建立](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)，[正在還原](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick)和[比較](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version)個版本

* [發佈](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)，[取消發佈](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page)頁面

* [編輯頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [支架](/help/sites-authoring/scaffolding.md)

* [使用者端內容](/help/sites-administering/client-context.md)

## 插入元件 {#inserting-a-component}

### 插入元件 {#inserting-a-component-1}

開啟頁面後，您可以開始新增內容。 若要這麼做，請新增元件（也稱為段落）。

要插入新元件：

1. 選取要插入的段落型別的方法有幾種：

   * 按兩下標示為&#x200B;**將元件或資產拖曳到這裡……**&#x200B;的區域 — **插入新元件**&#x200B;工具列開啟。 選取元件並按一下&#x200B;**確定**。

   * 從浮動工具列拖曳元件（稱為sidekick）以插入新段落。
   * 以滑鼠右鍵按一下現有段落並選取&#x200B;**新增……** — 「插入新元件」工具列開啟。 選取元件並按一下&#x200B;**確定**。

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. 在sidekick和&#x200B;**插入新元件**&#x200B;工具列中您會看到可用元件（段落型別）的清單。 這些區段可以分成不同的區段（例如，「一般」、「欄」等），可視需要加以展開。

   視您的生產環境而定，這些選項可能會有所不同。 如需元件的完整詳細資訊，請參閱[預設元件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)。

1. 在頁面上插入您想要的元件。 然後按兩下段落，就會開啟一個視窗，讓您設定段落並新增內容。

### 使用內容尋找器插入元件 {#inserting-a-component-using-the-content-finder}

您也可以從[內容尋找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)拖曳資產，將新元件新增至頁面。 這樣會自動建立包含資產的適當型別的元件。

這適用於下列資產型別（部分將取決於頁面/段落系統）：

| 資產類型 | 產生的元件型別 |
|---|---|
| 影像 | 影像 |
| 文件 | 下載 |
| 產品 | 產品 |
| 影片 | 閃光燈 |

>[!NOTE]
>
>您可針對您的安裝設定此行為。 如需詳細資訊，請參閱[設定段落系統，以便拖曳資產建立元件執行個體](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance)。

若要拖曳上述任一資產型別來建立元件：

1. 確定您的頁面處於&#x200B;[**編輯**&#x200B;模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)。
1. 開啟[內容尋找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)。
1. 將所需的資產拖曳至所需的位置。 [元件預留位置](#componentplaceholder)顯示元件將放置的位置。

   適合資產型別的元件將在所需位置建立 — 它將包含所選資產。

1. 如有必要，請[編輯](#editmovecopypastedelete)元件。

## 編輯元件（內容和屬性） {#editing-a-component-content-and-properties}

若要編輯現有段落，請執行下列任一項動作：

* **按兩下**&#x200B;該段落以開啟。 您會看到與使用現有內容建立段落時相同的視窗。 進行變更，然後按一下[確定]。****

* **在段落上按一下滑鼠右鍵**，然後按一下&#x200B;**編輯**。

* **在段落上按兩下**&#x200B;兩次（緩慢連按兩下）以進入就地編輯模式。 您將能夠直接編輯頁面上的文字，而不是在對話方塊視窗內。 在此模式中，頁面頂端會提供工具列。 只需進行變更，系統就會自動儲存變更。

## 移動元件 {#moving-a-component}

若要移動段落：

>[!NOTE]
>
>您也可以使用[剪下並貼上](#cut-copy-paste-a-component)來移動元件。

1. 選取要移動的段落：

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 將段落拖曳至新位置 — AEM會以綠色核取記號指出可將段落移動到的位置。 將其拖曳至所需位置。
1. 此時會移動您的段落：

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## 刪除元件 {#deleting-a-component}

若要刪除段落：

1. 選取段落並&#x200B;**按一下滑鼠右鍵**：

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 從功能表中選取&#x200B;**刪除**。 AEM WCM會要求確認您要刪除段落，因為此動作無法復原。
1. 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>如果您已將[使用者屬性設定為顯示全域編輯工具列](/help/sites-classic-ui-authoring/author-env-user-props.md)，您也可使用可用的&#x200B;**複製**、**剪下**、**貼上**、**刪除**&#x200B;按鈕，對段落執行某些動作。
>
>也提供各種[鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。

## 剪下/複製/貼上元件 {#cut-copy-paste-a-component}

如同在[刪除元件](#deleting-a-component)時一樣，您可以使用內容功能表來複製、剪下和/或貼上元件

>[!NOTE]
>
>如果您已將[使用者屬性設定為顯示全域編輯工具列](/help/sites-classic-ui-authoring/author-env-user-props.md)，您也可使用可用的&#x200B;**複製**、**剪下**、**貼上**、**刪除**&#x200B;按鈕，對段落執行某些動作。
>
>也提供各種[鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。

>[!NOTE]
>
>僅支援在同一頁面中剪下、複製和貼上內容。

## 繼承元件 {#inherited-components}

繼承的元件可能是各種情況的產物，包括：

* [多網站管理](/help/sites-administering/msm.md)；同時搭配[支架](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance)。

* [啟動](/help/sites-classic-ui-authoring/classic-launches.md) （當以Livecopy為基礎時）。
* 特定元件；例如Geometrixx中的繼承段落系統。

您可以取消（然後重新啟用）繼承。 此功能可從以下來源取得（視元件而定）：

1. **即時副本**

   如果元件屬於livecopy或launch的一部分，則會以掛鎖圖示表示。 您可以按一下掛鎖來取消繼承。

   * 選取元件時，掛鎖圖示隨即顯示；例如：

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * 掛鎖也會顯示在元件的對話方塊中；例如：

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **繼承的段落系統**

   設定對話方塊。 例如，如同Geometrixx中的繼承段落系統：

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 新增註解 {#adding-annotations}

[註解](/help/sites-classic-ui-authoring/classic-page-author-annotations.md)可讓其他作者針對您的內容提供意見回饋。 這通常用於稽核和驗證目的。

## 預覽頁面 {#previewing-pages}

Sidekick的底部邊框中有兩個圖示對預覽頁面很重要：

![Sidekick的下框線，水準列有7個圖示。 列開頭的兩個圖示（編輯圖示和預覽模式圖示）分別以鉛筆符號和放大鏡符號表示。](do-not-localize/chlimage_1-5.png)

* 鉛筆圖示會顯示您目前處於編輯模式，您可以在此新增、修改、移動或刪除內容。

  ![以鉛筆符號表示的編輯圖示。](do-not-localize/chlimage_1-6.png)

* 放大鏡圖示可讓您選取預覽模式，其中頁面會顯示在發佈環境中（有時也需要重新整理頁面）：

  ![以放大鏡符號表示的預覽模式圖示。](do-not-localize/chlimage_1-7.png)

  在預覽模式中，sidekick將會減少，按一下向下箭頭圖示以返回編輯模式：

  ![以AEM為標題的列，在標題右邊有一個編輯模式圖示，以向下箭頭符號表示。](do-not-localize/chlimage_1-8.png)

## 尋找和取代 {#find-replace}

若要對相同片語進行更大規模的編輯，**[尋找和取代](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)**&#x200B;功能表選項可讓您在網站的某個區段中搜尋和取代字串的多個執行個體。

## 鎖定頁面 {#locking-a-page}

AEM可讓您鎖定頁面，不讓其他人變更內容。 當您對某個特定頁面進行大量編輯，或需要凍結頁面一段時間時，此功能會很有用。

>[!CAUTION]
>
>在鎖定頁面時，應謹慎使用，因為唯一可以解鎖頁面的人是鎖定頁面的人（或具有管理員許可權的帳戶）。

若要鎖定頁面：

1. 在&#x200B;**網站**&#x200B;索引標籤中，選取您要鎖定的頁面。
1. 連按兩下頁面以開啟頁面進行編輯。
1. 在sidekick的&#x200B;**頁面**&#x200B;標籤中，選取&#x200B;**鎖定頁面**：

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   訊息會顯示您的頁面已鎖定給其他使用者。 此外，在&#x200B;**網站**&#x200B;主控台的右窗格中，AEM WCM會將頁面顯示為已鎖定，並指出已鎖定頁面的使用者。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## 解鎖頁面 {#unlocking-a-page}

若要解除鎖定頁面：

1. 在&#x200B;**網站**&#x200B;索引標籤中，選取您要解除鎖定的頁面。
1. 連按兩下頁面以開啟。
1. 在sidekick的&#x200B;**頁面**&#x200B;索引標籤中，選取&#x200B;**解鎖頁面**。

## 復原和重做頁面編輯 {#undoing-and-redoing-page-edits}

當頁面的內容框架具有焦點時，請使用下列鍵盤快速鍵：

* 還原：Ctrl+Z (Windows)或Cmd+Z (Mac)
* 重做：Ctrl+Y (Windows)或Cmd+Y (Mac)

當您復原或重做一個或多個段落的移除、增加或重新定位時，閃爍（預設行為）的醒目提示會指出受影響的段落。

>[!NOTE]
>
>如需復原和重做頁面編輯時可行方法的完整詳細資訊，請參閱[復原和重做頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory)。

## 還原和重做頁面編輯 — 理論 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系統管理員可以根據您執行個體的需求[設定復原/重做功能的各個方面](/help/sites-administering/config-undo.md)。

AEM會儲存您執行之動作的歷史記錄，以及您執行動作的順序。 因此，您可以依照執行順序復原數個動作。 接著，您可以使用重做來重新套用一或多個動作。

如果選取了內容頁面上的元素，則復原和重做指令會套用至選取的專案，例如文字元件。

復原和重做指令的行為與其他軟體程式中的類似。 在您決定內容時，請使用命令來還原網頁的最近狀態。 例如，如果您將文欄位落移至頁面上的不同位置，您可以使用復原指令將段落移回。 如果您隨後再次決定移動段落，請使用重做指令。

>[!NOTE]
>
>您可以：
>
>* 只要您使用復原後尚未進行頁面編輯，就可以重做動作。
>* 最多可復原20個編輯動作（預設設定）。
>* 也使用[鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)進行還原和重做。
>

您可以對下列型別的頁面變更使用還原和重做：

* 新增、編輯、移除和移動段落
* 就地編輯段落內容
* 在頁面中複製、剪下和貼上專案
* 跨頁面複製、剪下和貼上專案
* 新增、移除和變更檔案與影像
* 新增、移除和變更註釋和草繪
* 支架的變更
* 新增和移除參照
* 變更元件對話方塊中的屬性值。

表單元件轉譯的表單欄位不應在編寫頁面時指定值。 因此，「復原」和「重做」指令不會影響您對這些元件型別值所做的變更。 例如，您無法還原在下拉式清單中選取值的作業。

>[!NOTE]
>
>需要特殊許可權才能復原和重做檔案與影像的變更。 此外，復原檔案和影像變更的歷史記錄至少會持續數小時。 然而，在這段時間之後，變更的復原則無法保證。 您的管理員可提供許可權並變更十小時的預設時間。
