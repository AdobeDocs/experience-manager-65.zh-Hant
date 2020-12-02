---
title: 空格和圖元
seo-title: 開發AEM Mobile內容服務
description: 此頁面提供開發AEM Mobile Content Services的登陸頁面。
seo-description: 此頁面提供開發AEM Mobile Content Services的登陸頁面。
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 1%

---


# 空格和實體{#spaces-and-entities}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉換的專案使用SPA編輯器（例如React）。 [了解更多](/help/sites-developing/spa-overview.md).

空間是儲存透過Content Services REST API公開之實體的便利位置。 這特別有用，因為應用程式（或任何渠道）可與許多實體關聯。 強制實體位於空間內，會強制採用將應用程式需求分組的最佳實務。 或者，您可以將AEM中的應用程式與少量的「空格」建立關聯。

>[!NOTE]
>
>若要讓內容服務的任何通道都能使用內容，它必須位於空間之下。

## 建立空格{#creating-a-space}

如果使用者想要將許多內容和資產公開給行動應用程式，使用者會使用AEM Mobile儀表板建立空間。

對於尚未設定內容服務以搭配空格運作的首次使用者，AEM Mobile儀表板在選取&#x200B;**Content Services**&#x200B;後，只會顯示「應用程式」。

>[!CAUTION]
>
>**添加空間的先決條件**
>
>勾選「啟用AEM Content Services **以搭配空格使用」，並在您的AEM Mobile應用程式儀表板中啟用它。**
>
>如需詳細資訊，請參閱[管理內容服務](/help/mobile/developing-content-services.md)。

在控制面板中配置空格後，請依照下列步驟建立空格：

1. 從Content Services中選擇&#x200B;**空格**。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 選擇&#x200B;**建立**&#x200B;以建立空格。 輸入&#x200B;**Title**、**Name**&#x200B;和&#x200B;**Description**&#x200B;作為空間。

   按一下&#x200B;**建立**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空間{#managing-a-space}

建立空間後，按一下左側以管理清單中的空間。

您可以檢視空間的屬性、刪除空間，或將空間及其內容發佈至AEM發佈例項。

![chlimage_1-85](assets/chlimage_1-85.png)

**查看和編輯空間的屬性**

1. 從清單中選擇空間
1. 從工具欄中選擇&#x200B;**屬性**
1. 完成時按一下&#x200B;**關閉**

**發佈空** 間發佈空間時，該空間中的所有資料夾和實體也會發佈。

1. 按一下「空間控制台」清單中的空間表徵圖以選擇空間
1. 選擇&#x200B;**發佈樹**

