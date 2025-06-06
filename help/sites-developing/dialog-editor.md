---
title: 對話方塊編輯器
description: 對話方塊編輯器提供圖形介面，可輕鬆建立和編輯對話方塊和支架。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 對話方塊編輯器{#dialog-editor}

對話方塊編輯器提供圖形介面，可輕鬆建立和編輯對話方塊和支架。

若要檢視其運作方式，請前往「CRXDE Lite」，開啟`/libs/foundation/components/chart`的瀏覽器樹狀結構，然後按兩下節點`dialog`：

![chlimage_1-247](assets/chlimage_1-247.png)

對話方塊節點會在&#x200B;**對話方塊編輯器**&#x200B;中開啟：

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 使用者介面概觀 {#user-interface-overview}

對話方塊編輯器介面由四個窗格組成：

* 左上角的&#x200B;**浮動視窗**。 此窗格包含可用來建立對話方塊的Widget，例如Tab面板、文字欄位、選取專案清單和按鈕。 您可以按一下所需的分隔線列，以展開浮動視窗中的不同類別。
* 左下角的&#x200B;**結構**&#x200B;窗格。 此窗格顯示組成對話方塊定義的節點階層結構。 您可以在CRXDE Lite或CRX Content Explorer中展開對話方塊節點，以檢視相同的結構。
* **轉譯**&#x200B;窗格，位於視窗中央。 此窗格顯示結構窗格中定義的對話方塊定義如何呈現為實際對話方塊。
* **屬性**&#x200B;窗格。 此窗格顯示結構窗格中反白顯示的節點屬性。

### 使用對話方塊編輯器 {#using-the-dialog-editor}

若要建立對話方塊，使用者會將浮動視窗中的元素拖放到結構窗格中對話方塊定義階層內的位置。

完成所需的結構後，使用者在轉譯器窗格頂端按一下&#x200B;**儲存**。

>[!CAUTION]
>
>對話方塊編輯器用於建立簡單的對話方塊。 它可能無法編輯更複雜的對話方塊定義。 如果對話方塊編輯器不允許編輯對話方塊結構，則必須手動建立或編輯對話方塊定義，或兩者都手動進行。 例如，您可以使用CRXDE Lite或CRX Content Explorer直接編輯節點結構來完成此操作。

### 建立新對話方塊 {#creating-a-new-dialog}

若要建立對話方塊，請選取所需的元件，按一下&#x200B;**建立……**，然後按&#x200B;**建立對話方塊……**。

輸入必要的詳細資料，然後按一下[儲存全部]&#x200B;**&#x200B;** — 現在您可以連按兩下對話方塊，以使用編輯器開啟對話方塊。

### 使用支架的對話方塊編輯器 {#using-the-dialog-editor-for-scaffolds}

架構是包含表單的特殊頁面，可在單一步驟中填寫和提交。 這可讓您使用輸入的內容快速建立頁面。

組成支架的表單是由對話方塊定義所定義，就像一般的對話方塊，不過它以不同的形式出現在支架頁面上。 因為對話方塊定義是用來定義支架，所以可使用對話方塊編輯器來設計支架。 以這種方式使用對話方塊編輯器時，轉譯器窗格仍會以對話方塊的形式顯示對話方塊定義，而不是以支架顯示。

如需使用對話方塊編輯器建立支架的詳細資訊，請參閱[支架](/help/sites-authoring/scaffolding.md)。
