---
title: 對話方塊編輯器
seo-title: 對話方塊編輯器
description: 對話框編輯器提供了圖形介面，可輕鬆建立和編輯對話框和支架
seo-description: 對話框編輯器提供了圖形介面，可輕鬆建立和編輯對話框和支架
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---

# 對話框編輯器{#dialog-editor}

對話框編輯器提供了圖形介面，可輕鬆建立和編輯對話框和支架。

要查看其工作原理，請轉到CRXDE Lite，開啟瀏覽器樹到`/libs/foundation/components/chart`，然後按兩下節點`dialog`:

![chlimage_1-248](assets/chlimage_1-247.png)

對話框節點將在&#x200B;**對話框編輯器**&#x200B;中開啟：

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 用戶介面概述{#user-interface-overview}

對話框編輯器介面由四個窗格組成：

* 左上角的&#x200B;**浮動視窗**。 此窗格包含可用於構建對話框的小部件，如頁簽面板、文本欄位、選擇清單和按鈕。 您可以按一下所需的分隔列，以展開浮動視窗中的不同類別。
* 左下角的&#x200B;**structure**&#x200B;窗格。 此窗格顯示構成對話框定義的節點的層次結構。 您可以在「CRXDE Lite」或「CRX內容總管」中展開對話方塊節點，以查看相同的結構。
* 在窗口的中央的&#x200B;**render**&#x200B;窗格。 此窗格顯示在結構窗格中定義的對話框定義如何呈現為實際對話框。
* **properties**&#x200B;窗格。 此窗格顯示結構窗格中當前突出顯示的節點的屬性。

### 使用對話框編輯器{#using-the-dialog-editor}

若要建立對話方塊，使用者會將元素從浮動視窗拖放至結構窗格，置於對話方塊定義階層中。

完成所需結構後，用戶按一下呈現窗格頂部的&#x200B;**Save**。

>[!CAUTION]
>
>請注意，對話框編輯器用於建立相對簡單的對話框，可能無法編輯更複雜的對話框定義。 如果對話框編輯器不允許編輯對話框結構，則必須通過使用(例如，CRXDE Lite或CRX內容資源管理器)直接編輯節點結構來手動建立和/或編輯對話框定義。

### 建立新對話框{#creating-a-new-dialog}

要建立新的對話框，需要選擇所需的元件，請按一下「**建立……」**，然後&#x200B;**建立對話框……**。

輸入所需的詳細資訊，然後按一下&#x200B;**全部保存** — 現在，您可以連按兩下對話框以使用編輯器開啟它。

### 使用Scaffold的對話框編輯器{#using-the-dialog-editor-for-scaffolds}

架構是一種特殊頁面，其中包含可在一個步驟中填入並提交的表單。 這可讓您使用輸入的內容快速建立頁面。

組成架構的表單是由對話方塊定義，就像一般對話方塊一樣，但會以不同形式顯示在架構頁面上。 由於對話框定義用於定義支架，因此可以使用對話框編輯器來設計支架。 請注意，以此方式使用對話框編輯器時，渲染窗格仍將以對話框的形式顯示對話框定義，而不是以架構形式顯示。

有關使用對話框編輯器建立支架的詳細資訊，請參閱[支架](/help/sites-authoring/scaffolding.md)。
