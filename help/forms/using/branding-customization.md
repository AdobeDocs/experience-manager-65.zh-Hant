---
title: 品牌自訂
seo-title: Branding Customization
description: 自定義應用程式表徵圖、應用程式名稱、啟動映像和登錄頁，為AEM Forms應用程式提供獨特的組織特定外觀。
seo-description: Customize the application icon, application name, launch images, and login page to provide a distinct organization-specific look and feel to AEM Forms app.
uuid: fece0fa8-c417-45eb-93f1-a91b49835fa0
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: f6440a36-719a-4f89-b7db-1af918a3469a
exl-id: 9333705b-9944-4a74-a30f-7d9ec85fd824
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 2%

---

# 品牌自訂 {#branding-customization}

您可以自定義應用程式表徵圖、應用程式名稱、啟動映像和登錄頁，以便為AEM Forms應用程式提供特定於組織的獨特外觀。 例如，您可以更改影像以使用組織中的徽標。 AEM Forms應用支援以下自定義：

* 自定義應用程式表徵圖和啟動映像
* 自定義應用名稱
* 在登錄頁上自定義影像
* 在應用菜單中自定義徽標

## 自定義表徵圖並啟動影像 {#customizing-icon-and-launch-images}

執行以下步驟來自定義預設應用表徵圖和AEM Forms應用的啟動映像：

>[!NOTE]
>
>對於所有表徵圖和影像，使用隔行掃描PNG格式。

### 自定義表徵圖並啟動映像 {#to-customize-icon-and-launch-images}

#### 為iOS {#for-ios}

1. 開啟 `Capture.xcodeproj` Xcode中的項目。
1. (***用於自定義表徵圖***)在「捕獲」的導航器視圖中，導航到 **[!UICONTROL 「捕獲」>「捕獲」>「支援檔案」>「捕獲 — info.plist」]**。 按一下「Icon files（表徵圖檔案）」旁邊的下拉框。 指定表徵圖檔案(.png)的名稱，並在 **[!UICONTROL 捕獲>捕獲>資源>表徵圖]**。 當前支援的維包括：29x29、50x50、58x58、72x72、100x100和144x144。
1. (***用於自定義啟動映像***)確保映像的檔案名為：

   * 對於縱向： `Default-Portrait~ipad.png` 和 `Default-Portrait@2x~ipad.png`
   * 對於橫向： `Default-Landscape~ipad.png` 和 `Default-Landscape@2x~ipad.png`

   將它們上載到「捕獲」項目以替換項目中的現有檔案。

   >[!NOTE]
   >
   >確保映像的名稱和解析度與您在項目中替換的映像匹配。

1. 在iOS設備或iOS模擬器上構建和運行AEM Forms應用。

#### 對於Android {#for-android}

1. 將應用程式表徵圖檔案命名為：

   `ic_launcher.png`

1. 將相應的表徵圖檔案放在以下目錄中：

   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-hdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-mdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxhdpi`
   * `[User_Home]/Projects/[your-project]/src/android/res/drawable-xxxhdpi`

   >[!NOTE]
   >
   >確保映像的名稱和解析度與您在項目中替換的映像匹配。

1. 重建AEM Forms應用。

### 對於Windows {#for-windows}

1. 替換路徑中的表徵圖：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\icons\windows`

