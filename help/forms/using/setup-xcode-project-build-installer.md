---
title: 設定Xcode項目並生成iOS應用
seo-title: Set up the Xcode project and build the iOS app
description: 解釋如何為iOS構建標準AEM Forms應用。
seo-description: Explains how to build standard AEM Forms app for iOS.
uuid: 29779bbb-06b4-4ece-9f29-786afab59eaf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 88555db2-712f-4ef9-bf47-76c7ba83d964
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 4%

---

# 設定Xcode項目並生成iOS應用{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms應用的完整原始碼。 源包含構建自定義AEM Forms應用的所有元件。 原始碼存檔， `adobe-lc-mobileworkspace-src-<version>.zip` 是 `adobe-aemfd-forms-app-src-pkg-<version>.zip` 軟體分發上的軟體包。

要獲取AEM Forms應用程式源，請執行以下步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 點一下頁首功能表中的 **[!UICONTROL Adobe Experience Manager]**。
1. 在 **[!UICONTROL 篩選器]** 部分：
   1. 選擇 **[!UICONTROL Forms]** 從 **[!UICONTROL 解決方案]** 的子菜單。
   2. 選擇包的版本和類型。 您還可以使用 **[!UICONTROL 搜索下載]** 選項。
1. 點擊適用於您的作業系統的包名稱，選擇 **[!UICONTROL 接受EULA條款]**，然後點擊 **[!UICONTROL 下載]**。
1. 開啟[套件管理器](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 「上傳套件」]**&#x200B;即可上傳套件。
1. 選擇包並按一下 **[!UICONTROL 安裝]**。

1. 要下載原始碼存檔，請開啟 `https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip` 的子菜單。
源包已下載到您的設備上。

下圖顯示 `adobe-lc-mobileworkspace-src-<version>.zip`。

![mws內容](assets/mws-content.png)

下表詳細說明了 `adobe-lc-mobileworkspace-src-[version]/ios` 的子菜單。

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
   <td><p>資源、PhoneGap插件和應用程式的主模組</p> </td>
  </tr>
  <tr>
   <td><p><code>AEM Forms.xcodeproj</code></p> </td>
   <td><p>用於AEM Forms應用的Xcode項目</p> </td>
  </tr>
  <tr>
   <td><p><code>www</code></p> </td>
   <td><p>HTML、CSS、影像和AEM Forms應用程式項目的JavaScript檔案</p> </td>
  </tr>
 </tbody>
</table>

有關代碼簽名和將設備添加到iOS預配門戶的詳細資訊，請參見 [iOS代碼簽名設定、處理和故障排除](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 構建標準AEM Forms應用 {#set-up-the-xcode-project}

1. 執行以下步驟以在Xcode中設定項目並提供簽名標識：

   登錄到安裝並配置了Xcode和MacSDK的iOS電腦。

1. 複製 `adobe-lc-mobileworkspace-src-<version>.zip` 從下載資料夾存檔到 `[User_Home]/Projects/`。
1. 解壓縮中的存檔 `[User_Home]/Projects/[your-project]`的子菜單。
1. 導航到 ` [User_Home]/Projects/ `[您的項目]`/adobe-lc-mobileworkspace-src-[version]/ios` 的子菜單。
1. 開啟 `AEM Forms.xcodeproj` Xcode中的項目。
1. 按一下 **AEM Forms**&#x200B;下 **目標**&#x200B;選中 **AEM Forms**。 選擇 **生成設定** 頁籤 **代碼簽名權利** 和「調試」和「發行」欄位中執行下列操作之一：

   * 未指定欄位以生成標準Mobile Workspace應用
   * 按中的說明指定要指定的欄位 [為iOS構建安全的AEM Forms應用](/help/forms/using/building-secure-mobile-workspace-app.md) 構建安全的AEM Forms應用。

1. 在 **生成設定** 按鈕 **全部** 然後按一下 **組合**。
1. 從 **設定** 清單，展開 **代碼簽名**。
1. 對於 **代碼簽名標識**，選擇相應的簽名。 有關建立新簽名的詳細資訊，請參見 [建立和下載開發預配配置檔案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 確保為 **調試**。 **發佈**, **任何iOSSDK**。
1. 替換 `AEM Forms-info.plist` 檔案：

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
   >只有在AEM Forms應用需要連接到不遵循應用傳輸安全要求的伺服器時，才需要此步驟。

1. 下 **項目**&#x200B;選中 **AEM Forms** 確保為 **代碼簽名標識**。 **調試**。 **發佈** 和 **任何iOSSDK**。
1. 將預配的iPad連接到Mac電腦。
1. 為 **AEM Forms** 項目。

   ![ipad](assets/ipad.png)

   選擇預配設備iPad2。

1. 選擇 **產品** > **清潔**。
1. 選擇 **產品** > **生成**。

## 生成AEM Forms應用的安裝程式 {#build-the-installer-for-the-mobile-workspace-app}

您需要存檔Xcode項目以生成安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含托管的內部應用程式的配置資訊，如應用程式的名稱和托管位置。 有關屬性清單檔案的詳細資訊，請參見 [關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 將預配的iPad連接到Mac電腦。 有關設定iPad的詳細資訊，請參見 [建立和下載開發預配配置檔案](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 為 **AEM Forms** 項目。

   ![ipad-1](assets/ipad-1.png)

   選擇預配設備iPad2。

1. 選擇 **產品** > **清潔**。
1. 選擇 **產品** > **生成**。
1. 選擇 **產品** > **存檔**。
1. 在管理器 — 存檔中，選擇項目的最新存檔，然後按一下 **分發**。
1. 選擇 **為企業或臨時部署保存** 作為分發方法，然後按一下 **下一個**。
1. 選擇相應的 **代碼簽名標識** 按一下 **下一個**。 按一下 **允許** 的子菜單。
1. 提供應用的名稱並選擇 **為企業分發保存**。
1. 提供 **應用程式URL** 的下一頁。 例如，要在CRX伺服器上承載應用，請提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在 **標題** 欄位，指定AEM Forms。
1. 按一下 **保存** 關閉Xcode。

   安裝程式檔案， `AEM Forms.ipa`，和屬性清單檔案， `AEM Forms-info.plist`，在指定的位置建立。

1. 開啟 `AEM Forms-info.plist` 的子菜單。
1. 將.ipa檔案URL中的所有空格替換為%20。
1. 保存並關閉 `AEM Forms-info.plist` 的子菜單。
