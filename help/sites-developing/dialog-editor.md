---
title: 對話框編輯器
seo-title: Dialog Editor
description: 對話框編輯器提供了圖形介面，可輕鬆建立和編輯對話框和支架
seo-description: The dialog editor provides a graphical interface for easily creating and editing dialog boxes and scaffolds
uuid: 64d3fb12-8638-441b-8595-c590d48f3072
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: b7ac457d-3689-4f5d-9ceb-ff6a9944e7eb
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 對話框編輯器{#dialog-editor}

對話框編輯器提供了圖形介面，可輕鬆建立和編輯對話框和支架。

要查看其工作原理，請轉到CRXDE Lite，開啟瀏覽器樹以 `/libs/foundation/components/chart` 並按兩下該節點 `dialog`:

![chlimage_1-247](assets/chlimage_1-247.png)

對話框節點將在 **對話框編輯器**:

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## 用戶介面概述 {#user-interface-overview}

對話框編輯器介面由四個窗格組成：

* 的 **調色板**&#x200B;的上界。 此窗格包含可用於生成對話框的小部件，如頁籤面板、文本欄位、選擇清單和按鈕。 通過按一下所需的分隔條，可以展開調色板中的不同類別。
* 的 **結構** 的子菜單。 此窗格顯示構成對話框定義的節點的層次結構。 通過在CRXDE Lite或CRX內容瀏覽器中展開對話框節點，可以看到相同的結構。
* 的 **呈現** 的上界。 此窗格顯示如何將結構窗格中定義的對話框定義呈現為實際對話框。
* 的 **屬性** 的子菜單。 此窗格顯示結構窗格中當前突出顯示的節點的屬性。

### 使用對話框編輯器 {#using-the-dialog-editor}

要生成對話框，用戶將元素從元件面板拖放到結構窗格中，並將其放到對話框定義層次結構中的位置。

完成所需結構後，用戶按一下 **保存**，位於渲染窗格的頂部。

>[!CAUTION]
>
>請注意，對話框編輯器用於建立相對簡單的對話框，可能無法編輯更複雜的對話框定義。 如果對話框編輯器不允許編輯對話框結構，則必須通過直接使用CRXDE Lite或CRX內容瀏覽器編輯節點結構來手動建立和/或編輯對話框定義。

### 建立新對話框 {#creating-a-new-dialog}

要建立新對話框，需要選擇所需的元件，請按一下 **建立……** 然後 **建立對話框……**。

輸入所需的詳細資訊，然後按一下 **全部保存**  — 現在，您可以按兩下該對話框以使用編輯器將其開啟。

### 使用對話框編輯器進行Scaffold {#using-the-dialog-editor-for-scaffolds}

腳手架是一個特殊頁面，包含一個可以一步填充和提交的表單。 這允許您使用輸入的內容快速建立頁面。

構成腳手架的形式由對話定義來定義，就像正常對話一樣，儘管它以不同的形式出現在腳手架頁面上。 由於對話框定義用於定義支架，因此可以使用對話框編輯器來設計支架。 請注意，以此方式使用對話框編輯器時，渲染窗格仍將以對話框的形式顯示對話框定義，而不是以腳手架的形式顯示。

請參閱 [腳手架](/help/sites-authoring/scaffolding.md) 的子菜單。
