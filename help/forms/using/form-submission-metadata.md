---
title: 從使用者資料新增資訊至表單提交中繼資料
seo-title: Adding information from user data to form submission metadata
description: 了解如何使用使用者提供的資料，將資訊新增至已提交表單的中繼資料。
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

# 從使用者資料新增資訊至表單提交中繼資料{#adding-information-from-user-data-to-form-submission-metadata}

您可以使用在表單的元素中輸入的值，計算草稿或表單提交的中繼資料欄位。 中繼資料可讓您根據使用者資料篩選內容。 例如，使用者在表單的名稱欄位中輸入John Doe。 您可以使用此資訊計算元資料，這些元資料可將此提交分類為縮寫JD。

若要使用使用者輸入的值運算中繼資料欄位，請在中繼資料中新增表單的元素。 當使用者在該元素中輸入值時，指令碼會使用值來運算資訊。 此資訊會新增至中繼資料中。 將元素新增為中繼資料欄位時，您會提供其索引鍵。 索引鍵會新增為中繼資料中的欄位，並針對該欄位記錄計算資訊。

例如，健康保險公司發佈表單。 在此表單中，欄位會擷取使用者的年齡。 若干使用者提交表單後，客戶會想檢查特定年齡範圍內的所有提交內容。 額外的中繼資料不會處理隨著表單數量增加而變得複雜的所有資料，而是可協助客戶。 表單作者可設定將使用者填入的屬性/資料儲存在最上層，以便最輕鬆進行搜尋。 其他中繼資料是使用者填入的資訊，如作者所設定，儲存在中繼資料節點的頂層。

請考慮另一個擷取電子郵件id和電話號碼的表單範例。 當使用者以匿名方式造訪此表單並放棄表單時，作者可將表單設定為自動儲存電子郵件id和電話號碼。 此表單會自動儲存，而電話號碼和電子郵件ID會儲存在草稿的中繼資料節點中。 此設定的使用案例為銷售機會管理控制面板。

## 將表單元素新增至中繼資料 {#adding-form-elements-to-metadata}

執行下列步驟以在中繼資料中新增元素：

1. 在編輯模式中開啟最適化表單。\
   若要在編輯模式中開啟表單，請在表單管理器中，選取表單並點選 **開啟**.
1. 在編輯模式中，選取元件，點選 ![欄位層級](assets/field-level.png) > **適用性表單容器**，然後點選 ![cppr](assets/cmppr.png).
1. 在側欄中，按一下 **中繼資料**.
1. 在「中繼資料」區段中，按一下 **新增**.
1. 使用中繼資料索引標籤的值欄位來新增指令碼。 您新增的指令碼會收集表單上元素的資料，並計算饋送至中繼資料的值。

   例如， **true** 如果輸入的年齡大於21，則會記錄在中繼資料中，且 **false** 小於21時則記錄。 在「中繼資料」索引標籤中輸入下列指令碼：

   `(agebox.value >= 21) ? true : false`

   ![中繼資料指令碼](assets/add-element-metadata.png)

   在「元資料」頁簽中輸入的指令碼

1. 按一下&#x200B;**「確定」**。

當使用者在選為中繼資料欄位的元素中輸入資料後，計算資訊便記錄在中繼資料中。 您可以在設定為儲存中繼資料的存放庫中看到中繼資料。

## 查看更新的表單提交元資料： {#seeing-updated-form-nbsp-submission-metadata}

在上例中，中繼資料儲存在CRX存放庫中。 中繼資料看起來類似：

![中繼資料](assets/metadata_entry_new.png)

如果您在中繼資料中新增核取方塊元素，選取的值會以逗號分隔字串的形式儲存。 例如，您可在表單中新增核取方塊元件，並將其名稱指定為 `checkbox1`. 在複選框元件屬性中，添加值0、1和2的「駕駛證」、「社會安全號」和「護照」項。

![從核取方塊儲存多個值](assets/checkbox-metadata.png)

您選取最適化表單容器，然後在表單屬性中新增中繼資料索引鍵 `cb1` 商店 `checkbox1.value`，並發佈表單。 當客戶填寫表單時，客戶會在核取方塊欄位中選取「護照」和「社會安全號碼」選項。 值1和2儲存為1、2，在提交元資料的cb1欄位中。

![核取方塊欄位中選取之多個值的中繼資料項目](assets/metadata-entry.png)

>[!NOTE]
>
>上述範例僅供學習之用。 請確定您在AEM Forms實作中所設定的正確位置尋找中繼資料。
