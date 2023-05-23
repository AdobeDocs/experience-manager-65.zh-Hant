---
title: 使用PhoneGap CLI開發應用
seo-title: Developing Apps with PhoneGap CLI
description: 有關使用PhoneGap CLI開發應用的資訊，請訪問此頁。
seo-description: Follow this page to learn about developing apps with PhoneGap CLI.
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 1%

---

# 使用PhoneGap CLI開發應用{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

在任何給定時間，作為開發人員，只要您已配置開發環境，您就可以在設備或模擬器中運行應用程式。

要運行以下示例，您需要一個使用Xcode運行OSx(Mac)的系統，或一個安裝了Android SDK的Mac/Win/Linux系統。

## Bootstrap您的開發環境 {#bootstrap-your-development-environment}

[設定PhoneGap CLI](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

iOS:要為iPhone和iPad開發，您需要Apple的Xcode IDE。

* 免費下載 [這裡](https://developer.apple.com/xcode/downloads/)。
* [PhoneGapiOS平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

對於Android:要為iPhone和iPad開發，你需要Google的Android Stuido IDE。

* 免費下載 [這裡](https://developer.android.com/sdk/index.html)。
* [PhoneGap Android平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## 下載源 {#download-the-source}

成功引導開發環境後，請從「應用生成磁貼」下AEM載源：

* 按一下PhoneGap Build磁貼下拉雪形。

![chlimage_1-45](assets/chlimage_1-45.png)

* 按一下「Download Source（下載源）」。
* 從「下載源」模式中選擇所需的源。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>開發源包含應用的最新狀態，同時包含未暫存的更改。 使用暫存源生成提交到應用商店供應商的發佈候選。
>
>如果從未存放應用，選擇「暫存」將觸發暫存工作流(提示：這將在AppStore和GooglePlayStore中提供的PhoneGap Enterprise Viewer App中顯示為暫存應用。)

* 按一下「Download（下載）」 ，然後將ZIP保存到您的電腦。
* 將下載的zip檔案解壓到工作區。

## 生成並載入應用程式（從源） {#build-and-load-the-app-from-source}

PhoneGap CLI可以建立平台項目、編譯源，並以單個命令部署應用。

>[!NOTE]
>
>您可以分別執行這些步驟，請參閱 [PhoneGap CLI文檔](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/)。

1. 確保已安裝PhoneGap CLI，請參閱上文。
1. 在控制台（或終端）窗口中，導航到解壓源的根目錄。
1. 輸入以下命令：

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>如果你目前有問題，請回到基本的問題解決。
>
>1. 建立新資料夾(mkdirtest)
>1. 導航到此新資料夾(CDtest)
>1. 運行「phonegap create helloWorld」
>1. 導航到helloWorld(cd helloWorld)
>1. 運行「phonegap運行android（或將android替換為上面的ios）。
>1. 模擬器將開啟運行新建立的PhoneGap應用程式，如果JavaScript本機橋接可以運行，則會說「設備就緒」。

>
>這將驗證您是否正確啟動和運行了PhoneGap CLI開發環境。

## 使用Safari和IOS調試調試Javascript {#debug-javascripts-with-safari-and-ios-debug}

您可以使用Safari的開發人員工具調試應用程式的JavaScripts，與使用Web應用程式時的方法相同。

## 啟用Safari開發人員工具 {#enable-safari-developer-tools}

要啟用開發人員工具：

* 開啟Safari的首選項

   * 在菜單欄中按一下Safari
   * 按一下「首選項」

* 按一下「首選項」窗口中的「高級」

![chlimage_1-47](assets/chlimage_1-47.png)

* 選中「在菜單欄中顯示開髮菜單」
* 關閉「首選項」窗口

## 將Safari連接到iOS {#connect-safari-to-ios}

您可以將Safari連接到iOS設備或模擬器。

* 在控制台窗口中，導航到解壓源的根目錄。
* 輸入以下命令以在設備或模擬器上啟動應用。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* 開啟Safari
* 按一下菜單欄中的「開發」
* 選擇iOS模擬器子菜單
* 按一下home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## 使用Safari的Web檢查器調試JavaScript {#debug-javascript-with-safari-s-web-inspector}

可以在源中的任何位置設定斷點。 當您與模擬器或設備交互時，應用程式的執行將停止在這些斷點處。 您可以逐步執行並檢查變數中的值。

* 在「Web檢查器」窗口中按一下「資源」
* 導航源樹並按一下所需的源檔案
* 按一下相鄰行號以添加斷點
* 與設備或模擬器交互

![chlimage_1-49](assets/chlimage_1-49.png)

* 使用控制按鈕繼續執行、逐步執行、逐步執行和退出方法：

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>要查看變數值，請在當前方法中將滑鼠懸停。

## 後續步驟 {#the-next-steps}

一旦您瞭解了使用PhoneGap CLI開發應用，請參閱 [訪問設備功能](/help/mobile/phonegap-access-device-features.md)。
