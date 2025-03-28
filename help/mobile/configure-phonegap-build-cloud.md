---
title: 設定您的Adobe PhoneGap BuildCloud Service
description: 請依照本頁面的說明設定雲端服務，並使用PhoneGap Build建置您的應用程式。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# 設定您的Adobe PhoneGap BuildCloud Service {#configure-your-adobe-phonegap-build-cloud-service}

{{ue-over-mobile}}

應用程式儀表板上的&#x200B;**PhoneGap Build磚**&#x200B;可讓您透過Adobe PhoneGap Build Service建置及發佈PhoneGap行動應用程式。

推播含有&#x200B;**PhoneGap Build**&#x200B;圖磚的遠端組建時，**管理應用程式**&#x200B;圖磚內定義的所有支援平台都是以PhoneGap Build建置。

您可以將遠端組建推送至`https://build.phonegap.com`，或下載來源以使用`https://docs.phonegap.com/references/phonegap-cli/`的PhoneGap CLI在本機建置。

![PhoneGap Build磚](assets/chlimage_1-60.png)

## 設定Cloud Service {#configuring-the-cloud-service}

若要充分利用PhoneGap Build功能，您必須使用您的PhoneGap Build帳戶資訊來設定AEMPhoneGap BuildCloud Service。

如果您目前沒有帳戶，請瀏覽至`https://build.phonegap.com`並註冊！ 如果您擁有Adobe Creative Cloud會籍，最多可支援25個私人應用程式（非開放原始碼應用程式）。

在確認您的PhoneGap Build帳戶有效後，請導覽至您的AEM Cloud Management Console，尤其是[PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用&#x200B;**管理Cloud Service**&#x200B;圖磚來設定新的雲端服務組態。

### 使用「管理Cloud Service」圖磚 {#using-manage-cloud-services-tile}

開始使用&#x200B;**PhoneGap Build**&#x200B;圖磚建置您的應用程式之前，您必須使用AEM Mobile儀表板的&#x200B;**管理Cloud Service**&#x200B;圖磚來設定您的雲端服務。

若要設定應用程式的雲端服務，請遵循下列步驟：

1. 按一下&#x200B;**管理Cloud Service**&#x200B;圖磚的右上角。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 從&#x200B;**新增或編輯PhoneGap Build**&#x200B;畫面中選擇&#x200B;**Cloud Service**&#x200B;選項。

   按一下「**下一步**」。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 輸入您的憑證以便建立雲端設定。

   驗證後，按一下&#x200B;**提交**。 此已設定的雲端設定現在顯示在&#x200B;**管理Cloud Service**&#x200B;圖磚中。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build建置您的應用程式 {#building-your-application-with-phonegap-build}

設定雲端服務後，您就可以使用&#x200B;**PhoneGap Build**&#x200B;圖磚建置應用程式。 按一下右上角，您就可以從&#x200B;**建置遠端**&#x200B;或&#x200B;**下載Source**&#x200B;選項中選擇。

![chlimage_1-64](assets/chlimage_1-64.png)

若要使用Adobe PhoneGap Build叫用遠端組建，請按一下&#x200B;**組建遠端**。

>[!NOTE]
>
>如果組建因任何原因失敗(下方紅色的iOS圖示表示平台失敗)，您可以將游標停留在圖示上以取得錯誤訊息。 或者，您可以按一下圖磚底部的三點圖示「……」，直接導覽至`https://build.phonegap.com` （您必須驗證），並直接觀看及管理您的組建。

### 使用PhoneGap CLI建置您的應用程式 {#building-your-application-with-phonegap-cli}

PhoneGap提供命令列介面，可在本機建置您的應用程式。

使用PhoneGap命令列介面(CLI)編譯電腦上的PhoneGap應用程式。 為了將AEM內容納入您的應用程式，AEM會建立一個ZIP檔案，其中包含您行動應用程式的內容、Content Sync設定和其他必要的資產。 下載ZIP檔案並將其包含在您的組建中。

若要利用PhoneGap的CLI，您必須設定本機環境，以包含：

1. 平台SDK (iOS、Android™、WindowsPhone...)和
1. PhoneGap CLI

您可以在`https://docs.phonegap.com/references/phonegap-cli/`閱讀更多資訊。

安裝先決條件後，請從終端機嘗試建立簡單的應用程式，並在模擬器中或更好的裝置上執行，以進行簡單的測試：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>新增 — 如果您不想在連線的裝置上執行，請在這行的結尾進行模擬。

一旦您確認上述方法正確無誤，請使用&#x200B;**PhoneGap Build**&#x200B;磁貼來&#x200B;**下載Source**。 將檔案儲存並解壓縮至本機系統。 完成此操作後：

* 導覽至該儲存的檔案（資料夾）
* 執行「phonegap run ios」（或android等）

### 其他資源 {#additional-resources}

若要瞭解作者和開發人員的角色和責任，請參閱以下資源：

* [使用AEM為Adobe PhoneGap Enterprise開發](/help/mobile/developing-in-phonegap.md)
* [在AEM中為Adobe PhoneGap Enterprise製作](/help/mobile/phonegap.md)
