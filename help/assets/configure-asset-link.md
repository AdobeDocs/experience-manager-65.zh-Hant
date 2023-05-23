---
title: 為Adobe資產連結配置Experience Manager Assets
description: 配置Experience Manager Assets，以便與Adobe資產連結擴展一起用於Creative Cloud應用程式。
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 1%

---

# 為Adobe資產連結配置Experience Manager Assets {#adobe-asset-link}

[Adobe資產連結(AAL)](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html) 優化了內容建立過程中創意人員和營銷人員之間的協作。 它將Adobe Experience Manager資產與Creative Cloud案頭應用Adobe InDesign、Adobe Photoshop和Adobe Illustrator連接起來。 Adobe資產連結面板允許創意人員訪問和修改儲存在AEM Assets的內容，而不留下他們最熟悉的創意應用。

要將Experience Manager Assets配置為與資產連結一起使用，請執行以下任務。 使用Experience Manager管理員帳戶進行配置：

1. 根據需要安裝軟體包。 詳細資訊在 [先決條件](#prerequisites)。

1. 配置Experience Manager [手動](#manual-configuration) 或使用 [包](#configure-using-package)。

1. 要將Creative Cloud許可用戶與Experience Manager用戶映射，請管理 [用戶訪問控制](#user-access)。

1. 建立 [自定義查詢索引](#create-custom-index)配置 [FPO格式副本](/help/assets/configure-fpo-renditions.md) 對於InDesign，配置 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)，配置 [視覺或相似性搜索](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch)。

## 各種功能的先決條件和支援 {#prerequisites}

確保根據需要安裝相應的Service Pack和軟體包。 請參見每個Experience Manager版本和特定權能的以下要求。

| 資產能力 | Experience Manager版本和支援要求 |
|--- |--- |
| 預設情況下，資產連結有效 | Experience Manager6.5和6.5.2或更高版本。 </br> Experience Manager6.4.4和6.4.6或更高版本。 </br> Adobe建議安裝最新 [Experience Manager服務包(SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) 使用AAL。 |
| 安裝軟體包後，資產連結工作 | 對於Experience Manager6.4.0 - 6.4.3，安裝 [adobe資產連結支援](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 檔案。 |
| Adobe Stock整合 | Experience Manager6.4.2或更高版本 |
| 可視或相似性搜索 | Experience Manager6.5.0或更高版本 |


## 使用配置包配置Experience Manager {#configure-using-package}

Adobe建議您安裝 [adobe asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) 配置包以自動執行大多數配置任務，然後執行幾項手動任務。 或者，您可以 [手動配置](#manual-configuration)。

>[!CAUTION]
>
>如果已將Experience Manager實例配置為使用Adobe IMS帳戶進行用戶登錄，則不要使用配置包。 相反， [手動配置](#manual-configuration) 你的Experience Manager。

1. 要開啟包管理器，請在Experience ManagerWeb介面中訪問 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 包共用]**。 安裝 `adobe-asset-link-config` 檔案。

1. 存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web 主控台」]**。定位 **[!UICONTROL Adobe花崗岩OAuth IMS提供程式]** ，然後按一下以編輯。

   設定以下屬性並保存更改。

   * [!UICONTROL 組映射]:除非需要，否則保留為空。 有關詳細資訊，請參閱 [組映射](#group-mapping)。
   * [!UICONTROL 組織]:輸入您在Adobe Admin Console中使用的組織ID。 有關組織ID的詳細資訊，請參見 [建立用戶組](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html)。

1. 定位 **[!UICONTROL Adobe花崗岩載體驗證處理程式]** ，然後按一下以編輯。

   添加 **[!UICONTROL InDesignAem2]** 到的客戶端ID **[!UICONTROL 允許的OAuth客戶端ID]** configuration屬性。


## 手動配置Experience Manager {#manual-configuration}

如果您選擇不使用配置包，或者您的Experience Manager部署配置為支援用戶使用Adobe IMS帳戶登錄，則手動配置Experience Manager。

要手動配置Experience Manager:

1. 要訪問配置管理器，請訪問 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web控制台]**。 選擇 **[!UICONTROL OSGi]** > **[!UICONTROL 配置]** 的上界。

1. 查找 **[!UICONTROL Adobe花崗岩OAuth IMS提供程式]** 配置，然後按一下以編輯。

   設定以下配置，然後按一下 **[!UICONTROL 保存]**。

   * [!UICONTROL 授權終結點]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL 令牌終結點]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL 配置檔案終結點]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 驗證URL]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 組織]:設定為中的組織ID [Adobe Admin Console](https://adminconsole.adobe.com/)。
   * [!UICONTROL 組映射]:除非你有特殊的案子，否則留空。 有關詳細資訊，請參閱 [組映射](#group-mapping)。

1. 定位 **[!UICONTROL Adobe花崗岩載體驗證處理程式]** ，然後按一下以編輯。

   將以下客戶端ID添加到 **[!UICONTROL 允許的OAuth客戶端ID]** 配置屬性： `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`。

   添加每個 `Client ID`按一下 `+`。 按一下 **[!UICONTROL 保存]** 添加所有ID後。

1. 在 **[!UICONTROL Adobe花崗岩OAuth應用程式和提供程式]** 配置，檢查現有 **[!UICONTROL Adobe花崗岩OAuth身份驗證處理程式]** 實例。 如果您找到的實例 `Config ID` 值 `ims`，請在此過程中使用它。 否則，按一下 `+` 建立配置實例。 設定以下屬性值，然後按一下 **[!UICONTROL 保存]**。

   * [!UICONTROL 客戶端ID]:不更改
   * [!UICONTROL 客戶端密碼]:不更改
   * [!UICONTROL 配置ID]: ` ims`
   * [!UICONTROL 範圍]: `AdobeID, OpenID, read_organizations` （其他值也可能在配置中）
   * [!UICONTROL 提供程式ID]: ` ims`
   * [!UICONTROL 建立用戶]: ` Checked`
   * [!UICONTROL 用戶ID屬性]: `Email` 為新建立的配置。 否則，不要更改。

1. 查找 **[!UICONTROL Apache Jackrabbit Oak預設同步處理程式]** 配置 **[!UICONTROL 同步處理程式名稱]** `ims` 並按一下以編輯。

   設定以下配置屬性，然後按一下 **[!UICONTROL 保存]**。

   * [!UICONTROL 用戶過期時間和用戶成員資格過期]:「m」之後的時間（以分鐘為單位），沒有空格。 比如說， `15m` 15分鐘。 有關詳細資訊，請參閱 [組映射](#group-mapping)。
   * [!UICONTROL 用戶自動成員身份]:不更改
   * [!UICONTROL 用戶動態成員身份]: ` Deslect`

1. 查找 **[!UICONTROL Adobe花崗岩OAuth身份驗證處理程式]** 配置，然後按一下以編輯。 不進行任何更改，請按一下 **[!UICONTROL 保存]**。

1. 要調整承載驗證處理程式的相對優先順序，請在CRXDE中導航到 `/apps/system/config`。 定位 `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` 並開啟其配置。 最後，添加 `service.ranking=I"-10"`。 儲存變更。

   >[!NOTE]
   >
   >使用承載令牌進行身份驗證的每個請求都會產生對Adobe IMS的三次調用的開銷、用戶同步以及在Experience Manager中建立登錄令牌。 為了克服此開銷，Adobe資產連結將捕獲從Experience Manager返回的響應中返回的登錄令牌，並隨後發送請求。 要使此過程工作，必須調整承載驗證處理程式的相對優先順序。

1. （可選）如果Experience Manager用戶的電子郵件ID中包含大寫或混合大小寫域名，請選擇 **[!UICONTROL 將鎖定用戶更改為小寫]** 在 **[!UICONTROL Adobe花崗岩ACP平台配置]** Experience ManagerWeb控制台。

## 遷移到業務配置檔案後的其他配置 {#configure-migration-activity}

Adobe資產連結用戶能夠連接到Experience Manager，以允許從企業(CCE)組織的主Creative Cloud登錄IMS。 Experience Manager使用客戶端ID標識允許的IMS組織。 遷移到業務配置檔案後，需要為承載驗證處理程式配置Experience Manager中IMS組織的客戶端ID和密鑰。 有關業務配置檔案的詳細資訊，請參閱 [介紹Adobe配置檔案](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html)。

只有當您使用不同的Adobe IMS組織進行企業(CCE)的Experience Manager和Creative Cloud，並且這兩個組織之間建立了域信任關係時，才需要進行其他配置。

>[!NOTE]
>
>* Business Profiles的修復在6.5.11.0Experience Manager中。
>* 如果您使用的是具有Experience Manager和CCE的同一Adobe IMS組織，則現有配置將繼續有效。



**必備條件**

1. 為AAL配置承載Experience Manager的啟動和運行的驗證實例。
1. 在Experience Manager6.5實例上安裝以下軟體包(Service Pack 11)。

   [下載Experience Manager6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 聯繫人 [!UICONTROL 客戶支援] 獲取IMS組織的承載驗證的客戶端ID和密鑰。

以下是遷移到業務配置檔案後所需的其他配置：

1. 在 **[!UICONTROL Adobe花崗岩OAuth IMS配置提供程式]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`)，設定：

   * OAuth配置ID(`oauth.configmanager.ims.configid`): `ims` （驗證一次，您可能已配置它）

   * IMS擁有實體(`ims.owningEntity`):您的IMS組織ID

   ![IMS配置ID](assets/bearer-authentication1.png)

1. 開啟 **[!UICONTROL 承載驗證處理程式]** 配置並添加從 [!UICONTROL 客戶支援] 清單 **[!UICONTROL 允許的OAuth客戶端ID]**。

   ![添加客戶端ID](assets/add-clientid-bearer-auth.png)

1. 開啟 **[!UICONTROL Adobe花崗岩OAuth應用程式和提供程式]** 配置並添加 **[!UICONTROL 客戶端ID]** 和 **[!UICONTROL 客戶端密碼]** （密鑰）從客戶支援獲得。

   確保 **[!UICONTROL 配置ID]** 欄位(D)`oauth.config.id`)包含的值與 **[!UICONTROL OAuth配置ID]** 欄位(D)`oauth.configmanager.ims.configid`)。

   ![驗證客戶端ID](assets/clientid-secretkey.png)

1. 開啟 **[!UICONTROL Adobe花崗岩IMS簇交換令牌預處理器]** 將其設定為 `enable`。

## 管理用戶訪問控制 {#user-access}

本節介紹如何管理用戶及其對Experience Manager儲存庫的訪問。

### 組映射 {#group-mapping}

組映射確定Experience Manager中的組與Adobe IMS中的組的對應方式。 它在如何授予Adobe資產連結用戶訪問Experience Manager Assets的權限方面起著重要作用。

當與Adobe資產連結一起使用時，Experience Manager將用戶管理功能委派給Adobe IMS。 它自動建立與Adobe IMS中的用戶和組對應的用戶和組。 此外，它還使Experience Manager中的用戶、組和組成員身份同步，以與Adobe IMS中的成員身份相匹配。

例如，考慮Adobe資產連結用戶是Adobe IMS組資產連結用戶成員的情形。 在這種情況下，當來自Adobe IMS組的用戶首次連接到Experience Manager資產連結時，將在Adobe中建立名為assetlink-users的同步組。 當Adobe IMS組中的每個新用戶首次通過Experience Manager資產連結連接到Experience Manager時，他們將添加到該Adobe中的相應組。

Experience Manager中與Adobe IMS中的組對應並與其同步的組可以被直接授予訪問權限，也可以通過使它們成為另一組的成員來授予訪問權限。 下面是如何管理權限的示例。

![組示例](assets/group-examples.png)

以下規則適用於Experience Manager中的組映射：

* 確保 **[!UICONTROL 組映射]** 物業 **[!UICONTROL Adobe花崗岩OAuth IMS提供程式]** 配置為空。
* Adobe資產連結用戶組成員身份將在用戶驗證和時間段時評估 **[!UICONTROL 用戶到期時間]** 物業 **[!UICONTROL Apache Jackrabbit Oak預設同步處理程式]** 配置已過。 目前，用戶可以添加到Experience Manager中的組或從組中刪除，以便與Adobe IMS中的內容同步。
* 避免組名衝突。 確保在Adobe IMS中建立的組（用於管理用戶）所使用的名稱與所有Experience Manager系統組名稱不同。

   例如，確保它們與 `dam-users` 組和由Experience Manager管理員建立的組。

   名稱與Experience Manager系統組或手動建立的組的名稱衝突的Adobe IMS組不用於控制用戶權限。
* 如果Adobe IMS用戶連接到用戶名與先前建立的Experience Manager用戶衝突的Experience Manager實例，則Adobe IMS用戶會被賦予另一個名稱，並添加數字使其唯一。

**設定首次訪問控制**

通過Adobe資產連結進行連接的用戶只有在獲得所需權限後才能查看資產並與其進行交互。 的 [組映射](#group-mapping) 上面的一節討論如何在Experience Manager中建立用戶組，這些用戶組與您組織中Adobe IMS內的用戶組對應並同步。 建議Experience Manager管理員使用這些組來管理Adobe資產連結用戶的訪問控制。

對於與Adobe IMS組（用於管理用戶訪問控制）同步的每個Experience Manager組：

1. 確保組具有可用於從Adobe資產連結進行初始連接的成員。
1. 使用該用戶登錄到Adobe資產連結，並連接到Experience Manager。 此連接預期會失敗。
1. 在Experience Manager中，在Adobe IMS中找到與組對應的組，並授予它所需的訪問控制。 例如，新組將成為dam-users組的成員。
1. 關閉Adobe資產連結並重新啟動Creative Cloud應用程式。
1. 要驗證用戶是否具有預期的訪問權限，請重新開啟Adobe資產連結。

執行這些步驟後，同一組中的其他用戶可以在首次嘗試時使用Adobe資產連結連接到Experience Manager。 它們自動具有與組中的其他用戶相同的權限。

## 為Experience Manager資產連結管理Adobe用戶 {#manage-users}

Adobe資產連結用戶在登錄到其Experience Manager應用程式時能夠與Creative Cloud連接。 此身份驗證使用Adobe IMS技術，並在Experience Manager中建立用戶資訊（如果不存在）。 Experience Manager企業客戶使用與Experience Manager整合的外部身份提供程式來管理其用戶是常見的。 標識提供程式包括Adobe IMS和使用SAML和LDAP協定的其他產品。 或者，用戶可以在本地Experience Manager建立和管理。

從Adobe資產連結連接到Experience Manager的用戶與以前直接登錄Experience Manager中儲存的現有用戶資訊沒有衝突，如果：

* 用於直接登錄到Experience Manager的所有用戶名與Adobe IMS中用於Creative Cloud登錄的用戶名不同。
* Adobe IMS用作直接Experience Manager登錄的標識提供器。
* 用戶在使用同一帳戶直接Experience Manager登錄之前，從Adobe資產連結連接到Experience Manager。


另一方面，必須更新因直接Experience Manager登錄而建立的用戶資訊，以便在以下情況下使用Adobe資產連結：

* 同一用戶名（如用戶的電子郵件地址）用於兩者：Creative Cloud中的帳戶（使用Adobe IMS），以及外部身份提供程式（不是Adobe IMS）中的帳戶。
* 同一用戶名用於Creative Cloud中的帳戶和本地Experience Manager帳戶。
* Adobe IMS中的Creative Cloud帳戶是聯合ID，由與Experience Manager整合以便直接登錄的同一外部身份提供程式提供服務。

通過這些方案建立的用戶沒有與Adobe IMS同步的用戶所需的屬性。

要更新Experience Manager中的此類用戶以使用Adobe資產連結，請執行以下操作：

1. 在Experience ManagerWeb控制台中，找到 **[!UICONTROL Apache Jackrabbit Oak外部主配置]** 配置，然後按一下以編輯。 取消選擇 **[!UICONTROL 外部身份保護]** 複選框，然後按一下 **[!UICONTROL 保存]**。
1. 要訪問Experience Manager中的用戶管理介面，請導航至 **[!UICONTROL 工具]** > **[!UICONTROL 安全]** > **[!UICONTROL 用戶]**。 選擇要更新的用戶，然後記下該用戶的瀏覽器URL路徑的結尾，從 `/home/users`。 或者，可以在CRXDE中搜索用戶名。 示例用戶路徑： `/home/users/x/xTac082TDh-guJzzG7WM`。
1. 在CRXDE中，導航到用戶路徑，選擇用戶節點，通過選擇 **[!UICONTROL 屬性]** 的下界。 此節點具有 `jcr:primaryType` 屬性值 `rep:User`。
1. 在 **[!UICONTROL 屬性]** 頁籤，輸入 `Name` 值 `rep:externalId`。 `Type` 值 `String`的 `Value` 值 `rep:authorizableId`;`ims`，也請參見Wiki頁。 `rep:authorizableId` 是 `rep:authorizableId` 節點的屬性。 (分號不帶空格，用於分隔 `rep:authorizableId` 值 `ims`。)
1. 按一下 **[!UICONTROL 添加]** 按鈕，然後按一下 **[!UICONTROL 全部保存]**。
1. 對要升級以使用Adobe資產連結的任何其他用戶重複步驟2至5。
1. 在Experience ManagerWeb控制台中，找到 **[!UICONTROL Apache Jackrabbit Oak外部主配置]** 配置，然後按一下以編輯。 取消選擇 **[!UICONTROL 外部身份保護]** 複選框，然後按一下 **[!UICONTROL 保存]**。

>[!NOTE]
>
>如果服務在幾分鐘內未恢復，請重新啟動Experience Manager以允許成功進行身份驗證。

此更改後，更新的Experience Manager用戶可以與Adobe資產連結連接，並繼續使用更新前使用的直接登錄Experience Manager的方法。 在成功使用Adobe IMS進行身份驗證時，Experience Manager用戶配置檔案資訊與Adobe IMS中的用戶配置檔案同步。

有一種方法，通過它可以執行多個Experience Manager用戶的批量遷移，以使他們能夠使用Adobe資產連結。 聯繫Adobe關注啟用此選項的詳細資訊和幫助。

作為該步驟的替代方法，在某些情況下，可向Adobe資產連結用戶提供對Experience Manager的快速訪問。 在這種情況下，在與Experience Manager資產連結連接之前，利用Experience Manager用戶管理或AdobeCRXDE查找並刪除預先存在的用戶資訊。 在連接後的Experience Manager中建立新用戶資訊。 僅當確定沒有作為用戶節點的子節點添加的重要資料時，才使用此方法。 此類額外資料是用戶節點的子節點，而不是 `tokens`。 `preferences`。 `profile`。 `profiles`。 `profiles/public`, `rep:policy/*` 節點。

## 自動啟動工作流以有條件地處理資產 {#auto-start-workflow}

在Experience Manager6.4和Experience Manager6.5中，管理員可以配置工作流以根據預定義的條件自動執行和處理資產。

此配置對於業務線用戶和營銷人員非常有用，例如，在幾個特定資料夾上建立自定義工作流。 假設某機構照片中的所有資產都可以加水印，或者自由撰稿人上傳的所有資產都可以被處理，以建立特定的格式副本。

有關詳細資訊和Experience Manager配置，請參見 [自動執行資產工作流](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets)。


## 在Experience Manager6.4.x版中建立自定義索引 {#create-custom-index}

Experience Manager包含用於查詢的索引。 為指定的版本建立以下自定義索引。 Experience Manager6.5.0預設包含此索引。 Adobe資產連結需要此索引來確定用戶已簽出的資產。

1. 在CRXDE中，找到 `/oak:index` 的下界。 建立名為 `cqDrivelock` 設定 `Type` 至 `oak:QueryIndexDefinition`。

1. 將以下屬性添加到新節點並保存更改：

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 配置可視或相似性搜索 {#configure-visual-similarity-search}

「可視搜索」功能允許您使用「Adobe資產連結」面板在AEM Assets儲存庫中搜索外觀相似的資產。 該功能在6.5.0或更高版本中可用，只搜索索引資產。 有關詳細資訊，請參見 [如何配置可視搜索](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch)。

## 生成僅用於放置的Adobe InDesign格式副本 {#fpo-renditions}

Experience Manager提供僅用於放置(FPO)的格式副本。 這些FPO格式副本的檔案大小較小，但長寬比相同。 如果FPO格式副本不可用於資產，Adobe InDesign將改用原始資產。 此回退機制確保創作工作流不中斷即可繼續。 有關詳細資訊，請參見 [生成FPO格式副本](/help/assets/configure-fpo-renditions.md)。


## 與Adobe Stock整合 {#adobe-stock-integration}

各組織將其Adobe Stock賬戶與Experience Manager Assets合併。 它幫助營銷人員為其創意和營銷項目提供經許可的高質量、免版稅的照片、向量、插圖、視頻、模板和3D資產。 創意專業人員可以使用「資產連結」面板使用這些資產。

要與Adobe Stock整合，請參閱 [Adobe StockExperience Manager Assets資產](/help/assets/aem-assets-adobe-stock.md)。 Experience Manager6.4.2或更高版本需要與Adobe Stock合併。


## 排除與Experience Manager相關的問題 {#troubleshoot}


如果在配置或使用Adobe資產連結時遇到問題，請嘗試以下操作：

* 確保部署滿足先決條件。 具體來說，確保安裝了相應的功能包或軟體包。
* 請與組織的合作夥伴或系統整合商聯繫。
* 如果您的Creative Cloud用戶無法在已簽出的資產中驗證，則檢查電子郵件ID中的域名。 要修復，請參閱 [手動配置](#manual-configuration)。
* 有關詳細資訊，請參見 [資產連結疑難解答](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html)。


>[!MORELIKETHIS]
>
>* [關於 Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [在Creative Cloud案頭應用中使用資產連結並管理資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [配置Adobe Experience Manager資產as a Cloud Service](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html)。

