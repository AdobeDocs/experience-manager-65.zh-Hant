---
title: 如何建立或自訂最適化表單主題？
description: 瞭解如何使用BEM規格建立或自訂最適化Forms核心元件的主題
keywords: 建立最適化表單核心元件主題、建立新主題、自訂主題、上傳新主題、在表單中使用主題、刪除主題、在AEM 6.5表單中建立主題
contentOwner: Khushwant Singh
topic-tags: Adaptive Forms
docset: aem65
role: Admin, Developer
feature: Adaptive Forms,Core Components
exl-id: 9f9b35a3-0479-4179-9fad-994a482c96b6
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 4%

---

# 建立或自訂最適化表單主題 {#introduction-to-theme}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM as a Cloud Service  | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html) |
| AEM 6.5 | 本文 |


<!--**Applies to:** ✅ Adaptive Form Core Components ❎ [Adaptive Form Foundation Components](/help/forms/using/create-adaptive-form.md).-->

在AEM Forms 6.5中，主題是AEM使用者端資料庫，可用來定義最適化表單的樣式（外觀）。 主題包含元件和面板的樣式詳細資訊。 樣式包括背景顏色、狀態顏色、透明度、對齊方式和大小等屬性。套用主題時，指定的樣式會反映在對應的元件上。主題是獨立管理，不需參照最適化表單，且可在多個最適化Forms中重複使用。

## 可用主題 {#available-theme}

