---
title: 為iOS建立安全的AEM Forms應用程式
seo-title: Building a secure AEM Forms app for iOS
description: 建立安全AEM Forms應用程式的步驟。
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

# 為iOS建立安全的AEM Forms應用程式 {#building-a-secure-aem-forms-app-for-ios}

您必須封存AEM Forms應用程式的Xcode專案，才能建立安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含托管於內部應用程式的設定資訊，例如應用程式的名稱和托管位置。 如需屬性清單檔案的詳細資訊，請參閱 [關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 登入下列網站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 建立應用程式ID。 如需建立應用程式ID的詳細步驟，請參閱 [建立和設定應用程式ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. 若要設定您應用程式的iOS應用程式套件識別碼，請按一下 **[!UICONTROL 設定應用程式ID]**.
1. 在網頁底部，選取 **[!UICONTROL 啟用資料保護]**. 指定資料保護選項。

   按一下 **[!UICONTROL 完成]**.

1. 導覽至布建 — >分發，並使用步驟3中設定的應用程式ID建立新的設定檔。
1. 下載布建設定檔，並將其新增至Xcode和iPad。
1. 登入已安裝及設定Xcode和iOS SDK的Mac電腦。
1. 開啟 `AEM Forms.xcodeproj` 專案。
1. 按一下 **[!UICONTROL AEM Forms]**，在 **[!UICONTROL 目標]**，選取 **[!UICONTROL AEM Forms]**. 選取 **[!UICONTROL 建置設定]** 頁簽，找到 **[!UICONTROL 代碼簽名權限]** 在「權益」下拉式清單中，選取 **[!UICONTROL LC Enterprise]** 選項。
1. 找出並開啟 `LC Enterprise.entitlements` 檔案進行編輯。 在 **Xcode使用權限**，新增與布建設定檔中相同的機碼值組。
1. 在 **[!UICONTROL 建置設定]** 按一下 **[!UICONTROL 全部]** 然後按一下 **[!UICONTROL 結合]**.
1. 從 **[!UICONTROL 設定]** 清單，展開 **[!UICONTROL 程式碼簽署]**.
1. 針對 **[!UICONTROL 代碼簽名標識]**，請選取適當的簽名。 確保為 **[!UICONTROL 除錯]**, **[!UICONTROL 發行]**，和 **[!UICONTROL 任何iOS SDK]**.
1. 在 **[!UICONTROL 專案]**，選取 **[!UICONTROL AEM Forms]** 並確保為 **[!UICONTROL 代碼簽名標識]**, **[!UICONTROL 除錯]**, **[!UICONTROL 發行]** 和 **[!UICONTROL 任何iOS SDK]**.
1. 建置和發佈AEM Forms應用程式。 如需建立和發佈AEM Forms應用程式的詳細指示，請參閱 [建置AEM Forms應用程式的安裝程式](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
