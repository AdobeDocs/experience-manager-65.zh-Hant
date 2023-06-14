---
title: 使用PhoneGap CLI開發應用程式
description: 瞭解如何使用PhoneGap CLI開發應用程式。
uuid: 9a66171d-19af-40db-9c07-f5dd9561e1b5
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 4a034e15-3394-4be3-9e8e-bc894668946a
exl-id: fbeceb70-b199-478b-907b-253ed212ff99
source-git-commit: 78c584db8c35ea809048580fe5b440a0b73c8eea
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 1%

---

# 使用PhoneGap CLI開發應用程式{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobe建議對需要以單頁應用程式框架為基礎的使用者端轉譯（例如React）的專案使用SPA編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

在任何指定時間，身為開發人員，只要您已設定開發環境，即可在裝置或模擬器內執行應用程式。

若要執行下列範例，您需要執行作業系統X (Mac)並安裝Xcode的系統，或安裝Android™ SDK的Mac/Win/Linux系統。

## Bootstrap您的開發環境 {#bootstrap-your-development-environment}

[設定PhoneGap CLI](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

iOS：若要針對iPhone和iPad開發，您需要Apple的Xcode IDE。

* 免費下載 [此處](https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&amp;path=%2Fdownload%2F&amp;rv=1).
* [PhoneGap iOS平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

Android™：若要開發iPhone和iPad，您需要使用Google的Android™ Stuido IDE。

* 免費下載 [此處](https://developer.android.com/studio).
* [PhoneGap Android™平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## 下載來源 {#download-the-source}

成功啟動您的開發環境後，請從AEM App Build動態磚下載來源：

* 按一下PhoneGap Build圖磚下拉式>形箭號。

![chlimage_1-45](assets/chlimage_1-45.png)

* 按一下「下載來源」。
* 從「下載來源」強制回應視窗中選取所需的來源。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>開發來源包含應用程式的最新狀態，其中包含未分階段的變更。 使用測試來源來建立提交至應用程式商店供應商的候選版本。
>
>如果您從未安裝應用程式，請選取「安裝」，觸發安裝工作流程(提示：在AppStore和Google PlayStore提供的PhoneGap Enterprise Viewer應用程式中顯示為安裝應用程式)。

* 按一下「下載」並將ZIP儲存至您的電腦。
* 將下載的zip檔案解壓縮至您的工作區。

## 建置和載入應用程式（從來源） {#build-and-load-the-app-from-source}

PhoneGap CLI可以透過單一命令建立平台專案、編譯來源及部署應用程式。

>[!NOTE]
>
>您可以個別執行所有這些步驟，請參閱 [PhoneGap CLI檔案](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. 請確定您已安裝PhoneGap CLI，請參閱上文。
1. 在主控台（或終端機）視窗中，導覽至解壓縮來源的根目錄。
1. 輸入下列命令：

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
>1. 執行 `phonegap create helloWorld`
>1. 導覽至helloWorld (cd helloWorld)
>1. 執行 `phonegap run android` (或以上述iOS取代android)。
>1. 模擬器隨即開啟，執行您新建立的PhoneGap應用程式，顯示「裝置就緒」（如果原生的JavaScript橋接器正常運作）。
>
>此疑難排解會驗證您的PhoneGap CLI開發環境是否正確執行。

## 使用Safari和IOS Debug針對JavaScript進行偵錯 {#debug-javascripts-with-safari-and-ios-debug}

您可以使用Safari的開發人員工具對應用程式的JavaScript進行偵錯，就像對網頁應用程式進行偵錯一樣。

## 啟用Safari開發人員工具 {#enable-safari-developer-tools}

若要啟用開發人員工具：

* 開啟Safari的偏好設定

   * 按一下功能表列中的Safari
   * 按一下偏好設定

* 按一下偏好設定視窗中的進階

![chlimage_1-47](assets/chlimage_1-47.png)

* 勾選「在選單列中顯示『開發』選單」
* 關閉偏好設定視窗

## 將Safari連線至iOS {#connect-safari-to-ios}

您可以將Safari連線至iOS裝置或模擬器。

* 在主控台視窗中，導覽至解壓縮來源的根目錄。
* 輸入以下命令，以便在裝置或模擬器上啟動應用程式。

```xml
phonegap run <platform> --device

// -- or -- //

phonegap run <platform> --emulator
```

* 開啟Safari
* 按一下功能表列中的開發
* 選取iOS Simulator子功能表
* 按一下home.html

![chlimage_1-48](assets/chlimage_1-48.png)

## 使用Safari的Web Inspector除錯JavaScript {#debug-javascript-with-safari-s-web-inspector}

您可以在來源中的任何位置設定中斷點。 當您與模擬器或裝置互動時，應用程式的執行會在這些中斷點停止。 您可以逐步執行並檢查變數中的值。

* 按一下「網頁檢測器」視窗中的「資源」
* 瀏覽來源樹狀結構，然後按一下所需的來源檔案
* 按一下新增中斷點旁邊的行號
* 與裝置或模擬器互動

![chlimage_1-49](assets/chlimage_1-49.png)

* 使用控制按鈕來繼續執行、跳過、逐步執行或逐步退出方法：

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>若要檢視變數的值，請在目前的方法中，將滑鼠游標暫留。

## 後續步驟 {#the-next-steps}

瞭解使用PhoneGap CLI開發應用程式後，請參閱 [存取裝置功能](/help/mobile/phonegap-access-device-features.md).
