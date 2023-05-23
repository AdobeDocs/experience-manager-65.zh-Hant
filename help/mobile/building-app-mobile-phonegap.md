---
title: 構建移動應用程式
seo-title: Building Mobile Applications
description: 此頁提供了一個完整的分步文章，介紹如何使用GitHub提供的代碼構建移動應用程式。構建應用程式以安裝到設備或模擬器以進行測試或發佈到應用商店。 您可以使用PhoneGap命令行介面在本地構建應用程式，或使用PhoneGap Build在雲中構建應用程式。
seo-description: This page provides a complete step-by-step article on how to build a mobile application using code available from GitHub is available here.Build your application to install to a device or simulator for testing or for publishing to app stores. You can build applications locally using the PhoneGap Command Line Interface, or in the cloud using PhoneGap Build.
uuid: 1ff6fe1a-24cc-4973-a2cd-8d356bc649b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: b2778086-8280-4306-bf3a-f6ec2a0e04df
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
source-git-commit: 85d39e59b82fdfdcd310be61787a315668aebe38
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 1%

---

# 構建移動應用程式{#building-mobile-applications}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

構建應用程式以安裝到設備或模擬器以進行測試或發佈到應用商店。 您可以使用PhoneGap命令行介面在本地構建應用程式，或使用PhoneGap Build在雲中構建應用程式。

有關如何使用GitHub提供的代碼構建移動應用程式的完整分步文章可用 [這裡](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html)。

## 將應用程式移動到發佈實例 {#moving-the-application-to-the-publish-instance}

將應用程式檔案移動到發佈實例，以便您可以向已安裝的移動應用程式實例提供內容更新，並使用發佈的內容構建應用程式。 應用程式由儲存庫中的兩個節點分支組成：

* `/content/phonegap/apps/<application name>`:作者建立和激活的網頁。
* `/content/phonegap/content/<application name>`:應用程式配置檔案和內容同步配置。

>[!NOTE]
>
>如果不將應用程式檔案移動到發佈實例，內容作者將無法更新內容同步快取。

您只需要移動 `/content/phonegap/content/<application name>` 分支到發佈實例。 中的檔案 `/content/phonegap/apps/<application name>` 當作者激活頁面時，將移動分支。

提AEM供了兩種將批量內容移動到發佈實例的方法：

* [使用「激活樹」命令](/help/sites-authoring/publishing-pages.md) 在複製控制台上。
* [建立包](/help/sites-administering/package-manager.md) 包含內容並複製包。

例如，將建立名為phonegapapp的移動應用程式。 必須將以下節點移動到發佈實例：/content/phonegap/content/phonegapp。

**提示：** 要將包從作者實例移動到發佈實例，請使用包上的「複製」命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令行介面構建 {#building-using-the-phonegap-command-line-interface}

使用PhoneGap命令行介面(CLI)在電腦上編譯PhoneGap應用程式。 要將內AEM容包括到應AEM用程式中，請建立包含移動應用程式內容、內容同步配置和其他必需資產的ZIP檔案。 下載ZIP檔案並將其包含在您的生成中。

### 準備生成環境 {#preparing-your-build-environment}

要使用PhoneGap CLI構建，需要安裝Node.js和PhoneGap客戶端實用程式。 您需要Internet連接才能執行以下過程。

1. 下載並安裝 [節點.js](https://nodejs.org/)。
1. 開啟終端或命令提示符，然後輸入以下節點命令以安裝PhoneGap實用程式：

   ```shell
   npm install -g phonegap
   ```

   在Unix或Linux系統上，可能需要在命令前加上前置詞 `sudo`。

   終端顯示一系列HTTPGET命令的結果。 安裝成功後，終端將顯示庫的安裝位置，與以下示例類似：

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

1. （可選）獲取您所針對的移動平台的SDK:

   * 要為iOS平台構建應用，請安裝 [Xcode](https://developer.apple.com/xcode/)。
   * 要構建Android應用，請安裝 [Android SDK](https://developer.android.com/)。

### 下載內容ZIP檔案 {#downloading-the-content-zip-file}

將移動應用程式的內容移動到檔案系統。

1. 在「移動應用程式」頁面上，選擇您的應用程式。
1. （可選）要構建應用程式以完成安裝，請在工具欄上按一下或點擊「清除快取」表徵圖。

   ![](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >快取保存已安裝應用程式的內容更新。 清除快取會撤消所有快取的更新。

1. 在工具欄上，按一下或點擊「下載CLI資產」表徵圖。

   ![](do-not-localize/chlimage_1-1.png)

1. 保存ZIP檔案後，按一下「成功」對話框上的「關閉」。
1. 解壓ZIP檔案的內容。

### 使用PhoneGap CLI生成 {#using-the-phonegap-cli-to-build}

使用PhoneGap CLI編譯和安裝應用程式。 有關如何使用PhoneGap CLI的資訊，請參見PhoneGap [命令行介面](https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html) 文檔。

1. 開啟終端或命令提示符，並將當前目錄更改為下載的應用程式ZIP檔案。 例如，以下命令將目錄更改為ng-app-cli.1392137825303.zip檔案：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 輸入要瞄準的平台的phonegap命令。 例如，以下命令為Android生成應用：

   ```shell
   phonegap build android
   ```

## 使用PhoneGap Build {#building-using-phonegap-build}

使用PhoneGap雲服務構建您的應用。 要執行此過程，必須先建立PhoneGap Build配置。

### 正在連線到 PhoneGap Build {#connecting-to-phonegap-build}

建立PhoneGap Build配置，以便從內部使用PhoneGap Build服AEM務。 提供將用於構建移動應用程式的PhoneGap Build帳戶的用戶名和密碼。

1. 開啟「工具」頁。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在「CQ操作」區域，按一下Cloud Services。
1. 按一下「Configure Now（立即配置）」連結以獲取PhoneGap Build。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在「建立配置」對話框中，鍵入「標題」屬性的值。 預設情況下，「名稱」屬性的值是從標題派生的，但您可以輸入名稱。 按一下建立。
1. 在「PhoneGap Build配置」對話框中，鍵入PhoneGap Build用戶名和密碼，然後按一下「確定」。

### 使用PhoneGap Build {#using-phonegap-build}

將應用程式資源發送到PhoneGap Build，以便為各種移動平台進行編譯。

1. 在「移動應用程式」頁面上，開啟移動應用程式。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （可選）要構建應用程式以完成安裝，請選擇該應用程式，然後按一下「清除快取」表徵圖。

   ![](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >快取保存已安裝應用程式的內容更新。 清除快取會撤消所有快取的更新。

1. 選擇閃屏頁，然後按一下「生成遠程」表徵圖。

   ![](do-not-localize/chlimage_1-3.png)

   **注：** 成功完成生AEM成後，測試版不會建立收件箱通知。

1. 在「成功」對話框中，按一下「PhoneGap Build」開啟「Adobe PhoneGap Build」頁面， [https://build.phonegap.com/apps](https://build.phonegap.com/apps)。 如果您正在等待應用程式出現，您可以檢查 [PhoneGap Build狀態](https://status.build.phonegap.com/) 的子菜單。

   有關安裝生成的資訊，請參見 [PhoneGap Build文檔](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build)。

   >[!NOTE]
   >
   >免費PhoneGap Build帳戶允許使用一個專用應用程式。 如果您正在構建其他專用應用程式，則PhoneGap生成失敗。

### 後續步驟 {#the-next-steps}

構建過程後的下一步是瞭解 [應用的結構](/help/mobile/phonegap-structure-an-app.md)。
