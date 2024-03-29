---
title: 目錄製作者
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
description: 目錄製作者
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 1%

---

# 目錄製作者{#catalog-producer}

瞭解如何在AEM Assets中使用目錄製作程式，使用您的數位資產產生產品目錄。

使用Adobe Experience Manager (AEM) Assets目錄製作程式，您可以使用從InDesign應用程式匯入的InDesign範本建立品牌產品的目錄。 若要匯入InDesign範本，請先將AEM Assets與InDesign伺服器整合。

## 與InDesign伺服器整合 {#integrating-with-indesign-server}

在整合程式中，設定 **DAM更新資產** 工作流程，適合與InDesign整合。 此外，請為InDesign伺服器設定Proxy Worker。 如需詳細資訊，請參閱 [將AEM Assets與InDesign Server整合](/help/assets/indesign.md).

>[!NOTE]
>
>您可以先從InDesign檔案產生InDesign範本，然後再將其匯入AEM Assets。 如需詳細資訊，請參閱 [使用檔案和範本](https://helpx.adobe.com/indesign/using/files-templates.html).
>
>您可以將InDesign範本中的元素對應至XML標籤。 當您在「目錄製作程式」中將產品屬性與範本屬性對應時，對應的標籤會顯示為屬性。 若要瞭解InDesign檔案中的XML標籤，請參閱 [標籤XML的內容](https://helpx.adobe.com/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>只有InDesign檔案(.indd)被用作範本。 不支援副檔名為.indt的檔案。

## 建立目錄 {#creating-a-catalog}

目錄製作者使用產品資訊管理(PIM)資料，將產品屬性與範本中顯示的XML屬性對應。 若要建立目錄，請執行下列步驟：

1. 從Assets使用者介面，按一下 **AEM標誌**，並前往 **資產>目錄**.
1. 在 **目錄** 頁面，按一下 **建立** 從工具列中，然後選取 **目錄** 從清單中。
1. 在 **建立目錄** 頁面，輸入目錄的名稱和說明（選擇性），並指定標籤（如果有的話）。 您也可以為目錄新增縮圖影像。

   ![create_catalog](assets/create_catalog.png)

1. 按一下「**儲存**」。確認對話方塊會通知目錄已建立。 按一下 **完成** 以關閉對話方塊。
1. 若要開啟您建立的目錄，請從 **目錄** 頁面。

   >[!NOTE]
   >
   >若要開啟目錄，您也可以按一下 **開啟** 在上一步所述的確認對話方塊中。

1. 若要將頁面新增至目錄，請按一下 **建立** 從工具列中，然後選擇 **新頁面** 選項。
1. 從精靈中，選取頁面的InDesign範本。 然後，按一下 **下一個**.
1. 指定頁面的名稱和選擇性說明。 指定標籤（如果有）。
1. 按一下 **建立** 工具列中的。 然後，按一下 **開啟** 從對話方塊。 產品的屬性會顯示在左窗格中。 InDesign範本的預定義屬性會出現在右窗格中。
1. 從左窗格，將產品屬性拖曳至InDesign範本屬性，並建立它們之間的對應。

   若要即時檢視頁面的顯示方式，請按一下 **預覽** 索引標籤在右窗格中。

1. 若要建立更多頁面，請重複步驟6-9。 若要為其他產品建立類似的頁面，請選取頁面並按一下 **建立類似的頁面** 圖示。

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >您只能為具有類似結構的產品建立類似頁面。

   按一下新增圖示，從產品選擇器選取產品，然後按一下 **選取** 工具列中的。

   ![select_product](assets/select_product.png)

1. 在工具列中按一下 **建立**. 按一下 **完成** 以關閉對話方塊。 類似頁面會包含在您的目錄中。
1. 若要新增任何現有的InDesign檔案至您的目錄，請按一下 **建立** 從工具列中，然後選擇 **新增至現有頁面** 選項。
1. 選取InDesign檔案，然後按一下 **新增** 工具列中的。 然後，按一下 **確定** 以關閉對話方塊。

   如果您在目錄頁面中參考的產品中繼資料已變更，這些變更不會自動反映在目錄頁面中。 標示為的橫幅 **過時** 會出現在參考目錄頁面的產品影像中，指出參考產品的中繼資料不是最新的。

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   為確保產品影像反映最新的中繼資料變更，請在「目錄」主控台中選取頁面，然後按一下 **更新頁面** 圖示。

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >若要變更參考產品的中繼資料，請導覽至「產品」主控台(**AEM標誌** > **商務** > **產品**)，然後選取產品。 然後，按一下 **檢視屬性** 圖示，並在資產的屬性頁面中編輯中繼資料。

1. 若要重新排列目錄中的頁面，請按一下 **建立** 圖示，然後選擇 **合併** 功能表中。 在精靈中，頂端的轉盤可讓您拖曳頁面以重新排序頁面。 您也可以移除頁面。

1. 按一下「**下一步**」。若要新增現有的InDesign檔案作為封面頁，請按一下 **瀏覽** 在 **選擇封面** 方塊，並指定封面範本的路徑。
1. 按一下 **儲存**，然後按一下 **完成** 以關閉確認對話方塊。
選取 **完成** 選項，會開啟一個對話方塊以選取您是否需要.pdf轉譯。
   ![匯出為pdf](assets/CatalogPDF.png)
如果選取了Acrobat(PDF)選項，則會在中建立PDF轉譯  **/jcr：content/renditions** 除了indesign轉譯。 您可以選取下載對話方塊中的「轉譯」核取方塊來下載所有轉譯。

1. 若要為您建立的目錄產生預覽，請在 **目錄** 主控台，然後按一下 **預覽** 圖示。

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   在預覽中檢閱目錄中的頁面。 按一下 **關閉** 以關閉預覽。
