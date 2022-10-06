---
title: 設定Experience Manager Assets以Adobe資產連結
description: 設定Experience Manager Assets以與Adobe資產連結擴充功能搭配使用，以供Creative Cloud應用程式使用。
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
source-git-commit: 84b16dd1a60f731b568dd87ef89699875cb86596
workflow-type: tm+mt
source-wordcount: '3149'
ht-degree: 1%

---

# 設定Experience Manager Assets以Adobe資產連結 {#adobe-asset-link}

[Adobe資產連結(AAL)](https://www.adobe.com/creativecloud/business/enterprise/adobe-asset-link.html) 可簡化創意人員與行銷人員在內容建立程式中的協作。 它可將Adobe Experience Manager Assets與Creative Cloud案頭應用程式Adobe InDesign、Adobe Photoshop和Adobe Illustrator連接在一起。 「Adobe資產連結」面板可讓創意人員存取及修改儲存在AEM Assets中的內容，而不需離開最熟悉的創意應用程式。

若要設定Experience Manager Assets以搭配資產連結使用，請執行下列工作。 使用Experience Manager管理員帳戶進行配置：

1. 視需要安裝套件。 詳細資訊位於 [必要條件](#prerequisites).

1. 配置Experience Manager [手動](#manual-configuration) 或使用 [套件](#configure-using-package).

1. 若要將Creative Cloud授權使用者與Experience Manager使用者對應，請管理 [使用者存取控制](#user-access).

1. 建立 [自訂查詢索引](#create-custom-index)，設定 [FPO轉譯](/help/assets/configure-fpo-renditions.md) 針對InDesign，請設定 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)，然後設定 [視覺或相似性搜尋](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## 各種功能的必要條件和支援 {#prerequisites}

請務必視需要安裝適當的Service Pack和套件。 如需各個Experience Manager版本和特定功能，請參閱下列需求。

| 資產功能 | Experience Manager版本和支援需求 |
|--- |--- |
| 資產連結預設可運作 | Experience Manager6.5和6.5.2或更新版本。 </br> Experience Manager6.4.4和6.4.6或更新版本。 </br> Adobe建議安裝最新 [Experience Manager服務包(SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html) 使用AAL之前。 |
| 安裝套件後，資產連結便可運作 | 對於Experience Manager6.4.0 - 6.4.3，安裝 [adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support) 包。 |
| Adobe Stock整合 | Experience Manager6.4.2或更新版本 |
| 視覺或相似性搜尋 | Experience Manager6.5.0或更新版本 |


## 使用配置包配置Experience Manager {#configure-using-package}

Adobe建議您安裝 [adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config) 配置包，以自動執行大部分配置任務，然後執行一些手動任務。 或者，您也可以 [手動配置](#manual-configuration).

>[!CAUTION]
>
>如果您的Experience Manager例項已設定為使用者透過Adobe IMS帳戶登入，請勿使用設定套件。 相反， [手動配置](#manual-configuration) 您的Experience Manager例項。

1. 要開啟「包管理器」，請在Experience ManagerWeb介面中訪問 **[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 封裝共用]**. 安裝 `adobe-asset-link-config` 包。

1. 存取&#x200B;**[!UICONTROL 「工具]** > **[!UICONTROL 作業]** > **[!UICONTROL Web 主控台」]**。找出 **[!UICONTROL AdobeGranite OAuth IMS提供者]** 設定，然後按一下以編輯。

   設定下列屬性並儲存變更。

   * [!UICONTROL 組映射]:除非需要，否則保留空白。 如需詳細資訊，請參閱 [群組對應](#group-mapping).
   * [!UICONTROL 組織]:在Adobe Admin Console中輸入您使用的組織ID。 如需組織ID的詳細資訊，請參閱 [建立使用者群組](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html).

1. 找出 **[!UICONTROL AdobeGranite承載驗證處理常式]** 設定，然後按一下以編輯。

   新增 **[!UICONTROL InDesignAem2]** 用戶端ID **[!UICONTROL 允許的OAuth用戶端ID]** 設定屬性。


## 手動配置Experience Manager {#manual-configuration}

如果您選擇不使用設定套件或您的Experience Manager部署已設定為支援使用者以Adobe IMS帳戶登入，請手動設定Experience Manager。

手動配置Experience Manager:

1. 若要存取設定管理器，請存取 **[!UICONTROL 工具]** > **[!UICONTROL 操作]** > **[!UICONTROL Web主控台]**. 選擇 **[!UICONTROL OSGi]** > **[!UICONTROL 設定]** 的上方。

1. 找出 **[!UICONTROL AdobeGranite OAuth IMS提供者]** 設定，然後按一下以編輯。

   設定下列設定，然後按一下 **[!UICONTROL 儲存]**.

   * [!UICONTROL 授權端點]: ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL 代號端點]: ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL 設定檔端點]: ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 驗證URL]: ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 組織]:設為 [Adobe Admin Console](https://adminconsole.adobe.com/).
   * [!UICONTROL 組映射]:除非您有特殊案例，否則請保留空白。 如需詳細資訊，請參閱 [群組對應](#group-mapping).

1. 找出 **[!UICONTROL AdobeGranite承載驗證處理常式]** 設定，然後按一下以編輯。

   將下列用戶端ID新增至 **[!UICONTROL 允許的OAuth用戶端ID]** 配置屬性： `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`.

   新增每個 `Client ID`，按一下 `+`. 按一下 **[!UICONTROL 儲存]** 新增所有ID之後。

1. 在 **[!UICONTROL AdobeGranite OAuth應用程式和提供者]** 設定，檢查現有 **[!UICONTROL AdobeGranite OAuth驗證處理常式]** 例項。 若您找到的例項與 `Config ID` 值 `ims`，請依照本程式的指示使用。 否則，按一下 `+` 來建立設定例項。 設定下列屬性值，然後按一下 **[!UICONTROL 儲存]**.

   * [!UICONTROL 用戶端ID]:請勿變更
   * [!UICONTROL 用戶端密碼]:請勿變更
   * [!UICONTROL 設定ID]: ` ims`
   * [!UICONTROL 範圍]: `AdobeID, OpenID, read_organizations` （其他值也可能在設定中）
   * [!UICONTROL 提供者ID]: ` ims`
   * [!UICONTROL 建立使用者]: ` Checked`
   * [!UICONTROL 使用者ID屬性]: `Email` 新建立的配置。 否則，請勿變更。

1. 找出 **[!UICONTROL Apache Jackrabbit Oak Default同步處理常式]** 配置 **[!UICONTROL 同步處理程式名稱]** `ims` 然後按一下以編輯它。

   設定下列配置屬性，然後按一下 **[!UICONTROL 儲存]**.

   * [!UICONTROL 用戶過期時間和用戶成員資格過期]:「m」後面的時間（以分鐘為單位），沒有空格。 例如， `15m` 15分鐘。 如需詳細資訊，請參閱 [群組對應](#group-mapping).
   * [!UICONTROL 用戶自動成員資格]:請勿變更
   * [!UICONTROL 使用者動態成員資格]: ` Deslect`

1. 找出 **[!UICONTROL AdobeGranite OAuth驗證處理常式]** 設定，然後按一下以編輯。 若不進行任何變更，請按一下 **[!UICONTROL 儲存]**.

1. 要調整承載身份驗證處理程式的相對優先順序，請在CRXDE中導航到 `/apps/system/config`. 找出 `com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config` 並開啟其設定。 最後，新增 `service.ranking=I"-10"`. 儲存變更。

   >[!NOTE]
   >
   >每個以不記名權杖驗證的請求會產生三次Adobe IMS呼叫、使用者同步，以及在Experience Manager中建立登入權杖的額外負荷。 為了克服此額外負荷，「Adobe資產連結」會從Experience Manager擷取回應中傳回的登入代號，並隨後傳送要求。 為了使此過程工作，必須調整承載身份驗證處理程式的相對優先順序。

1. （選用）如果Experience Manager使用者的電子郵件ID中有大寫或混合大小寫的網域名稱，請選取 **[!UICONTROL 將鎖定用戶更改為小寫]** in **[!UICONTROL AdobeGranite ACP平台配置]** Experience ManagerWeb主控台中。

## 遷移到業務配置檔案後的其他配置 {#configure-migration-activity}

Adobe資產連結使用者可以連線至Experience Manager，允許從企業(CCE)組織的主要Creative Cloud登入IMS。 Experience Manager使用用戶端ID來識別允許的IMS組織。 移轉至業務設定檔後，必須為IMS組織設定用戶端ID和密鑰，以Experience Manager為承載驗證處理常式。 有關業務配置檔案的詳細資訊，請參閱 [Adobe設定檔簡介](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html).

只有在您使用不同的Adobe IMS組織來Experience Manager和Creative Cloud企業版(CCE)，且這兩個組織之間已建立網域信任關係時，才需要額外設定。

>[!NOTE]
>
>* Experience Manager6.5.11.0中提供Business Profiles的修正。
>* 如果您使用相同的Adobe IMS組織搭配Experience Manager和CCE，現有的設定會繼續運作。



**必備條件**

1. 為AAL配置了承載身份驗證的啟動和運行Experience Manager實例。
1. 在您的Experience Manager6.5執行個體上安裝下列套件(Service Pack 11)。

   [下載Experience Manager6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 連絡人 [!UICONTROL 客戶支援] 取得用戶端ID和密碼金鑰，以驗證您的IMS組織。

以下是遷移到業務配置檔案後需要的其他配置：

1. 在 **[!UICONTROL AdobeGranite OAuth IMS設定提供者]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`)，設定：

   * OAuth設定ID(`oauth.configmanager.ims.configid`): `ims` （驗證一次，您可能已設定）

   * IMS擁有實體(`ims.owningEntity`):您的IMS組織ID

   ![IMS設定ID](assets/bearer-authentication1.png)

1. 開啟 **[!UICONTROL 承載身份驗證處理程式]** 設定，並新增從 [!UICONTROL 客戶支援] 到 **[!UICONTROL 允許的OAuth用戶端ID]**.

   ![新增用戶端ID](assets/add-clientid-bearer-auth.png)

1. 開啟 **[!UICONTROL AdobeGranite OAuth應用程式和提供者]** 設定，並新增 **[!UICONTROL 用戶端ID]** 和 **[!UICONTROL 用戶端密碼]** （秘密金鑰）從客戶支援取得。

   確保 **[!UICONTROL 設定ID]** 欄位()`oauth.config.id`)包含的值與 **[!UICONTROL OAuth設定ID]** 欄位()`oauth.configmanager.ims.configid`)。

   ![驗證客戶端ID](assets/clientid-secretkey.png)

1. 開啟 **[!UICONTROL AdobeGranite IMS叢集交換代號預處理器]** 設定並將其設為 `enable`.

## 管理用戶訪問控制 {#user-access}

本節說明如何管理使用者及其對Experience Manager存放庫的存取權。

### 群組對應 {#group-mapping}

群組對應決定Experience Manager中的群組對應至Adobe IMS中群組的方式。 在Adobe資產連結使用者如何獲得存取Experience Manager Assets的權限方面，它扮演著重要的角色。

與Adobe資產連結搭配使用時，Experience Manager會將使用者管理功能委派至Adobe IMS。 它會自動建立對應至Adobe IMS中使用者和群組的使用者和群組。 此外，它會同步Experience Manager中的使用者、群組和群組成員資格，以符合Adobe IMS中的使用者、群組和群組成員資格。

例如，假設Adobe資產連結使用者是Adobe IMS群組資產連結使用者的成員， 在此情況下，當來自該Adobe IMS群組的使用者首次連線至Adobe資產連結時，即會在Experience Manager中建立名為assetlink-users的同步群組。 當Adobe IMS群組中的每個新使用者首次透過Experience Manager資產連結連線至Experience Manager時，都會新增至該Adobe中的對應群組。

與Adobe IMS中的群組對應並與其同步之Experience Manager中的群組，可以直接取得存取權，或讓這些群組成為其他群組的成員。 以下是如何管理權限的範例。

![群組範例](assets/group-examples.png)

下列規則適用於Experience Manager中的群組對應：

* 確保 **[!UICONTROL 組映射]** 屬性 **[!UICONTROL AdobeGranite OAuth IMS提供者]** 設定為空白。
* Adobe資產連結使用者群組成員資格是在使用者驗證時評估，以及 **[!UICONTROL 使用者過期時間]** 屬性 **[!UICONTROL Apache Jackrabbit Oak Default同步處理常式]** 配置已過。 目前，使用者可以新增至Experience Manager中的群組，或從群組中移除，以便與Adobe IMS中找到的同步。
* 避免組名衝突。 確認在Adobe IMS中建立之群組（以管理使用者）所使用的名稱，與所有Experience Manager系統群組名稱不同。

   例如，請確定它們與 `dam-users` 群組和Experience Manager管理員建立的群組。

   名稱與Experience Manager系統群組或手動建立的群組名稱衝突的Adobe IMS群組，不會用來控制使用者權限。
* 如果Adobe IMS使用者連線至Experience Manager例項，而該使用者的名稱與先前建立的Experience Manager使用者衝突，系統會為Adobe IMS使用者提供另一個名稱，並加上數字以使其唯一。

**設定首次存取控制**

透過Adobe資產連結連線的使用者，只有在獲得必要權限後，才能檢視資產並與資產互動。 此 [群組對應](#group-mapping) 上節探討如何在Adobe IMS中建立與貴組織的使用者群組對應且與Experience Manager同步的使用者群組。 建議Experience Manager管理員使用這些群組來管理Adobe資產連結使用者的存取控制。

對於與Adobe IMS群組同步的每個Experience Manager群組（用於管理使用者存取控制）:

1. 確認群組擁有可從Adobe資產連結進行初始連線的成員。
1. 使用該使用者登入Adobe資產連結，並連線至Experience Manager。 此連線預期會失敗。
1. 在Experience Manager中，找出與Adobe IMS中的群組相對應的群組，並授予其所需的存取控制權。 例如，新群組會設為dam-users群組的成員。
1. 關閉Adobe資產連結並重新啟動Creative Cloud應用程式。
1. 若要確認使用者具有預期的存取權，請重新開啟Adobe資產連結。

執行這些步驟後，同一群組中的其他使用者第一次嘗試時，就可以透過Adobe資產連結連線至Experience Manager。 他們會自動擁有與群組中其他使用者相同的權限。

## 管理Experience ManagerAdobe資產連結的使用者 {#manage-users}

AdobeExperience Manager連結使用者登入Creative Cloud應用程式時，便能與資產連結。 此驗證會使用Adobe IMS技術，並在Experience Manager中建立使用者資訊（如果不存在）。 Experience Manager企業客戶通常使用與Experience Manager整合的外部身分提供者來管理其使用者。 身分提供者包括Adobe IMS和其他使用SAML和LDAP通訊協定的產品。 或者，您也可以在本機Experience Manager中建立和管理使用者。

透過Adobe資產連結連線至Experience Manager的使用者，與先前直接登入所儲存在Experience Manager中的現有使用者資訊沒有衝突，條件是：

* 所有直接登入Experience Manager的使用者名稱，都與Adobe IMS中用於Creative Cloud登入的使用者名稱不同。
* Adobe IMS是直接Experience Manager登入的身分提供者。
* 使用者透過Adobe資產連結連線至Experience Manager，再透過相同帳戶直接Experience Manager登入。


另一方面，在下列情況下，必須更新因直接Experience Manager登入而建立的使用者資訊，才能與Adobe資產連結搭配使用：

* 兩者會使用相同的使用者名稱（例如使用者的電子郵件地址）：使用Adobe IMS的Creative Cloud帳戶，以及使用Adobe IMS以外之外部身分提供者的帳戶。
* 兩者都使用相同的使用者名稱 — Creative Cloud中的帳戶和本機Experience Manager帳戶。
* Adobe IMS中的Creative Cloud帳戶為Federated ID，由與Experience Manager整合以直接登入的相同外部身分提供者提供。

透過這些案例建立的使用者沒有使用者需要的屬性，這些屬性會與Adobe IMS同步。

若要更新Experience Manager中的這類使用者，以使用Adobe資產連結：

1. 在Experience ManagerWeb主控台中，找到 **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** 設定，然後按一下以編輯。 取消選取 **[!UICONTROL 外部身份保護]** 複選框，然後按一下 **[!UICONTROL 儲存]**.
1. 若要存取Experience Manager中的「使用者管理」介面，請導覽至 **[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**. 選取您要更新的使用者，然後記下該使用者的瀏覽器URL路徑結尾(從 `/home/users`. 或者，您也可以在CRXDE中搜尋使用者名稱。 範例使用者路徑： `/home/users/x/xTac082TDh-guJzzG7WM`.
1. 在CRXDE中，導覽至使用者路徑、選取使用者節點，並透過選取 **[!UICONTROL 屬性]** 標籤。 此節點具有 `jcr:primaryType` 屬性值 `rep:User`.
1. 在 **[!UICONTROL 屬性]** 頁簽區域，輸入 `Name` 值 `rep:externalId`, `Type` 值 `String`和 `Value` 值 `rep:authorizableId`;`ims`，其中 `rep:authorizableId` 是 `rep:authorizableId` 屬性。 (會使用分號來分隔 `rep:authorizableId` 值自 `ims`.)
1. 按一下 **[!UICONTROL 新增]** 按鈕，然後按一下 **[!UICONTROL 全部儲存]**.
1. 對於您想要升級以使用Adobe資產連結的任何其他使用者，請重複步驟2到5。
1. 在Experience ManagerWeb主控台中，找到 **[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]** 設定，然後按一下以編輯。 取消選取 **[!UICONTROL 外部身份保護]** 複選框，然後按一下 **[!UICONTROL 儲存]**.

>[!NOTE]
>
>如果幾分鐘內未恢復服務，請重新啟動Experience Manager以允許成功驗證。

此變更後，更新後的Experience Manager使用者可以連線Adobe資產連結，並繼續使用在更新前使用的直接登入Experience Manager方法。 成功與Adobe IMS驗證時，Experience Manager使用者設定檔資訊會與Adobe IMS中的使用者設定檔同步。

有一種方法可讓多個Experience Manager使用者執行大量移轉，以便他們能使用Adobe資產連結。 如需啟用此選項的詳細資訊和協助，請聯絡Adobe服務。

作為步驟的替代方法，在某些情況下，可向Adobe資產連結使用者提供Experience Manager的快速存取。 在這種情況下，在Experience Manager用戶管理或Experience ManagerCRXDE與Adobe資產連結建立連接之前，會找到並刪除預先存在的用戶資訊。 連線後會在Experience Manager中建立新的使用者資訊。 只有在您確定沒有重要資料會新增為使用者節點的子節點時，才使用此方法。 此類額外資料是用戶節點的子節點，而不是 `tokens`, `preferences`, `profile`, `profiles`, `profiles/public`，和 `rep:policy/*` 節點。

## 有條件式處理資產的自動啟動工作流程 {#auto-start-workflow}

在Experience Manager6.4和Experience Manager6.5中，管理員可以設定工作流程，以根據預先定義的條件自動執行和處理資產。

此設定對於業務線使用者和行銷人員非常實用，例如在幾個特定資料夾上建立自訂工作流程。 假設某個機構拍攝的所有資產都可以加上水印，或者自由職業者上傳的所有資產都可以經過處理，以建立特定的轉譯。

如需詳細資訊和Experience Manager設定，請參閱 [對資產自動執行工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets).


## 在Experience Manager6.4.x版中建立自訂索引 {#create-custom-index}

Experience Manager包含用於查詢的索引。 為指定版本建立以下自定義索引。 Experience Manager6.5.0預設包含此索引。 Adobe資產連結需要此索引，才能判斷使用者已結帳的資產。

1. 在CRXDE中，找到 `/oak:index` 節點。 建立名為的節點 `cqDrivelock` 設定 `Type` to `oak:QueryIndexDefinition`.

1. 將下列屬性新增至新節點並儲存變更：

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 配置視覺搜索或相似性搜索 {#configure-visual-similarity-search}

「視覺化搜尋」功能可讓您使用「AEM Assets資產連結」面板，在Adobe存放庫中搜尋視覺上類似的資產。 6.5.0或更新版本提供此功能，且只會搜尋已索引的資產。 如需詳細資訊，請參閱 [如何配置visual search](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch).

## 僅針對Adobe InDesign產生版位轉譯 {#fpo-renditions}

Experience Manager提供僅用於版位(FPO)的轉譯。 這些FPO轉譯的檔案大小很小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此後援機制可確保創意工作流程持續進行，不會有任何中斷。 如需詳細資訊，請參閱 [生成FPO轉譯](/help/assets/configure-fpo-renditions.md).


## 整合Adobe Stock {#adobe-stock-integration}

組織將其Adobe Stock帳戶與Experience Manager Assets整合。 它可協助行銷人員為其創意和行銷專案提供授權的高品質、免版稅像片、向量圖、插圖、影片、範本和3D資產。 創意專業人員可以使用Asset Link面板來使用這些資產。

若要與Adobe Stock整合，請參閱 [Adobe Stock資產(Experience Manager Assets)](/help/assets/aem-assets-adobe-stock.md). Experience Manager6.4.2或更新版本才能與Adobe Stock整合。


## 疑難排解Experience Manager相關問題 {#troubleshoot}


如果您在設定或使用Adobe資產連結時遇到問題，請嘗試下列步驟：

* 確定您的部署符合必要條件。 具體來說，請確定已安裝適當的功能套件或套件。
* 請聯絡貴組織的合作夥伴或系統整合商。
* 如果您的Creative Cloud使用者無法驗證已結帳的資產，請檢查電子郵件ID中的網域名稱大小寫。 若要修正，請參閱 [手動配置](#manual-configuration).
* 如需詳細資訊，請參閱 [疑難排解資產連結](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html).


>[!MORELIKETHIS]
>
>* [關於 Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [在Creative Cloud案頭應用程式中使用資產連結及管理資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [設定Adobe Experience Manager Assetsas a Cloud Service](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html).

