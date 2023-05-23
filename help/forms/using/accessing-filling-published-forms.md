---
title: 訪問和填寫已發佈表單
seo-title: Accessing and filling published forms
description: Forms門戶為Web開發人員提供元件，以在使用Adobe Experience Manager()創作的網站上建立和自定義表AEM單門戶。
seo-description: Forms Portal equips Web Developers with components to create and customize a forms portal on websites authored using Adobe Experience Manager (AEM).
uuid: 44731604-5d97-46fa-baa9-0c020c634fa7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 88dc8ef2-95ce-4906-ac28-eecc3a32a64e
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 訪問和填寫已發佈表單{#accessing-and-filling-published-forms}

在以表單為中心的門戶部署設定中，表單開發和門戶開發是兩個截然不同的活動。 表單設計者在儲存庫中設計和儲存表單時，Web開發人員會建立一個Web應用程式，以列出表單並處理提交。 然後，將Forms複製到web層，因為表單儲存庫和web應用程式之間沒有通信。

這通常會導致管理設定和生產延遲的問題。 例如，如果儲存庫中提供了較新版本的表單，則表單設計器將替換Web層上的表單，修改Web應用程式，並在公共站點上重新部署表單。 重新部署Web應用程式可能會導致伺服器停機。 由於伺服器停機是計畫內活動，因此無法立即將更改推送到公共站點。

Forms門戶減少了管理費用和生產延遲。 它使Web開發人員具有元件，以在使用Adobe Experience Manager()創作的網站上建立和自定義表AEM單門戶。

有關表單門戶及其功能的詳細資訊，請參見 [門戶上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md)。

## 表單門戶入門 {#getting-started-with-forms-portal}

導航到已發佈的表單門戶頁面。 有關建立表單門戶頁面的詳細資訊，請參見 [建立表單門戶頁](../../forms/using/creating-form-portal-page.md)。

roms門戶的Search和Lister元件顯示伺服器的Publish實例上可用的AEM表單。 此清單包括在建立表單門戶頁面時在篩選器中定義的所有表單或表單。 表單門戶頁面的外觀與下圖所示類似：

![表單門戶頁面示例 ](assets/forms-portal-page.png)

表單門戶頁面示例

### 搜索和李斯特 {#search-and-lister}

Search和Lister元件允許您向表單門戶添加以下功能：

* 在面板、卡或網格視圖中列出現成的表單。 它還支援自定義模板列出Forms管理器中特定資料夾中的表單。
* 指定表單的呈現方式 — HTML5、PDF或兩者。
* 指定PDF和XFA表單的呈現方式 — HTML5、PDF或兩者。 非XFA形式為HTML5。
* 啟用基於條件（如表單屬性、元資料和標籤）的表單搜索。
* 將表單資料提交到Servlet。
* 使用自定義樣式表(CSS)來自定義門戶的外觀。
* 建立到表單的連結。

您可以使用以下選項在Forms門戶頁面中搜索表單：

* 全文搜索
* 進階搜尋

全文搜索允許您根據指定的關鍵字查找和列出表單。

![高級搜索對話框](assets/search-panel.png)

高級搜索對話框

「高級搜索」允許您根據指定的表單屬性搜索表單。 這比全文搜索提供了更具體的結果。 高級搜索包括基於標籤、屬性（如「作者」、「說明」和「標題」）、修改日期和全文的搜索。

李斯特根據搜索參數顯示表單。 搜索結果中的每個表單都顯示一個表徵圖，該表徵圖被超連結到關聯表單。 您可以按一下該表徵圖以開啟和使用關聯的表單。

### 填寫表單 {#filling-a-form}

![示例自適應形式](assets/filling_a_form.png)

示例自適應形式

可以從頁面的「搜索」和「Lister」元件中提供的連結訪問表單。

每個表單都包含幫助資訊，用戶可以填寫表單。

#### 草稿和提交 {#drafts-and-submission}

用戶可以通過按一下「保存」按鈕來保存表單的草稿。 這允許用戶在提交表單之前在一段時間內處理表單。

表單（包括附件）中填寫的資料將作為草稿保存在伺服器上。 表單的草稿可以保存任意次數。 保存的表單將出現在頁面「草稿和提交」元件的「草稿」頁籤中。

填寫完表單後，用戶通過按一下表單上的「提交」按鈕提交表單。 提交的表單顯示在頁面的「草稿和提交」元件的「提交」頁籤中。

>[!NOTE]
>
>僅當將自適應表單的提交操作配置為「Forms門戶提交操作」時，提交的表單才會顯示在「已提交的Forms」頁籤中。 有關提交操作的詳細資訊，請參閱 [配置提交操作](../../forms/using/configuring-submit-actions.md)。

![草稿和提交元件](assets/draft-submission.png)

草稿和提交元件

## 使用提交的表單資料啟動新表單 {#start-a-new-form-using-submitted-form-data}

您需要經常填寫和提交某些表單。 如個人納稅申報表每年提交一次， 在這種情況下，雖然每次填寫表單時都會更改一些資訊，但大多數資訊像個人和家庭詳細資訊一樣不會更改。 但是，您仍需要從頭開始重新填寫整個表單。

AEM Forms可以幫助優化表單填寫體驗，並顯著減少重新填寫和提交表單的時間。 最終用戶可以使用已提交表單中的資料啟動新表單。 此功能內置於 [草稿和提交元件](../../forms/using/draft-submission-component.md)。 當您將「草稿」和「提交」元件添加到表單門戶頁面並發佈它時，最終用戶將在「已提交的Forms」和「草稿Forms」頁籤中找到一個選項，以便使用已提交表單中的資料啟動新表單。 下圖突出顯示該選項。

![新格式](assets/start-a-new-form.png)

按一下按鈕以啟動新表單時，它將開啟一個新表單，其中包含來自相應已提交表單的資料。 您現在可以根據需要複查和更新資訊並提交表單。
