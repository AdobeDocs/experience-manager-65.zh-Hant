---
title: 建立行動應用程式
description: 本頁面提供有關如何使用GitHub提供的程式碼來建立行動應用程式的完整逐步文章，請參見此處。 建置您的應用程式以安裝至裝置或模擬器，以進行測試或發佈至應用程式商店。 您可以使用PhoneGap命令列介面在本機建立應用程式，或使用PhoneGap Build在雲端中建立應用程式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7c2e5ed8-9f8e-4a81-b736-589ef4089f29
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 建立行動應用程式{#building-mobile-applications}

{{ue-over-mobile}}

建置您的應用程式以安裝至裝置或模擬器，以進行測試或發佈至應用程式商店。 您可以使用PhoneGap命令列介面在本機建立應用程式，或使用PhoneGap Build在雲端中建立應用程式。

[這裡](https://helpx.adobe.com/experience-manager/using/aem62_mobile.html)提供有關如何使用GitHub提供的程式碼建置行動應用程式的完整逐步文章。

## 將應用程式移至Publish例項 {#moving-the-application-to-the-publish-instance}

將應用程式檔案移至發佈執行個體，以便您能夠為已安裝的行動應用程式執行個體提供內容更新，並使用發佈的內容建置應用程式。 應用程式包含存放庫中的兩個節點分支：

* `/content/phonegap/apps/<application name>`：作者建立和啟動的網頁。
* `/content/phonegap/content/<application name>`：應用程式組態檔與內容同步設定。

>[!NOTE]
>
>如果您未將應用程式檔案移至發佈例項，內容作者將無法更新Content Sync快取。

您只需要將`/content/phonegap/content/<application name>`分支中的檔案移至發佈執行個體。 當作者啟動頁面時，會移動`/content/phonegap/apps/<application name>`分支中的檔案。

AEM提供將大量內容移至發佈執行個體的兩種方法：

* [在復寫主控台上使用[啟動樹狀結構]命令](/help/sites-authoring/publishing-pages.md)。
* [建立包含內容的封裝](/help/sites-administering/package-manager.md)，並復寫該封裝。

例如，系統會建立名為phonegapapp的行動應用程式。 下列節點必須移至發佈執行個體： /content/phonegap/content/phonegapapp。

**提示：**&#x200B;若要將套件從製作執行個體移至發佈執行個體，請對套件使用Replicate命令。

![chlimage_1-16](assets/chlimage_1-16.png)

## 使用PhoneGap命令列介面進行建置 {#building-using-the-phonegap-command-line-interface}

使用PhoneGap命令列介面(CLI)編譯電腦上的PhoneGap應用程式。 為了將AEM內容納入您的應用程式，AEM會建立一個ZIP檔案，其中包含您行動應用程式的內容、Content Sync設定和其他必要的資產。 下載ZIP檔案並將其包含在您的組建中。

### 準備您的組建環境 {#preparing-your-build-environment}

若要使用PhoneGap CLI建置，您必須安裝Node.js和PhoneGap使用者端公用程式。 您需要網際網路連線才能執行下列程式。

1. 下載並安裝[Node.js](https://nodejs.org/en)。
1. 開啟終端機或命令提示字元並輸入下列節點命令以安裝PhoneGap公用程式：

   ```shell
   npm install -g phonegap
   ```

   在UNIX®或Linux®系統上，您可能需要使用`sudo`作為命令的前置詞。

   終端機會顯示一系列HTTPGET命令的結果。 安裝成功後，終端機會顯示程式庫的安裝位置，類似於以下範例：

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

1. （選用）取得您鎖定目標之行動平台的SDK：

   * 若要建置iOS平台的App，請安裝最新版本的[Xcode](https://developer.apple.com/xcode/)。
   * 若要建置Android™ App，請安裝[Android™ SDK](https://developer.android.com/)。

### 下載內容ZIP檔案 {#downloading-the-content-zip-file}

將行動應用程式的內容移至檔案系統。

1. 在行動應用程式頁面上，選取您的應用程式。
1. （選擇性）若要建置應用程式以進行完整安裝，請按一下工具列上的「清除快取」圖示。

   ![清除以中斷連結符號表示的快取圖示。](do-not-localize/chlimage_1.png)

   >[!NOTE]
   >
   >快取會儲存已安裝應用程式的內容更新。 清除快取將會使所有快取的更新失效。

1. 在工具列上，按一下下載CLI Assets圖示。

   ![下載CLI Assets圖示，以重疊的平板電腦符號表示。](do-not-localize/chlimage_1-1.png)

1. 儲存ZIP檔案後，按一下「成功」對話方塊上的「關閉」 。
1. 解壓縮ZIP檔案的內容。

### 使用PhoneGap CLI建置 {#using-the-phonegap-cli-to-build}

使用PhoneGap CLI編譯及安裝應用程式。 如需有關如何使用PhoneGap CLI的資訊，請參閱PhoneGap Command-line Interface (`https://docs.phonegap.com/en/3.0.0/guide_cli_index.md.html`)檔案。

1. 開啟終端機或命令提示字元，並將目前目錄變更為下載的應用程式ZIP檔案。 例如，下列會將目錄變更為ng-app-cli.1392137825303.zip檔案：

   ```shell
   cd ~/Downloads/ng-app-cli.1392137825303
   ```

1. 針對您要定位的平台輸入phonegap指令。 例如，下列命令會建置Android的應用程式™：

   ```shell
   phonegap build android
   ```

## 使用PhoneGap Build建置 {#building-using-phonegap-build}

使用PhoneGap雲端服務建置您的應用程式。 若要執行此程式，您必須先建立PhoneGap Build組態。

### 正在連線到PhoneGap Build {#connecting-to-phonegap-build}

建立PhoneGap Build設定，以便您可以使用AEM中的PhoneGap Build服務。 提供您將用來建置行動應用程式之PhoneGap Build帳戶的使用者名稱和密碼。

1. 開啟「工具」頁面。 ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))。
1. 在「CQ操作」區域中，按一下「Cloud Service」。
1. 按一下PhoneGap Build的「立即設定」連結。

   ![chlimage_1-17](assets/chlimage_1-17.png)

1. 在「建立組態」對話方塊中，輸入Title屬性的值。 依預設，Name屬性的值是從標題衍生而來，但您可以輸入名稱。 按一下「建立」。
1. 在「PhoneGap Build組態」對話方塊中，輸入您的PhoneGap Build使用者名稱和密碼，然後按一下「確定」。

### 使用PhoneGap Build {#using-phonegap-build}

將您的應用程式資源傳送至PhoneGap Build，以便針對各種行動平台進行編譯。

1. 在行動應用程式頁面上，開啟您的行動應用程式。 ([http://localhost:4502/mobile.html/content/phonegap](http://localhost:4502/mobile.html/content/phonegap))
1. （選擇性）若要建立應用程式以完成安裝，請選取該應用程式，然後按一下「清除快取」圖示。

   ![清除以中斷連結符號表示的快取圖示。](do-not-localize/chlimage_1-2.png)

   >[!NOTE]
   >
   >快取會儲存已安裝應用程式的內容更新。 清除快取將會使所有快取的更新失效。

1. 選取啟動顯示頁面，然後按一下「建置遠端」圖示。

   ![由兩個圓形齒輪指示的「建置遠端」圖示。](do-not-localize/chlimage_1-3.png)

   **注意：** AEM Beta的Beta版本不會在組建成功完成時建立收件匣通知。

1. 在「成功」對話方塊中，按一下「PhoneGap Build」以開啟`https://build.phonegap.com/apps`的Adobe PhoneGap Build頁面。 如果您正在等候應用程式出現，可以在`https://status.build.phonegap.com/`檢視PhoneGap Build狀態。

   如需有關安裝組建的資訊，請參閱[PhoneGap Build檔案](https://github.com/phonegap/phonegap-docs/tree/master/docs/4-phonegap-build)。

   >[!NOTE]
   >
   >允許一個私用應用程式的自由PhoneGap Build帳戶。 如果您要建置其他私人應用程式，PhoneGap建置會失敗。

### 後續步驟 {#the-next-steps}

建置程式之後的下一個步驟是學習應用程式](/help/mobile/phonegap-structure-an-app.md)的[結構。
