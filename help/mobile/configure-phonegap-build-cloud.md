---
title: 設定您的Adobe PhoneGap BuildCloud Service
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: 請依照本頁所述，配置雲服務並使用PhoneGap組建構建應用程式。
seo-description: Follow this page for configuring the cloud services and building your application with PhoneGap build.
uuid: 59aa99c3-1425-4cc5-9839-a57a6a545d45
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 3c84f4ec-d89b-4ad4-802e-ee3e2d49d916
exl-id: d91a00d1-12fa-4c84-a426-49413f61c126
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# 設定您的Adobe PhoneGap BuildCloud Service {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

此 **PhoneGap Build圖磚** 在應用程式控制面板上，可透過Adobe PhoneGap Build服務建置和發佈您的PhoneGap行動應用程式。

在 **管理應用程式** 使用推送遠端組建時，會使用PhoneGap Build建置圖磚 **PhoneGap Build** 平鋪。

您可以推送遠端組建至 [https://build.phonegap.com](https://build.phonegap.com) 或下載來源以在本機建置 [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/).

![PhoneGap Build圖磚](assets/chlimage_1-60.png)

## 設定Cloud Service {#configuring-the-cloud-service}

若要善用PhoneGap Build，您必須使用您的PhoneGap Build帳戶資訊設定AEMPhoneGap BuildCloud Service。

如果您目前沒有帳戶，請導覽至 [https://build.phonegap.com](https://build.phonegap.com) 註冊！ 如果您有Adobe Creative Cloud會籍，則最多可支援25個私人應用程式（非開放原始碼應用程式）。

在您驗證PhoneGap Build帳戶是否有效後，請導覽至您的AEM Cloud Management Console，尤其是 [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用 **管理Cloud Services** 並排以設定新的雲端服務設定。

### 使用「管理Cloud Services」圖磚 {#using-manage-cloud-services-tile}

開始使用建立應用程式之前 **PhoneGap Build** 圖磚，您必須使用 **管理Cloud Services** 圖磚。

若要為您的應用程式設定雲端服務，請遵循下列步驟：

1. 按一下 **管理Cloud Services** 方塊。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 選擇 **PhoneGap Build** 選項 **新增或編輯Cloud Service** 螢幕。

   按一下&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 輸入您的憑證以建立新的雲配置。

   驗證後，按一下 **提交**. 此已設定的雲端設定現在會顯示在 **管理Cloud Services** 方塊。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build構建應用程式 {#building-your-application-with-phonegap-build}

設定雲端服務後，您就可以使用 **PhoneGap Build** 方塊。 按一下右上角以從 **建立遠端** 或 **下載來源** 選項。

![chlimage_1-64](assets/chlimage_1-64.png)

若要使用Adobe PhoneGap Build叫用遠端組建，請按一下 **建立遠端**.

>[!NOTE]
>
>如果建置因任何原因而失敗(下方的紅色iOS圖示表示平台失敗)，您可以將游標暫留在圖示上方，即可取得錯誤訊息。 或者，您也可以按一下三點，「……」 位於圖磚底部，可直接導覽至https://build.phonegap.com（您必須驗證），並直接觀看及管理您的組建。

### 使用PhoneGap CLI構建應用程式 {#building-your-application-with-phonegap-cli}

PhoneGap提供命令列介面，可在本機建置您的應用程式。

使用PhoneGap命令行介面(CLI)在您的電腦上編譯PhoneGap應用程式。 若要將AEM內容納入您的應用程式，AEM會建立ZIP檔案，其中包含您行動應用程式的內容、內容同步設定及其他必要資產。 下載ZIP檔案，並將其納入您的組建中。

為了利用PhoneGap的命令行介面，您需要設定本地環境以包括：

1. Platform SDK(iOS、Android、WindowsPhone、...)和，
1. PhoneGap CLI

您可以閱讀更多資訊 [此處](https://docs.phonegap.com/references/phonegap-cli/).

安裝先決條件後，請建立簡單應用程式，然後透過終端機嘗試讓其在模擬器中執行，或在裝置上執行更佳，借此進行簡單測試：

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>添加 — 如果不想在連接的設備上運行，則在此行末尾模擬。

一旦您確認上述功能有效後，請使用 **PhoneGap Build** 平鋪至 **下載來源**. 將檔案儲存並解壓縮至本機系統。 完成後：

* 導覽至該儲存的檔案（資料夾）
* 執行&#39;phonegap run ios&#39;（或android等）

### 其他資源 {#additional-resources}

若要了解作者和開發人員的角色和責任，請參閱下列資源：

* [使用AEM為Adobe PhoneGap企業開發](/help/mobile/developing-in-phonegap.md)
* [在AEM中為Adobe PhoneGap Enterprise編寫](/help/mobile/phonegap.md)
