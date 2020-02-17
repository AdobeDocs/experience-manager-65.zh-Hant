---
title: 建立iOS適用的安全AEM Forms應用程式
seo-title: 建立iOS適用的安全AEM Forms應用程式
description: 建立安全AEM Forms應用程式的步驟。
seo-description: 建立安全AEM Forms應用程式的步驟。
uuid: 6c4b160f-4d0c-4976-9609-9196795b6c8e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 90cd8ba5-4f47-4074-bc54-6a7bb8afe256
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# 建立iOS適用的安全AEM Forms應用程式 {#building-a-secure-aem-forms-app-for-ios}

您必須封存AEM Forms應用程式的Xcode專案，才能建立安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含代管內部應用程式的設定資訊，例如應用程式的名稱和代管位置。 有關屬性清單檔案的詳細資訊，請參 [閱關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登入下列網站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 建立應用程式ID。 如需建立應用程式ID的詳細步驟，請參 [閱建立和設定應用程式ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 若要為您的應用程式設定iOS應用程式的套件識別碼，請按一下「 **[!UICONTROL 設定應用程式ID]**」。
1. 在網頁底部，選擇「啟 **[!UICONTROL 用資料保護」]**。 指定資料保護選項。

   按一 **[!UICONTROL 下完成]**。

1. 導覽至「布建」->「散發」，並使用步驟3中設定的應用程式ID建立新的設定檔。
1. 下載布建設定檔並新增至Xcode和iPad。
1. 登入已安裝並設定Xcode和iOS SDK的Mac電腦。
1. 在Xcode中 `AEM Forms.xcodeproj` 開啟專案。
1. 按一 **[!UICONTROL 下「AEM Forms]**」，在「 **[!UICONTROL TARGETS]**」下方選 **[!UICONTROL 取「AEM Forms]**」。 選擇「 **[!UICONTROL Build Settings]** (構建設定 **[!UICONTROL )」頁籤，找到「Code Signing Entitlement（代碼簽名權益）」部分，然後在「Entitlements（權益）」下拉菜單中，選擇]** LC Enterprise **** （LC企業版）選項。
1. 在Xcode中尋找並 `LC Enterprise.entitlements` 開啟檔案以進行編輯。 在 **XCode權益下**，新增與布建設定檔中相同的金鑰值配對。
1. 在「建 **[!UICONTROL 置設定]** 」索引標籤中，按一 **[!UICONTROL 下「全部]** 」，然後按一 **[!UICONTROL 下「組合]**」。
1. 從「設定 **[!UICONTROL 」清單]** ，展開「 **[!UICONTROL 程式碼簽署」]**。
1. 針對 **[!UICONTROL 程式碼簽署識別]**，請選取適當的簽名。 請確定已針對 **[!UICONTROL Debug]**、 **[!UICONTROL Release]**&#x200B;和 **[!UICONTROL Any iOS SDK選取相同的簽名]**。
1. 在 **[!UICONTROL PROJECT下]**，選擇 **[!UICONTROL AEM Forms]** ，並確保為 **[!UICONTROL Signing Identity]**, DebugDebugIntity,ReleaseAndAny iOS SDK ************&#x200B;選擇適當的簽名。
1. 建立和散發AEM Forms應用程式。 如需建立和散發AEM Forms應用程式的詳細指示，請參 [閱「建立AEM Forms應用程式的安裝程式」](/help/forms/using/setup-xcode-project-build-installer.md#main-pars-text-12)。

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
