---
title: 使用PhoneGap CLI開發應用程式
description: 瞭解如何使用可開機的開發環境，透過PhoneGap CLI開發行動應用程式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 2%

---

# 使用PhoneGap CLI開發應用程式{#developing-apps-with-phonegap-cli}

{{ue-over-mobile}}

在任何指定時間，身為開發人員，只要您已設定開發環境，就可以在裝置或模擬器內執行應用程式。

若要執行下列範例，您需要執行含有Xcode的macOS X的系統，或安裝有Android™ SDK的Mac/Win/Linux系統。

## Bootstrap您的開發環境 {#bootstrap-your-development-environment}

設定PhoneGap CLI (`https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface`)

iOS：若要開發iPhone和iPad，您需要使用Apple的Xcode IDE。

* 免費下載[這裡](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1)。
* PhoneGap iOS平台指南(`https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide`)

Android™：若要開發iPhone和iPad，您需要使用Google的Android™ Stuido IDE。

* 免費下載[這裡](https://developer.android.com/studio)。
* PhoneGap Android™平台指南(`https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide`)

## 下載Source {#download-the-source}

當您成功啟動您的開發環境時，請從AEM App Build動態磚下載來源：

* 按一下PhoneGap Build圖磚下拉式>形箭號。

![chlimage_1-45](assets/chlimage_1-45.png)

* 按一下「下載Source」 。
* 從下載Source強制回應視窗中選取所需的來源。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>開發來源包含應用程式的最新狀態，且包含未分階段的變更。 使用測試來源，建置要提交至應用程式商店廠商的候選版本。
>
>如果您從未暫存應用程式，選取暫存會觸發暫存工作流程(提示：在AppStore和Google PlayStore提供的PhoneGap Enterprise Viewer應用程式中，顯示為暫存應用程式)。

* 按一下「下載」並將ZIP儲存到您的電腦。
* 將下載的zip檔案解壓縮至您的工作區。

## 建置並載入應用程式（從來源） {#build-and-load-the-app-from-source}

PhoneGap CLI可以透過單一命令建立平台專案、編譯來源及部署應用程式。

>[!NOTE]
>
>您可以個別執行所有這些步驟，請參閱PhoneGap CLI檔案(`https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/`)。

1. 請確定您已安裝PhoneGap CLI，請參閱上文。
1. 在主控台（或終端機）視窗中，導覽至您擷取之來源的根目錄。
1. 輸入以下命令：

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>如果您目前遇到問題，請回到基本知識以進行疑難排解 — 
>
>1. 建立資料夾（mkdir測試）
>1. 瀏覽至這個新資料夾（光碟測試）
>1. 執行`phonegap create helloWorld`
>1. 導覽至helloWorld (cd helloWorld)
>1. 執行`phonegap run android` (或將Android™取代為上述iOS)。
>1. 執行您新建立的PhoneGap應用程式時，模擬器會開啟，並顯示「裝置就緒」(如果JavaScript Bridge to native正常運作)。
>
>此疑難排解會驗證您的PhoneGap CLI開發環境是否正確執行。

## 使用Safari和IOS Debug除錯JavaScript {#debug-javascripts-with-safari-and-ios-debug}

您可以使用Safari的開發人員工具對應用程式的JavaScript進行除錯，就像對網頁應用程式進行除錯一樣。

## 啟用Safari開發人員工具 {#enable-safari-developer-tools}

若要啟用開發人員工具：

* 開啟Safari的偏好設定

   * 按一下功能表列中的Safari
   * 按一下偏好設定

* 按一下偏好設定視窗中的進階

![chlimage_1-47](assets/chlimage_1-47.png)

* 勾選「在功能表列中顯示『開發』功能表」
* 關閉偏好設定視窗

## 將Safari連線至iOS {#connect-safari-to-ios}

您可以將Safari連線至iOS裝置或模擬器。

* 在主控台視窗中，導覽至您擷取之來源的根目錄。
* 輸入以下命令，您便可以在裝置或模擬器上啟動應用程式。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* 開啟Safari
* 按一下功能表列中的「開發」
* 選取iOS模擬器子功能表
* 按一下home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## 使用Safari的Web Inspector除錯JavaScript {#debug-javascript-with-safari-s-web-inspector}

您可以在來源的任何位置設定中斷點。 當您與模擬器或裝置互動時，應用程式的執行會在這些中斷點停止。 您可以逐步執行並檢查變數中的值。

* 按一下「網頁檢測器」視窗中的「資源」
* 瀏覽來源樹狀結構，然後按一下所需的來源檔案
* 按一下旁邊的行號以新增中斷點
* 與裝置或模擬器互動

![chlimage_1-49](assets/chlimage_1-49.png)

* 使用控制按鈕來繼續執行、跳過、逐步執行及跳出方法：

![五個功能不同的控制項按鈕在水準列對齊。](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>若要檢視目前方法中的變數值，請將滑鼠游標停留。

## 後續步驟 {#the-next-steps}

瞭解使用PhoneGap CLI開發應用程式後，請參閱[存取裝置功能](/help/mobile/phonegap-access-device-features.md)。