AEM 6.5環境提供下列基於核心元件的最適化Forms的主題：

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)
* [FSI主題](https://github.com/adobe/aem-forms-theme-fsi)
* [醫療保健主題](https://github.com/adobe/aem-forms-theme-healthcare)
* [公用主題](https://github.com/adobe/aem-forms-theme-public)
* [製造主題](https://github.com/adobe/aem-forms-theme-manufacturing)

## 瞭解主題的結構 {#understanding-structure-of-theme}

主題是一個套件，其中包含定義最適化Forms樣式的CSS檔案、JavaScript檔案和資源（如圖示）。 最適化表單主題會依循特定組織，包含下列元件：

* `src/theme.scss`：此資料夾包含對整個主題有廣泛影響的CSS檔案。 它是定義和管理佈景主題樣式和行為的集中位置。 透過編輯此檔案，您可以進行在整個主題中普遍套用的變更，這會影響最適化Forms和AEM Sites頁面的外觀和功能。

* `src/site`：此資料夾包含套用至整個AEM網站頁面的CSS檔案。 這些檔案包含程式碼和樣式，會影響AEM網站頁面的整體功能和版面。 此處所做的任何修改會反映在您的網站的所有頁面中。

* `src/components`：此資料夾中的CSS檔案是針對個別AEM核心元件所設計。 元件的每個專用資料夾都包含 `.scss` 在最適化表單中設定該特定元件樣式的檔案。 例如， `/src/components/button/_button.scss` 檔案包含最適化Forms按鈕元件的樣式資訊。

  ![畫布布主題結構](/help/forms/using/assets/component-based-theme-folder-structure.png)

* `src/resources`：此資料夾包含靜態檔案，例如圖示、標誌和字型。 這些資源用於增強主題的視覺元素和整體設計。

## 建立主題

AEM Forms 6.5提供下列核心元件型最適化Forms的主題。

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)
* [公用主題](https://github.com/adobe/aem-forms-theme-public)
* [製造主題](https://github.com/adobe/aem-forms-theme-manufacturing)

您可以 [自訂這些主題的任何一個來建立主題](#customize-a-theme-core-components).

## 自訂主題 {#customize-a-theme-core-components-based-adaptive-forms}

自訂主題是指修改及個人化主題外觀的程式。 自訂主題時，您可以變更其設計元素、版面、顏色、印刷樣式，有時也會變更基礎程式碼。 這可讓您為網站或應用程式建立獨一無二的量身打造外觀，同時維持主題提供的基本結構和功能。

>[!NOTE]
>
> * 使用封裝管理員可在所有製作和發佈執行個體上部署主題。
> * 佈景主題使用者端程式庫會透過封裝管理員匯入或匯出，就像任何其他封裝一樣。

### 自訂主題的先決條件 {#prerequisites}

* [啟用最適化Forms核心元件](/help/forms/using/enable-adaptive-forms-core-components.md) 適合您的環境。

* 安裝最新版本的 [Apache Maven。](https://maven.apache.org/download.cgi) Apache Maven是常用於Java™專案的組建自動化工具。 安裝最新版本可確保您擁有佈景主題自訂的必要相依性。

* 瞭解如何建立 [Adobe Experience Manager中的使用者端資源庫](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html). AEM提供使用者端程式庫，可讓您將使用者端程式碼儲存在存放庫中、將其組織成類別，並定義每個類別程式碼何時及如何提供給使用者端。

* 安裝純文字編輯器。 例如，Microsoft® Visual Studio Code。 使用純文字編輯器(例如Microsoft® Visual Studio Code)可提供方便使用的環境，用於編輯和修改佈景主題檔案。

* 確保AEM Forms環境正常運作。

### 自訂主題的考量事項 {#consideration}

* 請務必使用 [用於啟用最適化Forms核心元件的原型專案](/help/forms/using/enable-adaptive-forms-core-components.md) 以自訂您的主題。

* 發佈最適化表單時，使用者端程式庫不會自動發佈在發佈執行個體上。 請確定您手動將在最適化表單中參考的使用者端程式庫發佈到您的發佈環境。

* Adobe建議不要變更使用者端程式庫的類別名稱。

### 自訂主題 {#customize-a-theme-core-components}

建立或自訂主題是多步驟流程。 依照列出的順序執行步驟，以建立/自訂主題：

1. [原地複製主題](#clone-git-repo-of-theme)
1. [自訂主題的外觀](#customize-the-theme)
1. [準備好本機部署的主題](#generate-the-clientlib)
1. [在本機環境中部署主題](#deploy-the-theme-on-a-local-environment)
1. [在生產環境中部署主題](#5-deploy-a-theme-on-your-production-environment)

<!--
 ![Theme Customization workflow](/help/forms/using/assets/custom-theme-steps.png)
-->

檔案中提供的範例是根據 **畫布** 佈景主題，但您可以複製任何佈景主題，並使用相同的指示加以自訂。 這些指示適用於任何主題，可讓您根據特定需求修改主題。

#### 1.複製主題的Git存放庫 {#clone-git-repo-of-theme}

若要複製以核心元件為基礎的最適化Forms主題，請選擇下列其中一種主題：

* [畫布主題](https://github.com/adobe/aem-forms-theme-canvas)
* [WKND主題](https://github.com/adobe/aem-forms-theme-wknd)
* [畫架佈景主題](https://github.com/adobe/aem-forms-theme-easel)

執行下列指示以複製主題：

1. 在本機開發環境中開啟命令提示字元或終端機視窗。

1. 執行 `git clone` 複製佈景主題的命令。

   ```
      git clone [Path of Git Repository of the theme]
   ```

   取代 [主題的Git存放庫路徑] 和主題的對應Git存放庫的實際URL

   例如，若要複製畫布主題，請執行下列命令：

   ```
      git clone https://github.com/adobe/aem-forms-theme-canvas
   ```

1. 選取&#x200B;**信任上層資料夾中所有文件的作者**，並點選&#x200B;**是的，我信任作者**。

成功執行命令後，您的電腦上便可在下列位置取得主題的本機復本：  `aem-forms-theme-canvas` 資料夾。

#### 2.自訂主題 {#customize-the-theme}

您可以彈性地自訂個別元件，或使用佈景主題的全域變數進行佈景主題層級的變更。 修改全域變數會對所有個別元件產生階層式效果。 例如，您可以利用全域變數來變更最適化表單中所有元件的邊框顏色，或對「號召性用語」(CTA)按鈕套用生動的填色顏色。 您可以：

* [設定主題層級樣式](#theme-customization-global-level)

* [設定元件層級樣式](#component-based-customization)

##### 設定主題層級樣式 {#theme-customization-global-level}

此 `variable.scss` 檔案包含佈景主題的全域變數。 透過更新這些變數，您可以在主題層級進行樣式相關的變更。 若要套用佈景主題層級樣式，請依照下列步驟進行：

1. 開啟 `<your-theme-sources>/src/site/_variables.scss` 檔案進行編輯。
1. 變更任何屬性的值。 例如，預設的錯誤顏色為紅色。 若要將錯誤顏色從紅色變更為藍色，請將 `$error`變數中。 例如，`$error: #196ee5`。

   ![範例：錯誤顏色設定為藍色](/help/forms/using/assets/theme-level-changes.png)

1. 儲存並關閉檔案。


同樣地，您可以使用 `variable.scss` 檔案來設定字型系列和型別、佈景主題和字型顏色、字型大小、佈景主題間距、錯誤圖示、佈景主題框線樣式，以及其他可影響多個最適化表單元件的變數。

##### 設定元件層級樣式 {#component-based-customization}

您也可以選擇自訂特定Adaptive Form核心元件的字型、顏色、大小和其他CSS屬性，例如按鈕、核取方塊、容器、頁尾等。 透過編輯與特定元件相關聯的CSS檔案，您可以將其樣式與組織的品牌保持一致。 若要自訂元件的樣式，請遵循下列步驟：

1. 開啟檔案 `<your-theme-sources>/src/components/<component>/<component.scss>` 以進行編輯。 例如，若要變更按鈕元件的字型顏色，請開啟 `<your-theme-sources>/src/components/button/button.scss`，檔案。
1. 根據您的需求變更任何的值。 例如，若要將滑鼠懸停時按鈕元件的顏色變更為綠色，請將 `color: $white` 中的屬性 `cmp-adaptiveform-button__widget:hover` 類別到十六進位程式碼#12b453或其他任何綠色的陰影。 最終程式碼如下所示：

   ```
    .cmp-adaptiveform-button__widget:hover {
    background: $dark-gray;
    color: #12b453;
    }
   ```


1. 儲存並關閉檔案。

<!--

   ![Example: Hover color set to green](/help/forms/using/assets/button-customization.png)

-->

>[!NOTE]
>
> 在主題和元件層級同時定義樣式時，在元件層級定義的樣式會優先執行。

#### 3.準備好部署主題 {#generate-the-clientlib}

若要將主題部署至AEM執行個體，必須將其轉換為使用者端資料庫。 請依照下列步驟，將主題轉換為使用者端資源庫：

1. 開啟命令提示字元或終端機視窗。
1. 導覽至 `<your-theme-sources>` 資料夾。 例如 `C:\aem-forms-theme-canvas`
1. 執行以下命令：

   ```
      npm run create-clientlib --category=adaptiveform.theme.[yourtheme]
   ```

   取代 `[yourtheme]` 以自訂佈景主題命名。 例如，如果自訂主題的名稱為 `customcanvastheme`，執行以下命令

   ```
       npm run create-clientlib --category=adaptiveform.theme.customcanvastheme
   ```

   成功執行命令時，使用者端程式庫資料夾會建立在 `themerepo\theme-clientlibs\[yourtheme]`.

   ![使用者端資料庫產生](/help/forms/using/assets/clientlib_created.png)


   ![使用者端資料庫位置](/help/forms/using/assets/adaptiveform.theme.easel.png)

#### 4.在本機環境中部署主題 {#deploy-the-theme-on-a-local-environment}

若要將主題部署至本機開發或測試環境，請遵循下列步驟：

1. 將上一節建立的使用者端資料庫複製到原型專案，路徑如下：

   `/ui.apps/src/main/content/jcr_root/apps/[AEM Archetype Project Folder]/clientlibs/<yourtheme>`

1. 開啟命令提示字元或終端機。
1. 導覽至AEM Archetype專案的根目錄，此專案用於啟用最適化表單核心元件。
1. 執行以下命令以在您的環境中部署自訂主題：

   `mvn clean install`

   ![使用者端資料庫組建](/help/forms/using/assets/mvndeploy.png)

<!--

#### 5. Test the theme with a local Adaptive Form {#test-the-theme-with-a-local-adaptive-form}

To apply and test the customized theme with an Adaptive Form:

**Apply theme while creating an Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Click **Create** > **Adaptive Forms**. The wizard for creating Adaptive Form opens.

1. Select the core component template in the **Source** tab.
1. Select the theme in the **Style** tab.
1. Click **Create**.

An Adaptive Form with the selected theme is created. 

**Apply theme to an existing Adaptive Form**

1. Log in to your AEM Forms author instance. 

1. Select **Adobe Experience Manager** > **Forms** > **Forms & Documents**.

1. Select an Adaptive Form and click Properties. 

1. For the **Theme Client Library** option, select the theme. 

1. Click **Save & Close**.

The selected theme is applied to the Adaptive Form. 
-->

#### 5.在您的生產環境中部署主題 {#deploy-theme}

一旦您在本機開發環境中成功測試主題後，您就可以繼續將主題部署到您的生產環境，包括製作和發佈執行個體。 請依照下列步驟，將主題部署在生產環境中：

1. 登入您的AEM環境。
1. 開啟封裝管理員。 預設URL為 `https://localhost:4502/crx/packmgr/index.jsp`.
1. 按一下 **上傳套裝** 並按一下 **瀏覽**.
1. 導覽至並選取 `[AEM Archetype Project Folder]\all\target[appid].all-[version].zip`. 按一下 **開啟**.
1. 按一下「安裝」。 在所有生產環境中重複此步驟。


安裝套件後，就可以選取主題。

![主題使用者端資源庫](/help/forms/using/assets/themeclientlibrary.png)

>[!NOTE]
>
>
> 如果您在存取發佈執行個體的登入對話方塊以透過封裝管理員安裝套件時遇到困難，請嘗試透過以下URL登入： `http://[Publish Server URL]:[PORT]/system/console`. 這可讓您登入發佈執行個體，讓您繼續安裝程式。

## 將主題套用至最適化表單 {#using-theme-in-adaptive-form}

將主題套用至最適化表單的步驟如下：

1. 登入您的本機AEM作者執行個體。
1. 在 Experience Manager 登入頁面上輸入您的認證。選取 **Adobe Experience Manager** > **Forms** > **Forms與檔案**.
1. 按一下 **建立** > **最適化Forms**.
1. 選取最適化Forms核心元件範本，然後按一下 **下一個**. 此 **新增屬性** 出現
1. 指定 **名稱** 最適化表單的預設值。


   >[!NOTE]
   >
   > * 根據預設， `adaptiveform.theme.canvas3` 已選取主題。
   > * 您可以從中選擇不同的主題 **主題使用者端資源庫** 下拉式功能表。

1. 按一下&#x200B;**建立**。

最適化表單主題用於最適化表單範本的一部分，以便在建立最適化表單時定義樣式。

## 刪除主題 {#delete-a-theme}

若要移除未使用或不需要的主題：

1. 登入您的作者執行個體。
1. 開啟 `http://[Publish Server URL]:[PORT]/crx/de/index.jsp`
1. 導覽至 `apps/[AEM Archetype Project Folder]/clientlibs/[yourtheme]`。
1. 刪除主題資料夾並儲存變更。


## 常問的問題 {#faq}

**問：** 在全域和元件層級的主題資料夾中進行自訂時，哪個自訂專案優先？

**Ans：** 在佈景主題和元件層級同時定義樣式時，在元件層級定義的樣式優先。

**問：** 如果自訂主題未顯示在 **[!UICONTROL 主題使用者端資源庫]**？

**Ans：**  如果您的自訂主題未出現在 **[!UICONTROL 主題使用者端資源庫]** 請依照下列步驟下拉式清單：

1. 導覽至您新增自訂主題使用者端資料庫的位置。 建議的路徑為 `/ui.apps/src/main/content/jcr_root/apps[AEM Archetype Project Folder]/clientlibs/<yourtheme>`.

1. 開啟 `.content.xml` 並包含下列中繼資料：

   ```
       formstheme:true
       allowproxy:true
   ```

1. 儲存檔案並重新部署主題。

## 另請參閱

* [建立以核心元件為基礎的最適化表單](create-an-adaptive-form-core-components.md)
* [使用規則編輯器將動態行為新增至表單](rule-editor.md)
* [建立或自訂核心元件型最適化Forms的主題](create-or-customize-themes-for-adaptive-forms-core-components.md)
* [建立核心元件型最適化Forms的範本](template-editor.md)
* [建立最適化表單或新增最適化表單至AEM Sites頁面或體驗片段](create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [範例主題範本和表單資料模型](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html)
