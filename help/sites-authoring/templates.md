---
title: 建立頁面範本
seo-title: 建立頁面範本
description: 範本會定義產生頁面的結構，而使用範本編輯器，建立和維護範本不再是僅限開發人員的工作
seo-description: 範本會定義產生頁面的結構，而使用範本編輯器，建立和維護範本不再是僅限開發人員的工作
uuid: e14cd298-289f-43f0-aacb-314ed5d56c12
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: b53348ca-fc50-4e7d-953d-b4c03a5025bb
docset: aem65
translation-type: tm+mt
source-git-commit: 149cdd00f745ad897f506434d7156b8147ef5bae
workflow-type: tm+mt
source-wordcount: '4901'
ht-degree: 9%

---


# 建立頁面範本{#creating-page-templates}

建立頁面時，您必須選取範本，此範本將用作建立新頁面的基礎。 範本會定義結果頁面的結構、任何初始內容，以及可使用的元件。

使用范 **本編輯器**，建立和維護範本不再是開發人員專屬的工作。也可以涉及一種稱為模板作 **者的權**&#x200B;力用戶。開發人員仍需要設定環境、建立用戶端程式庫和建立要使用的元件，但是當這些基本功能準備就緒後，範本作者就可以彈性地建立和設定範本，而不需要開發專案。****

**Templates Console**&#x200B;允許模板作者：

* 建立新範本或複製現有範本。
* 管理範本的生命週期。

**範本編輯器**&#x200B;可讓範本作者：

* 將元件新增至範本，並將它們置於互動式格線上。
* 預先設定元件。
* 定義哪些元件可在使用範本建立的頁面上編輯。

本檔案說明&#x200B;**範本作者**&#x200B;如何使用範本主控台和編輯器來建立和管理可編輯的範本。

如需可編輯範本在技術層級運作的詳細資訊，請參閱開發人員檔案[頁面範本- Editable](/help/sites-developing/page-templates-editable.md)以取得詳細資訊。

>[!NOTE]
>
>范 **** 本編輯器不支援直接在範本層級定位。可以定位根據可編輯的範本建立的頁面，但無法定位範本本身。

>[!CAUTION]
>
>使用&#x200B;**Templates Console**&#x200B;建立的頁面和範本不適用於傳統UI，也不支援這類使用。

## 啟動{#before-you-start}之前

>[!NOTE]
>
>管理員必須在&#x200B;**Configurations Browser**&#x200B;中配置模板資料夾，並應用適當的權限，模板作者才能在該資料夾中建立模板。

在您開始之前，請務必考慮以下幾點：

