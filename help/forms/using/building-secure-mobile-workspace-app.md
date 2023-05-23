---
title: 為iOS打造安全的AEM Forms應用
seo-title: Building a secure AEM Forms app for iOS
description: 構建安全的AEM Forms應用的步驟。
seo-description: Steps to build a secure AEM Forms app.
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 為iOS打造安全的AEM Forms應用 {#building-a-secure-aem-forms-app-for-ios}

您需要將AEM Forms應用的Xcode項目存檔，以生成安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含托管的內部應用程式的配置資訊，如應用程式的名稱和托管位置。 有關屬性清單檔案的詳細資訊，請參見 [關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登錄到以下網站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 建立應用ID。 有關建立應用程式ID的詳細步驟，請參見 [建立和配置應用ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 要為您的應用配置iOS應用程式的捆綁標識符，請按一下 **[!UICONTROL 配置應用ID]**。
1. 在網頁底部，選擇 **[!UICONTROL 啟用資料保護]**。 指定資料保護選項。

   按一下 **[!UICONTROL 完成]**。

1. 導航到「預配」 — >「分發」，然後使用步驟3中配置的應用程式ID建立新配置檔案。
1. 下載並將預配配置檔案添加到Xcode和iPad。
1. 登錄到安裝並配置了Xcode和MacSDK的iOS電腦。
1. 開啟 `AEM Forms.xcodeproj` Xcode中的項目。
1. 按一下 **[!UICONTROL AEM Forms]**&#x200B;下 **[!UICONTROL 目標]**&#x200B;選中 **[!UICONTROL AEM Forms]**。 選擇 **[!UICONTROL 生成設定]** 頁籤 **[!UICONTROL 代碼簽名權利]** 部分，在「權利」下拉清單中，選擇 **[!UICONTROL LC企業]** 的雙曲餘切值。
1. 查找並開啟 `LC Enterprise.entitlements` 的子菜單。 在 **XCode權利**，添加與預配配置檔案中相同的鍵值對。
1. 在 **[!UICONTROL 生成設定]** 按鈕 **[!UICONTROL 全部]** 然後按一下 **[!UICONTROL 組合]**。
1. 從 **[!UICONTROL 設定]** 清單，展開 **[!UICONTROL 代碼簽名]**。
1. 對於 **[!UICONTROL 代碼簽名標識]**，選擇相應的簽名。 確保為 **[!UICONTROL 調試]**。 **[!UICONTROL 發佈]**, **[!UICONTROL 任何iOSSDK]**。
1. 下 **[!UICONTROL 項目]**&#x200B;選中 **[!UICONTROL AEM Forms]** 確保為 **[!UICONTROL 代碼簽名標識]**。 **[!UICONTROL 調試]**。 **[!UICONTROL 發佈]** 和 **[!UICONTROL 任何iOSSDK]**。
1. 構建和分發AEM Forms應用。 有關構建和分發AEM Forms應用的詳細說明，請參見 [為AEM Forms應用生成安裝程式](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)。
