---
title: 使用PhoneGap CLI開發應用程式
seo-title: Developing Apps with PhoneGap CLI
description: 請參閱本頁面，了解如何使用PhoneGap CLI開發應用程式。
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

# 使用PhoneGap CLI開發應用程式{#developing-apps-with-phonegap-cli}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

只要您已設定開發環境，您就能在任何指定時間，以開發人員身分，在裝置或模擬器中執行應用程式。

若要執行下列範例，您需要系統執行含Xcode的OSx(Mac)，或是Mac/Win/Linux系統並安裝Android SDK。

## Bootstrap您的開發環境 {#bootstrap-your-development-environment}

[安裝PhoneGap CLI](https://docs.phonegap.com/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

若為iOS:若要針對iPhone和iPad進行開發，您需要Apple的Xcode IDE。

* 免費下載 [此處](https://developer.apple.com/xcode/downloads/).
* [PhoneGap iOS平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_ios_index.md.html#iOS%20Platform%20Guide)

對於Android:若要針對iPhone和iPad進行開發，您需要Google的Android Stuido IDE。

* 免費下載 [此處](https://developer.android.com/sdk/index.html).
* [PhoneGap Android平台指南](https://docs.phonegap.com/en/4.0.0/guide_platforms_android_index.md.html#Android%20Platform%20Guide)

## 下載來源 {#download-the-source}

成功布建開發環境後，請從「AEM應用程式建置方塊」下載來源：

* 按一下PhoneGap Build圖磚下拉式>形圖。

![chlimage_1-45](assets/chlimage_1-45.png)

* 按一下「下載源」。
* 從「下載來源」強制回應視窗中選取所需的來源。

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>開發來源包含應用程式的最新狀態，但包含未分段的變更。 使用測試來源來建立要提交至應用程式商店廠商的發行候選項目。
>
>如果您從未預備應用程式，選取測試將觸發預備工作流程(提示：這會在AppStore和Google PlayStore提供的PhoneGap Enterprise Viewer應用程式中顯示為分階段應用程式)。

* 按一下「下載」 ，並將ZIP儲存至您的電腦。
* 將下載的zip檔案解壓縮至您的工作區。

## 建立並載入應用程式（從來源） {#build-and-load-the-app-from-source}

PhoneGap CLI可以建立平台項目、編譯源，並以單一命令部署應用程式。

>[!NOTE]
>
>您可以分別執行這些步驟，請參閱 [PhoneGap CLI檔案](https://phonegap.com/blog/2014/11/13/phonegap-cli-3-6-3/).

1. 請確定您已安裝PhoneGap CLI，請參閱上文。
1. 在主控台（或終端機）視窗中，導覽至擷取之來源的根目錄。
1. 輸入以下命令：

```xml
phonegap run android

// -- or -- //

phonegap run ios
```

>[!NOTE]
>
>如果您目前有問題，請回到基本概念，了解疑難問題 — 
>
>1. 建立新資料夾（mkdir測試）
>1. 導覽至此新資料夾（光碟測試）
>1. 執行&#39;phonegap create helloWorld&#39;
>1. 導航到helloWorld(cd helloWorld)
>1. 執行&#39;phonegap run android（或以ios取代android，如上所述）。
>1. 模擬器會開啟，執行您新建立的PhoneGap應用程式，說「設備就緒」（如果JavaScript至原生的橋接器可運作）。

>
>這將驗證您的PhoneGap CLI開發環境是否正常運作。

## 使用Safari和IOS除錯Javascript {#debug-javascripts-with-safari-and-ios-debug}

您可以使用Safari的開發人員工具來除錯應用程式的JavaScripts，如同使用Web應用程式的方式。

## 啟用Safari開發人員工具 {#enable-safari-developer-tools}

若要啟用開發人員工具：

* 開啟Safari的偏好設定

   * 在功能表列中按一下「Safari」
   * 按一下「首選項」

* 按一下「首選項」(Preference)窗口中的「高級」(Advanced)

![chlimage_1-47](assets/chlimage_1-47.png)

* 勾選「在功能表列中顯示開發功能表」
* 關閉「首選項」窗口

## 將Safari連線至iOS {#connect-safari-to-ios}

您可以將Safari連線至iOS裝置或模擬器。

* 在控制台視窗中，導覽至擷取之來源的根目錄。
* 輸入下列命令，在裝置或模擬器上啟動您的應用程式。

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

## 使用Safari的Web檢查器除錯JavaScript {#debug-javascript-with-safari-s-web-inspector}

可以在源中的任意位置設定斷點。 當您與模擬器或裝置互動時，應用程式的執行將停止在這些中斷點。 您可以逐步執行，並檢查變數中的值。

* 在「Web檢查器」窗口中按一下「資源」
* 導航源樹，然後按一下所需的源檔案
* 按一下相鄰的行號以添加斷點
* 與裝置或模擬器互動

![chlimage_1-49](assets/chlimage_1-49.png)

* 使用控制按鈕來繼續執行、逐步執行、逐步執行和退出方法：

![](do-not-localize/chlimage_1-4.png)

>[!NOTE]
>
>若要查看變數的值，請在目前方法中暫留滑鼠。

## 後續步驟 {#the-next-steps}

了解「使用PhoneGap CLI開發應用程式」後，請參閱 [訪問設備功能](/help/mobile/phonegap-access-device-features.md).
