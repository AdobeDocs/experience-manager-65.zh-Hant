---
title: 設定驗證提供者
seo-title: 設定驗證提供者
description: 新增、編輯或刪除驗證提供者、變更驗證設定，以及閱讀使用者的即時布建。
seo-description: 新增、編輯或刪除驗證提供者、變更驗證設定，以及閱讀使用者的即時布建。
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定驗證提供者 {#configuring-authentication-providers}

混合網域需要至少一個驗證提供者，而企業網域則需要至少一個驗證提供者或目錄提供者。

如果使用SPNEGO啟用SSO，請添加啟用SPNEGO的Kerberos驗證提供程式和LDAP提供程式作為備份。 如果SPNEGO不工作，此配置將啟用用戶ID和口令的用戶驗證。 (請參 [閱使用SPNEGO啟用SSO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego))。

## 新增驗證提供者 {#add-an-authentication-provider}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中的現有域。 如果要為新域添加驗證，請參 [閱添加企業域](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain)[或添加混合域](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)。
1. 按一下「新增驗證」，然後在「驗證提供者」清單中，根據貴組織使用的驗證機制，選取提供者。
1. 提供頁面所需的其他資訊。 (請參閱 [驗證設定](configuring-authentication-providers.md#authentication-settings)。)
1. （可選）按一下「測試」以測試設定。
1. 按一下「OK（確定）」 ，然後再次按一下「OK（確定）」。

## 編輯現有的驗證提供者 {#edit-an-existing-authentication-provider}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在清單中按一下適當的網域。
1. 在顯示的頁面上，從清單中選擇適當的驗證提供方，並根據需要進行更改。 (請參閱 [驗證設定](configuring-authentication-providers.md#authentication-settings)。)
1. 按一下「確定」。

## 刪除驗證提供者 {#delete-an-authentication-provider}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在清單中按一下適當的網域。
1. 選擇要刪除的驗證提供者的複選框，然後按一下刪除。
1. 在顯示的確認頁面上按一下「確定」，然後再按一下「確定」。

## Authentication settings {#authentication-settings}

下列設定可供使用，視您選擇的網域類型和驗證類型而定。

### LDAP設定 {#ldap-settings}

如果要為企業或混合域配置身份驗證並選擇LDAP身份驗證，您可以選擇使用目錄配置中指定的LDAP伺服器，也可以選擇其他LDAP伺服器進行身份驗證。 如果您選擇不同的伺服器，則用戶必須同時存在於兩個LDAP伺服器上。

要使用在目錄配置中指定的LDAP伺服器，請選擇LDAP作為驗證提供程式，然後按一下確定。

要使用不同的LDAP伺服器來執行驗證，請選擇LDAP作為驗證提供程式，然後選擇「自定義LDAP驗證」複選框。 將顯示以下配置設定。

**** 伺服器：（強制）目錄伺服器的完全限定域名(FQDN)。 例如，對於corp.example.com網路上名為x的電腦，FQDN為x.corp.example.com。 IP地址可用來代替FQDN伺服器名。

**** 埠：（必要）目錄伺服器使用的埠。 通常為389或636(如果安全通訊端層(SSL)通訊協定用於透過網路傳送驗證資訊)。

**** SSL:（必要）指定目錄伺服器在通過網路發送資料時是否使用SSL。 預設值為「否」。 當設定為「是」時，應用程式伺服器的Java™運行時環境(JRE)必須信任相應的LDAP伺服器證書。

**綁定** （強制）指定如何訪問目錄。

**** 匿名：不需要用戶名或密碼。

**** 使用者：需要驗證。 在「名稱」框中，指定可以訪問目錄的用戶記錄的名稱。 最好輸入用戶帳戶的完整唯一判別名(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」方塊中，指定相關的密碼。 當您選取「使用者」作為「系結」選項時，就需要這些設定。

**** 檢索基本DN:（非必要）擷取基本DN並在下拉式清單中顯示。 當您有多個基本DN且需要選擇值時，此設定非常有用。

**** 基本DN:（必要）用作從LDAP階層同步使用者和群組的起點。 最好在層次結構的最低級別指定基本DN，該DN包括所有需要同步服務的用戶和組。 請勿在此設定中包含使用者的DN。 若要同步特定使用者，請使用「搜尋篩選」設定。

**** 填入頁面的方式為：（非強制性）選取此選項時，使用對應的預設LDAP值填入「使用者」和「群組」設定頁面上的屬性。

**** 搜尋篩選：（必要）用於查找與用戶關聯的記錄的搜索篩選器。 請參閱搜尋篩選語法。

### Kerberos設定 {#kerberos-settings}

如果您正在為企業或混合域配置身份驗證並選擇Kerberos身份驗證，則可使用以下設定。

**** DNS IP:執行AEM表單之伺服器的DNS IP位址。 在Windows上，可以通過在命令行運行ipconfig /all來確定此IP地址。

**** KDC主機：用於驗證的Active Directory伺服器的完全限定主機名或IP地址。

**** 服務用戶：如果使用Active Directory 2003，則此值是為表單中的服務承擔者建立的映射 `HTTP/<server name>`。 如果您使用Active Directory 2008，此值是服務承擔者的登錄ID。 例如，假設服務承擔者名為um spnego，用戶ID為spnegodemo，映射為HTTP/example.corp.yourcompany.com。 在Active Directory 2003中，您將「服務用戶」設定為HTTP/example.corp.yourcompany.com。 在Active Directory 2008中，您將Service User設定為spnegodemo。 （請參閱使用SPNEGO啟用SSO）。

**** 服務領域：Active Directory的域名

**** 服務密碼：服務使用者的密碼

**** 啟用SPNEGO:啟用單一登入(SSO)的SPNEGO。 （請參閱使用SPNEGO啟用SSO）。

### SAML設定 {#saml-settings}

如果您要為企業或混合網域設定驗證並選取SAML驗證，則可使用下列設定。 如需其他SAML設定的詳細資訊，請參 [閱設定SAML服務提供者設定](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)。

**** 請選取要匯入的SAML身分提供者中繼資料檔案：按一下「瀏覽」以選取從IDP產生的SAML身分提供者中繼資料檔案，然後按一下「匯入」。 將顯示來自IDP的詳細資訊。

**** 標題：EntityID所表示之URL的別名。 標題也會顯示在企業與本機使用者的登入頁面上。

**** 身分提供者支援用戶端基本驗證：當IDP使用SAML Artifact Resolution描述檔時，會使用用戶端基本驗證。 在此設定檔中，使用者管理會連線回IDP上執行的Web服務，以擷取實際的SAML斷言。 IDP可能需要驗證。 如果IDP需要驗證，請選取此選項，並在提供的方塊中指定使用者名稱和密碼。

**** 自訂屬性：可讓您指定其他屬性。 其他屬性是由新行分隔的name=value對。

如果使用對象綁定，則需要以下自定義屬性。

* 新增下列自訂屬性，以指定代表AEM表單服務提供者的使用者名稱，此使用者名稱將用來驗證IDP Artifact Resolution服務。
   `saml.idp.resolve.username=<username>`

* 新增下列自訂屬性，以指定中指定之使用者的密碼 `saml.idp.resolve.username`。
   `saml.idp.resolve.password=<password>`

* 新增下列自訂屬性，以允許服務提供者在建立與SSL上的Artifact Resolution服務的連線時忽略憑證驗證。
   `saml.idp.resolve.ignorecert=true`

### 自訂設定 {#custom-settings}

如果您正在為企業或混合域配置驗證，並選擇「自定義驗證」，請選擇自定義驗證提供程式的名稱。

## 即時布建使用者 {#just-in-time-provisioning-of-users}

在使用者透過驗證提供者成功驗證後，即時布建會自動在使用者管理資料庫中建立使用者。 相關角色和群組也會動態指派給新使用者。 您可以為企業和混合網域啟用即時布建。

此程式說明傳統驗證在AEM表單中的運作方式：

1. 當使用者嘗試登入AEM表單時，「使用者管理」會依序將其認證傳送給所有可用的驗證提供者。 （登錄憑據包括用戶名／密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供者會驗證憑證。
1. 然後驗證提供者會檢查使用者是否存在於使用者管理資料庫中。 可能有下列狀態：

   **存在** ：如果使用者是最新且已解除鎖定，「使用者管理」會傳回驗證成功。 不過，如果使用者不是最新或已鎖定，使用者管理會傳回驗證失敗。

   **不存在** 「用戶管理」返回驗證失敗。

   **無效的** 「使用者管理」會傳回驗證失敗。

1. 驗證提供者傳回的結果會進行評估。 如果驗證提供者傳回驗證成功，則允許使用者登入。 否則，使用者管理會檢查下一個驗證提供者（步驟2-3）。
1. 如果沒有可用的驗證提供者驗證使用者憑證，則會傳回驗證失敗。

當啟用即時布建時，如果其中一個驗證提供者驗證其認證，就會在使用者管理中動態建立新使用者。 （在上述程式的步驟3之後）。

如果沒有及時提供，當用戶成功驗證但在用戶管理資料庫中未找到時，驗證將失敗。 即時布建會在驗證程式中新增一個步驟，以建立使用者並指派角色和群組給使用者。

### 為域啟用及時資源調配 {#enable-just-in-time-provisioning-for-a-domain}

1. 編寫實施IdentityCreator和AssignmentProvider介面的服務容器。 (請參 [閱「使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63)」)。
1. 將服務容器部署到表單伺服器。
1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。

   選取現有網域，或按一下「新建企業網域」。

1. 若要建立網域，請按一下「新建企業網域」或「新建混合網域」。 要編輯現有域，請按一下域的名稱。
1. 選擇「Enable Just In Time Provisioning」（啟用準時設定）。

   ***注意&#x200B;**:如果缺少「Enable Just In Time Provisioning」（啟用及時預配）複選框，請按一下「Home」（首頁）>「Settings」（設定）>「User Management」（用戶管理）>「Configuration」（配置）>「Advanced System Attributes」（高級系統屬性），然後按一下「Reload」（重新載入）。*

1. 新增驗證提供者。 新增驗證提供者時，在「新增驗證」畫面上，選取已註冊的Identity Creator和Assignment Provider。 (請參閱 [設定驗證提供者](configuring-authentication-providers.md#configuring-authentication-providers)。)
1. 儲存網域。

