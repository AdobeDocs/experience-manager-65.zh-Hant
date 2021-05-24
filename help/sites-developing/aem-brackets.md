---
title: AEM Brackets擴充功能
seo-title: AEM Brackets擴充功能
description: AEM Brackets擴充功能
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
exl-id: 829d8256-b415-4a44-a353-455ac16950f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---

# AEM Brackets擴充功能{#aem-brackets-extension}

## 概覽 {#overview}

AEM Brackets擴充功能提供編輯AEM元件和用戶端程式庫的流暢工作流程，並運用[Brackets](https://brackets.io/)程式碼編輯器的功能，此編輯器可讓您從程式碼編輯器中存取Photoshop檔案和層。 擴充功能提供的輕鬆同步化功能（不需要Maven或File Vault）可提高開發人員的效率，也有助於具備有限AEM知識的前端開發人員參與專案。 此擴充功能也提供[HTML範本語言(HTL)](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)的部分支援，免除了JSP的複雜性，讓元件開發更輕鬆、更安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

AEM Brackets擴充功能的主要功能為：

* 將變更的檔案自動同步至AEM開發例項。
* 手動雙向同步檔案和資料夾。
* 專案的完整內容套件同步。
* 運算式和`data-sly-*`區塊陳述式的HTL程式碼完成。

此外，Brackets還隨附許多對AEM字型端開發人員有用的功能：

* Photoshop檔案支援從PSD檔案中擷取資訊，如圖層、測量、顏色、字型、文字等。
* 從PSD中提示代碼，以便在代碼中輕鬆地重複利用這些提取的資訊。
* CSS預處理器支援，如LESS和SCSS。
* 還有數以百計的額外擴充功能，可涵蓋更具體的需求。

## 安裝 {#installation}

### 方括弧 {#brackets}

AEM Brackets擴充功能支援Brackets 1.0版或更新版本。

請從[brackets.io](https://brackets.io/)下載最新的Brackets版本。

### 擴充功能{#the-extension}

若要安裝擴充功能，請依下列步驟執行：

1. 開啟括弧。 在菜單&#x200B;**檔案**&#x200B;中，選擇&#x200B;**Extension Manager...**
1. 在搜尋列中輸入&#x200B;**AEM**&#x200B;並尋找&#x200B;**AEM Brackets Extension**。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 按一下&#x200B;**安裝**。
1. 安裝完成後，關閉對話方塊和Extension Manager。

## 快速入門 {#getting-started}

### 內容包項目{#the-content-package-project}

安裝擴充功能後，您可以使用Brackets從檔案系統開啟內容套件資料夾，以開始開發AEM元件。

專案必須至少包含：

1. a `jcr_root`資料夾(例如`myproject/jcr_root`

1. a `filter.xml`檔案(例如`myproject/META-INF/vault/filter.xml`);有關`filter.xml`檔案結構的詳細資訊，請參閱[工作區篩選器定義](https://jackrabbit.apache.org/filevault/filter.html)。

在括弧的&#x200B;**檔案**&#x200B;菜單中，選擇&#x200B;**開啟資料夾……**&#x200B;並選擇`jcr_root`資料夾或父項目資料夾。

>[!NOTE]
>
>如果您沒有包含內容包的專案，則可以嘗試[ HTL TodoMVC示例](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)。 在GitHub上，按一下「**下載ZIP**」，在本機解壓檔案，並依照上述指示，在方括弧中開啟`jcr_root`資料夾。 然後，請依照下列步驟來設定&#x200B;**專案設定**，最後執行&#x200B;**匯出內容套件**，將整個套件上傳至AEM開發執行個體，如完整內容套件同步區段中的進一步指示。
>
>執行這些步驟後，您應該可以存取AEM開發執行個體上的`/content/todo.html` URL，並開始對Brackets中的程式碼進行修改，並查看在Web瀏覽器中重新整理後，變更會立即同步至AEM伺服器。

### 專案設定{#project-settings}

若要將內容與AEM開發執行個體同步，您必須定義專案設定。 您可以前往&#x200B;**AEM**&#x200B;功能表，然後選擇&#x200B;**專案設定……**

![chlimage_1-55](assets/chlimage_1-55a.png)

「專案設定」可定義：

1. 伺服器URL(例如`http://localhost:4502`
1. 是否允許沒有有效HTTPS證書的伺服器（請取消選中，除非需要）
1. 用於同步內容的使用者名稱(例如`admin`
1. 使用者的密碼(例如`admin`

## 同步內容{#synchronizing-content}

AEM Brackets擴充功能針對`filter.xml`中定義的篩選規則所允許的檔案和資料夾，提供下列類型的內容同步：

### 自動同步更改的檔案{#automated-synchronization-of-changed-files}

這只會將Brackets的變更同步至AEM例項，但絕不會以相反的方式同步。

### 手動雙向同步{#manual-bidirectional-synchronization}

在「項目資源管理器」中，通過按一下右鍵任何檔案或資料夾來開啟上下文菜單，並且可以訪問&#x200B;**導出到伺服器**&#x200B;或&#x200B;**從伺服器**&#x200B;導入選項。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果所選條目位於`jcr_root`資料夾之外，則&#x200B;**導出到伺服器**&#x200B;和&#x200B;**從伺服器**&#x200B;導入上下文菜單條目將被禁用。

### 完整內容包同步{#full-content-package-synchronization}

在&#x200B;**AEM**&#x200B;菜單中，**導出內容包**&#x200B;或&#x200B;**導入內容包**&#x200B;選項允許將整個項目與伺服器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步狀態{#synchronization-status}

AEM Brackets Extension在Brackets視窗右側的工具列中顯示通知圖示，指出上次同步的狀態：

* 綠色 — 已成功同步所有檔案
* 藍色 — 正在執行同步操作
* 黃色 — 某些檔案未同步
* 紅色 — 未同步任何檔案

按一下通知表徵圖將開啟「同步狀態」報告對話框，其中列出每個已同步檔案的所有狀態。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>無論使用何種同步方法，都只會同步`filter.xml`中的篩選規則所標示為包含的內容。
>
>此外，`.vltignore`檔案支援將內容排除在與存放庫同步或與存放庫同步之外。

## 編輯HTL程式碼{#editing-htl-code}

AEM Brackets擴充功能也提供一些自動完成功能，以方便編寫HTL屬性和運算式。

### 屬性自動完成{#attribute-auto-completion}

1. 在HTML屬性中，鍵入`sly`。 屬性自動完成為`data-sly-`。
1. 在下拉式清單中選取HTL屬性。

### 表達式自動完成{#expression-auto-completion}

在運算式`${}`中，通用變數名稱會自動完成。

## 更多資訊 {#more-information}

AEM Brackets擴充功能是開放原始碼專案，由[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud)組織在GitHub上，依Apache授權規範2.0版托管：

* 代碼儲存庫：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache授權，2.0版：[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets程式碼編輯器也是開放原始碼專案，由[Adobe Systems Incorporated](https://github.com/adobe)組織托管於GitHub:

* 代碼儲存庫：[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

歡迎貢獻內容！
