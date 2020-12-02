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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---


# 設定Xcode專案並建立iOS應用程式{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始碼存檔`adobe-lc-mobileworkspace-src-<version>.zip`是軟體分發上`adobe-aemfd-forms-app-src-pkg-<version>.zip`軟體包的一部分。

若要取得AEM Forms應用程式來源，請執行下列步驟：

1. 開啟[軟體分發](https://experience.adobe.com/downloads)。 您必須有Adobe ID才能登入「軟體散發」。
1. 點選頁首功能表中的「Adobe Experience Manager **[!UICONTROL 」。]**
1. 在&#x200B;**[!UICONTROL Filters]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL Solution]**&#x200B;下拉式清單中選擇&#x200B;**[!UICONTROL Forms]**。
   2. 選擇包的版本和類型。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 點選適用於您作業系統的套件名稱，選取「**[!UICONTROL 接受EULA條款]**」，然後點選「**[!UICONTROL 下載]**」。
1. 開啟[包管理器](https://docs.adobe.com/content/help/en/experience-manager-65/administering/contentmanagement/package-manager.html) ，然後按一下&#x200B;**[!UICONTROL 上載包]**&#x200B;來上載包。
1. 選擇軟體包並按一下&#x200B;**[!UICONTROL Install]**。

1. 若要下載原始碼封存檔，請在您的瀏覽器中開啟`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。
來源套件會下載在您的裝置上。

下圖顯示`adobe-lc-mobileworkspace-src-<version>.zip`的提取內容。

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

如需有關「程式碼簽署」和將裝置新增至iOS布建入口網站的詳細資訊，請參閱[iOS程式碼簽署設定、程式和疑難排解](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 建立標準AEM Forms應用程式{#set-up-the-xcode-project}

1. 執行下列步驟，以在Xcode中設定專案並提供簽署識別碼：

   登入已安裝並設定Xcode和iOS SDK的Mac電腦。

1. 從下載資料夾將`adobe-lc-mobileworkspace-src-<version>.zip`封存複製至`[User_Home]/Projects/`。
1. 在`[User_Home]/Projects/[your-project]`目錄中解壓縮存檔。
1. 導覽至` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios`目錄。
1. 在Xcode中開啟`AEM Forms.xcodeproj`專案。
1. 按一下&#x200B;**AEM Forms**，在&#x200B;**TARGETS**&#x200B;下方，選取&#x200B;**AEM Forms**。 選擇「**建置設定**」標籤，找到「代碼簽署權益&#x200B;**」區段，並在「除錯與發行」欄位中執行下列任一作業：**

   * 將欄位保留為未指定，以建立標準的行動工作區應用程式
   * 指定欄位，如[建立適用於iOS的安全AEM Forms應用程式以建立安全AEM Forms應用程式中所述。](/help/forms/using/building-secure-mobile-workspace-app.md)

1. 在&#x200B;**建置設定**&#x200B;頁籤中，按一下&#x200B;**全部** ，然後按一下&#x200B;**組合**。
1. 從&#x200B;**Settings**&#x200B;清單中，展開&#x200B;**Code Signing**。
1. 對於&#x200B;**代碼簽名身份**，請選擇適當的簽名。 如需建立新簽名的詳細資訊，請參閱[建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 請確定已針對&#x200B;**Debug**、**Release**&#x200B;和&#x200B;**任何iOS SDK**&#x200B;選取相同的簽名。
1. 在`AEM Forms-info.plist`檔案中取代下列程式碼：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   將`yourserver.com`取代為您伺服器的適當主機名稱時，使用下列程式碼。

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
   >只有當AEM Forms應用程式需要連線至未遵循App Transport Security要求的伺服器時，才需要此步驟。

1. 在&#x200B;**PROJECT**&#x200B;下，選擇&#x200B;**AEM Forms**&#x200B;並確保為&#x200B;**代碼簽名身份**、**Debug**、**Release**&#x200B;和&#x200B;**任何iOS選擇適當的簽名SDK**。
1. 將布建的iPad連接至Mac電腦。
1. 為&#x200B;**AEM Forms**&#x200B;專案選取已布建的裝置。

   ![ipad](assets/ipad.png)

   已選取已布建的iPad Air 2裝置。

1. 選擇「**產品** > **清潔**」。
1. 選擇&#x200B;**Product** > **Build**。

## 建立AEM Forms應用程式的安裝程式{#build-the-installer-for-the-mobile-workspace-app}

您需要封存Xcode專案，才能建立安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含代管內部應用程式的設定資訊，例如應用程式的名稱和代管位置。 有關屬性清單檔案的詳細資訊，請參閱[關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 將布建的iPad連接至Mac電腦。 如需iPad布建的詳細資訊，請參閱[建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 為&#x200B;**AEM Forms**&#x200B;專案選取已布建的裝置。

   ![ipad-1](assets/ipad-1.png)

   已選取已布建的iPad Air 2裝置。

1. 選擇「**產品** > **清潔**」。
1. 選擇&#x200B;**Product** > **Build**。
1. 選擇「**產品** > **歸檔**」。
1. 在「組織工具——封存」中，選取專案的最新封存，然後按一下「散發」**。**
1. 選擇&#x200B;**「儲存為企業用」或「臨機部署」作為散發方法，然後按一下「下一步」。******
1. 選擇適當的&#x200B;**代碼簽名標識** ，然後按一下&#x200B;**Next**。 按一下&#x200B;**允許**&#x200B;應用簽名。
1. 提供應用程式的名稱，並選取「儲存以供企業散發」**。**
1. 提供應用程式的&#x200B;**應用程式URL**。 例如，若要在CRX伺服器上主控應用程式，請提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在&#x200B;**Title**&#x200B;欄位中，指定AEM Forms。
1. 按一下&#x200B;**保存**&#x200B;並關閉Xcode。

   安裝程式檔案`AEM Forms.ipa`和屬性清單檔案`AEM Forms-info.plist`會建立在指定的位置。

1. 在編輯器中開啟`AEM Forms-info.plist`檔案。
1. 將。ipa檔案URL中的所有空格取代為%20。
1. 保存並關閉`AEM Forms-info.plist`檔案。