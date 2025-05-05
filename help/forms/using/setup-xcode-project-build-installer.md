---
title: 設定Xcode專案並建置iOS應用程式
description: 說明如何建置適用於iOS的標準AEM Forms應用程式。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 78ce6107-8821-47d6-86ab-7ab968945e7c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 2%

---

# 設定Xcode專案並建置iOS應用程式{#set-up-the-xcode-project-and-build-the-ios-app}

AEM Forms提供AEM Forms應用程式的完整原始碼。 來源包含建立自訂AEM Forms應用程式的所有元件。 原始程式碼封存`adobe-lc-mobileworkspace-src-<version>.zip`是Software Distribution上`adobe-aemfd-forms-app-src-pkg-<version>.zip`套件的一部分。

若要取得AEM Forms應用程式來源，請執行以下步驟：

1. 開啟 [Software Distribution](https://experience.adobe.com/downloads)。您需要 Adobe ID 才能登入 Software Distribution。
1. 選取標題功能表中可用的&#x200B;**[!UICONTROL Adobe Experience Manager]**。
1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中：
   1. 從&#x200B;**[!UICONTROL 解決方案]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Forms]**。
   2. 選取封裝的版本和型別。 您也可以使用&#x200B;**[!UICONTROL 搜尋下載]**&#x200B;選項來篩選結果。
1. 選取適用於您作業系統的封裝名稱，選取&#x200B;**[!UICONTROL 接受EULA條款]**，然後選取&#x200B;**[!UICONTROL 下載]**。
1. 開啟[封裝管理員](https://experienceleague.adobe.com/docs/experience-manager-65/administering/contentmanagement/package-manager.html)，然後按一下&#x200B;**[!UICONTROL 上傳封裝]**&#x200B;以上傳封裝。
1. 選取封裝並按一下&#x200B;**[!UICONTROL 安裝]**。

1. 若要下載原始程式碼封存，請在瀏覽器中開啟`https://<server>:<port>/crx/de/content/forms/mobileapps/src/adobe-lc-mobileworkspace-src-<version>.zip`。
來源套件會下載到您的裝置上。

下列影像顯示`adobe-lc-mobileworkspace-src-<version>.zip`的擷取內容。

![mws-content](assets/mws-content.png)

下表詳細列出`adobe-lc-mobileworkspace-src-[version]/ios`資料夾的內容。

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

如需有關程式碼簽署和將裝置新增到iOS布建入口網站的詳細資訊，請參閱[iOS程式碼簽署設定、處理和疑難排解](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html)。

## 建置標準AEM Forms應用程式 {#set-up-the-xcode-project}

1. 執行以下步驟，在Xcode中設定專案並提供簽署身分：

   登入已安裝並設定Xcode和iOS SDK的Mac電腦。

1. 將`adobe-lc-mobileworkspace-src-<version>.zip`封存從下載資料夾複製到`[User_Home]/Projects/`。
1. 擷取`[User_Home]/Projects/[your-project]`目錄中的封存。
1. 導覽至` [User_Home]/Projects/ `[your-project]`/adobe-lc-mobileworkspace-src-[version]/ios`目錄。
1. 在Xcode中開啟`AEM Forms.xcodeproj`專案。
1. 按一下「**AEM Forms**」，在「**目標**」下方選取「**AEM Forms**」。 選取「**組建設定**」標籤，找到「**程式碼簽署權利**」區段，並在「除錯」和「發行」欄位執行下列其中一項作業：

   * 將欄位保留為未指定，以便建置標準的行動Workspace應用程式
   * 依照[為iOS建置安全AEM Forms應用程式](/help/forms/using/building-secure-mobile-workspace-app.md)中的說明指定要使用的欄位，以建置安全的AEM Forms應用程式。

1. 在&#x200B;**組建設定**&#x200B;索引標籤中，按一下&#x200B;**全部**，然後按一下&#x200B;**組合**。
1. 從&#x200B;**設定**&#x200B;清單，展開&#x200B;**程式碼簽署**。
1. 針對&#x200B;**程式碼簽署身分識別**，請選取適當的簽章。 如需有關建立新簽章的詳細資訊，請參閱[建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)。
1. 確保為&#x200B;**Debug**、**版本**&#x200B;和&#x200B;**任何iOS SDK**&#x200B;選取相同的簽章。
1. 取代`AEM Forms-info.plist`檔案中的下列程式碼：

   ```xml
   <key>NSAppTransportSecurity</key>
   <dict>
   <key>NSAllowsArbitraryLoads</key>
   <true/>
   </dict>
   ```

   下列專案取代`yourserver.com`，並使用伺服器的適當主機名稱。

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
   >只有在AEM Forms應用程式需要連線到未遵循App Transport Security要求的伺服器時，才需要執行此步驟。

1. 在&#x200B;**專案**&#x200B;下，選取&#x200B;**AEM Forms**，並確定已針對&#x200B;**程式碼簽署身分識別**、**偵錯**、**版本**&#x200B;和&#x200B;**任何iOS SDK**&#x200B;選取適當的簽章。
1. 將布建的iPad連線至Mac電腦。
1. 選取&#x200B;**AEM Forms**&#x200B;專案的布建裝置。

   ![ipad](assets/ipad.png)

   已選取已布建的裝置iPad Air 2。

1. 選取&#x200B;**產品** > **清除**。
1. 選取&#x200B;**產品** > **組建**。

## 建立AEM Forms應用程式的安裝程式 {#build-the-installer-for-the-mobile-workspace-app}

您必須封存Xcode專案，才能建置安裝程式（.ipa檔案）和屬性清單（.plist檔案）檔案。 屬性清單檔案包含託管內部應用程式的設定資訊，例如應用程式的名稱和託管位置。 如需屬性清單檔案的詳細資訊，請參閱[關於資訊屬性清單檔案](https://developer.apple.com/library/ios/#documentation/general/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html)。

1. 將布建的iPad連線至Mac電腦。 如需布建iPad的詳細資訊，請參閱[建立和下載開發佈建設定檔](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppStoreDistributionTutorial/CreatingYourTeamProvisioningProfile/CreatingYourTeamProvisioningProfile.html)
1. 選取&#x200B;**AEM Forms**&#x200B;專案的布建裝置。

   ![ipad-1](assets/ipad-1.png)

   已選取已布建的裝置iPad Air 2。

1. 選取&#x200B;**產品** > **清除**。
1. 選取&#x200B;**產品** > **組建**。
1. 選取&#x200B;**產品** > **封存**。
1. 在[組織者 — 封存]中，選取您專案的最新封存，然後按一下[發佈]。**&#x200B;**
1. 選取&#x200B;**儲存以供企業或臨機部署**&#x200B;作為發佈方法，然後按一下&#x200B;**下一步**。
1. 選取適當的&#x200B;**程式碼簽署身分識別**，然後按一下&#x200B;**下一步**。 按一下&#x200B;**允許**&#x200B;以套用簽章。
1. 提供應用程式的名稱，並選取&#x200B;**儲存以供企業發佈**。
1. 提供應用程式的&#x200B;**應用程式URL**。 例如，若要在CRX伺服器上裝載應用程式，請提供URL `https://[LC_host]:'port'/lc/content/distribution/mobileworkspace/APP_NAME.ipa`。
1. 在&#x200B;**標題**&#x200B;欄位中，指定AEM Forms。
1. 按一下&#x200B;**儲存**&#x200B;並關閉Xcode。

   安裝程式檔案`AEM Forms.ipa`和屬性清單檔案`AEM Forms-info.plist`是在指定的位置建立的。

1. 在編輯器中開啟`AEM Forms-info.plist`檔案。
1. 將.ipa檔案URL中的所有空格取代為%20。
1. 儲存並關閉`AEM Forms-info.plist`檔案。
