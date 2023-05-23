---
title: 括弧AEM擴展
seo-title: AEM Brackets Extension
description: 括弧AEM擴展
seo-description: null
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: 43a30b5ba76ea470cc50a962d4f04b4a1508964d
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 2%

---

# 括弧AEM擴展{#aem-brackets-extension}

## 概觀 {#overview}

方括AEM號擴展提供了一個平滑的工作流AEM程來編輯元件和客戶端庫，並利用 [括弧](https://brackets.io/) 代碼編輯器，它允許從代碼編輯器內訪問Photoshop檔案和層。 擴展提供的輕鬆同步（不需要Maven或File Vault）提高了開發人員效率，還幫助知識有限的前AEM端開發人員參與項目。 此擴展還為 [HTML模板語言(HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html)這就消除了JSP的複雜性，使元件開發更容易、更安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

「括弧」(Crakets)「延伸AEM」(Extension)的主要功能是：

* 將更改的檔案自動同步到AEM開發實例。
* 檔案和資料夾的手動雙向同步。
* 項目的完整內容包同步。
* 用於表達式和 `data-sly-*` 塊語句。

此外，方括弧還為字型端開發AEM人員提供了許多有用功能：

* Photoshop檔案支援從PSD檔案中提取資訊，如圖層、測量、顏色、字型、文本等。
* PSD中的代碼提示，以便輕鬆地在代碼中重用提取的資訊。
* CSS預處理器支援，如LESS和SCSS。
* 還有數以百計的擴展，涵蓋更具體的需求。

## 安裝 {#installation}

### 括弧 {#brackets}

括弧延AEM伸支援1.0或更高版本的括弧。

從下載最新的括弧版本 [括弧.io](https://brackets.io/)。

### 擴展 {#the-extension}

要安裝擴展，請按如下方式繼續：

1. 開啟括弧。 在菜單中 **檔案**&#x200B;選中 **Extension Manager...**
1. 輸入 **AEM** 在搜索欄中查找 **括弧AEM擴展**。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 按一下 **安裝**。
1. 安裝完成後關閉對話框和Extension Manager。

## 快速入門 {#getting-started}

### 內容包項目 {#the-content-package-project}

安裝擴展後，可以通過從檔案系統AEM中開啟帶有方括弧的內容包資料夾來開始開發元件。

項目必須至少包含：

1. a `jcr_root` 資料夾(例如 `myproject/jcr_root`)

1. a `filter.xml` 檔案(例如 `myproject/META-INF/vault/filter.xml`);的 `filter.xml` 檔案請參閱 [工作區篩選器定義](https://jackrabbit.apache.org/filevault/filter.html)。

括弧中 **檔案** 菜單，選擇 **開啟資料夾……** 然後選擇 `jcr_root` 資料夾或父項目資料夾。

>[!NOTE]
>
>如果您沒有包含內容包的項目，可以嘗試 [HTL TodoMVC示例](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)。 在GitHub上，按一下 **下載ZIP**，在本地解壓檔案，並按上面的說明開啟 `jcr_root` 方括弧中的。 然後按照以下步驟設定 **項目設定**，並通過執行以下操作將整個AEM包上載到開發實例 **導出內容包** 按照「完整內容包同步」部分的進一步說明。
>
>完成這些步驟後，您應能夠訪問 `/content/todo.html` 開發實AEM例上的URL，您可以開始對方括弧中的代碼進行修改，並查看在Web瀏覽器進行刷新後如何立即將更改同步到服AEM務器。

### 項目設定 {#project-settings}

為了將內容與開發實例同步，AEM需要定義項目設定。 通過 **AEM** 菜單和選擇 **項目設定……**

![chlimage_1-55](assets/chlimage_1-55a.png)

項目設定允許定義：

1. 伺服器URL(例如 `http://localhost:4502`)
1. 是否容忍沒有有效HTTPS證書的伺服器（未選中，除非需要）
1. 用於同步內容的用戶名(例如 `admin`)
1. 用戶的密碼(例如 `admin`)

## 同步內容 {#synchronizing-content}

方括弧AEM擴展為檔案和資料夾提供了下列類型的內容同步，這些檔案和資料夾由中定義的篩選規則所允許 `filter.xml`:

### 已更改檔案的自動同步 {#automated-synchronization-of-changed-files}

這將僅同步從方括弧到實例的AEM更改，但永遠不會同步。

### 手動雙向同步 {#manual-bidirectional-synchronization}

在「項目瀏覽器」中，按一下右鍵任何檔案或資料夾，開啟上下文菜單， **導出到伺服器** 或 **從伺服器導入** 選項。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果所選條目位於 `jcr_root` 資料夾 **導出到伺服器** 和 **從伺服器導入** 上下文菜單條目被禁用。

### 完整內容包同步 {#full-content-package-synchronization}

在 **AEM** 的子菜單。 **導出內容包** 或 **導入內容包** 選項允許將整個項目與伺服器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步狀態 {#synchronization-status}

「方AEM括弧擴展」在「方括弧」窗口右側的工具欄中顯示一個通知表徵圖，該表徵圖指示上次同步的狀態：

* 綠色 — 所有檔案都已成功同步
* 藍色 — 同步操作正在進行
* 黃色 — 某些檔案未同步
* 紅色 — 未同步任何檔案

按一下通知表徵圖將開啟「同步狀態」報告對話框，其中列出了每個已同步檔案的所有狀態。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>只有篩選規則中標籤為包含的內容 `filter.xml` 將同步，而不管使用的同步方法。
>
>此外， `.vltignore` 支援將內容從同步到儲存庫和從儲存庫中排除。

## 編輯HTL代碼 {#editing-htl-code}

方括弧AEM擴展還具有一些自動完成功能，可簡化HTL屬性和表達式的編寫。

### 屬性自動完成 {#attribute-auto-completion}

1. 在HTML屬性中，鍵入 `sly`。 屬性自動完成為 `data-sly-`。
1. 在下拉清單中選擇HTL屬性。

### 表達式自動完成 {#expression-auto-completion}

在表達式內 `${}`，公共變數名稱自動完成。

## 更多資訊 {#more-information}

括弧AEM擴展是一個開源項目，由 [Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud) 組織，在Apache許可證2.0版下：

* 代碼儲存庫： [https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache許可證，版本2.0: [https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

括弧代碼編輯器也是一個開源項目，由 [Adobe Systems Incorporated](https://github.com/adobe) 組織：

* 代碼儲存庫： [https://github.com/adobe/brackets](https://github.com/adobe/brackets)

請隨便貢獻！
