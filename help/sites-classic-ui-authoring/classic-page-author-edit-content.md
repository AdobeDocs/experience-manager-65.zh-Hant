---
title: 編輯頁面內容
seo-title: 編輯頁面內容
description: 使用可拖曳至頁面上的元件來新增內容。 接著，您就可以就地編輯、移動或刪除這些項目。
seo-description: 使用可拖曳至頁面上的元件來新增內容。 接著，您就可以就地編輯、移動或刪除這些項目。
uuid: e7b65ceb-263c-46f2-91e3-11dec3a016fa
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: de321869-ebf9-41a1-8203-e12bdb088678
docset: aem65
exl-id: e1b5aea0-983c-4e7b-9d35-d7beeee45dc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1780'
ht-degree: 1%

---

# 編輯頁面內容{#editing-page-content}

建立頁面後（新頁面或作為啟動或即時副本的一部分），您可以編輯內容以進行所需的更新。

使用可拖曳至頁面的[元件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)（適合內容類型）來新增內容。 接著，您就可以就地編輯、移動或刪除這些項目。

>[!NOTE]
>
>您的帳戶需要[適當的存取權限](/help/sites-administering/security.md)和[權限](/help/sites-administering/security.md#permissions)才能編輯頁面；例如，添加、編輯或刪除元件、批注、解鎖。
>
>如果您遇到任何問題，建議您與系統管理員聯繫。

## Sidekick {#sidekick}

製作頁面時，sidekick是重要工具。 編寫頁面時會浮動，因此一律可見。

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

這些功能提供了對多種功能的訪問；包括：

* [選擇元件](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [顯示參考](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [訪問審核日誌](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [切換模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* [建立](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)、還 [](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick) 原和比 [](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version) 較

* [發佈](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)、取消 [](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page) 發佈頁面

* [編輯頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [支架](/help/sites-authoring/scaffolding.md)

* [用戶上下文](/help/sites-administering/client-context.md)

## 插入元件{#inserting-a-component}

### 插入元件{#inserting-a-component-1}

開啟頁面後，您可以開始新增內容。 若要這麼做，請新增元件（也稱為段落）。

插入新元件：

1. 選擇要插入的段落類型的方法有幾種：

   * 連按兩下標示為&#x200B;**將元件或資產拖曳到此處……** — 將開啟&#x200B;**插入新元件**&#x200B;工具欄。 選擇元件並按一下&#x200B;**確定**。

   * 從浮動工具列拖曳元件（稱為sidekick）以插入新段落。
   * 按一下右鍵現有段落，然後選擇&#x200B;**新建……** — 「插入新元件」工具欄開啟。 選擇元件並按一下&#x200B;**確定**。

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. 在sidekick和&#x200B;**插入新元件**&#x200B;工具列中，您會看到可用元件的清單（段落類型）。 這些區段可分為不同區段（例如一般、欄等），可視需要展開。

   這些選項可能會因您的生產環境而異。 有關元件的完整詳細資訊，請參閱[預設元件](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)。

1. 在頁面上插入您要的元件。 然後按兩下段落，將開啟一個窗口，允許您配置段落並添加內容。

### 使用內容查找器{#inserting-a-component-using-the-content-finder}插入元件

您也可以從[內容尋找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)拖曳資產，將新元件新增至頁面。 這會自動建立包含資產之適當類型的新元件。

這對下列資產類型有效（有些將取決於頁面/段落系統）:

| 資產類型 | 合成元件類型 |
|---|---|
| 影像 | 影像 |
| 文件 | 下載 |
| 產品 | 產品 |
| 影片 | 閃光燈 |

>[!NOTE]
>
>您可以針對安裝設定此行為。 如需詳細資訊，請參閱[設定段落系統，以便拖曳資產會建立元件例項](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance) 。

若要借由拖曳上述其中一個資產類型來建立元件：

1. 請確定您的頁面處於&#x200B;[**Edit**&#x200B;模式](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)。
1. 開啟[內容尋找器](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)。
1. 將所需資產拖曳至所需位置。 [元件佔位符](#componentplaceholder)顯示元件的位置。

   在所需位置建立與資產類型相適用的元件，其中會包含選取的資產。

1. [](#editmovecopypastedelete) 視需要編輯元件。

## 編輯元件（內容和屬性）{#editing-a-component-content-and-properties}

要編輯現有段落，請執行以下操作之一：

* **按兩下** 段落以開啟它。您會看到與使用現有內容建立段落時相同的窗口。 進行更改，然後按一下&#x200B;**OK**。

* **以滑鼠右鍵** 按一下段落，然後按一 **下編輯**。

* **** 按兩下段落（按兩下滑鼠即可進入就地編輯模式）。您將能直接編輯頁面上的文字，而非在對話方塊視窗內。 在此模式中，頁面頂端會提供工具列。 只需進行變更，系統就會自動儲存。

## 移動元件{#moving-a-component}

要移動段落：

>[!NOTE]
>
>您也可以使用[剪下並貼上](#cut-copy-paste-a-component)來移動元件。

1. 選擇要移動的段落：

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 將段落拖曳到新位置 — AEM表示可以使用綠色勾號將段落移至的位置。 將其放置在您想要的位置。
1. 已移動您的段落：

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## 刪除元件{#deleting-a-component}

要刪除段落：

1. 選擇段落，然後按一下右鍵&#x200B;**:**

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. 從菜單中選擇&#x200B;**Delete**。 AEM WCM會要求確認您要刪除該段落，因為此動作無法復原。
1. 按一下&#x200B;**「確定」**。

>[!NOTE]
>
>如果已將[用戶屬性設定為顯示全局編輯工具欄](/help/sites-classic-ui-authoring/author-env-user-props.md)，則還可以使用&#x200B;**Copy**、**Cut**、**Paste**、**Delete**&#x200B;按鈕對段落執行某些操作。
>
>也提供各種[鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。

## 剪下/複製/貼上元件{#cut-copy-paste-a-component}

與[刪除元件](#deleting-a-component)時一樣，您可以使用上下文菜單來複製、剪切和/或貼上元件

>[!NOTE]
>
>如果已將[用戶屬性設定為顯示全局編輯工具欄](/help/sites-classic-ui-authoring/author-env-user-props.md)，則還可以使用&#x200B;**Copy**、**Cut**、**Paste**、**Delete**&#x200B;按鈕對段落執行某些操作。
>
>也提供各種[鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)。

>[!NOTE]
>
>剪下、複製和貼上內容僅支援在同一頁內。

## 繼承的元件{#inherited-components}

繼承的元件可以是各種情況的產品，包括：

* [多站點管理](/help/sites-administering/msm.md);也與支架結 [合](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance)。

* [啟動](/help/sites-classic-ui-authoring/classic-launches.md) （根據LiveCopy時）。
* 特定元件；例如Geometrixx內的繼承段落系統。

您可以取消（然後重新啟用）繼承。 視元件而定，這可從下列位置取得：

1. **即時副本**

   如果元件是Live Copy或啟動的一部分，則會以掛鎖圖示表示。 您可以按一下掛鎖來取消繼承。

   * 選取元件時，掛鎖圖示會隨即顯示；例如：

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * 掛鎖也顯示在元件對話方塊中；例如：

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **繼承的段落制度**

   配置對話框。 例如，與Geometrixx內的繼承段落系統一樣：

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 添加註釋{#adding-annotations}

[](/help/sites-classic-ui-authoring/classic-page-author-annotations.md) 附註請其他作者提供您內容的意見反應。這通常用於檢閱和驗證用途。

## 預覽頁面{#previewing-pages}

Sidekick的底邊有兩個圖示，這對預覽頁面很重要：

![](do-not-localize/chlimage_1-5.png)

* 鉛筆圖示會顯示您目前處於編輯模式，可在此新增、修改、移動或刪除內容。

   ![](do-not-localize/chlimage_1-6.png)

* 放大鏡圖示可讓您選取預覽模式，在此顯示頁面，就像在發佈環境中看到頁面一樣（有時也需要重新整理頁面）:

   ![](do-not-localize/chlimage_1-7.png)

   在預覽模式中，sidekick將會減少，按一下向下箭頭圖示即可返回編輯模式：

   ![](do-not-localize/chlimage_1-8.png)

## 尋找和取代 {#find-replace}

若要更大規模地編輯相同片語，可使用&#x200B;**[尋找和取代](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)**&#x200B;功能表選項，在網站的某個區段內搜尋和取代字串的多個例項。

## 鎖定頁面{#locking-a-page}

AEM可讓您鎖定頁面，讓其他人無法修改內容。 當您對特定頁面進行許多編輯，或需要將頁面凍結一段時間時，這個功能會很實用。

>[!CAUTION]
>
>鎖定頁面時應謹慎使用，因為唯一能夠解除鎖定頁面的人是鎖定頁面的人（或具有管理員權限的帳戶）。

若要鎖定頁面：

1. 在&#x200B;**網站**&#x200B;標籤中，選取您要鎖定的頁面。
1. 連按兩下頁面以開啟頁面進行編輯。
1. 在sidekick的&#x200B;**Page**&#x200B;標籤中，選擇&#x200B;**Lock Page**:

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   訊息會顯示您的頁面已鎖定給其他使用者。 此外，在&#x200B;**Websites**&#x200B;控制台的右窗格中，AEM WCM將頁面顯示為已鎖定，並指示已鎖定該頁面的用戶。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## 解鎖頁面{#unlocking-a-page}

解除鎖定頁面：

1. 在&#x200B;**網站**&#x200B;標籤中，選擇要解鎖的頁面。
1. 連按兩下頁面以開啟它。
1. 在sidekick的&#x200B;**Page**&#x200B;標籤中，選擇&#x200B;**解除鎖定頁面**。

## 撤消和重新執行頁面編輯{#undoing-and-redoing-page-edits}

當頁面的內容框架有焦點時，請使用以下鍵盤快速鍵：

* 還原：Ctrl+Z(Windows)或Cmd+Z(Mac)
* 重做：Ctrl+Y(Windows)或Cmd+Y(Mac)

撤消或重做一個或多個段落的刪除、添加或重定位時，閃爍（預設行為）突出顯示指示受影響的段落。

>[!NOTE]
>
>請參閱[還原和重新執行頁面編輯 — 理論](#undoing-and-redoing-page-edits-the-theory) ，以取得還原和重新執行頁面編輯時可能採取的完整詳細資訊。

## 撤消和重新執行頁面編輯 — 理論{#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>您的系統管理員可以根據您實例的要求配置「撤消/重做」功能的各個方面](/help/sites-administering/config-undo.md)。[

AEM會儲存您執行之動作的歷史記錄，以及執行動作的順序。 因此，您可以依照執行動作的順序來還原數個動作。 然後，您可以使用重做來重新套用一或多個動作。

如果選取了內容頁面上的元素，則還原和重做命令會套用至選取的項目，例如文字元件。

撤消和重做命令的行為與其他軟體程式中的行為類似。 在您決定內容時，可使用命令還原網頁的最近狀態。 例如，如果將文本段落移動到頁面上的其他位置，則可以使用撤消命令將段落移回。 如果然後再次決定移動段落，請使用重做命令。

>[!NOTE]
>
>您可以：
>
>* 只要您自使用還原功能後未進行頁面編輯，就重做動作。
>* 最多可還原20個編輯動作（預設設定）。
>* 還可使用[鍵盤快速鍵](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)進行還原和重做。

>



您可以對下列類型的頁面變更使用還原和重做：

* 添加、編輯、刪除和移動段落
* 就地編輯段落內容
* 複製、剪下和貼上頁面中的項目
* 在頁面間複製、剪切和貼上項目
* 添加、刪除和更改檔案和影像
* 添加、刪除和更改注釋和草繪
* 架構的變更
* 添加和刪除引用
* 在元件對話框中更改屬性值。

表單元件轉譯的表單欄位在編寫頁面時無法指定值。 因此，撤消和重做命令不會影響您對這些類型元件的值所做的更改。 例如，您無法還原下拉式清單中選取值的作業。

>[!NOTE]
>
>若要還原和重做檔案和影像的變更，需要特殊權限。 此外，還可以還原檔案和影像變更的歷史記錄，最短持續數小時。 但是，在此之後，變更的還是無法保證。 管理員可以提供權限並更改10小時的預設時間。