* 建立新範本需要共同作業。 因此，會為每個任務指示[角色](#roles)。

* 根據您的例項設定方式，請注意AEM現在提供[兩種基本範本類型](/help/sites-authoring/templates.md#editable-and-static-templates)可能會很有用。 這不會影響您實際[使用範本建立頁面](#using-a-template-to-create-a-page)的方式，但會影響您可建立的範本類型，以及頁面與其範本的關聯方式。

### 角色 {#roles}

使用「模板控制台」和「模 **板編輯器** 」建立新模板時 **** ，需要在以下角色之間協作：

* **管理員**:

   * 為模板建立新資料夾需要`admin`權限。

   * 這類工作通常也可由開發人員完成

* **開發人員**:

   * 重點介紹技術／內部細節
   * 需要開發環境的經驗。
   * 提供範本作者必要的資訊。

* **範本作者**:

   * 此作者是群組`template-authors`的成員

      * 這會分配所需的權限和權限。
   * 可以配置元件的使用和其他需要的高級詳細資訊：

      * 一些技術知識

         * 例如，在定義路徑時使用圖樣。
      * 開發人員的技術資訊。



由於某些任務的性質（如建立資料夾），因此需要開發環境，這需要知識／經驗。

本文檔中詳述的任務將列出負責執行這些任務的角色。

### 可編輯和靜態模板{#editable-and-static-templates}

AEM現在提供兩種基本範本類型：

* [可編輯的範本](/help/sites-authoring/templates.md#creatingandmanagingnewtemplates)

   * 範本作者可使用&#x200B;**Template**&#x200B;主控台和編輯器，建立[](#creatinganewtemplate)和[edited](#editingatemplate)。 可在&#x200B;**工具**&#x200B;控制台的&#x200B;**一般**&#x200B;部分訪問&#x200B;**模板**&#x200B;控制台。

   * 建立新頁面後，頁面與範本之間會維持動態連線。 這表示對範本結構和／或鎖定內容所做的變更將反映在使用該範本建立的任何頁面上。 不會反映對解鎖（即初始）內容的變更。
   * 使用內容原則（您可從範本編輯器中定義這些原則）來保存設計屬性。 頁面編輯器中的設計模式不再用於可編輯的範本。

* 靜態範本

   * AEM的數個版本都提供靜態範本。
   * 它們由您的開發人員](/help/sites-developing/page-templates-static.md)提供，因此作者無法建立或編輯它們。[
   * 複製以建立新頁面，但此後不存在動態連線（雖然已註冊範本名稱以取得資訊）。
   * 使用[設計模式](/help/sites-authoring/default-components-designmode.md)來保存設計屬性。
   * 由於編輯靜態範本是開發人員的專屬工作，請參閱開發人員檔案[頁面範本- Static](/help/sites-developing/page-templates-static.md)以取得詳細資訊。

根據定義，範本主控台和範本編輯器只允許建立和編輯可編輯的範本。 因此，本檔案只針對可編輯的範本。

### 使用範本建立頁面{#using-a-template-to-create-a-page}

使用範本建立新頁面[時，靜態和可編輯範本之間沒有可見的差異和指示。 ](/help/sites-authoring/managing-pages.md#creating-a-new-page)對於頁面作者，此程式是透明的。

## 建立和管理模板{#creating-and-managing-templates}

建立新的可編輯範本時：

* 使用&#x200B;**Template**&#x200B;控制台。 這可在&#x200B;**工具**&#x200B;控制台的&#x200B;**一般**&#x200B;區段中使用。

   * 或直接在：[https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf](https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf)

* 如有必要，[可以為模板建立資料夾](#creating-a-template-folder-admin)
* [建立新範本](#creatinganewtemplateauthor)，此範本一開始會是空的  [](#templatedefinitions)

* [視需要](#definingtemplatepropertiesauthor) 為範本定義其他屬性
* [編輯范](#editingtemplates) 本以定義：

   * [結構](#editingatemplatestructureauthor) -在使用範本建立的頁面上無法變更的預先定義內容。
   * [初始內容](#editing-a-template-initial-content-author) -可在使用範本建立之頁面上變更的預先定義內容。
   * [版面](#editingatemplatelayoutauthor) -適用於各種裝置。
   * [樣式](/help/sites-authoring/style-system.md) -定義要與模板及其元件一起使用的樣式。

* [啟用范](#enablingatemplateauthor) 本，以便在建立頁面時使用
* [允許](#allowing-a-template-author) 您網站的必要頁面或分支的範本
* [發佈范](#publishingatemplateauthor) 本，使其可在發佈環境中使用

>[!NOTE]
>
>**允許的範本**&#x200B;通常會在您的網站初次設定時預先定義。

>[!CAUTION]
>
>切勿在模板中輸入任何需要[國際化](/help/sites-developing/i18n.md)的資訊。 為了內部化，建議使用核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/get-started/localization.html)的[本地化功能。

### 建立模板資料夾——管理{#creating-a-template-folder-admin}

應為您的專案建立範本資料夾，以存放專案專用的範本。 這是一項管理任務，在文檔[頁面模板- Editable](/help/sites-developing/page-templates-editable.md#template-folders)中有說明。

### 建立新模板——模板作者{#creating-a-new-template-template-author}

1. 開啟范 **本主控台** (透過工具-> **一** 般 ****)，然後導覽至所需的檔案夾。

   >[!NOTE]
   >
   >在標準AEM例項中，範本主控台中已存在&#x200B;**global**&#x200B;資料夾。 如果當前資料夾中未找到策略和／或模板類型，則此選項將保留預設模板並充當備援。
   >
   >
   >建議使用為您的項目](/help/sites-developing/page-templates-editable.md#template-folders)建立的[模板資料夾的最佳做法。

1. 選擇&#x200B;**建立**，然後選擇&#x200B;**建立模板**&#x200B;以開啟嚮導。

1. 選擇&#x200B;**模板類型**，然後選擇&#x200B;**Next**。

   >[!NOTE]
   >
   >範本類型是預先定義的範本版面，可視為範本的範本。 這些是由開發人員或系統管理員預先定義的。 如需詳細資訊，請參閱開發人員檔案[頁面範本- Editable](/help/sites-developing/page-templates-editable.md#template-type)。

1. 完成&#x200B;**Template Details**:

   * **範本名稱**
   * **說明**

1. 選擇 **建立**。將顯示確認資訊，選擇&#x200B;**Open**&#x200B;開始[編輯模板](#editingatemplate)或&#x200B;**Done**&#x200B;以返回模板控制台。

   >[!NOTE]
   >
   >建立新範本時，在主控台中會標示為&#x200B;**Draft**，這表示該範本尚未可供頁面作者使用。

### 定義模板屬性——模板作者{#defining-template-properties-template-author}

範本可以有下列屬性：

* 影像

   * 影像將用作範本[的縮圖，以協助選取，例如在「建立頁面」精靈中。](/help/sites-authoring/templates.md#template-thumbnail-image)

      * 可上傳
      * 可根據範本內容產生

* 標題

   * 用於標識模板的標題，如&#x200B;**建立頁**&#x200B;嚮導中。

* 說明

   * 提供範本及其使用的詳細資訊的選用說明，例如在&#x200B;**建立頁面**&#x200B;精靈中。

要查看和／或編輯屬性：

1. 在&#x200B;**範本控制台**&#x200B;中，選擇範本。
1. 從工 **具欄中選擇** 「查看屬性」(View Properties)或快速選項以開啟對話框。
1. 您現在可以檢視或編輯範本屬性。

>[!NOTE]
>
>範本是功能強大的工具，可簡化您的頁面建立工作流程。 不過，太多範本可能會讓作者感到不知所措，並讓頁面建立變得困惑。 一個很好的經驗法則是將範本數控制在100以下。
>
>Adobe不建議使用超過1000個範本，因為可能會影響效能。

>[!NOTE]
>
>控制台會指出範本的狀態（草稿、啟用或停用）。

#### 範本縮圖影像{#template-thumbnail-image}

要定義模板縮覽圖，請執行以下操作：

1. 編輯範本屬性。
1. 選擇您要上傳縮圖或是從範本內容產生縮圖。

   * 如果您想要上傳縮圖，請按一下或點選「上傳影像」**。**
   * 如果您想要產生縮圖，請按一下或點選「產生預覽」(Generate Preview)****

1. 對於這兩種方法，都會顯示縮圖的預覽。

   如果不滿意，請按一下或點選&#x200B;**Clear**&#x200B;以上傳其他影像或重新產生縮圖。

1. 當您對縮圖感到滿意時，按一下或點選&#x200B;**儲存並關閉**。

### 啟用和允許模板——模板作者{#enabling-and-allowing-a-template-template-author}

若要在建立頁面時能夠使用範本，您必須：

* [啟用范](#enablingatemplate) 本，讓它可供建立頁面時使用。
* [允許范](#allowingatemplate) 本指定可使用範本的內容分支。

#### 啟用模板——模板作者{#enabling-a-template-template-author}

可以啟用或停用範本，以便在&#x200B;**建立頁面**&#x200B;精靈中提供或無法使用範本。

>[!CAUTION]
>
>當範本啟用後，當範本作者開始進一步更新範本時，將會顯示警告。 這是為了通知使用者範本可能被參考，因此任何變更都可能會影響參考範本的頁面。

1. 在&#x200B;**範本控制台**&#x200B;中，選擇範本。
1. 從工具欄中選擇&#x200B;**啟用**&#x200B;或&#x200B;**禁用**，然後在確認對話框中再次選擇。
1. 現在，當[建立新頁面](/help/sites-authoring/managing-pages.md#creating-a-new-page)時，您可以使用範本，不過您可能會想要根據您的需求編輯範本](#editingatemplate)。[

>[!NOTE]
>
>控制台會指出範本的狀態（草稿、啟用或停用）。

#### 允許範本——作者{#allowing-a-template-author}

範本可供某些頁面分支使用或無法使用。

1. 開啟[頁面屬性](/help/sites-authoring/editing-page-properties.md)，以查看希望模板可用的分支的根頁面。

1. 開啟&#x200B;**進階**&#x200B;標籤。

1. 在「 **範本設定** 」下 **，使用「新增」欄位** ，指定範本的路徑。

   路徑可以是明確的或使用模式。 例如：

   `/conf/<your-folder>/settings/wcm/templates/.*`

   路徑順序不相關，所有路徑都將被掃描，並檢索任何模板。

   >[!NOTE]
   >
   >如果&#x200B;**允許的模板**&#x200B;清單為空，則樹將一直上升，直到找到值／清單。
   >
   >
   >請參閱[範本可用性](/help/sites-developing/templates.md#template-availability) —— 允許範本的原則保持不變。

1. 按一下&#x200B;**保存**&#x200B;保存對頁面屬性的更改。

>[!NOTE]
>
>通常允許的範本會在設定時預先定義給整個網站。

### 發佈範本——範本作者{#publishing-a-template-template-author}

當轉譯頁面時參考範本時，必須發佈已完全設定的範本，以便在發佈環境中使用。

1. 在&#x200B;**範本控制台**&#x200B;中，選擇範本。
1. 從工具列選擇&#x200B;**Publish**&#x200B;以開啟精靈。
1. 選擇要串聯發佈的&#x200B;**內容策略**。

1. 從工具列選擇&#x200B;**Publish**&#x200B;以完成動作。

## 編輯模板——模板作者{#editing-templates-template-authors}

建立或編輯範本時，您可以定義多個方面。 編輯範本類似於頁面製作。

可編輯模板的以下方面：

* [結構](#editingatemplatestructure)

   此處新增的元件無法由頁面作者從產生的頁面移動／移除。 如果您希望頁面作者能夠將元件新增及移除至產生的頁面，則必須將段落系統新增至範本。

   當元件鎖定時，您可以新增內容，頁面作者無法編輯這些內容。 您可以解除鎖定元件，以允許定義[初始內容](#editingatemplateinitialcontent)。

   >[!NOTE]
   >
   >在結構模式下，任何作為解鎖元件的父級的元件都不能移動、剪切或刪除。

* [初始內容](#editingatemplateinitialcontent)

   解除鎖定元件後，您可以定義將複製到結果頁面（從範本建立）的初始內容。 這些解鎖的元件可在產生的頁面上編輯。

   >[!NOTE]
   >
   >在&#x200B;**初始內容**&#x200B;模式以及結果頁面中，可以刪除任何具有可存取父項（即佈局容器中的元件）的解鎖元件。

* [配置](#editingatemplatelayout)

   您可以在這裡預先定義所需裝置格式的範本版面。 **範本製作的** 「版面」模式與頁面製作的「版面 [**** 」模式功能相同](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)。

* [頁面原則](#editingatemplatepagepolicies)

   在頁面原則下，您可以將預先定義的頁面原則連接至頁面。 這些頁面原則可定義各種設計組態。

* [樣式](/help/sites-authoring/style-system.md)

   樣式系統允許模板作者在元件的內容策略中定義樣式類，以便內容作者在編輯頁面上的元件時能夠選擇它們。 這些樣式可以替代元件的視覺變化，讓元件更具彈性。

   如需詳細資訊，請參閱[Style System說明檔案](/help/sites-authoring/style-system.md)。

工具列中的&#x200B;**Mode**&#x200B;選擇器允許您選擇和編輯模板的適當方面：

* [結構](#editingatemplatestructure)
* [初始內容](#editingatemplateinitialcontent)
* [配置](#editingatemplatelayout)

![chlimage_1-133](assets/chlimage_1-133.png)

雖然&#x200B;**頁面資訊**&#x200B;功能表上的&#x200B;**頁面原則**&#x200B;選項可讓您選擇所需的頁面原則](#editingatemplatepagepolicies):[

![screen_shot_2018-03-23at120604](assets/screen_shot_2018-03-23at120604.png)

>[!CAUTION]
>
>如果作者開始編輯已啟用的範本，將會顯示警告。 這是為了通知使用者範本可能被參考，因此任何變更都可能會影響參考範本的頁面。

### 編輯模板——結構——模板作者{#editing-a-template-structure-template-author}

在&#x200B;**結構**&#x200B;模式中，您定義模板的元件和內容，並定義模板及其元件的策略。

* 在範本結構中定義的元件無法在產生的頁面上移動，也無法從任何產生的頁面刪除。
* 如果您希望頁面作者能夠新增和移除元件，請將段落系統新增至範本。
* 可以解除鎖定並再次鎖定元件，以允許您定義[初始內容](#editingatemplateinitialcontent)。

* 定義了元件和頁面的設計策略。

![screen_shot_2018-03-23at120819](assets/screen_shot_2018-03-23at120819.png)

在模板編輯器的&#x200B;**Structure**&#x200B;模式下：

* **新增元件**

   有幾種機制可將元件新增至範本：

   * 從側面板的&#x200B;**Components**&#x200B;瀏覽器。
   * 使用範本上元件工具列上的&#x200B;**插入元件**&#x200B;選項（**+**&#x200B;圖示）或&#x200B;**拖曳元件至此處**&#x200B;方塊。

   * 將資產（從側面板的&#x200B;**Assets**&#x200B;瀏覽器）直接拖曳至範本上，就地產生適當的元件。

   新增後，每個元件都會標示為：

   * 邊框
   * 顯示元件類型的標籤
   * 要在元件已解鎖時顯示的標籤

   >[!NOTE]
   >
   >將現成可用的標題元件新增至範本時 **** ，其中會包含預設的文字 **結構**。
   >
   >
   >如果您變更此項，並新增您自己的文字，則從範本建立頁面時，將會使用此更新的文字。
   >
   >
   >如果您保留預設文字（結構），則標題將預設為後續頁面的名稱。

   >[!NOTE]
   >
   >雖然不相同，但將元件和資產新增至範本與[頁面編寫](/help/sites-authoring/editing-content.md)時的類似動作有許多相似之處。

* **元件操作**

   將元件新增至範本後，請對元件採取動作。 每個單獨實例都有一個工具欄，允許您訪問可用操作，該工具欄取決於元件類型。

   ![screen_shot_2018-03-23at120909](assets/screen_shot_2018-03-23at120909.png)

   它也可以取決於所採取的操作，例如當策略與元件關聯時，設計配置表徵圖變為可用。

* **編輯和設定**

   透過這兩個動作，您可以將內容新增至元件。

* **邊框以指示結構**

   當在&#x200B;**Structure**&#x200B;模式下工作時，橙色邊框表示當前選擇的元件。 虛線也表示父元件。

   例如，在下方的螢幕擷取中，選取&#x200B;**Text**&#x200B;元件，位於&#x200B;**版面容器**（回應格線）中。

   ![chlimage_1-134](assets/chlimage_1-134.png)

* **原則與屬性（一般）**

   內容（或設計）原則可定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。

   為元件建立內容策略或選擇現有策略。 這可讓您定義設計詳細資訊。

   ![chlimage_1-135](assets/chlimage_1-135.png) ![chlimage_1-136](assets/chlimage_1-136.png)

   配置窗口分為兩個部分。

   * 在對話框的左側，在&#x200B;**Policy**&#x200B;下，您可以選擇現有策略或選擇現有策略。
   * 在對話框的右側&#x200B;**Properties**&#x200B;下，可以設定特定於元件類型的屬性。

   可用的屬性取決於所選元件。 例如，對於文本元件，屬性定義了複製和貼上選項、格式設定選項和段落樣式等選項。

   ***政策***

   內容（或設計）原則可定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。

   在&#x200B;**Policy**&#x200B;下，您可以通過下拉清單選擇要應用於元件的現有策略。

   ![chlimage_1-137](assets/chlimage_1-137.png)

   通過選擇&#x200B;**選擇策略**&#x200B;下拉清單旁邊的添加按鈕，可以添加新策略。 然後，應在&#x200B;**Policy Title**&#x200B;欄位中指定新標題。

   ![chlimage_1-138](assets/chlimage_1-138.png)

   **選擇策略**&#x200B;下拉清單中選定的現有策略可以使用下拉清單旁的複製按鈕作為新策略進行複製。 然後，應在&#x200B;**Policy Title**&#x200B;欄位中指定新標題。 預設情況下，複製的策略的標題為&#x200B;**Copy of X** ，其中X是複製策略的標題。

   ![chlimage_1-139](assets/chlimage_1-139.png)

   策略說明在&#x200B;**策略說明**&#x200B;欄位中是可選的。

   在&#x200B;**也使用所選策略**&#x200B;部分的其他模板中，您可以輕鬆查看哪些其他模板使用在&#x200B;**選擇策略**&#x200B;下拉菜單中選擇的策略。

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >如果將相同類型的多個元件新增為初始內容，則相同的原則會套用至所有元件。 這反映了靜態模板&#x200B;[**設計模式**&#x200B;中的相同限制。](/help/sites-authoring/default-components-designmode.md)

   ***屬性***

   在&#x200B;**Properties**&#x200B;標題下，您可以定義元件的設定。 標題包含兩個標籤：

   * 主要
   * 功能

   *主要*

   在&#x200B;**Main**&#x200B;標籤上，定義了元件的最重要設定。

   例如，對於影像元件，可定義允許的寬度，並啟用延遲載入。

   如果設定允許多個配置，請按一下或點選&#x200B;**添加**&#x200B;按鈕以添加另一個配置。

   ![chlimage_1-141](assets/chlimage_1-141.png)

   要刪除配置，請按一下或點選配置右側的&#x200B;**Delete**&#x200B;按鈕。

   要刪除配置，請按一下或點選**刪除**按鈕。

   ![chlimage_1-142](assets/chlimage_1-142.png)

   *功能*

   **功能**&#x200B;標籤可讓您啟用或停用元件的其他功能。

   例如，對於影像元件，您可以定義裁切比例、允許的影像方向，以及允許上傳。

   ![chlimage_1-143](assets/chlimage_1-143.png)

   >[!CAUTION]
   >
   >請注意，在AEM裁切比例中，定義為&#x200B;**height/width**。 這與傳統的寬度／高度定義不同，而且是基於舊有相容性的原因。 如果您清楚地定義&#x200B;**Name**，則網頁編寫使用者將不會察覺到任何差異，因為這是UI中顯示的內容。

   >[!NOTE]
   >
   >[實施富格文本編輯器的組](/help/sites-administering/rich-text-editor.md#main-pars-header-206036638) 件的內容策略只能針對RTE通過其UI設定提供的選項進行定義。  [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638) [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638)

* **原則與屬性（版面容器）**

   版面容器的原則和屬性設定與一般用途類似，但有些差異。

   >[!NOTE]
   >
   >設定原則對於容器元件是必備的，因為它可讓您定義容器中可用的元件。

   配置窗口分為兩個部分，與窗口的一般用法相同。

   ***政策***

   內容（或設計）原則可定義元件的設計屬性。 例如，可用元件或最小／最大尺寸。 這些範本（和使用範本建立的頁面）適用。

   在&#x200B;**Policy**&#x200B;下，您可以通過下拉清單選擇要應用於元件的現有策略。 此功能與一般使用視窗時的功能相同。

   ***屬性***

   在&#x200B;**屬性**&#x200B;標題下，您可以選擇哪些元件適用於版面容器並定義其設定。 標題有三個標籤：

   * 允許的元件
   * 預設元件
   * 回應式設定

   *允許的元件*

   在&#x200B;**允許的元件**&#x200B;標籤上，您定義哪些元件可用於版面容器。

   * 這些元件依其元件群組分組，可展開和收合。
   * 您可以勾選整個群組，方法是勾選群組名稱，而取消勾選所有群組即可取消勾選。
   * 減號表示至少選取一個項目，但並非選取群組中的所有項目。
   * 可使用搜尋來依名稱篩選元件。
   * 列在元件群組名稱右側的計數代表這些群組中選取的元件總數，而不考慮篩選。

   ![chlimage_1-144](assets/chlimage_1-144.png)

   *預設元件*

   在&#x200B;**預設元件**&#x200B;標籤中，您定義哪些元件會自動與指定的媒體類型關聯，如此當作者從資產瀏覽器拖曳資產時，AEM就知道要將資產與哪個元件關聯。 請注意，只有具有放置區域的元件可用於此類配置。

   按一下或點選&#x200B;**添加映射**&#x200B;以添加全新的元件和MIME類型映射。

   在清單中選取元件，然後按一下或點選「 **新增類型** 」，將其他MIME類型新增至已映射的元件。按一下「 **刪除** 」圖示以移除MIME類型。

   ![chlimage_1-145](assets/chlimage_1-145.png)

   *回應式設定*

   在&#x200B;**回應式設定**&#x200B;標籤上，您可以設定版面容器的產生格線中的欄數。

* **解除鎖定／鎖定元件**

   您可以解除鎖定／鎖定元件，以定義內容是否可在&#x200B;**初始內容**&#x200B;模式中進行變更。

   當元件已解除鎖定時：

   * 邊框中顯示開啟的掛鎖指示符。
   * 元件工具列會隨之調整。
   * 已輸入的任何內容將不再顯示在&#x200B;**Structure**&#x200B;模式中。

      * 已輸入的內容被視為初始內容，且僅在&#x200B;**初始內容**&#x200B;模式中顯示。
   * 無法移動、剪切或刪除解鎖元件的父代。

   ![chlimage_1-146](assets/chlimage_1-146.png)

   這包括解除鎖定容器元件，以便在初始內容模式或產生的頁 **面中新增其他元件** 。如果您在解除鎖定容器之前已將元件/內容新增至容器，則這些元件/內容在「結構」模式中將不再顯示，但會以「初始內容 ******** 」模式顯示。在「 **結構模式**」中，只有容器元件本身會顯示其「允許的元 **件」清單**。

   ![chlimage_1-147](assets/chlimage_1-147.png)

   為節省空間，版面容器不會擴充以容納允許的元件清單。 容器會變成可捲動的清單。

   可配置的元件以「策略」表徵圖顯示 **** ，可以點選或按一下該表徵圖以編輯該元件的策略和屬性。

   ![chlimage_1-148](assets/chlimage_1-148.png)

* **與現有頁面的關係**

   如果在根據範本建立頁面後更新結構，則這些頁面將反映範本的變更。 工具列中會顯示警告，提醒您此事以及確認對話方塊。

   ![chlimage_1-149](assets/chlimage_1-149.png)

### 編輯模板——初始內容——作者{#editing-a-template-initial-content-author}

**初始** 內容模式用於定義在首次根據範本建立頁面時將顯示的內容。然後頁面作者就可以編輯初始內容。

雖然在「結構 **」模式下建立的所有內容在「初始內容」中都可** 見 ****，但只能選擇和編輯已解鎖的元件。

>[!NOTE]
>
>**使用** 該範本建立的頁面，可考慮編輯初始Contentmode。因此，策略不是在&#x200B;**初始內容**&#x200B;模式中定義，而是在&#x200B;[**結構**&#x200B;模式](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)中定義。

* 標籤可供編輯的解鎖元件。 選取後，它們會有藍色邊框：

   ![chlimage_1-150](assets/chlimage_1-150.png)

* 解除鎖定的元件有工具列，可讓您編輯和設定內容：

   ![chlimage_1-151](assets/chlimage_1-151.png)

* 如果容器元件已解除鎖定(在「結 **構** 」模式中)，則您可以在「初始內容 **** 」模式中新增元件至容器。在「初始內 **容」模式中新增的元件** ，可在產生的頁面上移動或從中刪除。

   您可以使用「拖曳元件到此處 **」區域，或從適當容器的工具列** 中使用「插入新元件 **** 」選項來新增元件。

   ![chlimage_1-152](assets/chlimage_1-152.png) ![chlimage_1-153](assets/chlimage_1-153.png)

* 如果在根據範本建立頁面後更新範本的初始內容，則這些頁面不會受到範本中初始內容變更的影響。

>[!NOTE]
>
>初始內容是用於準備元件和頁面版面，以做為建立內容的起點。 它並非實際內容，而是維持原狀。 因此，無法翻譯初始內容。
>
>如果您需要在範本中加入可翻譯的文字，例如在頁首或頁尾中，則可使用核心元件的[本地化功能](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/get-started/localization.html)。

### 編輯模板——佈局——模板作者{#editing-a-template-layout-template-author}

您可以為各種裝置定義範本版面。 [範本](/help/sites-authoring/responsive-layout.md) 的互動式版面運作方式與網頁製作相同。

>[!NOTE]
>
>對版面所做的變更將反映在「初始內容」模式中，但「結構」模式中未顯示任何變更。********

![chlimage_1-154](assets/chlimage_1-154.png)

### 編輯範本——頁面設計——範本作者／開發人員{#editing-a-template-page-design-template-author-developer}

頁面設計 (包括所需的用戶端程式庫和頁面原則) 會保留在「頁面資訊」功能表的「 **頁面設計** 」選 **** 項下。

要訪問&#x200B;**頁面設計**&#x200B;對話框：

1. 從&#x200B;**範本編輯器**&#x200B;中，從工具列選擇&#x200B;**頁面資訊**，然後選擇&#x200B;**頁面設計**&#x200B;以開啟對話方塊。
1. **頁面設計**&#x200B;對話方塊隨即開啟，並分為兩個區段：

   * 左半部分定義[頁面原則](/help/sites-authoring/templates.md#page-policies)
   * 右半部分定義[頁面屬性](/help/sites-authoring/templates.md#page-properties)

   ![chlimage_1-155](assets/chlimage_1-155.png)

#### 頁面原則 {#page-policies}

您可以將內容原則套用至範本或結果頁面。 這定義了頁面上主要段落系統的內容原則。

![chlimage_1-156](assets/chlimage_1-156.png)

* 您可以從&#x200B;**選擇策略**&#x200B;下拉式清單中選擇該頁的現有策略。

   ![chlimage_1-157](assets/chlimage_1-157.png)

   通過選擇&#x200B;**選擇策略**&#x200B;下拉清單旁邊的添加按鈕，可以添加新策略。 然後，應在&#x200B;**Policy Title**&#x200B;欄位中指定新標題。

   ![chlimage_1-158](assets/chlimage_1-158.png)

   **選擇策略**&#x200B;下拉清單中選定的現有策略可以使用下拉清單旁的複製按鈕作為新策略進行複製。 然後，應在&#x200B;**Policy Title**&#x200B;欄位中指定新標題。 預設情況下，複製的策略的標題為&#x200B;**Copy of X** ，其中X是複製策略的標題。

   ![chlimage_1-159](assets/chlimage_1-159.png)

* 在&#x200B;**策略標題**&#x200B;欄位中定義策略的標題。 必須有原則才能擁有標題，才能在&#x200B;**選擇原則**&#x200B;下拉式清單中輕鬆選取。

   ![chlimage_1-160](assets/chlimage_1-160.png)

* 策略說明在&#x200B;**策略說明**&#x200B;欄位中是可選的。
* 在&#x200B;**也使用所選策略**&#x200B;部分的其他模板中，您可以輕鬆查看哪些其他模板使用在&#x200B;**選擇策略**&#x200B;下拉菜單中選擇的策略。

   ![chlimage_1-161](assets/chlimage_1-161.png)

#### 頁面內容 {#page-properties}

使用頁面屬性，您可以使用&#x200B;**頁面設計**&#x200B;對話方塊來定義所需的用戶端程式庫。 這些用戶端程式庫包括要載入範本的樣式表和javascript，以及使用該範本建立的頁面。

![chlimage_1-162](assets/chlimage_1-162.png)

* 指定您要套用至使用此範本所建立之頁面的用戶端程式庫。 在&#x200B;**用戶端程式庫**&#x200B;區段的文字欄位中輸入程式庫名稱。

   ![chlimage_1-163](assets/chlimage_1-163.png)

* 如果需要多個庫，請按一下「添加」按鈕為庫名稱添加其他文本欄位。

   ![chlimage_1-164](assets/chlimage_1-164.png)

   視需要為用戶端程式庫新增多個文字欄位。

   ![chlimage_1-165](assets/chlimage_1-165.png)

* 使用拖曳控點拖曳欄位，以視需要定義程式庫的相對位置。

   ![chlimage_1-166](assets/chlimage_1-166.png)

>[!NOTE]
>
>雖然範本作者可以在範本上指定頁面原則，但他或她需要從開發人員取得適當用戶端程式庫的詳細資訊。

### 編輯模板——初始頁面屬性——作者{#editing-a-template-initial-page-properties-author}

使用&#x200B;**初始頁面屬性**&#x200B;選項，可以定義在建立結果頁面時使用的初始[頁面屬性](/help/sites-authoring/editing-page-properties.md)。

1. 從模板編輯器中，從工具欄中選擇&#x200B;**頁面資訊**，然後選擇&#x200B;**初始頁面屬性**&#x200B;以開啟該對話框。

1. 在對話方塊中，您可以定義要套用至使用此範本建立之頁面的屬性。

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. 使用&#x200B;**Done**&#x200B;確認您的定義。

## 最佳作法 {#best-practices}

建立範本時，您應考慮：

1. 從範本建立頁面後，範本變更的影響。

   以下列出範本上可能的不同作業，以及它們對從它們建立的頁面有何影響：

   * 結構變更：

      * 這些會立即套用至產生的頁面。
      * 訪客仍需要發佈已變更的範本，才能看到變更。
   * 變更內容原則和設計組態：

      * 這些項目會立即套用至產生的頁面。
      * 訪客需要發佈變更才能看到變更。
   * 初始內容的變更：

      * 這些僅適用於在範本變更後建立的頁面。
   * 版面的變更取決於修改的元件是否屬於：

      * 僅限結構——立即應用
      * 包含初始內容——僅限在變更後建立的頁面上

   在下列情況下，請格外小心：

   * 鎖定或解除鎖定啟用範本上的元件。
   * 這可能會產生副作用，因為現有的頁面已經在使用它。 通常：

      * 現有頁面上將遺失解除鎖定的元件（已鎖定）。
      * 鎖定元件（可編輯）將隱藏該內容，使其無法顯示在頁面上。

   >[!NOTE]
   >
   >AEM在變更不再是草稿之範本上元件的鎖定狀態時，會顯式提供警告。

1. [建立您自己](#creatingatemplatefolderdeveloper) 的網站特定範本資料夾。
1. [從「範本」](#publishingatemplateauthor) 主控台發佈 **** 您的範本。