>[!NOTE]
>
>您可以&#x200B;**取消發佈**&#x200B;空間，這會從發佈實例中刪除空間。
>
>下圖說明了發佈空間後可執行的操作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 在空間{#working-with-folders-in-a-space}中使用資料夾

空間可以包含資料夾，以幫助進一步組織空間的內容和資產。 使用者可以在空格下建立自己的階層。

### 建立資料夾{#creating-a-folder}

1. 按一下空間控制台清單中的空間並按一下&#x200B;**建立資料夾**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 為資料夾輸入&#x200B;**Title**、**Name、**&#x200B;和&#x200B;**Description**

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 按一下&#x200B;**建立**&#x200B;以在空間中建立資料夾

## 語言副本 {#language-copy}

>[!CAUTION]
>
>語言副本在本版本中無法完全運作。 它只設定結構。

**語言副本**&#x200B;功能可讓作者複製其主要語言副本，然後建立專案和工作流程以自動翻譯內容。 「語言副本」會建立正確的結構。 在空間中添加資料夾後，可以將「語言副本」添加到空間。

>[!NOTE]
>
>建議將任何可能翻譯的內容放在「語言複製」節點下。

### 添加語言副本{#adding-language-copy}

1. 建立空間後，按一下該空間可建立語言副本。

   按一下&#x200B;**建立**&#x200B;並選擇&#x200B;**語言副本**。

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >語言複製節點只能作為空間的直接子節點存在。

1. 選擇&#x200B;**Content Package Language&amp;ast;**，然後在&#x200B;**「建立語言副本」對話方塊中輸入** Title&amp;ast;**。**

   按一下&#x200B;**建立**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 建立語言副本後，該副本將出現在&#x200B;**語言主版**&#x200B;的空間中。

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >選擇&#x200B;**語言首頁**&#x200B;以查看語言副本資料夾。

### 從空間{#removing-a-folder-from-the-space}中刪除資料夾

1. 從空間內容清單中選擇資料夾
1. 從工具列按一下「刪除」****

   >[!NOTE]
   >
   >要導航到資料夾並查看其內容或添加子資料夾或實體，請按一下空間內容清單中該資料夾的標題。

## 在空間{#working-with-entities-in-a-space}中使用實體

實體代表透過web service端點公開的內容。 實體會儲存在空格中，因此可輕鬆找到並獨立於AEM儲存庫結構，而AEM儲存庫結構可保存其相關內容。

您可能希望在某些邏輯收集中將實體分組。 若要這麼做，您可以建立任意數目的檔案夾。

如果收集其他實體的實體子項以進行資料模型化，開發人員使用者可從「實體群組」模型類型（即裝即用）建立特定「群組模型」。

>[!NOTE]
>
>實體始終與空間相關聯，因此大部分實體用戶介面都通過空間控制台訪問。

### 建立實體{#creating-an-entity}

1. 開啟「空間」控制台，然後按一下空間標題。

   或者，您可以按一下清單中資料夾的標題，以導覽至資料夾。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 選擇圖元的模型。 這是您要建立的圖元類型。 按一下下一步。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以選擇&#x200B;**資產模型**、**頁面模型**，或您之前建立的實體類型模型。
   >
   >請參閱[建立模型](/help/mobile/administer-mobile-apps.md)以建立自訂實體。

1. 輸入實體的&#x200B;**標題**、**名稱**、**說明**&#x200B;和&#x200B;**標籤**。 按一下&#x200B;**建立**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成後，實體將出現在空間的子體中。

### 編輯實體{#editing-an-entity}

1. 建立實體後，請轉至資料夾或空間，然後從「空間」控制台選擇要編輯的實體。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 選擇要編輯的實體，然後按一下&#x200B;**編輯**。

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >視您選擇建立實體的範本而定，編輯和檢視實體屬性時，兩者的UI會有所不同。 如需詳細資訊，請參閱下列步驟。

   ***如果選擇將實體建立為「資產模型」(Assets Models***)的模板，則按一下「編輯」( **** Edit)允許您添加資產，如下圖所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，您也可以按一下&#x200B;**預覽**&#x200B;來檢視json連結。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果選擇用於建立實體的模板作為「頁面模型***」(Pages Models)，則按一下「編輯」( **** Edit)可添加資產，如下圖所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   按一下&#x200B;**Path**&#x200B;中的圖示以新增資產

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >新增實體後，必須儲存實體，「預覽」連結才能運作。 要查看預覽，請按一下「保存」。 ****&#x200B;按一下&#x200B;**預覽**&#x200B;會顯示新增資產的json，如下圖所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >將資產添加到實體後，可以選擇&#x200B;**保存**&#x200B;保存更改，或選擇&#x200B;**保存並關閉**&#x200B;保存並重定向到定義實體的空間控制台清單。

   此外，從空間控制台清單中選擇一個實體，然後按一下&#x200B;**屬性**&#x200B;以查看和編輯已定義實體的屬性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以編輯標題、說明、標籤，並將資產新增至實體。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 刪除實體{#removing-an-entity}

1. 從空間內容清單中選擇實體

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 按一下工具欄中的&#x200B;**Delete** ，從空間中刪除特定實體

### 發佈實體{#publishing-an-entity}

您可以選擇「**發佈樹狀結構**」或「**快速發佈**」來發佈實體。

1. 從空間控制台清單中選擇一個實體，然後按一下「發佈樹」**來發佈該實體及其子項。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或**,

   按一下「快速發佈」，以發佈該特定實體。****
