---
title: 空間和實體
seo-title: Developing AEM Mobile Content Services
description: 此頁面提供開發AEM Mobile內容服務的登陸頁面。
seo-description: This page serves a landing page for developing AEM Mobile Content Services.
uuid: eab5a61b-a9e8-4863-90a3-df1f18510cd8
contentOwner: Jyotika Syal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: ef568577-c74e-4fc2-b66e-eedac2948310
exl-id: 44591900-b01b-4a33-9910-839564477e7d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 3%

---

# 空間和實體{#spaces-and-entities}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

「空間」是儲存透過「內容服務REST API」公開之實體的便利位置。 這特別有用，因為應用程式（或任何管道）可以與許多實體相關聯。 強制實體位於空間內，可強制將應用程式需求分組的最佳實務。 您可以選擇將AEM中的應用程式與少量空格建立關聯。

>[!NOTE]
>
>若要讓內容服務的任何管道都能使用某些內容，其位置必須位於空間下方。

## 建立空間 {#creating-a-space}

如果使用者想要將一堆內容和資產公開至行動應用程式，使用者會使用AEM Mobile控制面板建立空間。

對於尚未將內容服務設定為搭配空格使用的使用者，AEM Mobile控制面板在選取 **內容服務**.

>[!CAUTION]
>
>**添加空間的先決條件**
>
>檢查 **啟用AEM Content Services** 使用空格，並在AEM Mobile應用程式控制面板中啟用。
>
>請參閱 [管理內容服務](/help/mobile/developing-content-services.md) 以取得更多詳細資訊。

在控制面板中配置空格後，請按照以下步驟建立空格：

1. 選擇 **空格** 從內容服務。

   ![chlimage_1-83](assets/chlimage_1-83.png)

1. 選擇 **建立** 來建立空間。 輸入 **標題**, **名稱**，和 **說明** 為了空間。

   按一下&#x200B;**建立**。

   ![chlimage_1-84](assets/chlimage_1-84.png)

## 管理空間 {#managing-a-space}

建立空間後，按一下左側以管理清單中的空間。

您可以檢視空間的屬性、刪除空間，或將空間及其內容發佈至AEM發佈例項。

![chlimage_1-85](assets/chlimage_1-85.png)

**查看和編輯空間的屬性**

1. 從清單中選取空格
1. 選擇 **屬性** 從工具列
1. 按一下 **關閉** 完成時

**發佈空間** 發佈空間時，該空間中的所有資料夾和實體也將發佈。

1. 按一下「空間控制台」清單中的表徵圖，選擇空間
1. 選擇 **發佈樹**

>[!NOTE]
>
>您可以 **取消發佈** 空間，會從發佈執行個體移除空間。
>
>下圖說明了發佈空間後可執行的動作。

![chlimage_1-86](assets/chlimage_1-86.png)

## 在空間中使用資料夾 {#working-with-folders-in-a-space}

空間可以包含資料夾，以幫助進一步組織空間的內容和資產。 使用者可以在空格下建立自己的階層。

### 建立資料夾 {#creating-a-folder}

1. 按一下空間控制台清單中的空間，然後按一下 **建立資料夾**

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. 輸入 **標題**, **名稱，** 和 **說明** （針對資料夾）

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. 按一下 **建立** 在空間中建立資料夾

## 語言副本 {#language-copy}

>[!CAUTION]
>
>語言副本在此版本中無法完全正常運作。 它只設定結構。

此 **語言副本** 功能可讓作者複製其主語言副本，然後建立專案和工作流程來自動翻譯內容。 「語言副本」會建立正確的結構。 在空間中添加資料夾後，可以將語言副本添加到空間。

>[!NOTE]
>
>建議將任何可能翻譯的內容放在「語言副本」節點下。

### 添加語言副本 {#adding-language-copy}

1. 建立空間後，按一下該空間以建立語言副本。

   按一下 **建立** 選擇 **語言副本**.

   ![chlimage_1-89](assets/chlimage_1-89.png)

   >[!NOTE]
   >
   >語言副本節點只能作為空間的直接子節點存在。

1. 選擇 **內容包語言(&amp;A);** 並輸入 **標題(&amp;A);** in **建立語言副本** 對話框。

   按一下&#x200B;**建立**。

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. 建立語言副本後，該副本會顯示在 **語言主版**.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   >[!NOTE]
   >
   >選擇 **語言主版** 查看語言副本資料夾。

