---
title: AEM Brackets擴充功能
description: 瞭解如何針對Brackets使用Adobe Experience Manager擴充功能。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 2%

---

# AEM Brackets擴充功能{#aem-brackets-extension}

## 概觀 {#overview}

AEM Brackets擴充功能提供流暢的工作流程，讓您可編輯AEM元件和使用者端程式庫，並利用的強大功能 [括弧](https://brackets.io/) 程式碼編輯器，可讓您從程式碼編輯器存取Photoshop檔案和圖層。 擴充功能提供的簡易同步功能（不需要Maven或檔案儲存庫）可提升開發人員效率，也可協助具備有限AEM知識的前端開發人員參與專案。 此擴充功能也提供以下支援： [HTML範本語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)，可降低JSP的複雜性，讓元件開發更容易、更安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

AEM Brackets擴充功能的主要功能包括：

* 將變更的檔案自動同步至AEM開發執行個體。
* 手動雙向同步檔案和資料夾。
* 專案的完整內容套件同步。
* 運算式和的HTL程式碼完成 `data-sly-*` 區塊陳述式。

此外，Brackets還為AEM前端開發人員提供了許多有用的功能：

* Photoshop檔案支援從PSD檔案中擷取資訊，例如圖層、測量、顏色、字型、文字等。
* 來自PSD的程式碼提示，可輕鬆在程式碼中重複使用此擷取的資訊。
* CSS前置處理器支援，例如LESS和SCSS。
* 以及數百種其他擴充功能，可滿足更具體的需求。

## 安裝 {#installation}

### 括弧 {#brackets}

AEM Brackets擴充功能支援Brackets 1.0或更新版本。

從下載最新的Brackets版本 [brackets.io](https://brackets.io/).

### 擴充功能 {#the-extension}

若要安裝擴充功能，請依照下列步驟進行：

1. 開啟Brackets。 在功能表中 **檔案**，選取 **Extension Manager...**
1. 輸入 **AEM** 在搜尋列中尋找 **AEM Brackets擴充功能**.

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 按一下 **安裝**.
1. 關閉對話方塊，並在安裝完成後Extension Manager。

## 快速入門 {#getting-started}

### Content-Package專案 {#the-content-package-project}

安裝擴充功能後，您可以從包含Brackets的檔案系統開啟content-package資料夾，以開始開發AEM元件。

專案必須至少包含：

1. a `jcr_root` 資料夾(例如 `myproject/jcr_root`)

1. a `filter.xml` 檔案(例如， `myproject/META-INF/vault/filter.xml`)；以取得有關架構的詳細資訊 `filter.xml` 檔案請參閱 [工作區篩選器定義](https://jackrabbit.apache.org/filevault/filter.html).

在方括弧中 **檔案** 功能表，選擇 **開啟資料夾……** 並選取 `jcr_root` 資料夾或父專案資料夾。

>[!NOTE]
>
>如果您沒有自己的專案與內容封裝，您可以嘗試 [HTL TodoMVC範例](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc). 在GitHub上，按一下 **下載ZIP**，將檔案解壓縮至本機，並依照上述指示，開啟 `jcr_root` 方括弧內的資料夾。 然後依照下列步驟設定 **專案設定** AEM ，最後透過執行 **匯出內容封裝** 如完整內容套件同步化一節中進一步指示。
>
>執行這些步驟後，您應該能夠存取 `/content/todo.html` 您的AEM開發執行個體上的URL，而且您可以開始在Brackets中修改程式碼，並瞭解在網頁瀏覽器中重新整理後，變更如何立即同步至AEM伺服器。

### 專案設定 {#project-settings}

若要將您的內容同步到AEM開發執行個體或從中同步內容，您需要定義您的專案設定。 您可以前往 **AEM** 功能表並選取 **專案設定……**

![chlimage_1-55](assets/chlimage_1-55a.png)

「專案設定」可讓您定義下列專案：

1. 伺服器URL (例如， `http://localhost:4502`)
1. 是否容忍沒有有效HTTPS憑證的伺服器（除非必要，否則請保持未勾選的狀態）
1. 用於同步內容的使用者名稱(例如， `admin`)
1. 使用者的密碼(例如， `admin`)

## 同步內容 {#synchronizing-content}

AEM Brackets擴充功能針對中定義的篩選規則所允許的檔案和資料夾，提供下列型別的內容同步 `filter.xml`：

### 自動同步已變更的檔案 {#automated-synchronization-of-changed-files}

這只會同步從Brackets到AEM例項的變更，反之則不會。

### 手動雙向同步 {#manual-bidirectional-synchronization}

在「專案總管」中，以滑鼠右鍵按一下任何檔案或資料夾，然後按一下 **匯出至伺服器** 或 **從伺服器匯入** 選項可供存取。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果選取的專案在 `jcr_root` 資料夾， **匯出至伺服器** 和 **從伺服器匯入** 內容功能表專案已停用。

### 完整內容套件同步 {#full-content-package-synchronization}

在 **AEM** 功能表， **匯出內容封裝** 或 **匯入內容封裝** 選項可讓您將整個專案與伺服器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步處理狀態 {#synchronization-status}

AEM Brackets擴充功能在Brackets視窗右側的工具列中有一個通知圖示，可指出上次同步處理的狀態：

* 綠色 — 所有檔案已成功同步化
* 藍色 — 同步處理作業正在進行中
* 黃色 — 部分檔案未同步
* 紅色 — 未同步處理任何檔案

按一下通知圖示會開啟「同步化狀態報告」對話方塊，其中列出每個已同步檔案的所有狀態。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>僅限被下列專案的篩選規則標籤為包含的內容： `filter.xml` 將會進行同步，無論使用何種同步方法。
>
>此外， `.vltignore` 支援檔案來排除與存放庫同步及從存放庫同步的內容。

## 編輯HTL程式碼 {#editing-htl-code}

AEM Brackets擴充功能也提供一些自動完成功能，以便寫入HTL屬性和運算式。

### 屬性自動完成 {#attribute-auto-completion}

1. 在HTML屬性中，輸入 `sly`. 屬性會自動完成至 `data-sly-`.
1. 在下拉式清單中選取HTL屬性。

### 運算式自動完成 {#expression-auto-completion}

在運算式內 `${}`，常用變數名稱會自動完成。

## 更多資訊 {#more-information}

AEM Brackets擴充功能是開放原始碼專案，由 [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) 組織，根據Apache授權2.0版：

* 程式碼存放庫： [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache授權2.0版： [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets程式碼編輯器也是開放原始碼專案，由 [Adobe Systems Incorporated](https://github.com/adobe) 組織：

* 程式碼存放庫： [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

歡迎您貢獻內容！
