---
title: AEM Brackets Extension
seo-title: AEM Brackets Extension
description: AEM Brackets Extension
seo-description: 'null'
uuid: 2f0dfa42-eb34-44ae-90eb-b5f321c03b79
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 8231a30a-dcb7-4156-bb45-c5a23e5b56ef
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 1%

---


# 方AEM括弧延伸{#aem-brackets-extension}

## 概覽 {#overview}

Brackets ExtensionAEM提供順暢的工作流程來編輯元件AEM和用戶端程式庫，並運用[Brackets](https://brackets.io/)程式碼編輯器的功能，讓您從程式碼編輯器存取Photoshop檔案和圖層。 擴充功能提供的簡易同步化功能（不需Maven或File Vault）可提高開發人員的效率，並協助知識有限的前AEM端開發人員參與專案。 此擴充功能也支援[HTML範本語言(HTL)](https://docs.adobe.com/content/help/zh-Hant/experience-manager-htl/using/overview.html)，這可免除JSP的複雜性，讓元件開發更輕鬆且更安全。

![chlimage_1-53](assets/chlimage_1-53a.png)

### 功能 {#features}

Brackets Extension的主要AEM功能包括：

* 將變更的檔案自動同步至開AEM發執行個體。
* 手動雙向同步檔案和資料夾。
* 項目的完整內容包同步。
* 運算式和`data-sly-*`區塊陳述式的HTL程式碼完成。

此外，Brackets還為字型端開發人員提供AEM許多實用功能：

* Photoshop檔案支援從PSD檔案擷取資訊，例如圖層、測量、色彩、字型、文字等。
* 從PSD中的程式碼提示，以輕鬆在程式碼中重複使用此擷取的資訊。
* CSS預處理器支援，例如LESS和SCSS。
* 還有數百個額外擴充功能，可涵蓋更多特定需求。

## 安裝{#installation}

### 括弧{#brackets}

Brackets延伸AEM功能支援Brackets 1.0版或更新版本。

從[brackets.io](https://brackets.io/)下載最新的Brackets版本。

### 副檔名{#the-extension}

要安裝擴展，請按如下步驟進行：

1. 開啟Brackets。 在菜單&#x200B;**檔案**&#x200B;中，選擇&#x200B;**Extension Manager...**
1. 在搜索欄中輸AEM入&#x200B;****&#x200B;並查找&#x200B;**AEM Brackets Extension**。

   ![chlimage_1-54](assets/chlimage_1-54a.png)

1. 按一下&#x200B;**Install**。
1. 安裝完成後，關閉對話框和Extension Manager。

## 快速入門 {#getting-started}

### Content-Package Project {#the-content-package-project}

在安裝擴充功能後，您就可以開始開發元AEM件，方法是使用Brackets從檔案系統開啟內容封裝檔案夾。

項目至少必須包含：

1. a `jcr_root`資料夾(例如`myproject/jcr_root`)

1. a `filter.xml`檔案(例如`myproject/META-INF/vault/filter.xml`;有關`filter.xml`檔案結構的詳細資訊，請參閱[工作區篩選定義](https://jackrabbit.apache.org/filevault/filter.html)。

在Brackets的&#x200B;**File**&#x200B;菜單中，選擇&#x200B;**開啟資料夾……**&#x200B;並選擇`jcr_root`資料夾或父項目資料夾。

>[!NOTE]
>
>如果您沒有包含內容套件的專案，則可以試用[HTL TodoMVC Example](https://github.com/Adobe-Marketing-Cloud/aem-sightly-sample-todomvc)。 在GitHub上，按一下「下載ZIP」，在本機解壓縮檔案，並依照上述指示，在Brackets中開啟「`jcr_root`」檔案夾。 ****&#x200B;然後，請依照下列步驟設定&#x200B;**專案設定**，最後依照完整內容封裝同步區段的進一步指示，執行&#x200B;**匯出內容封裝**，將整個封裝上傳至您的開發例項。
>
>在執行這些步驟後，您應可存取開發例項上的AEM`/content/todo.html` URL，並可開始在Brackets中修改程式碼，並檢視在Web瀏覽器中重新整理後，變更會立即同步至伺服AEM器。

### 專案設定{#project-settings}

為了同步您的內容與開發例項之AEM間，您必須定義您的「專案設定」。 您可前往&#x200B;**AEM**&#x200B;功能表並選擇&#x200B;**專案設定……**&#x200B;來完成此作業

![chlimage_1-55](assets/chlimage_1-55a.png)

「專案設定」可以定義：

1. 伺服器URL(例如`http://localhost:4502`)
1. 是否允許沒有有效HTTPS憑證的伺服器（請取消勾選，除非需要）
1. 用於同步內容的使用者名稱(例如`admin`)
1. 使用者的密碼(例如`admin`)

## 同步內容{#synchronizing-content}

Brackets AEM Extension為`filter.xml`中定義的篩選規則允許的檔案和檔案夾提供下列類型的內容同步：

### 自動同步更改的檔案{#automated-synchronization-of-changed-files}

這只會同步從Brackets到例項的變AEM更，但絕不會相反。

### 手動雙向同步{#manual-bidirectional-synchronization}

在「項目瀏覽器」中，通過按一下右鍵任何檔案或資料夾來開啟上下文菜單，可訪問&#x200B;**導出到伺服器**&#x200B;或&#x200B;**從伺服器**&#x200B;導入選項。

![chlimage_1-56](assets/chlimage_1-56a.png)

>[!NOTE]
>
>如果選定條目位於`jcr_root`資料夾外，則&#x200B;**導出到伺服器**&#x200B;和&#x200B;**從伺服器**&#x200B;導入上下文菜單條目將被禁用。

### 完整內容包同步{#full-content-package-synchronization}

在&#x200B;**AEM**&#x200B;功能表中，**匯出內容封裝**&#x200B;或&#x200B;**匯入內容封裝**&#x200B;選項可讓整個專案與伺服器同步。

![chlimage_1-57](assets/chlimage_1-57a.png)

### 同步狀態{#synchronization-status}

Brackets ExtensionAEM在Brackets視窗右側的工具列中加上通知圖示，指出上次同步的狀態：

* 綠色——所有檔案都已成功同步
* 藍色——正在進行同步操作
* 黃色——部分檔案未同步
* 紅色——未同步任何檔案

按一下通知表徵圖將開啟「同步狀態」報告對話框，其中列出了每個同步檔案的所有狀態。

![chlimage_1-58](assets/chlimage_1-58a.png)

>[!NOTE]
>
>無論使用何種同步方法，都只會同步`filter.xml`篩選規則中標示為包含的內容。
>
>此外，`.vltignore`檔案也支援將內容排除在與儲存庫同步和從儲存庫同步的範圍。

## 編輯HTL代碼{#editing-htl-code}

BracketsAEM擴充功能也包含一些自動完成功能，以簡化HTL屬性和運算式的編寫。

### 屬性自動完成{#attribute-auto-completion}

1. 在HTML屬性中，鍵入`sly`。 屬性自動完成至`data-sly-`。
1. 在下拉式清單中選取HTL屬性。

### 運算式自動完成{#expression-auto-completion}

在運算式`${}`中，通用變數名稱會自動完成。

## 更多資訊 {#more-information}

Brackets ExtensionAEM是開放原始碼專案，由[Adobe Marketing Cloud](https://github.com/Adobe-Marketing-Cloud)組織在GitHub上代管，位於Apache授權2.0版：

* 代碼儲存庫：[https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension](https://github.com/Adobe-Marketing-Cloud/aem-sightly-brackets-extension)
* Apache License, 2.0版：[https://www.apache.org/licenses/LICENSE-2.0.html](https://www.apache.org/licenses/LICENSE-2.0.html)

Brackets程式碼編輯器也是開放原始碼專案，由[Adobe Systems Incorporated](https://github.com/adobe)組織代管在GitHub上：

* 代碼儲存庫：[https://github.com/adobe/brackets](https://github.com/adobe/brackets)

盡情揮灑創意！