### 從空間中刪除資料夾 {#removing-a-folder-from-the-space}

1. 從空間內容清單中選擇資料夾
1. 按一下 **刪除** 從工具列

   >[!NOTE]
   >
   >要導航到資料夾並查看其內容或添加子資料夾或實體，請按一下空間內容清單中資料夾的標題。

## 使用空間中的實體 {#working-with-entities-in-a-space}

實體代表透過Web服務端點公開的內容。 實體會儲存在空格中，以便輕鬆找到，並且與保存其相關內容的AEM存放庫結構無關。

您可能希望將實體分組到某個邏輯收集中。 若要這麼做，您可以建立任意數量的資料夾。

如果為資料模型收集了實體子項（即其他實體），則開發人員用戶可以從「實體組」模型類型（現成提供）建立特定的「組模型」。

>[!NOTE]
>
>實體始終與空間相關聯，因此大多數實體用戶介面通過空間控制台訪問。

### 建立實體 {#creating-an-entity}

1. 開啟空間控制台，然後按一下空間的標題。

   或者，您可以按一下清單中資料夾標題，以導覽至資料夾。

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. 選擇圖元的模型。 這是您要建立的實體類型。 按一下下一步。

   ![chlimage_1-93](assets/chlimage_1-93.png)

   >[!NOTE]
   >
   >您可以選擇 **資產模型**, **頁面模型**，或之前建立的實體類型的模型。
   >
   >請參閱 [建立模型](/help/mobile/administer-mobile-apps.md)，以建立自訂實體。

1. 輸入 **標題**, **名稱**, **說明**，和 **標籤** ，則此參數不會變化。 按一下&#x200B;**建立**。

   ![chlimage_1-94](assets/chlimage_1-94.png)

   完成後，該實體將出現在空間的子體中。

### 編輯實體 {#editing-an-entity}

1. 建立實體後，轉至資料夾或空間，然後從「空間」控制台中選擇要編輯的實體。

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. 選取要編輯的實體，然後按一下 **編輯**.

   ![chlimage_1-96](assets/chlimage_1-96.png)

   >[!CAUTION]
   >
   >根據您選擇建立實體的範本，編輯和檢視實體屬性時，兩者的UI會不同。 如需詳細資訊，請參閱下列步驟。

   ***如果選擇用於將實體建立為「資產模型」的模板***，按一下 **編輯** 可讓您新增資產，如下圖所示：

   ![chlimage_1-97](assets/chlimage_1-97.png)

   或者，您也可以按一下 **預覽** 檢視json連結。

   ![chlimage_1-98](assets/chlimage_1-98.png)

   ***如果選擇用於將實體建立為「頁面模型」的模板***，按一下 **編輯** 可讓您新增資產，如下圖所示：

   ![chlimage_1-99](assets/chlimage_1-99.png)

   按一下 **路徑** 若要新增資產

   ![chlimage_1-100](assets/chlimage_1-100.png)

   >[!NOTE]
   >
   >新增實體後，必須儲存實體，「預覽」連結才能運作。 若要檢視預覽，請按一下 **儲存**. 按一下 **預覽** 顯示新增資產的json，如下圖所示：

   ![chlimage_1-101](assets/chlimage_1-101.png)

   >[!NOTE]
   >
   >將資產新增至實體後，您可以選擇 **儲存** 要保存更改或選擇 **儲存並關閉** 保存並重定向到定義實體的空間控制台清單。

   此外，從空間控制台清單中選擇一個實體，然後按一下 **屬性** 查看和編輯定義實體的屬性。

   ![chlimage_1-102](assets/chlimage_1-102.png)

   您可以編輯標題、說明、標籤，並將資產新增至實體。

   ![chlimage_1-103](assets/chlimage_1-103.png)

### 移除實體 {#removing-an-entity}

1. 從空間內容清單中選擇實體

   ![chlimage_1-104](assets/chlimage_1-104.png)

1. 按一下 **刪除** 從工具欄中移除空間中的特定實體

### 發佈實體 {#publishing-an-entity}

您可以選擇 **發佈樹** 或 **快速發佈** 來發佈您的實體。

1. 從空間控制台清單中選擇一個實體，然後按一下**發佈樹**以發佈該實體及其子項。

   ![chlimage_1-105](assets/chlimage_1-105.png)

   **或**,

   按一下 **快速發佈** 來發佈該特定實體。
