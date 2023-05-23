---
title: 從用戶資料添加資訊到表單提交元資料
seo-title: Adding information from user data to form submission metadata
description: 瞭解如何使用用戶提供的資料將資訊添加到已提交表單的元資料中。
seo-description: Learn how to add information to metadata of a submitted form with user provided data.
uuid: c3eea3c0-31f8-4bf8-b5cf-34f907bdbdba
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 2c971da0-5bd5-40d1-820d-4efc2a44b49d
docset: aem65
feature: Adaptive Forms
exl-id: 5ca850e3-30f0-4384-b615-356dc3c2ad0d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# 從用戶資料添加資訊到表單提交元資料{#adding-information-from-user-data-to-form-submission-metadata}

您可以使用在表單元素中輸入的值來計算草稿或表單提交的元資料欄位。 元資料允許您根據用戶資料篩選內容。 例如，用戶在表單的名稱欄位中輸入John Doe。 您可以使用此資訊來計算元資料，該元資料可以將此提交分類為縮寫JD。

要使用用戶輸入的值計算元資料欄位，請在元資料中添加表單的元素。 當用戶在該元素中輸入值時，指令碼將使用該值計算資訊。 此資訊將添加到元資料中。 將元素添加為元資料欄位時，將為其提供鍵。 該密鑰被添加為元資料中的欄位，並且根據該欄位記錄計算的資訊。

例如，一家健康保險公司發佈一份表格。 在此表單中，欄位捕獲最終用戶的年齡。 在多個用戶提交表單後，客戶希望檢查特定年齡範圍內的所有提交。 與其查看隨表單數量增加而變得複雜的所有資料，其他元資料可幫助客戶。 表單作者可以配置哪些由最終用戶填寫的屬性/資料儲存在頂層，以便最容易進行搜索。 其他元資料是用戶填充的資訊，儲存在元資料節點的頂層，如作者所配置的那樣。

請考慮另一個捕獲電子郵件ID和電話號碼的表單示例。 當用戶匿名訪問此表單並放棄該表單時，作者可以將表單配置為自動保存電子郵件ID和電話號碼。 此表單是自動保存的，電話號碼和電子郵件ID儲存在草稿的元資料節點中。 此配置的使用情形是銷售線索管理儀表板。

## 將表單元素添加到元資料 {#adding-form-elements-to-metadata}

執行以下步驟以在元資料中添加元素：

1. 在編輯模式下開啟自適應窗體。\
   要在編輯模式下開啟窗體，請在窗體管理器中選擇窗體，然後點擊 **開啟**。
1. 在編輯模式下，選擇一個元件，點擊 ![欄位級](assets/field-level.png) > **自適應窗體容器**，然後按一下 ![招商](assets/cmppr.png)。
1. 在提要欄中，按一下 **元資料**。
1. 在「元資料」部分，按一下 **添加**。
1. 使用「元資料」頁籤的「值」欄位添加指令碼。 您添加的指令碼從表單上的元素收集資料，並計算饋送到元資料的值。

   比如說， **真** 如果輸入的年齡大於21，則記錄在元資料中， **假** 的下界。 在元資料頁籤中輸入以下指令碼：

   `(agebox.value >= 21) ? true : false`

   ![元資料指令碼](assets/add-element-metadata.png)

   在元資料頁籤中輸入的指令碼

1. 按一下&#x200B;**「確定」**。

當用戶在選擇為元資料欄位的元素中輸入資料後，計算的資訊被記錄在元資料中。 您可以在配置用於儲存元資料的儲存庫中查看元資料。

## 查看更新的表單提交元資料： {#seeing-updated-form-nbsp-submission-metadata}

例如，元資料儲存在CRX儲存庫中。 元資料如下所示：

![中繼資料](assets/metadata_entry_new.png)

如果在元資料中添加複選框元素，則選定值將儲存為逗號分隔的字串。 例如，在表單中添加複選框元件，並將其名稱指定為 `checkbox1`。 在複選框元件屬性中，為值0、1和2添加「駕照」、「社會保險編號」和「護照」。

![從複選框儲存多個值](assets/checkbox-metadata.png)

選擇自適應表單容器，並在表單屬性中添加元資料鍵 `cb1` 商店 `checkbox1.value`，然後發佈窗體。 當客戶填寫表單時，客戶會在複選框欄位中選擇「護照」和「社會保險編號」選項。 值1和值2在提交元資料的cb1欄位中儲存為1、2。

![在複選框欄位中選擇的多個值的元資料條目](assets/metadata-entry.png)

>[!NOTE]
>
>上例僅用於學習。 確保在AEM Forms實施中配置的正確位置查找元資料。