1. 替換路徑中的啟動程式映像：

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\res\screens\windows`

   >[!NOTE]
   >
   >確保映像的名稱和解析度與您在項目中替換的映像匹配。

1. 重建AEM Forms應用。

## 自定義應用名稱 {#customize-the-app-name}

### 為iOS {#for-ios-1}

1. 開啟 `Capture.xcodeproj` Xcode中的項目。
1. 在「捕獲」的導航器視圖中，導航到 **[!UICONTROL 「捕獲」>「捕獲」>「支援檔案」>「InfoPlist.strings」]**。

   更新 `CFBundleDisplayName` 屬性。

1. 在iOS設備或iOS模擬器上構建和運行AEM Forms應用。

   有關為iOS構建應用程式的詳細資訊，請參閱 [設定Xcode項目並生成iOS應用](/help/forms/using/setup-xcode-project-build-installer.md)。

### 對於Android {#for-android-1}

1. 在任何文本或Xml編輯器中開啟以下Xml:

   `[User_Home]/Projects/[your-project]/src/android/res/values/strings.xml and android/res/values-en/strings.xml`

1. 更新鍵的值 `app_name`。
1. 重建AEM Forms應用。

   有關構建Android應用程式的詳細資訊，請參閱 [設定Eclipse項目並構建Android應用](/help/forms/using/setup-eclipse-project-build-installer.md)。

### 對於Windows {#for-windows-1}

1. 在任何文本編輯器中開啟以下Xml:

   `%HOMEPATH%\adobe-lc-mobileworkspace-src-<version>\src\windows\MWSWindows\config.xml`

1. 更新中的值 `<name>...</name>` 標籤。
1. 重建AEM Forms應用。

   有關構建Windows應用程式的詳細資訊，請參閱 [設定Visual Studio項目並生成Windows應用](/help/forms/using/setup-visual-studio-project-build-installer.md)。

## 在登錄頁上自定義影像 {#customizing-images-on-the-login-page}

AEM Forms應用的登錄頁面包含徽標和背景影像。 徽標位於登錄對話框的上方，背景影像位於登錄對話框的下方。 執行以下步驟以在登錄頁上自定義預設映像：

**開始之前**

確保您有以下映像：

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

**使用Xcode在登錄頁上自定義影像**

1. 開啟 `Capture.xcodeproj` Xcode中的項目。

1. 導航到 `www/wsmobile/images`的子菜單。
1. 要更改徽標，請替換預設 `LC-logo.png` 檔案 `LC-logo.png` 的子菜單。
1. 要更改背景，請替換預設 `Landing_bg.jpeg` 檔案 `Landing_bg.jpeg`的子菜單。
1. 在iOS設備或iOS模擬器上構建和運行AEM Forms應用。

### 使用Eclipse在登錄頁上自定義映像 {#to-customize-images-on-the-login-pages-using-eclipse}

1. 在Eclipse中開啟Android項目。

1. 導航到 `assets/www/wsmobile/images`的子菜單。
1. 要更改徽標，請替換預設 `LC-logo.png` 檔案 `LC-logo.png` 的子菜單。
1. 要更改背景，請替換預設 `Landing_bg.jpeg` 檔案 `Landing_bg.jpeg`的子菜單。
1. 在Android設備上構建並運行AEM Forms應用。

### 使用Visual Studio自定義登錄頁上的影像 {#to-customize-images-on-the-login-pages-using-visual-studio}

1. 開啟 `MWSWindows.sln` Visual Studio中的項目。

1. 導航到 `MWSWindows\www\wsmobile\images`的子菜單。
1. 要更改徽標，請替換預設 `LC-logo.png` 檔案 `LC-logo.png` 的子菜單。
1. 要更改背景，請替換預設 `Landing_bg.jpeg` 檔案 `Landing_bg.jpeg`的子菜單。
1. 在Windows設備上生成並運行AEM Forms應用。

## 在應用菜單中自定義徽標 {#customizing_images_on_the_login_page-1}

登錄AEM Forms應用並點擊菜單按鈕後，您可以在菜單上方看到徽標。 執行以下步驟以自定義預設徽標：

**開始之前**

確保您有以下映像：

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

**使用Xcode在登錄頁上自定義影像**

1. 開啟 `Capture.xcodeproj` Xcode中的項目。

1. 導航到 `www/wsmobile/images`的子菜單。
1. 要更改徽標，請替換預設 `aem_icon.png` 檔案 `aem_icon.png` 的子菜單。
1. 在iOS設備或iOS模擬器上構建和運行AEM Forms應用。

### 使用Eclipse在登錄頁上自定義映像 {#to-customize-images-on-the-login-pages-using-eclipse-1}

1. 在Eclipse中開啟Android項目。

1. 導航到 `assets/www/wsmobile/images`的子菜單。
1. 要更改徽標，請替換預設 `aem_icon.png` 檔案 `aem_icon.png` 的子菜單。
1. 在Android設備上構建並運行AEM Forms應用。

### 使用Visual Studio自定義登錄頁上的影像 {#to-customize-images-on-the-login-pages-using-visual-studio-1}

1. 開啟 `MWSWindows.sln` Visual Studio中的項目。

1. 導航到 `MWSWindows\www\wsmobile\images`的子菜單。
1. 要更改徽標，請替換預設 `aem_icon.png` 檔案 `aem_icon.png` 的子菜單。
1. 在Windows設備上生成並運行AEM Forms應用。
