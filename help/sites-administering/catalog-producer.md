---
title: 目錄製作者
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: 目錄製作者
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 0%

---

# 目錄製作者{#catalog-producer}

瞭解如何使用AEM Assets的目錄製作商使用您的數字資產生成產品目錄。

使用Adobe Experience Manager(AEM)資產目錄製造商，您可以使用從InDesign應用程式導入的InDesign模板為品牌產品建立目錄。 要導入InDesign模板，請首先將AEM Assets與InDesign伺服器整合。

## 與InDesign伺服器整合 {#integrating-with-indesign-server}

作為整合過程的一部分，配置 **DAM更新資產** 工作流，適合與InDesign整合。 此外，為InDesign伺服器配置代理工作程式。 有關詳細資訊，請參閱 [將AEM Assets與InDesign Server](/help/assets/indesign.md)。

>[!NOTE]
>
>在將InDesign檔案導入AEM Assets之前，可以從InDesign檔案生成模板。 有關詳細資訊，請參閱 [使用檔案和模板](https://helpx.adobe.com/indesign/using/files-templates.html)。
>
>可以將InDesign模板中的元素映射到XML標籤。 在目錄製作器中將產品屬性與模板屬性映射時，映射的標籤將顯示為屬性。 要瞭解InDesign檔案中的XML標籤，請參見 [為XML添加標籤內容](https://helpx.adobe.com/indesign/using/tagging-content-xml.html)。

>[!NOTE]
>
>僅InDesign檔案(.indd)用作模板。 不支援副檔名為.indt的檔案。

## 建立目錄 {#creating-a-catalog}

目錄製作者使用產品資訊管理(PIM)資料將產品屬性與模板中顯示的XML屬性映射。 要建立目錄，請執行以下步驟：

1. 在「Assets（資產）」用戶介面中，點擊/按一下 **AEM徽標**，然後轉到 **資產>目錄**。
1. 在 **目錄** 頁面，點擊/按一下 **建立** ，然後選擇 **目錄** 清單中。
1. 在 **建立目錄** 頁，輸入目錄的名稱和說明（可選）並指定標籤（如果有）。 您還可以為目錄添加縮略圖。

   ![建立目錄](assets/create_catalog.png)

1. 點擊/按一下 **保存**。 確認對話框通知已建立目錄。 點擊/按一下 **完成** 按鈕
1. 要開啟您建立的目錄，請從 **目錄** 的子菜單。

   >[!NOTE]
   >
   >要開啟目錄，您還可以點擊/按一下 **開啟** 確認對話框。

1. 要向目錄中添加頁面，請點擊/按一下 **建立** ，然後選擇 **新建頁面** 的雙曲餘切值。
1. 從嚮導中，為頁面選擇InDesign模板。 然後，點擊/按一下 **下一個**。
1. 指定頁的名稱和可選說明。 指定標籤（如果有）。
1. 點擊/按一下 **建立** 的子菜單。 然後，點擊/按一下 **開啟** 的雙曲餘切值。 產品的屬性顯示在左窗格中。 InDesign模板的預定義屬性顯示在右窗格中。
1. 從左窗格中，將產品屬性拖動到InDesign模板屬性，並在它們之間建立映射。

   要查看頁面的即時顯示方式，請點擊/按一下 **預覽** 的子菜單。

1. 要建立更多頁面，請重複步驟6-9。 要為其他產品建立類似的頁面，請選擇該頁面並點擊/按一下 **建立類似頁面** 的子菜單。

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >您只能為具有相似結構的產品建立相似的頁面。

   點擊/按一下「添加」表徵圖，從產品選取器中選擇產品，然後點擊/按一下 **選擇** 的子菜單。

   ![選擇產品](assets/select_product.png)

1. 在工具欄中，按一下/點擊 **建立**。 點擊/按一下 **完成** 按鈕 類似的頁面也包含在目錄中。
1. 要將任何現有InDesign檔案添加到目錄中，請點擊/按一下 **建立** ，然後選擇 **添加到現有頁** 的雙曲餘切值。
1. 選擇InDesign檔案，然後點擊/按一下 **添加** 的子菜單。 然後，點擊/按一下 **確定** 按鈕

   如果更改了在目錄頁中引用的產品的元資料，則更改不會自動反映在目錄頁中。 標有 **過時** 在引用目錄頁中的產品影像上顯示，表示引用產品的元資料不是最新的。

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   要確保產品映像反映最新的元資料更改，請在目錄控制台中選擇該頁，然後按一下/點擊 **更新頁** 的子菜單。

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >要更改引用產品的元資料，請導航到「產品」控制台(**標AEM志** > **商業** > **產品**)，然後選擇產品。 然後，按一下/點擊 **查看屬性** 表徵圖，並在資產的「屬性」頁中編輯元資料。

1. 要重新排列目錄中的頁面，請點擊/按一下 **建立** 表徵圖，然後選擇 **合併** 的子菜單。 在嚮導中，頂部的旋轉軸允許您通過拖動頁面來重新排序頁面。 您也可以刪除頁面。

1. 點擊/按一下 **下一個**。 要將現有InDesign檔案添加為封面，請點擊/按一下 **瀏覽** 欄 **選擇封面** ，然後指定封面模板的路徑。
1. 點擊/按一下 **保存**，然後點擊/按一下 **完成** 按鈕關閉確認對話框。
選擇 **完成** 的子菜單。
   ![導出至pdf](assets/CatalogPDF.png)
如果選擇了Acrobat(PDF)選項，則在  **/jcr：內容/格式副本** 除了在設計中呈現。 通過選中「下載」對話框中的「格式副本」複選框，可以下載所有格式副本。

1. 要生成所建立目錄的預覽，請在 **目錄** 控制台，然後按一下 **預覽** 的子菜單。

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   在預覽中查看目錄中的頁面。 點擊/按一下 **關閉** 來修改標籤元素的屬性。
