---
title: 建立行動應用程式
seo-title: Building Mobile Applications
description: 此頁面提供使用GitHub所提供程式碼來建立行動應用程式的完整逐步文章。建置您的應用程式以安裝至裝置或模擬器，以便進行測試或發佈至應用程式商店。 您可以使用PhoneGap命令行介面在本地構建應用程式，或使用PhoneGap Build在雲中構建應用程式。
seo-description: This page provides a complete step-by-step article on how to build a mobile application using code available from GitHub is available here.Build your application to install to a device or simulator for testing or for publishing to app stores. You can build applications locally using the PhoneGap Command Line Interface, or in the cloud using PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 1%

---

# 建立行動應用程式{#building-mobile-applications}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

建置應用程式以安裝至裝置或模擬器，以進行測試或發佈至應用程式商店。 您可以使用PhoneGap命令行介面在本地構建應用程式，或使用PhoneGap Build在雲中構建應用程式。

有關如何使用GitHub提供的程式碼建立行動應用程式的完整逐步文章已推出 [此處](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html).

## 將應用程式移至發佈例項 {#moving-the-application-to-the-publish-instance}

將應用程式檔案移至發佈例項，以便您能為已安裝的行動應用程式例項提供內容更新，並使用已發佈的內容建立應用程式。 應用程式在儲存庫中由兩個節點分支組成：

* `/content/phonegap/apps/<application name>`:作者建立和啟用的網頁。
* `/content/phonegap/content/<application name>`:應用程式配置檔案和內容同步配置。

>[!NOTE]
>
>如果您未將應用程式檔案移至發佈執行個體，內容作者將無法更新「內容同步」快取。

您只需要移動 `/content/phonegap/content/<application name>` 分支至發佈例項。 中的檔案 `/content/phonegap/apps/<application name>` 當作者啟動頁面時，會移動分支。

AEM提供兩種將大量內容移動至發佈例項的方法：

* [使用「激活樹」命令](/help/sites-authoring/publishing-pages.md) 在復寫主控台上。
* [建立套件](/help/sites-administering/package-manager.md) 包含內容並復寫套件的。

例如，會建立名為phonegapapp的行動應用程式。 下列節點必須移至發佈例項：/content/phonegap/content/phonegapp。

