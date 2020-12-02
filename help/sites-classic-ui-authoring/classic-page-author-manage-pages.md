---
title: 建立及組織頁面
seo-title: 建立及組織頁面
description: 本節說明如何使用AEM建立和管理頁面，以便您在這些頁面上建立內容。
seo-description: 本節說明如何使用AEM建立和管理頁面，以便您在這些頁面上建立內容。
uuid: 47ce137a-7a85-4b79-b4e0-fdf08a9e77bd
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 14b8758b-f164-429a-b299-33b0703f8bec
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1935'
ht-degree: 3%

---


# 建立及組織頁面{#creating-and-organizing-pages}

本節說明如何使用Adobe Experience Manager(AEM)建立和管理頁面，以便您接著可以[在這些頁面上建立內容](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md)。

>[!NOTE]
>
>您的帳戶需要[適當的存取權限](/help/sites-administering/security.md)和[權限](/help/sites-administering/security.md#permissions)才能對頁面採取動作，例如建立、複製、移動、編輯、刪除。
>
>如果您遇到任何問題，我們建議您與系統管理員聯繫。

## 組織您的網站{#organizing-your-website}

身為作者，您將需要在AEM中組織您的網站。 這包括建立和命名您的內容頁面，以便：

* 您可輕鬆在作者環境中找到
* 瀏覽您網站的訪客可輕鬆在發佈環境中瀏覽

您也可以使用[資料夾](#creating-a-new-folder)協助組織您的內容。

網站的結構可視為包含內容頁面的&#x200B;*樹狀結構*。 這些內容頁面的名稱用於形成URL，而標題則會在檢視頁面內容時顯示。

以下顯示Geometrixx網站的摘取；其中，例如，將訪問`Triangle`頁：

* 作者環境

   `http://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

* 發佈環境

   `http://localhost:4503/content/geometrixx/en/products/triangle.html`

   根據實例的配置，在發佈環境中使用`/content`可能是可選的。

```xml
  /content
    /geometrixx
      /en
        /toolbar...
        /products
          /triangle
            /overview
            /features
          /square...
          /circle...
          /...
        /...
      /fr...
      /de...
      /es...
      /...
    /...
```

此結構可從「網站」主控台檢視，您可使用此主控台瀏覽樹狀結構[。](/help/sites-classic-ui-authoring/author-env-basic-handling.md#main-pars-text-15)

![chlimage_1-151](assets/chlimage_1-151.png)

### 頁面命名慣例{#page-naming-conventions}

建立新頁面時，有兩個鍵字欄位：

* **[標題](#title)**:

   * 這會在主控台中向使用者顯示，並在編輯時顯示在頁面內容的頂端。
   * 此欄位為必填.

* **[名稱](#name)**:

   * 這用於生成URI。
   * 此欄位的使用者輸入為選擇性。 如果未指定，則名稱是從標題衍生而來。

建立新頁面時，AEM會根據AEM和JCR所強加的慣例[驗證頁面名稱。](/help/sites-developing/naming-conventions.md)

實作和允許的字元清單會因UI而略有不同（對於觸控式UI而言，這個範圍更廣），但允許的最低值是：

* &#39;a&#39;到&#39;z&#39;
* A到Z
* &#39;0&#39;到&#39;9&#39;
* _（下划線）
* `-` （連字型大小／減號）

如果您想確保接受／使用這些字元，請僅使用這些字元（如果您需要所有字元的完整詳細資訊，請參閱[命名慣例](/help/sites-developing/naming-conventions.md)）。

#### 標題 {#title}

如果您在建立新頁面時只提供頁面 **Title** ,AEM會從此字串衍生頁面 **Name**[ ，並根據AEM和JCR所強加的慣例來驗證名稱。](/help/sites-developing/naming-conventions.md)在兩個UI中，都會接受包含無效字元的&#x200B;**Title**&#x200B;欄位，但衍生的名稱會取代無效字元。 例如：

| 標題 | 衍生名稱 |
|---|---|
| 捨恩 | schoen.html |
| SC%&amp;&amp;ast;ç+ | sc---c-.html |

#### 名稱 {#name}

如果您在建立新頁面時提供頁面&#x200B;**Name**,AEM會根據AEM和JCR所強制的慣例[驗證名稱。](/help/sites-developing/naming-conventions.md)

在Classic UI中，**不能在** Name **欄位中輸入無效字元**。

>[!NOTE]
>在啟用觸控的UI中，您&#x200B;**無法在**&#x200B;名稱&#x200B;**欄位中提交無效字元**。 當AEM偵測到無效字元時，欄位會反白顯示，並顯示說明訊息，指出需要移除／取代的字元。

>[!NOTE]
>
>您應避免使用ISO-639-1所定義的雙字母代碼，除非它是語言根目錄。
>
>有關詳細資訊，請參閱[準備翻譯內容](/help/sites-administering/tc-prep.md)。

### 範本 {#templates}

在AEM中，範本會指定專用的頁面類型。 範本將用作建立任何新頁面的基礎。

範本定義頁面結構；包括縮圖影像和其他屬性。 例如，您可能有個別的產品頁面、網站地圖和連絡資訊範本。 範本由[元件](#components)組成。

AEM隨附數個現成可用的範本。 提供的範本取決於個別網站，而需要提供的資訊（建立新頁面時）則取決於使用的UI。 主要欄位包括：

* **標**
題顯示在結果網頁上的標題。

* **命名**
頁面時使用的名稱。

* **范**
本產生新頁面時可用的範本清單。

### 元件 {#components}

元件是AEM提供的元素，讓您可以新增特定類型的內容。 AEM隨附一系列現成可用的元件，提供完整的功能；這些包括：

* 文字
* 影像
* Slideshow
* 影片
* 更多

建立並開啟頁面後，您就可使用](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#insertinganewparagraph)sidekick[中提供的元件[新增內容。](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)

## 管理頁面{#managing-pages}

### 建立新頁面{#creating-a-new-page}

除非所有頁面都事先已為您建立，否則您必須先建立頁面，才能開始建立內容：

1. 從&#x200B;**Websites**&#x200B;主控台中，選取您要建立新頁面的層級。

   在以下示例中，您正在&#x200B;**Products**&#x200B;級別下建立一個頁面——如左窗格中所示；右窗格顯示&#x200B;**Products**&#x200B;下層級中已存在的頁面。

   ![screen_shot_2012-02-15at114413am](assets/screen_shot_2012-02-15at114413am.png)

1. 在&#x200B;**新……**&#x200B;功能表(按一下&#x200B;**新增……**)，選擇「新建頁面……」**。**&#x200B;將開啟&#x200B;**建立頁面**&#x200B;窗口。

   按一下&#x200B;**新建……**&#x200B;本身也是&#x200B;**新頁面……的捷徑。**&#x200B;選項。

1. 使用&#x200B;**建立頁面**&#x200B;對話框，您可以：

   * 提供&#x200B;**Title**;這會顯示給使用者。
   * 提供&#x200B;**名稱**;這用於生成URI。 如果未指定，則名稱將衍生自標題。

      * 如果您在建立新頁面時提供頁面&#x200B;**Name**,AEM會根據AEM和JCR所提供的慣例[驗證名稱。](/help/sites-developing/naming-conventions.md)
      * 在傳統UI中，**不能在**&#x200B;名稱&#x200B;**欄位中輸入無效字元**。
   * 按一下您要用來建立新頁面的範本。

      模板作為新頁面的基礎；例如，決定內容頁面的基本版面配置。
   >[!NOTE]
   >
   >請參閱[頁面命名慣例](#page-naming-conventions)。

   建立新頁面所需的最低資訊為&#x200B;**Title**&#x200B;和所需範本。

   ![screen_shot_2012-02-15at114845am](assets/screen_shot_2012-02-15at114845am.png)

   >[!NOTE]
   >
   >如果要在URL中使用Unicode字元，請設定「別名」(`sling:alias`)屬性（[頁面屬性](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)）。

1. 按一下&#x200B;**建立**&#x200B;以建立頁面。 您會返回至&#x200B;**Websites**&#x200B;主控台，您可在主控台中看到新頁面的項目。

   主控台會提供頁面的相關資訊（例如上次編輯時間和依據誰），並視需要更新。

   >[!NOTE]
   >
   >您也可以在編輯現有頁面時建立頁面。 使用側腳的&#x200B;**Page**&#x200B;標籤中的**建立子頁面**，將直接在編輯的頁面下建立新頁面。

### 開啟頁面進行編輯{#opening-a-page-for-editing}

您可以透過下列其中一種方法開啟要編輯[](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#editing-a-component-content-and-properties)的頁面：

* 在&#x200B;**Websites**&#x200B;主控台中，您可以按兩下&#x200B;**頁面項目以開啟它進行編輯。**

* 在&#x200B;**Websites**&#x200B;主控台中，您可以在&#x200B;**按一下右鍵**（上下文菜單）頁項，然後從菜單中選擇&#x200B;**開啟**。

* 開啟頁面後，您可以按一下超連結，導覽至網站內的其他頁面（以進行編輯）。

### 複製和貼上頁面{#copying-and-pasting-a-page}

在複製時，您可以複製下列任一項：

* 單頁
* 頁面與所有子頁面

1. 從&#x200B;**Websites**&#x200B;主控台中，選取您要複製的頁面。

   >[!NOTE]
   >
   >在此階段，無論您要複製單一頁面或基礎子頁面，都無關緊要。

1. 按一下&#x200B;**Copy**。

1. 導覽至新位置，然後按一下：

   * **貼上** -將頁面與所有子頁面一起貼上
   * **Shift + Paste** -僅貼上選定頁

   頁面會貼到新位置。

   >[!NOTE]
   >
   >如果現有頁面已有相同名稱，頁面名稱可能會自動調整。

   >[!NOTE]
   >
   >您也可以從側腳的&#x200B;**Page**&#x200B;標籤使用&#x200B;**Copy Page**。 這將開啟一個對話框，您可以在其中指定目標等。

### 移動或更名頁面{#moving-or-renaming-page}

>[!NOTE]
>
>在指定新頁面名稱時，重新命名頁面也應遵循[頁面命名慣例](#page-naming-conventions)。

移動或更名頁面的過程相同。 使用您可以執行的相同動作：

* 將頁面移至新位置
* 在相同位置重新命名頁面
* 將頁面移至新位置，並同時重新命名

AEM提供您更新內部連結至重新命名或移動之頁面的功能。 這可逐頁執行，以提供完整的彈性。

要移動或更名頁面：

1. 觸發移動有多種方法：

   * 在&#x200B;**Websites**&#x200B;控制台中，按一下選擇頁面，然後選擇&#x200B;**移動……**
   * 在&#x200B;**Websites**&#x200B;控制台中，您也可以選擇頁面項目，然後&#x200B;**按一下右鍵**&#x200B;並選擇&#x200B;**移動……**
   * 編輯頁面時，您可以從側腳的&#x200B;**Page**&#x200B;標籤中選擇&#x200B;**移動頁面**。

1. **Move**&#x200B;窗口開啟；您可以在這裡指定新位置、頁面的新名稱，或兩者皆可。

   ![screen_shot_2012-02-15at121336pm](assets/screen_shot_2012-02-15at121336pm.png)

   該頁還列出了參考所移動頁面的所有頁面。 視參考頁面的狀態而定，您可以調整頁面上的連結和／或重新發佈頁面。

1. 視需要填寫下列欄位：

   * **目的地**

      使用網站地圖（可透過下拉式選取器取得）來選取頁面應移至的位置。

      如果您只要重新命名頁面，請忽略此欄位。

   * **移動**

      指定要移動的頁面——這通常預設填入，具體取決於您啟動移動操作的方式和位置。

   * **重新命名為**

      目前的頁面標籤依預設會顯示。 視需要指定新頁面標籤。

   * **調整**

      更新列在指向已移動頁面之頁面上的連結：例如，如果頁面A有頁面B的連結，AEM會調整頁面A中的連結，以防您移動頁面B。

      您可以針對每個個別的參考頁面選取／取消選取此選項。

   * **重新發佈**

      重新發佈參考頁面；此外，您也可以針對每個頁面選取此選項。
   >[!NOTE]
   >
   >如果頁面已經啟動，移動頁面會自動停用它。 預設情況下，移動完成時將重新激活它，但可以通過取消選中&#x200B;**移動**&#x200B;窗口中頁面的&#x200B;**重新發佈**&#x200B;欄位來更改。

1. 按一下&#x200B;**移動**。 需要確認。 按一下&#x200B;**確定**&#x200B;確認。

   >[!NOTE]
   >
   >頁面標題不會更新。

### 刪除頁面{#deleting-a-page}

1. 您可以從不同位置刪除頁面：

   * 在&#x200B;**Websites**&#x200B;主控台中，按一下以選取頁面，然後按一下滑鼠右鍵，然後從產生的功能表中選取「刪除」。****
   * 在&#x200B;**Websites**&#x200B;主控台中，按一下以選取頁面，然後從工具列選單中選取&#x200B;**Delete**。
   * 在sidekick內，使用&#x200B;**Page**&#x200B;標籤來選擇&#x200B;**刪除頁面** —— 這會刪除目前開啟的頁面。

1. 選取刪除頁面後，您必須確認請求——因為動作無法復原。

   >[!NOTE]
   >
   >刪除後，如果頁面已發佈，您可以還原最新（或特定）版本，但是，如果進一步修改，則此版本可能與上一個版本的內容不完全相同。 如需詳細資訊，請參閱[如何還原頁面](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoringpages)。

>[!NOTE]
>
>如果頁面已經啟動，則會在刪除前自動停用。

### 鎖定頁面{#locking-a-page}

您可以從控制台或編輯個別頁面時，[鎖定／解除鎖定頁面](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#locking-a-page)。 有關頁面是否被鎖定的資訊也會顯示在這兩個位置。

### 建立新資料夾{#creating-a-new-folder}

>[!NOTE]
>
>指定新資料夾名稱時，資料夾也受[頁面命名約定](#page-naming-conventions)的約束。

1. 開啟&#x200B;**Websites**&#x200B;主控台，並導覽至所需位置。
1. 在&#x200B;**新……**&#x200B;功能表(按一下&#x200B;**新增……**)，選擇&#x200B;**新建資料夾……**。
1. 將開啟&#x200B;**建立資料夾**&#x200B;對話框。 在此處，您可以輸入&#x200B;**Name**&#x200B;和&#x200B;**Title**:

   ![chlimage_1-152](assets/chlimage_1-152.png)

1. 選擇&#x200B;**建立**&#x200B;以建立資料夾。

