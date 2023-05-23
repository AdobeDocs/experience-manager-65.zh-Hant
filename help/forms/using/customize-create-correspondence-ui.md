---
title: 自定義建立通信UI
seo-title: Customize create correspondence UI
description: 瞭解如何自定義建立通信UI。
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

# 自定義建立通信UI{#customize-create-correspondence-ui}

## 概觀 {#overview}

Tergement Management允許您重新品牌化其解決方案模板，以獲得更高的品牌價值，並遵守組織的品牌標準。 重新標籤用戶介面包括更改組織徽標，該徽標顯示在「建立對應UI」的左上角。

您可以使用組織的徽標更改「建立通信UI」中的徽標。

![建立對應用戶介面中的自定義表徵圖](assets/0_1_introscreenshot.png)

建立對應用戶介面中的自定義表徵圖

### 在「建立對應」UI中更改徽標 {#changing-the-logo-in-the-create-correspondence-ui}

要設定您選擇的徽標影像，請執行以下操作：

1. 建立相應 [CRX中的資料夾結構](#creatingfolderstructure)。
1. [上載新徽標檔案](#uploadlogo) 的子菜單。

1. [設定CSS](#createcss) 在CRX上參考新徽標。
1. 清除瀏覽器歷史記錄和 [刷新建立對應UI](#refreshccrui)。

## 建立所需的資料夾結構 {#creatingfolderstructure}

建立資料夾結構（如下所述），用於托管自定義徽標影像和樣式表。 根資料夾/apps的新資料夾結構與/libs資料夾的結構類似。

對於任何自定義，請在/apps分支中建立並行資料夾結構，如下所述。

/apps分支（資料夾結構）:

* 確保檔案在系統更新時是安全的。 在升級、功能包或熱修復程式時，將更新/libs分支，如果您將更改托管在/libs分支中，則會覆蓋這些更改。
* 幫助您不干擾當前系統/分支，如果使用預設位置儲存自定義檔案，則可能會錯誤地解除該分支。
* 在搜索資源時幫助您的AEM資源獲得更高優先順序。 配置AEM為先搜索/apps分支，然後搜索/libs分支以查找資源。 此機制表示系統使用您的覆蓋（以及在其中定義的自定義）。

使用以下步驟在/apps分支中建立所需的資料夾結構：

1. 轉到 `https://'[server]:[port]'/[ContextPath]/crx/de` 並以管理員身份登錄。
1. 在應用資料夾中，建立名為 `css` 路徑/結構與css資料夾（位於ccrui資料夾中）類似。

   建立css資料夾的步驟：

   1. 按一下右鍵 **cs** 資料夾，然後選擇 **覆蓋節點**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![覆蓋節點](assets/1_overlaynode_css.png)

   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已選中

      ![覆蓋節點路徑](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >不要在/libs分支中進行更改。 您所做的任何更改都可能丟失，因為在以下情況下，此分支可能會發生更改：
      >
      >    
      >    
      >    * 在實例上升級
      >    * 應用熱修復
      >    * 安裝功能包


   1. 按一下&#x200B;**「確定」**。css資料夾是在指定路徑中建立的。

1. 在應用資料夾中，建立名為 `imgs` 路徑/結構與imgs資料夾（位於ccrui資料夾中）類似。

   1. 按一下右鍵 **印** 資料夾，然後選擇 **覆蓋節點**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. 確保「覆蓋節點」對話框具有以下值：

      **路徑：** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **覆蓋位置：** /apps/

      **匹配節點類型：** 已選中

   1. 按一下&#x200B;**「確定」**。

      >[!NOTE]
      >
      >您還可以在/apps資料夾中手動建立資料夾結構。

1. 按一下 **全部保存** 以在伺服器上保存更改。

## 將新徽標上載到CRX {#uploadlogo}

將自定義徽標檔案上載到CRX。 標準HTML規則控制徽標的呈現。 支援的影像檔案格式取決於您用於訪問AEM Forms的瀏覽器。 所有瀏覽器都支援JPEG、GIF和PNG。 有關詳細資訊，請參閱支援的影像格式的瀏覽器特定文檔。

* 徽標影像的預設尺寸為48像素 &#42; 48像素 確保映像與此大小相似或大於48像素 &#42; 48像素
* 如果徽標影像的高度大於50像素，則「建立對應」用戶介面將影像縮放到最大高度50像素，因為這是標題的高度。 縮放影像時，「建立對應」用戶介面會維護影像的長寬比。
* 如果影像較小，則「建立對應用戶介面」不會縮放影像，因此請確保您使用的徽標影像在高度和寬度上至少為48像素，以便清晰。

使用以下步驟將自定義徽標檔案上載到CRX:

1. 前往 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，請以管理員身份登錄。
1. 在CRXDE中，按一下右鍵 **印** 資料夾，然後選擇 **建立>建立檔案**:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![在imgs資料夾中建立新節點](assets/2_contentexplorernewnode.png)

1. 在「建立檔案」對話框中，輸入檔案名為CustomLogo.png（或徽標檔案名）。

   ![CustomLogo.png作為新節點](assets/3_contentexplorernewnode_customlogo.png)

1. 按一下 **全部保存**。

   在您建立的新檔案（此處為CustomLogo.png）下，將顯示jcr:content屬性。

1. 按一下資料夾結構中的jcr:content。

   jcr:content的屬性出現。

   ![jcrcontent屬性](assets/jcrcontentproperties.png)

1. 按兩下 **jcr：資料** 屬性。

   將出現「編輯jcr:data」對話框。

   現在，按一下newlogo.png資料夾，按兩下jcr:content（dim選項），然後設定類型nt:resource。 如果不存在，請建立名為jcr:content的屬性。

1. 在「編輯jcr:data」對話框中，按一下 **瀏覽** 並選擇要用作徽標的影像檔案（此處為CustomLogo.png）。

   支援的影像檔案格式取決於您用於訪問AEM Forms的瀏覽器。 所有瀏覽器都支援JPEG、GIF和PNG。 有關詳細資訊，請參閱支援的影像格式的瀏覽器特定文檔。

   ![自定義徽標檔案示例](assets/geometrixx-outdoors.png)

   示例：CustomLogo.png用作自定義徽標

1. 按一下 **全部保存**。

## 建立CSS以將徽標與UI整合 {#createcss}

自定義徽標影像要求在內容上下文中載入附加樣式表。

使用以下步驟設定用於渲染徽標的樣式表：

1. 前往 `https://'[server]:[port]'/[contextpath]/crx/de`. 如有必要，請以管理員身份登錄。
1. 在以下位置建立名為customcss.css的檔案（不能使用其他檔案名）:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   建立customcss.css檔案的步驟：

   1. 按一下右鍵 **cs** 資料夾和 **建立>建立檔案**。
   1. 在「新建檔案」對話框中，將CSS的名稱指定為 `customcss.css`（不能使用其他檔案名），然後按一下 **確定**。
   1. 將以下代碼添加到新建立的css檔案。 在代碼的content:url中，指定已上載到CRXDE中imgs資料夾的影像名稱。

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. 按一下 **全部保存**。

## 刷新「建立對應UI」以查看自定義徽標 {#refreshccrui}

清除瀏覽器快取，然後在瀏覽器中開啟「建立對應UI」實例。 您應該看到您的自定義徽標。

![使用自定義徽標建立對應用戶介面](assets/0_1_introscreenshot-1.png)

建立對應用戶介面中的自定義表徵圖
