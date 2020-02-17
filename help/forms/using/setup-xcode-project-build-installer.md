---
title: 設定Xcode專案並建立iOS應用程式
seo-title: 設定Xcode專案並建立iOS應用程式
description: 說明如何建立iOS適用的標準AEM Forms應用程式。
seo-description: 說明如何建立iOS適用的標準AEM Forms應用程式。
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
translation-type: tm+mt
source-git-commit: 4a0f3f64095b4726f295a0c1857a1e999353f5f5

---


# 設定Xcode專案並建立iOS應用程式{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始碼存檔是包 `adobe-lc-mobileworkspace-src-<version>.zip` 共用上包的 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 導覽至套件shareURL: `https://<server>:<port>/crx/packageshare`。

1. 下載來源套件。 當您下載套件時，它會新增至您的AEM Forms套件管理員。
1. 下載後，導覽至：和 `https://<server>:<port>/crx/packmgr/index.jsp`安裝 `adobe-aemfd-forms-app-src-pkg-<version>.zip`。

1. 若要下載原始碼封存，請在您的瀏 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 覽器中開啟。
來源套件會下載在您的裝置上。

下圖顯示提取的內容 `adobe-lc-mobileworkspace-src-<version>.zip`。

![mws-content](assets/mws-content.png)

下表詳細說明了資料夾的 `adobe-lc-mobileworkspace-src-[version]/ios` 內容。

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
   <td><p>資源、PhoneGap增效模組及應用程式的主要模組</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>AEM Forms應用程式的Xcode專案</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>AEM Forms應用程式專案的HTML、CSS、影像和JavaScript檔案</p> </td>
  </tr>
 </tbody>
</table>

如需有關「程式碼簽署」和將裝置新增至iOS布建入口網站的詳細資訊，請參閱 [iOS程式碼簽署設定、程式和疑難排解](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 建立標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行下列步驟，以在Xcode中設定專案並提供簽署識別碼：

   登入已安裝並設定Xcode和iOS SDK的Mac電腦。

1. 將檔案 `adobe-lc-mobileworkspace-src-<version>.zip` 檔案從下載檔案夾複製到 `[User_Home]/Projects/`。
1. 解壓目錄中的存 `[User_Home]/Projects/[your-project]`檔。
1. 導覽至您 ` [User_Home]/Projects/ `[的專案目錄]`/adobe-lc-mobileworkspace-src-[version]/ios` 。
1. 在Xcode中 `AEM Forms.xcodeproj` 開啟專案。
1. 按一 **下「AEM Forms**」，在「 **TARGETS**」下方選 **取「AEM Forms**」。 選取「**建立設定**」標籤，找出「 **Code Signing Entitlement** 」區段，並在「Debug and Release」欄位中執行下列其中一項作業：

   * 將欄位保留為未指定，以建立標準的行動工作區應用程式
   * 指定欄位，如「建立iOS的 [](/help/forms/using/building-secure-mobile-workspace-app.md) Secure AEM Forms應用程式以建立安全的AEM Forms應用程式」中所述。

1. 在「建 **置設定** 」索引標籤中，按一 **下「全部** 」，然後按一 **下「組合**」。
1. 從「設定 **」清單** ，展開「 **程式碼簽署」**。
1. 針對 **程式碼簽署識別**，請選取適當的簽名。 如需建立新簽名的詳細資訊，請參閱建立 [和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 請確定已針對 **Debug**、 **Release**&#x200B;和 **Any iOS SDK選取相同的簽名**。
1. 在檔案中取代下列程 `AEM Forms-info.plist` 式碼：

   ```java
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   使用下列程式碼，並 `yourserver.com` 以伺服器的適當主機名稱取代。

   ```java
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
   >只有當AEM Forms應用程式需要連線至未遵循App Transport security要求的伺服器時，才需要此步驟。

1. 在 **PROJECT下**，選擇 **AEM Forms** ，並確保為 **Signing Identity**, DebugDebugIntity,ReleaseAndAny iOS SDK ************&#x200B;選擇適當的簽名。
1. 將布建的iPad連接至Mac電腦。
1. 選取 **AEM Forms專案的布建裝置** 。

   ![ipad](assets/ipad.png)

   已選取已布建的iPad Air 2裝置。

1. 選擇「 **產品** 」>「清 **除」**。
1. 選擇「 **產品** 」>「 **構建」**。

## 建立AEM Forms應用程式的安裝程式 {#build-the-installer-for-the-mobile-workspace-app}

您需要封存Xcode專案，才能建立安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含代管內部應用程式的設定資訊，例如應用程式的名稱和代管位置。 有關屬性清單檔案的詳細資訊，請參 [閱關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 將布建的iPad連接至Mac電腦。 如需iPad布建的詳細資訊，請參閱建立和下 [載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 選取 **AEM Forms專案的布建裝置** 。

   ![ipad-1](assets/ipad-1.png)

   已選取已布建的iPad Air 2裝置。

1. 選擇「 **產品** 」>「清 **除」**。
1. 選擇「 **產品** 」>「 **構建」**。
1. 選擇「 **產品** >存 **檔」**。
1. 在「組織工具——封存」中，選取專案的最新封存，然後按一下「分 **發」**。
1. 選 **擇「儲存為企業用」或「臨機部署** 」做為散發方法，然後按一下「下 **一步」**。
1. 選取適當的 **程式碼簽署識別** ，然後按 **下下一步**。 按一 **下** 「允許」以套用簽名。
1. 提供應用程式名稱，並選取「儲 **存為企業散發」**。
1. 提供應 **用程式的** 「應用程式URL」。 例如，若要在CRX伺服器上主控應用程式，請提供URL `https://[LC_host]:[port]/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在「標 **題** 」欄位中，指定AEM Forms。
1. 按一 **下「儲存** 」並關閉Xcode。

   安裝程式檔 `AEM Forms.ipa`案和屬性清單檔案 `AEM Forms-info.plist`會在指定的位置建立。

1. 在編輯器 `AEM Forms-info.plist` 中開啟檔案。
1. 將。ipa檔案URL中的所有空格取代為%20。
1. 儲存並關閉 `AEM Forms-info.plist` 檔案。