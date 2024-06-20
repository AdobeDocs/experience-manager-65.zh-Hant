---
title: 為iOS建置安全的AEM Forms應用程式
description: 瞭解如何透過封存Xcode專案，為iOS建置安全的AEM Forms應用程式。 這會建立安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 12cc2027-ae94-40c3-a7d1-553469426114
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---

# 為iOS建置安全的AEM Forms應用程式 {#building-a-secure-aem-forms-app-for-ios}

您必須封存AEM Forms應用程式的Xcode專案，才能建置安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含託管內部應用程式的設定資訊，例如應用程式的名稱和託管位置。 如需屬性清單檔案的詳細資訊，請參閱 [關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 登入下列網站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 建立應用程式ID。 如需建立應用程式ID的詳細步驟，請參閱 [建立和設定應用程式ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html).
1. 若要為應用程式設定iOS應用程式的套件組合識別碼，請按一下 **[!UICONTROL 設定應用程式ID]**.
1. 在網頁底部，選取 **[!UICONTROL 啟用資料保護]**. 指定資料保護選項。

   按一下&#x200B;**[!UICONTROL 「完成」]**。

1. 導覽至「布建>發佈」 ，並使用步驟3中設定的應用程式ID建立新的設定檔。
1. 下載布建設定檔並新增至Xcode和iPad。
1. 登入已安裝Xcode及已設定iOS SDK的Mac電腦。
1. 開啟 `AEM Forms.xcodeproj` Xcode中的專案。
1. 按一下 **[!UICONTROL AEM Forms]**，下 **[!UICONTROL 目標]**，選取 **[!UICONTROL AEM Forms]**. 選取 **[!UICONTROL 建置設定]** 索引標籤中，找到 **[!UICONTROL 程式碼簽署權利]** 區段，然後在權益下拉式清單中，選取 **[!UICONTROL LC Enterprise]** 選項。
1. 找到並開啟 `LC Enterprise.entitlements` 檔案進行編輯。 在 **Xcode權益**，新增與布建設定檔中存在的相同機碼值組。
1. 在 **[!UICONTROL 建置設定]** 標籤，按一下 **[!UICONTROL 全部]** 然後按一下 **[!UICONTROL 已合併]**.
1. 從 **[!UICONTROL 設定]** 清單，展開 **[!UICONTROL 程式碼簽署]**.
1. 的 **[!UICONTROL 程式碼簽署身分]**，選取適當的簽章。 確保為以下專案選取相同的簽章： **[!UICONTROL 偵錯]**， **[!UICONTROL 版本]**、和 **[!UICONTROL 任何iOS SDK]**.
1. 在 **[!UICONTROL 專案]**，選取 **[!UICONTROL AEM Forms]** 並確保已選取適當的簽章 **[!UICONTROL 程式碼簽署身分]**， **[!UICONTROL 偵錯]**， **[!UICONTROL 版本]** 和 **[!UICONTROL 任何iOS SDK]**.
1. 建置並發佈AEM Forms應用程式。 如需建置和分發AEM Forms應用程式的詳細指示，請參閱 [建立AEM Forms應用程式的安裝程式](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app).