**提示：** 若要將套件從製作例項移至發佈例項，請使用套件上的Replicate命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令行介面構建 {#building-using-the-phonegap-command-line-interface}

使用PhoneGap命令行介面(CLI)在您的電腦上編譯PhoneGap應用程式。 若要將AEM內容納入您的應用程式，AEM會建立ZIP檔案，其中包含您行動應用程式的內容、內容同步設定及其他必要資產。 下載ZIP檔案，並將其納入您的組建中。

### 準備您的建置環境 {#preparing-your-build-environment}

若要使用PhoneGap CLI建置，您必須安裝Node.js和PhoneGap用戶端公用程式。 您需要Internet連接才能執行以下過程。

1. 下載並安裝 [Node.js](https://nodejs.org/).
1. 開啟終端機或命令提示字元，然後輸入以下節點命令以安裝PhoneGap實用程式：

   ```shell
   npm install -g phonegap
   ```

   在Unix或Linux系統上，您可能需要為命令加上前置詞 `sudo`.

   終端顯示一系列HTTPGET命令的結果。 當安裝成功時，終端會顯示程式庫的安裝位置，如下列範例所示：

   ```xml
   /usr/local/bin/phonegap -> /usr/local/lib/node_modules/phonegap/bin/phonegap.js
   phonegap@3.3.0-0.19.6 /usr/local/lib/node_modules/phonegap
   ├── pluralize@0.0.4
   ├── colors@0.6.0-1
   ├── semver@1.1.0
   ├── qrcode-terminal@0.9.4
   ├── shelljs@0.1.4
   ├── optimist@0.6.0 (...)
   ├── prompt@0.2.11 (...)
   ├── phonegap-build@0.8.4 (...)
   ├── connect-phonegap@0.8.1 (...)
   └── cordova@3.3.0-0.1.1 (...)
   ```

1. （選用）取得您所定位之行動平台的SDK:

   * 若要建立iOS平台的應用程式，請安裝 [Xcode](https://developer.apple.com/xcode/).
   * 若要建置Android應用程式，請安裝 [Android SDK](https://developer.android.com/).

### 下載內容ZIP檔案 {#downloading-the-content-zip-file}

將行動應用程式的內容移至檔案系統。

1. 在「行動應用程式」頁面上，選取您的應用程式。
1. （可選）要構建應用程式以完成安裝，請在工具欄上，按一下或點選「清除快取」表徵圖。

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >快取保存已安裝應用程式的內容更新。 清除快取會撤消所有快取更新。

1. 在工具列上，按一下或點選「下載CLI資產」圖示。

   ![](do-not-localize/chlimage_1-1.png)

1. 儲存ZIP檔案後，按一下「成功」對話方塊上的「關閉」 。
1. 解壓縮ZIP檔案的內容。

### 使用PhoneGap CLI來建置 {#using-the-phonegap-cli-to-build}

使用PhoneGap CLI編譯和安裝應用程式。 有關如何使用PhoneGap CLI的資訊，請參見PhoneGap [命令行介面](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) 檔案。

1. 開啟終端機或命令提示字元，並將目前目錄變更為下載的應用程式ZIP檔案。 例如，下列項目會將目錄變更為ng-app-cli.1392137825303.zip檔案：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 輸入您所定位之平台的phonegap命令。 例如，下列命令會建置Android適用的應用程式：

   ```shell
   phonegap build android
   ```

## 使用建立PhoneGap Build {#building-using-phonegap-build}

使用PhoneGap雲端服務來建置您的應用程式。 要執行此過程，必須首先建立PhoneGap Build配置。

### 正在連線到 PhoneGap Build {#connecting-to-phonegap-build}

建立PhoneGap Build設定，以便從AEM內使用PhoneGap Build服務。 提供您將用來建立行動應用程式的PhoneGap Build帳戶的使用者名稱和密碼。

1. 開啟「工具」頁面。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在「CQ操作」區域中，按一下「Cloud Services」。
1. 按一下「立即配置」連結以獲取PhoneGap Build。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在「建立配置」對話框中，鍵入Title屬性的值。 預設情況下，Name屬性的值是從標題派生的，但您可以輸入名稱。 按一下建立。
1. 在「PhoneGap Build配置」對話框中，鍵入PhoneGap Build用戶名和密碼，然後按一下「確定」。

### 使用PhoneGap Build {#using-phonegap-build}

將您的應用程式資源發送到PhoneGap Build，以便為各種移動平台進行編譯。

1. 在「行動應用程式」頁面上，開啟您的行動應用程式。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （可選）要構建應用程式以完成安裝，請選擇該應用程式並按一下清除快取表徵圖。

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >快取保存已安裝應用程式的內容更新。 清除快取會撤消所有快取更新。

1. 選擇閃屏頁面，然後按一下「生成遠程」表徵圖。

   ![](do-not-localize/chlimage_1-3.png)

   **注意：** 測試版AEM Beta版不會在組建成功完成時建立收件匣通知。

1. 在「成功」對話方塊中，按一下「PhoneGap Build」以開啟Adobe PhoneGap Build頁面，位置為 [https://build.phonegap.com/apps](https://build.phonegap.com/apps). 如果您正在等待應用程式出現，可以檢查 [PhoneGap Build狀態](https://status.build.phonegap.com/) 頁面。

   如需安裝組建的相關資訊，請參閱 [PhoneGap Build檔案](https://docs.build.phonegap.com/en_US/3.1.0/#googtrans%28en%29).

   >[!NOTE]
   >
   >免費PhoneGap Build帳戶允許一個專用應用程式。 如果您要建立其他私人應用程式，PhoneGap組建會失敗。

### 後續步驟 {#the-next-steps}

建置程式後的下一步是了解 [應用程式的結構](/help/mobile/phonegap-structure-an-app.md).
