---
title: 存取和填寫已發佈的表單
description: Forms Portal為Web開發人員提供元件，以便在使用Forms (AEM)編寫的網站上建立和自訂Adobe Experience Manager Portal。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: aedf890c-a2f1-412f-8897-2492ffab335a
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# 存取和填寫已發佈的表單{#accessing-and-filling-published-forms}

在以表單為中心的入口網站部署設定中，表單開發和入口網站開發是兩個不同的活動。 當表單設計人員將表單設計和儲存在存放庫時，Web開發人員會建立一個Web應用程式到該清單表單並處理提交。 Forms接著會複製到Web層，因為Forms存放庫和Web應用程式之間沒有通訊。

這通常會導致管理設定和生產延遲的問題。 例如，如果儲存庫中有較新版本的表單，則表單設計工具會取代Web層上的表單、修改Web應用程式，並重新部署公用網站上的表單。 重新部署Web應用程式可能會造成伺服器停機時間。 由於伺服器停機時間是計畫的活動，因此變更無法立即推送至公用網站。

Forms Portal可減少管理開銷和生產延遲。 它為網頁開發人員配備元件，以便在使用Forms (AEM)編寫的網站上建立和自訂Adobe Experience Manager入口網站。

如需Forms入口網站及其功能的詳細資訊，請參閱 [在入口網站上發佈表單簡介](/help/forms/using/introduction-publishing-forms.md).

## Forms Portal快速入門 {#getting-started-with-forms-portal}

導覽至已發佈的Forms Portal頁面。 如需建立Forms入口網站頁面的詳細資訊，請參閱 [建立Forms入口網站頁面](../../forms/using/creating-form-portal-page.md).

Forms Portal的搜尋與清單元件會顯示AEM伺服器發佈執行個體上可用的表單。 此清單包含在編寫Forms入口網站頁面時，篩選條件中定義的所有表單或表單。 Forms入口網站頁面看起來類似於，如下圖所示：

![範例表單入口網站頁面 ](assets/forms-portal-page.png)

Forms Portal頁面範例

### 搜尋和列表器 {#search-and-lister}

「搜尋並製表器」元件可讓您將下列功能新增至Forms入口網站：

* 在面板、卡片或格線檢視中列出可立即使用的表單。 它也支援來自Forms Manager中特定資料夾的自訂範本清單表單。
* 指定表單的呈現方式 — HTML5、PDF或兩者。
* 指定PDF和XFA表單的呈現方式 — HTML5、PDF或兩者。 非XFA表單做為HTML5。
* 啟用根據條件搜尋表單，例如表單屬性、中繼資料和標籤。
* 將表單資料提交至servlet。
* 使用自訂樣式表(CSS)來自訂入口網站的外觀。
* 建立表單連結。

您可以使用下列選項，在Forms Portal頁面中搜尋表單：

* 全文檢索搜尋
* 進階搜尋

全文檢索搜尋可讓您根據指定的關鍵字尋找及列出表單。

![進階搜尋對話方塊](assets/search-panel.png)

進階搜尋對話方塊

進階搜尋可讓您根據指定的表單屬性來搜尋表單。 這比全文檢索搜尋提供更明確的結果。 進階搜尋包括根據標籤、屬性（例如作者、說明和標題）、修改日期和全文進行搜尋。

製表器會根據搜尋引數顯示表單。 搜尋結果中的每個表單都會顯示一個圖示，該圖示會以超連結方式連結到關聯的表單。 您可以按一下圖示以開啟及使用相關表單。

### 填寫表單 {#filling-a-form}

![最適化表單範例](assets/filling_a_form.png)

最適化表單範例

可從隨頁面的「搜尋並製表器」元件中的表單提供的連結存取表單。

每個表單都包含使用者填寫表單的說明資訊。

#### 草稿及提交 {#drafts-and-submission}

使用者可選擇按一下「 」，儲存表單草稿 **儲存**. 這可讓使用者在提交表單之前的一段時間內處理表單。

在表單中填入的資料（包括附件）會儲存為伺服器上的草稿。 表單的草稿可以儲存任意次數。 已儲存的表單會顯示在頁面「草稿與提交」元件的「草稿」標籤中。

填寫完表單後，使用者按一下表單上的提交按鈕即可提交表單。 提交的表單會顯示在頁面之「草稿和提交」元件的「提交」標籤中。

>[!NOTE]
>
>只有當最適化表單的提交動作設定為Forms Portal提交動作時，提交的表單才會顯示在已提交的Forms標籤中。 如需有關提交動作的詳細資訊，請參閱 [設定提交動作](../../forms/using/configuring-submit-actions.md).

![草稿和提交元件](assets/draft-submission.png)

草稿和提交元件

## 使用提交的表單資料開始新表單 {#start-a-new-form-using-submitted-form-data}

有些表格您必須經常填寫和提交。 例如，每年都會提交個人報稅表。 在這種情況下，雖然有些資訊會在您每次填寫表單時變更，但大部分像是個人和家庭詳細資料不會變更。 不過，您仍須從頭開始再次填寫整個表單。

AEM Forms可協助最佳化表單填寫體驗，並大幅縮短再次填寫和提交表單的時間。 一般使用者可使用提交的表單中的資料來開始新表單。 此功能內建於 [草稿與提交元件](../../forms/using/draft-submission-component.md). 當您將「草稿和提交」元件新增到Forms Portal頁面並發佈時，一般使用者會在已提交的Forms和「草稿Forms」標籤中看到一個選項。 選項可讓您使用已提交表單中的資料開始新表單。 下圖會醒目提示該選項。

![開始新表單](assets/start-a-new-form.png)

當您按一下按鈕以啟動新表單時，它會開啟一個新表單，其中包含來自相應提交表單的資料。 您現在可以根據需要檢閱和更新資訊，並提交表單。
