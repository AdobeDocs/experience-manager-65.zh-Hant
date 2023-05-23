---
title: 配置您的Adobe PhoneGap BuildCloud Service
seo-title: Configure your Adobe PhoneGap Build Cloud Service
description: 按照本頁配置雲服務並使用PhoneGap生成構建應用程式。
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

# 配置您的Adobe PhoneGap BuildCloud Service {#configure-your-adobe-phonegap-build-cloud-service}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

的 **PhoneGap Build磁貼** 在應用程式控制板上，您可以通過Adobe PhoneGap Build服務構建和分發您的PhoneGap移動應用程式。

在 **管理應用** 磁貼在推動遠程構建時將使用PhoneGap Build構建 **PhoneGap Build** 磁貼。

您可以將遠程生成推送到 [https://build.phonegap.com](https://build.phonegap.com) 或下載源以本地生成 [PhoneGap CLI](https://docs.phonegap.com/references/phonegap-cli/)。

![PhoneGap Build磁貼](assets/chlimage_1-60.png)

## 配置Cloud Service {#configuring-the-cloud-service}

為了利用PhoneGap Build，您需要使用您的帳AEM戶資訊配置PhoneGap BuildCloud Service。

如果您當前沒有帳戶，請導航到 [https://build.phonegap.com](https://build.phonegap.com) 註冊！ 如果您擁有Adobe Creative Cloud會員資格，則最多可支援25個私人應用（非開源應用）。

驗證您的PhoneGap Build帳戶是否處於活動狀態後，請導航AEM至雲管理控制台，尤其是 [PhoneGap BuildCloud Service](http://localhost:4502/etc/cloudservices/phonegap-build.html) (http://localhost:4502/etc/cloudservices/phonegap-build.html)。

使用 **管理Cloud Services** 磁貼以配置新的雲服務配置。

### 使用管理Cloud Services磁貼 {#using-manage-cloud-services-tile}

開始使用 **PhoneGap Build** 磁貼，您必須配置雲服務， **管理Cloud Services** AEM Mobile儀錶盤上的磁貼。

要為應用配置雲服務，請執行以下步驟：

1. 按一下 **管理Cloud Services** 平鋪。

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. 選擇 **PhoneGap Build** 的 **添加或編輯Cloud Service** 的上界。

   按一下&#x200B;**下一步**。

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. 輸入憑據以建立新的雲配置。

   驗證後，按一下 **提交**。 此配置的雲配置現在顯示在 **管理Cloud Services** 平鋪。

   ![chlimage_1-63](assets/chlimage_1-63.png)

### 使用PhoneGap Build構建應用程式 {#building-your-application-with-phonegap-build}

配置雲服務後，您可以使用 **PhoneGap Build** 平鋪。 按一下右上角，從 **生成遠程** 或 **下載源** 頁籤

![chlimage_1-64](assets/chlimage_1-64.png)

要使用Adobe PhoneGap Build調用遠程生成，請按一下 **生成遠程**。

>[!NOTE]
>
>如果生成因任何原因而失敗(下面的紅色iOS表徵圖表示平台失敗)，您可以將滑鼠懸停在表徵圖上以獲取錯誤消息。 或者，可按一下三點，「……」 在磁貼底部直接導航到https://build.phonegap.com（您必須進行身份驗證），並直接查看和管理生成。

### 使用PhoneGap CLI構建應用程式 {#building-your-application-with-phonegap-cli}

PhoneGap提供命令行介面以在本地構建應用程式。

使用PhoneGap命令行介面(CLI)在電腦上編譯PhoneGap應用程式。 要將內AEM容包括到應AEM用程式中，請建立包含移動應用程式內容、內容同步配置和其他必需資產的ZIP檔案。 下載ZIP檔案並將其包含在您的生成中。

為了利用PhoneGap的命令行介面，您需要設定本地環境以包括：

1. 平台SDK(iOS、Android、WindowsPhone...)和，
1. PhoneGap CLI

你可以閱讀更多 [這裡](https://docs.phonegap.com/references/phonegap-cli/)。

安裝完必備項後，通過建立一個簡單應用並通過終端嘗試使其在模擬器中運行或在設備上運行更好，為它提供簡單test:

```xml
phonegap create myApp
cd myApp
phonegap run ios (or android, ...)
```

>[!NOTE]
>
>add — 如果不想在連接的設備上運行，則在此行末尾進行模擬。

驗證上述功能後，使用 **PhoneGap Build** 平鋪到 **下載源**。 將檔案保存並解壓縮到本地系統。 一旦完成：

* 導航到該保存的檔案（資料夾）
* 運行「phonegap run ios」（或android等）

### 其他資源 {#additional-resources}

要瞭解作者和開發人員的角色和職責，請參閱以下資源：

* [Adobe PhoneGap企業AEM發展](/help/mobile/developing-in-phonegap.md)
* [為Adobe PhoneGap企業創AEM作](/help/mobile/phonegap.md)
