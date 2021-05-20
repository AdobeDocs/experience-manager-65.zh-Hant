---
title: 設定Xcode專案並建置iOS應用程式
seo-title: 設定Xcode專案並建置iOS應用程式
description: 說明如何建立iOS適用的標準AEM Forms應用程式。
seo-description: 說明如何建立iOS適用的標準AEM Forms應用程式。
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 5%

---

# 設定Xcode專案並建置iOS應用程式{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始碼存檔`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`包的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;部分：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取套件的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包，然後按一下&#x200B;**[!UICONTROL Install]**。

1. 若要下載原始碼存檔，請在瀏覽器中開啟`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。
源包已下載到您的設備上。

下圖顯示提取的`adobe-lc-mobileworkspace-src-<version>.zip`內容。

![mws-content](assets/mws-content.png)

下表詳細說明`adobe-lc-mobileworkspace-src-[version]/ios`資料夾的內容。

<table>
 <tbody>
  <tr>
   <th><p>目錄</p> </th>
   <th><p>內容</p> </th>
  </tr>
  <tr>
   <td><p><code>CordovaLib</code></p> </td>
   <td><p>PhoneGap SDK 6.4.0</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms</code></p> </td>
   <td><p>資源、PhoneGap外掛程式和應用程式的主要模組</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>適用於AEM Forms應用程式的Xcode專案</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms應用程式專案的HTML、CSS、影像和JavaScript檔案</p> </td>
  </tr>
 </tbody>
</table>

有關代碼簽名和將設備添加到iOS設定門戶的詳細資訊，請參閱[iOS代碼簽名設定、處理和疑難解答](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 建立標準AEM Forms應用程式{#set-up-the-xcode-project}

1. 執行下列步驟以在Xcode中設定專案，並提供簽署身分識別：

   登入已安裝及設定Xcode和iOS SDK的Mac電腦。

1. 將下載資料夾中的`adobe-lc-mobileworkspace-src-<version>.zip`封存複製到`[User_Home]/Projects/`。
1. 解壓縮`[User_Home]/Projects/[your-project]`目錄中的封存。
1. 導覽至` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios`目錄。
1. 在Xcode中開啟`AEM Forms.xcodeproj`專案。
1. 按一下&#x200B;**AEM Forms**，在&#x200B;**TARGETS**&#x200B;下，選擇&#x200B;**AEM Forms**。 選取「**建置設定**」標籤，找出「**代碼簽名權利檔案**」區段，並在「除錯」和「發行」欄位中執行下列任一操作：

   * 將欄位保留未指定，以建置標準行動工作區應用程式
   * 將欄位指定為，如[建立iOS適用的安全AEM Forms應用程式](/help/forms/using/building-secure-mobile-workspace-app.md)中所述，以建立安全的AEM Forms應用程式。

1. 在&#x200B;**Build Settings**&#x200B;標籤中，按一下&#x200B;**All**，然後按一下&#x200B;**Combined**。
1. 從&#x200B;**Settings**&#x200B;清單中，展開&#x200B;**Code Signing**。
1. 對於&#x200B;**代碼簽名標識**，選擇相應的簽名。 有關建立新簽名的詳細資訊，請參閱[建立和下載開發設定配置檔案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 確保為&#x200B;**Debug**、**Release**&#x200B;和&#x200B;**Any iOS SDK**&#x200B;選取了相同的簽名。
1. 在`AEM Forms-info.plist`檔案中取代下列程式碼：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   將`yourserver.com`替換為伺服器的適當主機名時，使用以下內容。

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSExceptionDomains</key>
   <dict>
   <key>yourserver.com</key>
   <dict>
   <!-Include to allow subdomains->
   <key>NSIncludesSubdomains</key>
   <true/>
   <!-Include to allow HTTP requests->
   <key>NSTemporaryExceptionAllowsInsecureHTTPLoads</key>
   <true/>
   <!-Include to support forward secrecy->
   <key>NSExceptionRequiresForwardSecrecy</key>
   <false/>
   <!-Include to specify minimum TLS version->
   <key>NSTemporaryExceptionMinimumTLSVersion</key>
   <string>TLSv1.1</string>
   </dict>
   </dict>
   </dict>
   ```

   >[!NOTE]
   >
   >只有在AEM Forms應用程式需要連線至未遵循App Transport Security要求的伺服器時，才需要執行此步驟。

1. 在&#x200B;**PROJECT**&#x200B;下，選擇&#x200B;**AEM Forms**&#x200B;並確保為&#x200B;**代碼簽名標識**、**Debug**、**Release**&#x200B;和&#x200B;**任何iOS SDK**&#x200B;選擇適當的簽名。
1. 將布建的iPad連接到Mac電腦。
1. 為&#x200B;**AEM Forms**&#x200B;專案選取已布建的裝置。

   ![ipad](assets/ipad.png)

   已選取布建裝置iPad Air 2。

1. 選擇&#x200B;**Product** > **Clean**。
1. 選擇&#x200B;**Product** > **Build**。

## 建立AEM Forms應用程式的安裝程式{#build-the-installer-for-the-mobile-workspace-app}

您需要封存Xcode專案以建置安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含托管於內部應用程式的設定資訊，例如應用程式的名稱和托管位置。 有關屬性清單檔案的詳細資訊，請參閱[關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 將布建的iPad連接到Mac電腦。 如需布建iPad的詳細資訊，請參閱[建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 為&#x200B;**AEM Forms**&#x200B;專案選取已布建的裝置。

   ![ipad-1](assets/ipad-1.png)

   已選取布建裝置iPad Air 2。

1. 選擇&#x200B;**Product** > **Clean**。
1. 選擇&#x200B;**Product** > **Build**。
1. 選擇&#x200B;**Product** > **Archive**。
1. 在「組織器 — 存檔」中，選擇項目的最新存檔，然後按一下&#x200B;**分發**。
1. 選擇&#x200B;**「為企業保存」或「臨機部署」**&#x200B;作為分發方法，然後按一下&#x200B;**「下一步」**。
1. 選擇適當的&#x200B;**代碼簽名標識**，然後按一下&#x200B;**下一步**。 按一下&#x200B;**允許**&#x200B;以應用簽名。
1. 提供應用程式的名稱，然後選取&#x200B;**儲存以供Enterprise Distribution**。
1. 提供應用程式的&#x200B;**應用程式URL**。 例如，若要在CRX伺服器上托管應用程式，請提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在&#x200B;**Title**&#x200B;欄位中，指定AEM Forms。
1. 按一下「**儲存**」並關閉Xcode。

   在指定位置建立安裝程式檔案`AEM Forms.ipa`和屬性清單檔案`AEM Forms-info.plist`。

1. 在編輯器中開啟`AEM Forms-info.plist`檔案。
1. 將.ipa檔案URL中的所有空格取代為%20。
1. 保存並關閉`AEM Forms-info.plist`檔案。
