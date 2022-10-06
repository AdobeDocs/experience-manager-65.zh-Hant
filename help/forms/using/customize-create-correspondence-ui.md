---
title: 自訂建立通信UI
seo-title: Customize create correspondence UI
description: 了解如何自訂建立通信UI。
seo-description: Learn how to customize create correspondence UI.
uuid: 9dee9b6f-4129-4560-9bf8-db48110b76f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 13a93111-c08c-4457-b69a-a6f6eb6da330
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 0%

---

# 自訂建立通信UI{#customize-create-correspondence-ui}

## 總覽 {#overview}

通信管理可讓您重新品牌化其解決方案範本，以提升品牌價值，並符合貴組織的品牌標準。 品牌化使用者介面包括變更組織標誌，該標誌會顯示在「建立通信UI」的左上角。

您可以使用組織的標誌來變更「建立通信UI」中的標誌。

![建立通信UI中的自訂圖示](assets/0_1_introscreenshot.png)

建立通信UI中的自訂圖示

### 變更建立通信UI中的標誌 {#changing-the-logo-in-the-create-correspondence-ui}

若要設定您所選擇的標誌影像，請執行下列操作：

1. 建立適當 [CRX中的資料夾結構](#creatingfolderstructure).
1. [上傳新的標誌檔案](#uploadlogo) 在CRX中建立的資料夾中。

1. [設定CSS](#createcss) 在CRX上，以參照新的標誌。
1. 清除瀏覽器歷史記錄，並 [刷新建立通信UI](#refreshccrui).

## 建立所需的資料夾結構 {#creatingfolderstructure}

建立資料夾結構（如下所述），用於托管自定義徽標影像和樣式表。 根資料夾/apps的新資料夾結構與/libs資料夾的結構類似。

對於任何自訂，請在/apps分支中建立平行資料夾結構，如下所述。

/apps分支（資料夾結構）:

* 確保檔案安全，以防系統更新。 若是升級、功能套件或Hotfix，則會更新/libs分支，而如果您將變更托管於/libs分支，則會覆寫變更。
* 幫助您不打擾當前的系統/分支，如果使用預設位置來儲存自定義檔案，則可能會錯誤地解決該問題。
* 當AEM搜尋資源時，可協助您的資源獲得較高的優先順序。 AEM設定為先搜尋/apps分支，再搜尋/libs分支以尋找資源。 此機制表示系統會使用您的覆蓋（以及那裡定義的自訂）。

使用下列步驟在/apps分支中建立所需的資料夾結構：

1. 前往 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身分登入。
1. 在應用程式資料夾中，建立名為 `css` 具有與css資料夾類似的路徑/結構（位於ccrui資料夾中）。

   建立CSS資料夾的步驟：

   1. 以滑鼠右鍵按一下 **cs** 資料夾（位於以下路徑），然後選取 **覆蓋節點**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![覆蓋節點](assets/1_overlaynode_css.png)

   1. 確定「覆蓋節點」對話方塊有下列值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已勾選

      ![覆蓋節點路徑](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >請勿在/libs分支中進行變更。 您所做的任何變更都可能會遺失，因為只要您符合以下條件，此分支就會發生變更：
      >
      >    
      >    
      >    * 在您的執行個體上升級
      >    * 套用Hotfix
      >    * 安裝功能套件


   1. 按一下&#x200B;**「確定」**。css資料夾會建立在指定的路徑中。

1. 在應用程式資料夾中，建立名為 `imgs` 具有與imgs資料夾類似的路徑/結構（位於ccrui資料夾中）。

   1. 以滑鼠右鍵按一下 **imgs** 資料夾（位於以下路徑），然後選取 **覆蓋節點**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. 確定「覆蓋節點」對話方塊有下列值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已勾選

   1. 按一下&#x200B;**「確定」**。

      >[!NOTE]
      >
      >您也可以手動在/apps資料夾中建立資料夾結構。

1. 按一下 **全部儲存** 以在伺服器上儲存變更。

## 將新標誌上傳至CRX {#uploadlogo}

將自訂標誌檔案上傳至CRX。 標準HTML規則控制標誌的轉譯。 支援的影像檔案格式會根據您用來存取AEM Forms的瀏覽器而定。 所有瀏覽器都支援JPEG、GIF和PNG。 如需詳細資訊，請參閱支援影像格式的瀏覽器專屬檔案。

* 標誌影像的預設尺寸為48像素 &#42; 48 px. 請確定您的影像類似此大小或大於48像素 &#42; 48 px.
* 如果標誌影像的高度超過50像素，「建立通信」使用者介面會將影像縮小至最大50像素的高度，因為這是標題的高度。 縮小影像時，「建立通信」使用者介面會維護影像的外觀比例。
* 如果影像較小，「建立通信用戶介面」不會放大影像，因此請確定您使用的徽標影像的高度至少為48像素，寬度足夠清晰。

使用下列步驟將自訂標誌檔案上傳至CRX:

1. 前往 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，請以管理員身分登入。
1. 在CRXDE中，以滑鼠右鍵按一下 **imgs** 資料夾（位於以下路徑），然後選取 **建立>建立檔案**:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![在imgs資料夾中建立新節點](assets/2_contentexplorernewnode.png)

1. 在「建立檔案」對話框中，輸入檔案名為CustomLogo.png（或徽標檔案的名稱）。

   ![CustomLogo.png作為新節點](assets/3_contentexplorernewnode_customlogo.png)

1. 按一下 **全部儲存**.

   在您建立的新檔案（此處為CustomLogo.png）下，jcr:content屬性隨即顯示。

1. 在資料夾結構中按一下jcr:content。

   jcr:content的屬性隨即出現。

   ![jcrcontentpropertys](assets/jcrcontentproperties.png)

1. 按兩下 **jcr:data** 屬性。

   將出現「編輯jcr:data」對話框。

   現在，按一下newlogo.png資料夾，按兩下jcr:content（dim選項）並設定nt:resource類型。 如果不存在，請建立名為jcr:content的屬性。

1. 在「編輯jcr:data」對話方塊中，按一下 **瀏覽** 並選取您要作為標誌的影像檔案（此處為CustomLogo.png）。

   支援的影像檔案格式會根據您用來存取AEM Forms的瀏覽器而定。 所有瀏覽器都支援JPEG、GIF和PNG。 如需詳細資訊，請參閱支援影像格式的瀏覽器專屬檔案。

   ![自訂標誌檔案範例](assets/geometrixx-outdoors.png)

   範例：CustomLogo.png作為自訂標誌使用

1. 按一下 **全部儲存**.

## 建立CSS以整合標誌與UI {#createcss}

自訂標誌影像需要在內容內容中載入額外的樣式表。

使用下列步驟來設定樣式表以呈現標誌：

1. 前往 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，請以管理員身分登入。
1. 在以下位置建立名為customcss.css的檔案（不能使用其他檔案名）:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   建立customcss.css檔案的步驟：

   1. 以滑鼠右鍵按一下 **cs** 資料夾和選取 **建立>建立檔案**.
   1. 在「新增檔案」對話方塊中，將CSS的名稱指定為 `customcss.css`（不能使用其他檔案名），然後按一下 **確定**.
   1. 將下列程式碼新增至新建立的css檔案。 在程式碼的content:url中，指定您已上傳至CRXDE中Imgs資料夾的影像名稱。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 按一下 **全部儲存**.

## 重新整理「建立通信UI」以查看自訂標誌 {#refreshccrui}

清除瀏覽器快取，然後在瀏覽器中開啟「建立通信UI」例項。 您應該會看到自訂標誌。

![使用自訂標誌建立通信使用者介面](assets/0_1_introscreenshot-1.png)

建立通信UI中的自訂圖示
