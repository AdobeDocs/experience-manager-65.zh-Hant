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
source-git-commit: 49da3dbe590f70b98185a6bc330db6077dc864c0
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 0%

---


# 建立iOS適用的安全AEM Forms應用程式{#building-a-secure-aem-forms-app-for-ios}

您必須封存AEM Forms應用程式的Xcode專案，才能建立安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含代管內部應用程式的設定資訊，例如應用程式的名稱和代管位置。 有關屬性清單檔案的詳細資訊，請參閱[關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 登入下列網站：

   [https://developer.apple.com/account/ios/identifier/bundle](https://developer.apple.com/account/ios/identifier/bundle)

1. 建立應用程式ID。 如需建立應用程式ID的詳細步驟，請參閱[建立和設定應用程式ID](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html)。
1. 若要為您的應用程式設定iOS應用程式的套件識別碼，請按一下「設定應用程式ID」**[!UICONTROL 。]**
1. 在網頁底部，選擇&#x200B;**[!UICONTROL 啟用資料保護]**。 指定資料保護選項。

   按一下&#x200B;**[!UICONTROL Done]**。

1. 導覽至「布建」->「散發」，並使用步驟3中設定的應用程式ID建立新的設定檔。
1. 下載布建設定檔並新增至Xcode和iPad。
1. 登入已安裝並設定Xcode和iOS SDK的Mac電腦。
1. 在Xcode中開啟`AEM Forms.xcodeproj`專案。
1. 按一下&#x200B;**[!UICONTROL AEM Forms]**，在&#x200B;**[!UICONTROL TARGETS]**&#x200B;下方，選取&#x200B;**[!UICONTROL AEM Forms]**。 選擇&#x200B;**[!UICONTROL 建置設定]**&#x200B;頁籤，找到&#x200B;**[!UICONTROL 代碼簽名權益]**&#x200B;部分，並在「權利」下拉菜單中，選擇&#x200B;**[!UICONTROL LC Enterprise]**&#x200B;選項。
1. 在Xcode中找到並開啟`LC Enterprise.entitlements`檔案以進行編輯。 在&#x200B;**XCode權利**&#x200B;下，添加與設定配置檔案中存在的相同密鑰值對。
1. 在&#x200B;**[!UICONTROL 建置設定]**&#x200B;頁籤中，按一下&#x200B;**[!UICONTROL 全部]** ，然後按一下&#x200B;**[!UICONTROL 組合]**。
1. 從&#x200B;**[!UICONTROL Settings]**&#x200B;清單中，展開&#x200B;**[!UICONTROL Code Signing]**。
1. 對於&#x200B;**[!UICONTROL 代碼簽名身份]**，請選擇適當的簽名。 請確定已針對&#x200B;**[!UICONTROL Debug]**、**[!UICONTROL Release]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS SDK]**&#x200B;選取相同的簽名。
1. 在&#x200B;**[!UICONTROL PROJECT]**&#x200B;下，選擇&#x200B;**[!UICONTROL AEM Forms]**&#x200B;並確保為&#x200B;**[!UICONTROL 代碼簽名身份]**、**[!UICONTROL Debug]**、**[!UICONTROL Release]**&#x200B;和&#x200B;**[!UICONTROL 任何iOS選擇適當的簽名SDK]**。
1. 建立和散發AEM Forms應用程式。 如需建立和散發AEM Forms應用程式的詳細指示，請參閱「建立AEM Forms應用程式的安裝程式」[。](setup-xcode-project-build-installer.md#build-the-installer-for-the-mobile-workspace-app)
