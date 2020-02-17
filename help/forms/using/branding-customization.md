---
title: 品牌自訂
seo-title: 品牌自訂
description: 自訂應用程式圖示、應用程式名稱、啟動影像和登入頁面，為AEM Forms應用程式提供獨特的組織特定外觀和感覺。
seo-description: 自訂應用程式圖示、應用程式名稱、啟動影像和登入頁面，為AEM Forms應用程式提供獨特的組織特定外觀和感覺。
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 品牌自訂 {#branding-customization}

您可以自訂應用程式圖示、應用程式名稱、啟動影像和登入頁面，為AEM Forms應用程式提供不同的組織特定外觀。 例如，您可以變更影像，以使用組織中的標誌。 AEM Forms應用程式支援下列自訂：

* 自訂應用程式圖示和啟動影像
* 自訂應用程式名稱
* 自訂登入頁面上的影像
* 自訂應用程式選單中的標誌

## 自訂圖示和啟動影像 {#customizing-icon-and-launch-images}

執行下列步驟，自訂AEM Forms應用程式的預設應用程式圖示和啟動影像：

>[!NOTE]
>
>對於所有圖示和影像，請使用非隔行掃描的PNG格式。

### 若要自訂圖示和啟動影像 {#to-customize-icon-and-launch-images}

#### 適用於iOS {#for-ios}

1. 在Xcode中 `Capture.xcodeproj` 開啟專案。
1. (用&#x200B;***於自定義表徵圖***)在「捕獲」的導航視圖中，導航至「捕 **[!UICONTROL 獲」>「捕獲」>「支援檔案」>「捕獲資訊。plist]**」。 按一下「圖示檔」旁的下拉式清單。 指定圖示檔案(.png)的名稱，並在「擷取>擷取>資源>圖 **[!UICONTROL 示」上傳檔案]**。 目前支援的維度包括：29x29、50x50、58x58、72x72、100x100和144x144。
1. (用&#x200B;***於自訂啟動影像***)請確定影像的檔名為：

   * 縱向： `Default-Portrait~ipad.png` 和 `Default-Portrait@2x~ipad.png`
   * 橫向： `Default-Landscape~ipad.png` 和 `Default-Landscape@2x~ipad.png`
   將檔案上傳到Capture項目，以替換項目中的現有檔案。

   >[!NOTE]
   >
   >請確定影像的名稱和解析度符合您在專案中取代的影像。

1. 在iOS裝置或iOS模擬器上建立並執行AEM Forms應用程式。

#### 適用於Android {#for-android}

1. 將應用程式表徵圖檔案命名為：

   `ic_launcher.png`

1. 將對應的表徵圖檔案放在以下目錄中：

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`
   >[!NOTE]
   >
   >請確定影像的名稱和解析度符合您在專案中取代的影像。

1. 重建AEM Forms應用程式。

### 適用於Windows {#for-windows}

1. 取代路徑中的圖示：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 在路徑中替換啟動程式映像：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >請確定影像的名稱和解析度符合您在專案中取代的影像。

1. 重建AEM Forms應用程式。

## 自訂應用程式名稱 {#customize-the-app-name}

### 適用於iOS {#for-ios-1}

1. 在Xcode中 `Capture.xcodeproj` 開啟專案。
1. 在Capture的導覽檢視中，導覽至 **[!UICONTROL Capture > Capture > Supporting Files > InfoPlist.strings]**。

   將屬性的值更 `CFBundleDisplayName` 新為您要為應用程式顯示的名稱。

1. 在iOS裝置或iOS模擬器上建立並執行AEM Forms應用程式。

   如需建立iOS適用應用程式的詳細資訊，請 [參閱「設定Xcode專案並建立iOS應用程式」](/help/forms/using/setup-xcode-project-build-installer.md)。

### 適用於Android {#for-android-1}

1. 在任何文字或Xml編輯器中開啟下列Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. 更新索引鍵的值 `app_name`。
1. 重建AEM Forms應用程式。

   如需建立Android適用應用程式的詳細資訊，請 [參閱「設定Eclipse專案並建立Android應用程式」](/help/forms/using/setup-eclipse-project-build-installer.md)。

### 適用於Windows {#for-windows-1}

1. 在任何文字編輯器中開啟下列Xml:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. 更新標籤中的 `<name>...</name>` 值。
1. 重建AEM Forms應用程式。

   如需建立Windows適用應用程式的詳細資訊，請 [參閱「設定Visual studio專案並建立Windows應用程式」](/help/forms/using/setup-visual-studio-project-build-installer.md)。

## 自訂登入頁面上的影像 {#customizing-images-on-the-login-page}

AEM Forms應用程式的登入頁面有標誌和背景影像。 標誌位於登錄對話框的上方，背景影像位於登錄對話框的下方。 執行下列步驟以自訂登入頁面上的預設影像：

**開始之前**

請確定您有下列影像：

<table>
 <tbody>
  <tr>
   <th><p>說明</p> </th>
   <th><p>大小</p> </th>
   <th><p>檔案名稱</p> </th>
  </tr>
  <tr>
   <td><p>標誌</p> </td>
   <td><p>72 x 72像素</p> </td>
   <td><p>LC-logo.png</p> </td>
  </tr>
  <tr>
   <td><p>背景影像（縱向）</p> </td>
   <td><p>1280 x 989像素</p> </td>
   <td><p>Landing_bg.jpeg</p> </td>
  </tr>
 </tbody>
</table>

**若要使用Xcode自訂登入頁面上的影像**

1. 在Xcode中 `Capture.xcodeproj` 開啟專案。

1. 導覽至資料 `www/wsmobile/images`夾。
1. 若要變更標誌，請以自訂 `LC-logo.png` 檔案取代預設 `LC-logo.png` 檔案。
1. 若要變更背景，請以自訂 `Landing_bg.jpeg` 檔案取代預設 `Landing_bg.jpeg`檔案。
1. 在iOS裝置或iOS模擬器上建立並執行AEM Forms應用程式。

### 若要使用Eclipse自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-eclipse}

1. 在Eclipse中開啟Android專案。

1. 導覽至資料 `assets/www/wsmobile/images`夾。
1. 若要變更標誌，請以自訂 `LC-logo.png` 檔案取代預設 `LC-logo.png` 檔案。
1. 若要變更背景，請以自訂 `Landing_bg.jpeg` 檔案取代預設 `Landing_bg.jpeg`檔案。
1. 在Android裝置上建立及執行AEM Forms應用程式。

### 使用Visual studio自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-visual-studio}

1. 在Visual studio `MWSWindows.sln` 中開啟專案。

1. 導覽至資料 `MWSWindows\www\wsmobile\images`夾。
1. 若要變更標誌，請以自訂 `LC-logo.png` 檔案取代預設 `LC-logo.png` 檔案。
1. 若要變更背景，請以自訂 `Landing_bg.jpeg` 檔案取代預設 `Landing_bg.jpeg`檔案。
1. 在Windows裝置上建立及執行AEM Forms應用程式。

## 自訂應用程式選單中的標誌 {#customizing_images_on_the_login_page-1}

當您登入AEM Forms應用程式並點選功能表按鈕後，您可以在功能表上方看到標誌。 執行下列步驟以自訂預設標誌：

**開始之前**

請確定您有下列影像：

<table>
 <tbody>
  <tr>
   <th><p>說明</p> </th>
   <th><p>大小</p> </th>
   <th><p>檔案名稱</p> </th>
  </tr>
  <tr>
   <td><p>標誌</p> </td>
   <td><p>72 x 72像素</p> </td>
   <td><p>aem_icon.png</p> </td>
  </tr>
 </tbody>
</table>

**若要使用Xcode自訂登入頁面上的影像**

1. 在Xcode中 `Capture.xcodeproj` 開啟專案。

1. 導覽至資料 `www/wsmobile/images`夾。
1. 若要變更標誌，請以自訂檔 `aem_icon.png` 案取代預設 `aem_icon.png` 檔案。
1. 在iOS裝置或iOS模擬器上建立並執行AEM Forms應用程式。

### 若要使用Eclipse自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. 在Eclipse中開啟Android專案。

1. 導覽至資料 `assets/www/wsmobile/images`夾。
1. 若要變更標誌，請以自訂檔 `aem_icon.png` 案取代預設 `aem_icon.png` 檔案。
1. 在Android裝置上建立及執行AEM Forms應用程式。

### 使用Visual studio自訂登入頁面上的影像 {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. 在Visual studio `MWSWindows.sln` 中開啟專案。

1. 導覽至資料 `MWSWindows\www\wsmobile\images`夾。
1. 若要變更標誌，請以自訂檔 `aem_icon.png` 案取代預設 `aem_icon.png` 檔案。
1. 在Windows裝置上建立及執行AEM Forms應用程式。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
