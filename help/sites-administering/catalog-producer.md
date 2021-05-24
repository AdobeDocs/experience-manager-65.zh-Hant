---
title: 目錄製作者
seo-title: 目錄製作者
seo-description: 了解如何使用AEM Assets中的目錄製作程式，使用您的數位資產產生產品目錄。
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
source-wordcount: '901'
ht-degree: 0%

---

# 目錄製作程式{#catalog-producer}

了解如何使用AEM Assets中的目錄製作程式，使用您的數位資產產生產品目錄。

使用Adobe Experience Manager(AEM)Assets目錄製作程式，您可以使用從InDesign應用程式匯入的InDesign範本，建立品牌產品的目錄。 若要匯入InDesign範本，請先整合AEM Assets與InDesign伺服器。

## 與InDesign伺服器{#integrating-with-indesign-server}整合

在整合程式中，設定&#x200B;**DAM更新資產**&#x200B;工作流程，此工作流程適合與InDesign整合。 此外，為InDesign伺服器配置代理工作器。 如需詳細資訊，請參閱[將AEM Assets與InDesign Server整合](/help/assets/indesign.md)。

>[!NOTE]
>
>您可以先從InDesign檔案產生InDesign範本，再將其匯入AEM Assets。 有關詳細資訊，請參閱[使用檔案和模板](https://helpx.adobe.com/indesign/using/files-templates.html)。
>
>您可以將InDesign範本中的元素對應至XML標籤。 在目錄製作程式中映射具有模板屬性的產品屬性時，映射的標籤將顯示為屬性。 要了解InDesign檔案中的XML標籤，請參閱[為XML標籤內容](https://helpx.adobe.com/indesign/using/tagging-content-xml.html)。

>[!NOTE]
>
>只有InDesign檔案(.indd)是範本。 不支援副檔名為.indt的檔案。

## 建立目錄{#creating-a-catalog}

目錄製作者使用產品資訊管理(PIM)資料，將產品屬性與模板中顯示的XML屬性映射。 若要建立目錄，請執行下列步驟：

1. 從「資產」使用者介面，點選/按一下&#x200B;**AEM標誌**，然後前往&#x200B;**資產>目錄**。
1. 在&#x200B;**目錄**&#x200B;頁面中，從工具列點選/按一下&#x200B;**建立**，然後從清單中選取&#x200B;**目錄**。
1. 在&#x200B;**建立目錄**&#x200B;頁面中，輸入目錄的名稱和說明（可選），並指定標籤（如果有）。 您也可以為目錄新增縮圖影像。

   ![create_catalog](assets/create_catalog.png)

1. 點選/按一下&#x200B;**儲存**。 確認對話方塊會通知目錄已建立。 點選/按一下&#x200B;**Done**&#x200B;以關閉對話方塊。
1. 若要開啟您建立的目錄，請從&#x200B;**目錄**&#x200B;頁麵點選/按一下它。

   >[!NOTE]
   >
   >若要開啟目錄，您也可以點選/按一下前一個步驟提及的確認對話方塊中的&#x200B;**開啟**。

1. 若要將頁面新增至目錄，請從工具列點選/按一下「建立&#x200B;****」，然後選擇「**新頁面**」選項。
1. 從精靈中，選取頁面的InDesign範本。 然後，點選/按一下&#x200B;**Next**。
1. 指定頁面名稱和選用說明。 指定標籤（如果有的話）。
1. 點選/按一下工具列中的&#x200B;**建立**。 然後，點選/按一下對話方塊中的「**開啟**」。 產品的屬性會顯示在左窗格上。 InDesign範本的預先定義屬性會顯示在右窗格中。
1. 從左窗格，將產品屬性拖曳至InDesign範本屬性，並在它們之間建立對應。

   若要即時檢視頁面的顯示方式，請點選/按一下右窗格上的&#x200B;**預覽**&#x200B;標籤。

1. 若要建立更多頁面，請重複步驟6-9。 若要為其他產品建立類似頁面，請選取頁面，然後點選/按一下工具列中的「建立類似頁面&#x200B;**」圖示。**

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >您只能為具有類似結構的產品建立類似頁面。

   點選/按一下「新增」圖示，從產品選擇器選取產品，然後從工具列點選/按一下「選取&#x200B;**** 」。

   ![select_product](assets/select_product.png)

1. 在工具列中，按一下/點選&#x200B;**建立**。 點選/按一下&#x200B;**Done**&#x200B;以關閉對話方塊。 您的目錄中包含類似的頁面。
1. 若要將任何現有InDesign檔案新增至目錄，請從工具列點選/按一下「**建立**」，然後選擇「**新增至現有頁面」選項。**
1. 選取InDesign檔案，然後從工具列點選/按一下「**新增**」。 然後，點選/按一下&#x200B;**確定**&#x200B;以關閉對話方塊。

   如果您在目錄頁面中參考之產品的中繼資料已變更，這些變更不會自動反映在目錄頁面中。 標籤為&#x200B;**Stale**&#x200B;的橫幅出現在參考目錄頁面的產品影像上，表示參考產品的中繼資料不是最新的。

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   若要確保產品影像反映最新的中繼資料變更，請在「目錄」主控台中選取頁面，然後按一下/點選工具列中的&#x200B;**更新頁面**&#x200B;圖示。

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >若要變更所參考產品的中繼資料，請導覽至「產品」主控台(**AEM Logo** > **Commerce** > **Products**)，然後選取產品。 然後，按一下/點選工具列中的&#x200B;**檢視屬性**&#x200B;圖示，然後在資產的屬性頁面中編輯中繼資料。

1. 若要重新排列目錄中的頁面，請點選/按一下工具列中的&#x200B;**建立**&#x200B;圖示，然後從功能表中選擇&#x200B;**合併**。 在精靈中，頂端的輪播可讓您拖曳頁面，以重新排序頁面。 您也可以移除頁面。

1. 點選/按一下&#x200B;**Next**。 若要將現有InDesign檔案新增為封面，請點選/按一下&#x200B;**選擇封面**&#x200B;方塊旁的&#x200B;**瀏覽** ，並指定封面範本的路徑。
1. 點選/按一下「**儲存**」，然後點選/按一下「**完成**」以關閉確認對話方塊。
選擇**Done**選項時，將開啟一個對話框，以選擇是否要.pdf格式副本。
   ![匯出至](assets/CatalogPDF.png)
pdf如果選取了Acrobat(PDF)選項，除了indesign轉譯外，還會在/jcr:content/rendition  **中建** 立pdf轉譯。您可以在下載對話方塊中選取「轉譯」核取方塊，以下載所有轉譯。

1. 要為您建立的目錄生成預覽，請在&#x200B;**目錄**&#x200B;控制台中選擇它，然後按一下工具欄中的&#x200B;**預覽**&#x200B;表徵圖。

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   在預覽中檢閱目錄中的頁面。 點選/按一下&#x200B;**關閉**&#x200B;以關閉預覽。
