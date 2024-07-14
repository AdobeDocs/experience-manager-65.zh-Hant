---
title: 設定Experience Manager Assets以進行Adobe資產連結
description: 設定Experience Manager Assets以與Creative Cloud應用程式的Adobe Asset Link擴充功能搭配使用。
contentOwner: Vishabh Gupta
role: Admin
feature: Asset Management
exl-id: 3a9b44d4-1756-4ad5-91df-df8d53e82193
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3060'
ht-degree: 0%

---

# 設定Experience Manager Assets以進行Adobe資產連結 {#adobe-asset-link}

[Adobe資產連結(AAL)](https://www.adobe.com/tw/creativecloud/business/enterprise/adobe-asset-link.html)可簡化創意人員與行銷人員在內容建立過程中的共同作業。 它會將Adobe Experience Manager Assets與Creative Cloud案頭應用程式Adobe InDesign、Adobe Photoshop和Adobe Illustrator連線。 「Adobe資產連結」面板可讓創意人員存取及修改儲存在AEM Assets中的內容，而不需離開他們最熟悉的創意應用程式。

若要設定Experience Manager Assets與Asset Link搭配使用，請實作下列工作。 使用Experience Manager管理員帳戶進行設定：

1. 視需要安裝套件。 詳細資料請參閱[必要條件](#prerequisites)。

1. 設定Experience Manager[手動](#manual-configuration)或使用[封裝](#configure-using-package)。

1. 若要對應Creative Cloud授權使用者與Experience Manager使用者，請管理[使用者存取控制](#user-access)。

1. 建立[自訂查詢索引](#create-custom-index)、設定InDesign的[FPO轉譯](/help/assets/configure-fpo-renditions.md)、設定[Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)，以及設定[視覺或相似性搜尋](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch)。

## 各種功能的先決條件和支援 {#prerequisites}

請務必視需要安裝適當的Service Pack和套件。 如需瞭解每個Experience Manager版本和特定功能，請參閱下列需求。

| Assets功能 | Experience Manager版本和支援需求 |
|--- |--- |
| Asset Link預設有效 | Experience Manager6.5和6.5.2或更新版本。 </br>Experience Manager6.4.4和6.4.6或更新版本。 </br>Adobe建議先安裝最新的[Experience ManagerService Pack (SP)](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html)，再使用AAL。 |
| Asset Link可在安裝套件後運作 | 若是Experience Manager6.4.0 - 6.4.3，請安裝[adobe-asset-link-support](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/featurepack/adobe-asset-link-support)套件。 |
| Adobe Stock整合 | Experience Manager 6.4.2或更新版本 |
| 視覺或相似性搜尋 | Experience Manager 6.5.0或更新版本 |


## 使用設定套件設定Experience Manager {#configure-using-package}

Adobe建議您安裝[adobe-asset-link-config](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/adobe-asset-link-config)設定套件以自動執行大部分的設定工作，然後再執行一些手動工作。 或者，您也可以[手動](#manual-configuration)設定。

>[!CAUTION]
>
>如果您的Experience Manager執行個體設定為使用Adobe IMS帳戶登入的使用者，請勿使用設定套件。 請改為[手動設定](#manual-configuration)您的Experience Manager執行個體。

1. 若要開啟封裝管理員，請在Experience Manager網頁介面中，存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 部署]** > **[!UICONTROL 封裝共用]**。 安裝`adobe-asset-link-config`封裝。

1. 存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。 找到&#x200B;**[!UICONTROL AdobeGranite OAuth IMS提供者]**&#x200B;設定，然後按一下以編輯它。

   設定下列屬性並儲存變更。

   * [!UICONTROL 群組對應]：除非需要，否則留空。 如需詳細資訊，請參閱[群組對應](#group-mapping)。
   * [!UICONTROL 組織]：輸入您在Adobe Admin Console中使用的組織ID。 如需有關組織ID的詳細資訊，請參閱[建立使用者群組](https://helpx.adobe.com/enterprise/using/create-aal-user-group.html)。

1. 找到&#x200B;**[!UICONTROL AdobeGranite Bearer驗證處理常式]**&#x200B;組態，然後按一下以編輯它。

   將&#x200B;**[!UICONTROL InDesignAem2]**&#x200B;使用者端ID新增至&#x200B;**[!UICONTROL 允許的OAuth使用者端ID]**&#x200B;設定屬性。


## 手動設定Experience Manager {#manual-configuration}

如果您選擇不使用設定套件，或您的Experience Manager部署設定為支援使用者使用Adobe IMS帳戶登入，請手動設定Experience Manager。

若要手動設定Experience Manager：

1. 若要存取組態管理員，請存取&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 作業]** > **[!UICONTROL 網頁主控台]**。 從頂端的功能表選取&#x200B;**[!UICONTROL OSGi]** > **[!UICONTROL 組態]**。

1. 找到&#x200B;**[!UICONTROL AdobeGranite OAuth IMS提供者]**&#x200B;設定，然後按一下以編輯它。

   設定下列組態，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   * [!UICONTROL 授權端點]： ` https://ims-na1.adobelogin.com/ims/authorize/v1`
   * [!UICONTROL 權杖端點]： ` https://ims-na1.adobelogin.com/ims/token/v1`
   * [!UICONTROL 設定檔端點]： ` https://ims-na1.adobelogin.com/ims/profile/v1`
   * [!UICONTROL 驗證URL]： ` https://ims-na1.adobelogin.com/ims/validate_token/v1`
   * [!UICONTROL 組織]：設定為[Adobe Admin Console](https://adminconsole.adobe.com/)中的組織識別碼。
   * [!UICONTROL 群組對應]：除非您有特殊的大小寫，否則請留空。 如需詳細資訊，請參閱[群組對應](#group-mapping)。

1. 找到&#x200B;**[!UICONTROL AdobeGranite Bearer驗證處理常式]**&#x200B;組態，然後按一下以編輯它。

   將下列使用者端ID新增至&#x200B;**[!UICONTROL 允許的OAuth使用者端ID]**&#x200B;設定屬性： `InDesignAem2, cc-europa-desktop_0_1, cc-europa-desktop_1_0, cc-europa-desktop_2_0, cc-europa-desktop_3_0, cc-europa-desktop_4_0, cc-europa-desktop_5_0, cc-europa-desktop_6_0, cc-europa-desktop_7_0, cc-europa-desktop_8_0, cc-europa-desktop_9_0, and cc-europa-desktop_10_0`。

   若要新增每個`Client ID`，請按一下`+`。 新增所有ID後，按一下&#x200B;**[!UICONTROL 儲存]**。

1. 在&#x200B;**[!UICONTROL AdobeGranite OAuth應用程式與提供者]**&#x200B;設定中，檢查現有的&#x200B;**[!UICONTROL AdobeGranite OAuth驗證處理常式]**&#x200B;執行個體。 如果您找到具有`Config ID`值`ims`的執行個體，請將其用於此程式中的指示。 否則，按一下`+`以建立設定執行個體。 設定下列屬性值，然後按一下&#x200B;**[!UICONTROL 儲存]**。

   * [!UICONTROL 使用者端識別碼]：不變更
   * [!UICONTROL 使用者端密碼]：不變更
   * [!UICONTROL 設定識別碼]： ` ims`
   * [!UICONTROL 領域]： `AdobeID, OpenID, read_organizations` （其他值可能也在設定中）
   * [!UICONTROL 提供者識別碼]： ` ims`
   * [!UICONTROL 建立使用者]： ` Checked`
   * [!UICONTROL 使用者ID屬性]：新建立的組態為`Email`。 否則，請勿變更。

1. 找到具有&#x200B;**[!UICONTROL 同步處理常式名稱]** `ims`的&#x200B;**[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]**&#x200B;設定，然後按一下以編輯它。

   設定下列組態屬性，然後按一下[儲存]。****

   * [!UICONTROL 使用者到期時間與使用者成員資格到期]：時間以&#39;m&#39;為單位且後面沒有空格。 例如，`15m`持續15分鐘。 如需詳細資訊，請參閱[群組對應](#group-mapping)。
   * [!UICONTROL 使用者自動成員資格]：不變更
   * [!UICONTROL 使用者動態成員資格]： ` Deslect`

1. 找到&#x200B;**[!UICONTROL AdobeGranite OAuth驗證處理常式]**&#x200B;設定，然後按一下以編輯它。 若不進行任何變更，請按一下[儲存]。****

1. 若要調整持有者驗證處理常式的相對優先順序，請在CRXDE中導覽至`/apps/system/config`。 找到`com.adobe.granite.auth.oauth.impl.BearerAuthenticationHandler.config`並開啟其組態。 最後，新增`service.ranking=I"-10"`。 儲存變更。

   >[!NOTE]
   >
   >以持有人權杖驗證的每個請求都會產生呼叫Adobe IMS、使用者同步和在Experience Manager中建立登入權杖的額外負荷。 為了克服這項額外負荷，Adobe Asset Link會擷取在Experience Manager回應中傳回的登入權杖，並隨後續請求傳送。 為了讓此程式運作，必須調整承載驗證處理常式的相對優先順序。

1. （選擇性）如果Experience Manager使用者的電子郵件ID中有大寫或混合大小寫的網域名稱，請在Experience ManagerWeb主控台的&#x200B;**[!UICONTROL AdobeGranite ACP平台設定]**&#x200B;中選取&#x200B;**[!UICONTROL 將鎖定使用者變更為小寫]**。

## 移轉至企業檔案後的其他設定 {#configure-migration-activity}

Adobe Asset Link使用者可連線至Experience Manager，允許從企業(CCE)組織的主要Creative CloudIMS登入。 Experience Manager會使用使用者端ID來識別允許的IMS組織。 在移轉至企業設定檔後，需要為IMS組織設定使用者端ID和秘密金鑰，以便Experience Manager持有者驗證處理常式。 如需企業基本資料的詳細資訊，請參閱[Adobe基本資料簡介](https://helpx.adobe.com/enterprise/kb/introducing-adobe-profiles.html)。

只有在您使用不同的Adobe IMS組織進行企業版(CCE)的Experience Manager和Creative Cloud，且在這兩個組織之間建立網域信任關係時，才需要額外設定。

>[!NOTE]
>
>* Experience Manager6.5.11.0中提供企業設定檔的修正。
>* 如果您透過Experience Manager和CCE使用相同的Adobe IMS組織，現有設定仍可繼續運作。


**必備條件**

1. 為AAL設定了持有者驗證且正常運作的Experience Manager執行個體。
1. 在您的Experience Manager6.5執行個體上安裝下列套件(Service Pack 11)。

   [下載Experience Manager6.5.11.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. 請連絡[!UICONTROL 客戶支援]，以取得您IMS組織的持有者驗證的使用者端ID和秘密金鑰。

以下是移轉至Business Profiles後所需的額外設定：

1. 在&#x200B;**[!UICONTROL AdobeGranite OAuth IMS設定提供者]** (`com.adobe.granite.auth.ims.impl.ImsConfigProviderImpl`)中，設定：

   * OAuth設定ID (`oauth.configmanager.ims.configid`)： `ims` （驗證一次，您可能已設定它）

   * IMS擁有實體(`ims.owningEntity`)：您的IMS組織ID

   ![IMS設定ID](assets/bearer-authentication1.png)

1. 開啟&#x200B;**[!UICONTROL 持有者驗證處理常式]**&#x200B;設定，並將從[!UICONTROL 客戶支援]取得的使用者端ID新增至&#x200B;**[!UICONTROL 允許的OAuth使用者端ID]**&#x200B;清單。

   ![新增使用者端識別碼](assets/add-clientid-bearer-auth.png)

1. 開啟&#x200B;**[!UICONTROL AdobeGranite OAuth應用程式和提供者]**&#x200B;設定，並新增從客戶支援取得的&#x200B;**[!UICONTROL 使用者端識別碼]**&#x200B;和&#x200B;**[!UICONTROL 使用者端密碼]** （密碼金鑰）。

   請確定&#x200B;**[!UICONTROL 設定識別碼]**&#x200B;欄位(`oauth.config.id`)包含的值與上述&#x200B;**[!UICONTROL OAuth設定識別碼]**&#x200B;欄位(`oauth.configmanager.ims.configid`)中提供的值相同。

   ![驗證使用者端識別碼](assets/clientid-secretkey.png)

1. 開啟&#x200B;**[!UICONTROL AdobeGranite IMS叢集Exchange Token前置處理器]**&#x200B;設定，並將其設定為`enable`。

## 管理使用者存取控制 {#user-access}

本節說明如何管理使用者及其對Experience Manager存放庫的存取權。

### 群組對應 {#group-mapping}

群組對應會決定Experience Manager中的群組如何對應至Adobe IMS中的群組。 在授予Adobe Asset Link使用者存取Experience Manager Assets的許可權中，資料來源扮演重要角色。

與Adobe Asset Link搭配使用時，Experience Manager會將使用者管理功能委派給Adobe IMS。 它會自動建立對應至Adobe IMS中使用者和群組的使用者和群組。 此外，它會同步Experience Manager中的使用者、群組和群組成員資格，以符合Adobe IMS中的使用者、群組和群組成員資格。

例如，假設AdobeAsset Link使用者是Adobe IMS群組assetlink使用者成員。 在此情況下，當該Adobe IMS群組中的使用者首次連線到Experience Manager Asset Link時，會在Adobe中建立名為assetlink-users的同步群組。 Adobe IMS群組中的每位新使用者首次透過Experience Manager Asset Link連線至Experience Manager時，都會新增至Adobe中的對應群組。

與Adobe IMS中群組相對應且已同步的Experience Manager群組，可以直接授予存取權，或透過使其成為其他群組的成員。 以下是如何管理許可權的範例。

![群組範例](assets/group-examples.png)

下列規則適用於Experience Manager中的群組對應：

* 請確定&#x200B;**[!UICONTROL AdobeGranite OAuth IMS提供者]**&#x200B;設定中的&#x200B;**[!UICONTROL 群組對應]**&#x200B;屬性是空白的。
* 當使用者驗證時，**[!UICONTROL Apache Jackrabbit Oak Default Sync Handler]**&#x200B;設定中的&#x200B;**[!UICONTROL 使用者到期時間]**&#x200B;屬性中的時段已過，就會評估Adobe資產連結使用者群組成員資格。 目前，您可以在Experience Manager中新增和移除使用者，以便與Adobe IMS中的專案同步。
* 避免群組名稱衝突。 確保在Adobe IMS中建立的群組所使用的名稱（以管理使用者）與所有Experience Manager系統群組名稱均不同。

  例如，請確定它們與`dam-users`群組及Experience Manager管理員建立的群組不同。

  若其Adobe IMS群組的名稱與Experience Manager系統群組或手動建立的群組名稱衝突，則不會使用該IMS群組來控制使用者許可權。
* 如果Adobe IMS使用者連線至Experience Manager執行個體(使用者名稱與先前建立的Experience Manager使用者衝突)，則會為Adobe IMS使用者指定另一個名稱，並新增編號使其唯一。

**安裝第一次存取控制**

透過Adobe Asset Link連結連結的使用者只有在獲得必要許可權後，才能檢視資產並與之互動。 上述[群組對應](#group-mapping)區段會討論使用者群組如何在Experience Manager中建立，其會對應並與Adobe IMS中您組織的使用者群組同步。 建議Experience Manager管理員使用這些群組來管理Adobe Asset Link使用者的存取控制。

對於與Adobe IMS群組（用於管理使用者存取控制）同步的每個Experience Manager群組：

1. 確保群組擁有可用於從Adobe Asset Link進行初始連線的成員。
1. 使用該使用者登入Adobe Asset Link，並連線到Experience Manager。 此連線預期會失敗。
1. 在Experience Manager中，找出與Adobe IMS中群組對應的群組，並授予其所需的存取控制。 例如，新群組成為dam-users群組的成員。
1. 關閉Adobe資產連結並重新啟動Creative Cloud應用程式。
1. 若要確認使用者是否具有預期的存取權，請重新開啟Adobe資產連結。

執行這些步驟後，同一群組中的其他使用者可在第一次嘗試時透過Adobe Asset Link連線到Experience Manager。 他們會自動擁有與群組中其他使用者相同的許可權。

## 管理Experience Manager資產連結的Adobe使用者 {#manage-users}

Adobe Asset Link使用者在登入Creative Cloud應用程式後，就能與Experience Manager連線。 此驗證使用Adobe IMS技術，並在Experience Manager中建立使用者資訊（如果沒有）。 Experience Manager企業客戶通常可使用與Experience Manager整合的外部身分提供者來管理其使用者。 身分提供者包括Adobe IMS和其他使用SAML和LDAP通訊協定的產品。 或者，您也可以在Experience Manager中在本機建立和管理使用者。

如果符合下列條件，從Adobe Asset Link連線至Experience Manager的使用者與先前直接登入儲存於Experience Manager中的現有使用者資訊不會發生衝突：

* 所有用於直接登入Experience Manager的使用者名稱，與Adobe IMS中用於Creative Cloud登入的使用者名稱不同。
* Adobe IMS會作為直接Experience Manager登入的身分提供者。
* 使用者先從Adobe資產連結連線到Experience Manager，再使用相同帳戶直接Experience Manager登入。


另一方面，在下列情況下，必須更新直接由Experience Manager登入所建立的使用者資訊，才能與Adobe Asset Link搭配使用：

* 相同的使用者名稱（例如使用者的電子郵件地址）會用於兩者 — 使用Adobe IMS的Creative Cloud帳戶，以及Adobe IMS以外的外部身分提供者帳戶。
* 相同的使用者名稱會用於兩者 — Creative Cloud中的帳戶和本機Experience Manager帳戶。
* Adobe IMS中的Creative Cloud帳戶為Federated ID，由與Experience Manager整合以供直接登入的相同外部身分提供者提供。

透過這些案例建立的使用者沒有使用者所需的屬性，而是與Adobe IMS同步。

若要在Experience Manager中更新這類使用者以使用Adobe Asset Link：

1. 在Experience ManagerWeb主控台中，找到&#x200B;**[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]**&#x200B;設定，然後按一下以編輯它。 取消選取&#x200B;**[!UICONTROL 外部身分保護]**&#x200B;核取方塊，然後按一下&#x200B;**[!UICONTROL 儲存]**。
1. 若要在Experience Manager中存取「使用者管理」介面，請瀏覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 安全性]** > **[!UICONTROL 使用者]**。 選取您要更新的使用者，然後記下該使用者的瀏覽器URL路徑結尾，從`/home/users`開始。 或者，您可以在CRXDE中搜尋使用者名稱。 範例使用者路徑： `/home/users/x/xTac082TDh-guJzzG7WM`。
1. 在CRXDE中，選取使用者路徑、選取使用者節點，並選取中下區域的&#x200B;**[!UICONTROL 屬性]**&#x200B;索引標籤來檢視節點的屬性。 此節點的`jcr:primaryType`屬性值是`rep:User`。
1. 在&#x200B;**[!UICONTROL 屬性]**&#x200B;索引標籤區域的底部，輸入`rep:externalId`的`Name`值、`String`的`Type`值以及`rep:authorizableId`；`ims`的`Value`值，其中`rep:authorizableId`是節點的`rep:authorizableId`屬性值。 （使用分號且不含空格，以區隔`rep:authorizableId`值與`ims`。）
1. 按一下新專案右側的&#x200B;**[!UICONTROL [新增]]**&#x200B;按鈕，然後按一下&#x200B;**[!UICONTROL [儲存全部]]**。
1. 對您要升級的任何其他使用者重複步驟2到5，以搭配Adobe Asset Link使用。
1. 在Experience ManagerWeb主控台中，找到&#x200B;**[!UICONTROL Apache Jackrabbit Oak External PrincipalConfiguration]**&#x200B;設定，然後按一下以編輯它。 取消選取&#x200B;**[!UICONTROL 外部身分保護]**&#x200B;核取方塊，然後按一下&#x200B;**[!UICONTROL 儲存]**。

>[!NOTE]
>
>如果數分鐘內未還原服務，請重新啟動Experience Manager以允許成功驗證。

進行此變更後，更新的Experience Manager使用者可以連線至Adobe資產連結，並繼續使用直接登入方法登入更新前使用的Experience Manager。 成功使用Adobe IMS驗證後，Experience Manager使用者設定檔資訊就會與Adobe IMS中的使用者設定檔同步。

有一個方法可以執行多個Experience Manager使用者的大量移轉，讓他們能夠使用Adobe資產連結。 如需啟用此選項的詳細資訊和協助，請聯絡Adobe服務。

作為這些步驟的替代方法，在某些情況下，Adobe Asset Link使用者可能會獲得快速存取Experience Manager的許可權。 在這種情況下，在與Adobe Asset Link連線之前，可以透過Experience Manager使用者管理或Experience ManagerCRXDE找到並刪除預先存在的使用者資訊。 新的使用者資訊會在連線後以Experience Manager建立。 只有在您確定沒有重要資料新增為使用者節點的子項時，才使用此方法。 這類額外資料是指任何節點，它是`tokens`、`preferences`、`profile`、`profiles`、`profiles/public`和`rep:policy/*`節點以外的使用者節點的子節點。

## 自動啟動工作流程以有條件地處理資產 {#auto-start-workflow}

在Experience Manager6.4和Experience Manager6.5中，管理員可設定工作流程，以根據預先定義的條件自動執行及處理資產。

例如，對業務線使用者和行銷人員來說，例如在幾個特定資料夾上建立自訂工作流程時，此設定會很有用。 假設機構拍照時的所有資產都可加上浮水印，或是自由譯者上傳的所有資產都可經過處理，以建立特定轉譯。

如需詳細資訊和Experience Manager設定，請參閱[在資產上自動執行工作流程](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html#auto-execute-workflow-on-some-assets)。


## 在Experience Manager6.4.x版本中建立自訂索引 {#create-custom-index}

Experience Manager包含用於查詢的索引。 為指定版本建立下列自訂索引。 Experience Manager6.5.0預設包含此索引。 Adobe資產連結需要此索引來判斷使用者已簽出哪些資產。

1. 在CRXDE中，找出`/oak:index`節點。 建立名為`cqDrivelock`的節點，並將其`Type`設定為`oak:QueryIndexDefinition`。

1. 將下列屬性新增至新節點並儲存變更：

   * `Name: type; Type: string; Value: property`

   * `Name: propertyNames; Type: Name[] (click the "Multi" button); Value: cq:drivelock`


## 設定視覺或相似性搜尋 {#configure-visual-similarity-search}

「視覺搜尋」功能可讓您使用「Adobe資產連結」面板，在AEM Assets存放庫中搜尋視覺上類似的資產。 6.5.0或更新版本提供此功能，而且只會搜尋已編制索引的資產。 如需詳細資訊，請參閱[如何設定視覺化搜尋](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/search-assets.html#configvisualsearch)。

## 產生Adobe InDesign的「僅供刊登」轉譯 {#fpo-renditions}

Experience Manager提供僅用於放置的轉譯(FPO)。 這些FPO轉譯的檔案大小較小，但外觀比例相同。 如果資產無法使用FPO轉譯，Adobe InDesign會改用原始資產。 此遞補機制可確保創意工作流程無任何中斷地進行。 如需詳細資訊，請參閱[產生FPO轉譯](/help/assets/configure-fpo-renditions.md)。


## 整合Adobe Stock {#adobe-stock-integration}

組織將其Adobe Stock帳戶與Experience Manager Assets整合。 它可協助行銷人員為其創意和行銷專案提供授權的高品質、免版稅像片、向量、插圖、影片、範本和3D資產。 創意專業人士可以使用Asset Link面板來使用這些資產。

若要與Adobe Stock整合，請參閱Experience Manager Assets中的[Adobe Stock資產](/help/assets/aem-assets-adobe-stock.md)。 若要與Adobe Stock整合，需要Experience Manager 6.4.2或更新版本。


## 疑難排解Experience Manager相關問題 {#troubleshoot}


如果您在設定或使用Adobe Asset Link時遇到問題，請嘗試下列步驟：

* 確定您的部署符合先決條件。 具體來說，請確定已安裝適當的功能套件或套件。
* 請聯絡貴組織的合作夥伴或系統整合商。
* 如果您的Creative Cloud使用者無法在已取出資產中進行驗證，請檢查電子郵件ID中網域名稱的大小寫。 若要修正，請參閱[手動組態](#manual-configuration)。
* 如需詳細資訊，請參閱[疑難排解Asset Link](https://helpx.adobe.com/enterprise/kb/asset-link-troubleshooting.html)。


>[!MORELIKETHIS]
>
>* [關於 Adobe Asset Link](https://helpx.adobe.com/tw/enterprise/using/adobe-asset-link.html)
>* [在Creative Cloud案頭應用程式中使用資產連結並管理資產](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html)
>* [設定Adobe Experience Manager Assetsas a Cloud Service](https://helpx.adobe.com/tw/enterprise/using/configure-aem-assets-for-asset-link.html)。
