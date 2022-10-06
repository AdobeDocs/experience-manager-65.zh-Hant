---
title: 設定Xcode專案並建置iOS應用程式
seo-title: Set up the Xcode project and build the iOS app
description: 說明如何為iOS建置標準AEM Forms應用程式。
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 6%

---

# 設定Xcode專案並建置iOS應用程式{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始碼檔案， `adobe-lc-mobileworkspace-src-<version>.zip` 是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 封裝。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 小節：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 下拉式清單。
   2. 選取套件的版本和類型。 您也可以使用 **[!UICONTROL 搜尋下載]** 選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，然後選取 **[!UICONTROL 接受EULA條款]**，然後點選 **[!UICONTROL 下載]**.
1. 開啟[套件管理器](https://docs.adobe.com/content/help/zh-Hant/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選取套件，然後按一下 **[!UICONTROL 安裝]**.

1. 要下載原始碼存檔，請開啟 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 在瀏覽器中。
源包已下載到您的設備上。

下列影像會顯示擷取的 `adobe-lc-mobileworkspace-src-<version>.zip`.

![mws-content](assets/mws-content.png)

下表詳細說明 `adobe-lc-mobileworkspace-src-[version]/ios` 檔案夾。

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

如需程式碼簽署和將裝置新增至iOS布建入口網站的詳細資訊，請參閱 [iOS程式碼簽署設定、程式和疑難排解](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html).

## 建立標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行下列步驟以在Xcode中設定專案，並提供簽署身分識別：

   登入已安裝及設定Xcode和iOS SDK的Mac電腦。

1. 複製 `adobe-lc-mobileworkspace-src-<version>.zip` 從下載資料夾封存至 `[User_Home]/Projects/`.
1. 解壓縮 `[User_Home]/Projects/[your-project]`目錄。
1. 導覽至 ` [User_Home]/Projects/ `[您的專案]`/adobe-lc-mobileworkspace-src-[version]/ios` 目錄。
1. 開啟 `AEM Forms.xcodeproj` 專案。
1. 按一下 **AEM Forms**，在 **目標**，選取 **AEM Forms**. 選取 **建置設定** 頁簽，找到 **代碼簽名權限** 區段中執行下列任一操作：

   * 將欄位保留未指定，以建置標準行動工作區應用程式
   * 指定要執行的欄位，如 [為iOS建立安全的AEM Forms應用程式](/help/forms/using/building-secure-mobile-workspace-app.md) 來建立安全的AEM Forms應用程式。

1. 在 **建置設定** 按一下 **全部** 然後按一下 **結合**.
1. 從 **設定** 清單，展開 **程式碼簽署**.
1. 針對 **代碼簽名標識**，請選取適當的簽名。 有關建立新簽名的詳細資訊，請參見 [建立和下載開發佈建配置檔案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html).
1. 確保為 **除錯**, **發行**，和 **任何iOS SDK**.
1. 在 `AEM Forms-info.plist` 檔案：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   替換 `yourserver.com` 具有適當的伺服器主機名。

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

1. 在 **專案**，選取 **AEM Forms** 並確保為 **代碼簽名標識**, **除錯**, **發行** 和 **任何iOS SDK**.
1. 將布建的iPad連結至Mac電腦。
1. 為 **AEM Forms** 專案。

   ![ipad](assets/ipad.png)

   已選取布建的裝置iPad Air 2。

1. 選擇 **產品** > **清除**.
1. 選擇 **產品** > **建置**.

## 建置AEM Forms應用程式的安裝程式 {#build-the-installer-for-the-mobile-workspace-app}

您需要封存Xcode專案以建置安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含托管於內部應用程式的設定資訊，例如應用程式的名稱和托管位置。 如需屬性清單檔案的詳細資訊，請參閱 [關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html).

1. 將布建的iPad連結至Mac電腦。 如需布建iPad的詳細資訊，請參閱 [建立和下載開發佈建配置檔案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 為 **AEM Forms** 專案。

   ![ipad-1](assets/ipad-1.png)

   已選取布建的裝置iPad Air 2。

1. 選擇 **產品** > **清除**.
1. 選擇 **產品** > **建置**.
1. 選擇 **產品** > **封存**.
1. 在「組織者 — 存檔」中，選擇項目的最新存檔，然後按一下 **分發**.
1. 選擇 **儲存以供企業或臨機部署** 作為分發和按一下的方法 **下一個**.
1. 選取適當的 **代碼簽名標識** 按一下 **下一個**. 按一下 **允許** 來應用簽名。
1. 提供應用程式名稱並選取 **儲存以供Enterprise Distribution使用**.
1. 提供 **應用程式URL** 的URL。 例如，若要在CRX伺服器上托管應用程式，請提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`.
1. 在 **標題** 欄位，指定AEM Forms。
1. 按一下 **儲存** 並關閉Xcode。

   安裝程式檔案， `AEM Forms.ipa`，和屬性清單檔案 `AEM Forms-info.plist`，會在指定位置建立。

1. 開啟 `AEM Forms-info.plist` 檔案。
1. 將.ipa檔案URL中的所有空格取代為%20。
1. 儲存並關閉 `AEM Forms-info.plist` 檔案。
