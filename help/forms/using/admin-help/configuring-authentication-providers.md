---
title: 配置身份驗證提供程式
seo-title: Configuring authentication providers
description: 添加、編輯或刪除身份驗證提供程式、更改身份驗證設定，以及閱讀有關用戶即時配置的資訊。
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# 配置身份驗證提供程式 {#configuring-authentication-providers}

混合域需要至少一個身份驗證提供程式，而企業域需要至少一個身份驗證提供程式或目錄提供程式。

如果使用SPNEGO啟用SSO，請添加已啟用SPNEGO的Kerberos身份驗證提供程式和作為備份的LDAP提供程式。 如果SPNEGO不工作，此配置將允許使用用戶ID和密碼進行用戶身份驗證。 （請參閱[使用SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego)啟用SSO。）

## 添加身份驗證提供程式 {#add-an-authentication-provider}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中的現有網域。 如果要添加新域的身份驗證，請參閱[添加企業域](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain)或[添加混合域](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain)。
1. 按一下「添加身份驗證」 ，然後在「身份驗證提供程式」清單中，根據您的組織使用的身份驗證機制選擇一個提供程式。
1. 提供頁面上所需的任何其他資訊。 （請參閱[驗證設定](configuring-authentication-providers.md#authentication-settings)。）
1. （選用）按一下測試以測試設定。
1. 按一下「確定」，然後再次按一下「確定」。

## 編輯現有的驗證提供程式 {#edit-an-existing-authentication-provider}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在清單中按一下適當的網域。
1. 在顯示的頁面上，從清單中選取適當的驗證提供者，並視需要進行變更。 （請參閱[驗證設定](configuring-authentication-providers.md#authentication-settings)。）
1. 按一下「確定」。

## 刪除驗證提供程式 {#delete-an-authentication-provider}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在清單中按一下適當的網域。
1. 選擇驗證提供程式要刪除的複選框，然後按一下「刪除」。
1. 在顯示的確認頁上按一下「確定」，然後再次按一下「確定」。

## 驗證設定 {#authentication-settings}

下列設定可供使用，具體取決於您選擇的域類型和驗證類型。

### LDAP設定 {#ldap-settings}

如果要為企業域或混合域配置身份驗證，並選擇LDAP身份驗證，則可以選擇使用目錄配置中指定的LDAP伺服器，或者可以選擇其他LDAP伺服器以用於身份驗證。 如果選擇不同的伺服器，則您的用戶必須存在於兩個LDAP伺服器上。

要使用在目錄配置中指定的LDAP伺服器，請選擇LDAP作為身份驗證提供程式，然後按一下確定。

要使用其他LDAP伺服器來執行身份驗證，請選擇LDAP作為身份驗證提供程式，然後選擇「自定義LDAP身份驗證」複選框。 將顯示以下配置設定。

**伺服器：** （強制）目錄伺服器的完全限定域名(FQDN)。例如，對於example.com網路上名為x的電腦，FQDN為x.example.com。 可以使用IP地址來取代FQDN伺服器名稱。

**埠：** （強制）目錄伺服器使用的埠。如果使用安全套接字層(SSL)協定通過網路發送身份驗證資訊，則通常為389或636。

**SSL:** （強制）指定在透過網路傳送資料時，目錄伺服器是否使用SSL。預設為「否」。 當設定為「是」時，應用程式伺服器的Java™運行時環境(JRE)必須信任相應的LDAP伺服器證書。

**綁定** （強制）指定如何訪問目錄。

**匿名：** 不需要用戶名或密碼。

**使用者：** 需要驗證。在「名稱」框中，指定可訪問目錄的用戶記錄的名稱。 最好輸入用戶帳戶的完整可分辨名稱(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」框中，指定關聯的密碼。 選擇「用戶」作為「綁定」選項時，需要這些設定。

**擷取基本DN:** （非必要）擷取基本DN並在下拉式清單中顯示。當您有多個基本DN且需要選取值時，此設定很實用。

**基本DN:** （必要）用作從LDAP階層同步使用者和群組的起點。最好在層次結構的最低級別指定基本DN，該DN包含所有需要同步服務的用戶和組。 請勿在此設定中加入使用者的DN。 要同步特定用戶，請使用「搜索篩選器」設定。

**以填入頁面：** （非必要）選取此選項時，會以對應的預設LDAP值填入「使用者」和「群組」設定頁面上的屬性。

**搜尋篩選：** （必要）用來尋找與使用者相關聯的記錄的搜尋篩選。請參閱搜尋篩選語法。

### Kerberos設定 {#kerberos-settings}

如果您正在為企業域或混合域配置身份驗證並選擇Kerberos身份驗證，則可使用以下設定。

**DNS IP:** 執行AEM表單之伺服器的DNS IP位址。在Windows上，可以通過在命令行中運行ipconfig /all來確定此IP地址。

**KDC主機：** 用於身份驗證的Active Directory伺服器的完全限定主機名或IP地址。

**服務用戶：** 如果您使用Active Directory 2003，則此值是為窗體中的服務主體建立的映 `HTTP/<server name>`射。如果您使用Active Directory 2008，則此值是服務主體的登錄ID。 例如，假設服務主體名為um spnego，用戶ID為spnegodemo，映射為HTTP/example.yourcompany.com。 使用Active Directory 2003，可將服務用戶設定為HTTP/example.yourcompany.com。 使用Active Directory 2008，可將Service User設定為spnegodemo。 （請參閱使用SPNEGO啟用SSO。）

**服務領域：** Active Directory的域名

**服務密碼：** 服務用戶的密碼

**啟用SPNEGO:** 啟用SPNEGO用於單一登入(SSO)。（請參閱使用SPNEGO啟用SSO。）

### SAML設定 {#saml-settings}

如果您要為企業或混合網域設定驗證，並選取SAML驗證，則可使用下列設定。 如需其他SAML設定的相關資訊，請參閱[設定SAML服務提供者設定](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings)。

**請選取要匯入的SAML身分提供者中繼資料檔案：** 按一下「瀏覽」，選取從IDP產生的SAML身分提供者中繼資料檔案，然後按一下「匯入」。系統會顯示來自IDP的詳細資訊。

**標題：** 別名，表示為EntityID表示的URL。企業和本機使用者的登入頁面也會顯示標題。

**身分提供者支援用戶端基本驗證：** 當IDP使用SAML工件解決設定檔時，會使用用戶端基本驗證。在此設定檔中，使用者管理會將連線回在IDP執行的Web服務，以擷取實際的SAML斷言。 IDP可能需要驗證。 如果IDP確實需要驗證，請選取此選項，並在提供的方塊中指定使用者名稱和密碼。

**自訂屬性：** 可讓您指定其他屬性。其他屬性是由新行分隔的name=value對。

如果使用對象綁定，則需要以下自定義屬性。

* 新增下列自訂屬性，以指定代表AEM表單服務提供者的使用者名稱，該使用者名稱將用來驗證IDP工件解決服務。
   `saml.idp.resolve.username=<username>`

* 添加以下自定義屬性以指定`saml.idp.resolve.username`中指定的用戶的密碼。
   `saml.idp.resolve.password=<password>`

* 新增下列自訂屬性，以允許服務提供者在建立與SSL上的工件解決服務的連線時忽略憑證驗證。
   `saml.idp.resolve.ignorecert=true`

### 自訂設定 {#custom-settings}

如果您要為企業或混合域配置身份驗證，並選擇「自定義身份驗證」，請選擇自定義身份驗證提供程式的名稱。

## 用戶即時布建 {#just-in-time-provisioning-of-users}

在通過驗證提供程式成功驗證用戶後，即時置備將在用戶管理資料庫中自動建立用戶。 相關角色和群組也會以動態方式指派給新使用者。 您可以為企業和混合網域啟用及時布建。

此程式說明傳統驗證在AEM表單中的運作方式：

1. 當使用者嘗試登入AEM表單時，「使用者管理」會依序將其憑證傳遞至所有可用的驗證提供者。 （登錄憑據包括用戶名/密碼組合、Kerberos票證、PKCS7簽名等。）
1. 驗證提供程式驗證憑據。
1. 然後，驗證提供程式將檢查用戶是否存在於用戶管理資料庫中。 可能的狀態如下：

   **** 存在如果用戶是最新的和未鎖定的，則用戶管理返回身份驗證成功。但是，如果用戶不是當前用戶或已鎖定用戶，則User Management將返回身份驗證失敗。

   **不存在用戶** 管理返回身份驗證失敗。

   **** InvalidUser Management返回身份驗證失敗。

1. 評估驗證提供程式返回的結果。 如果驗證提供程式返回驗證成功，則允許用戶登錄。 否則，「使用者管理」會與下一個驗證提供者檢查（步驟2-3）。
1. 如果沒有可用的驗證提供程式驗證用戶憑據，則返回驗證失敗。

啟用即時布建時，如果其中一個驗證提供者驗證其憑證，則會在「使用者管理」中動態建立新使用者。 （在上述程式的步驟3之後。）

如果沒有及時設定，當用戶成功驗證但在用戶管理資料庫中找不到用戶時，驗證將失敗。 即時預配在驗證過程中添加一個步驟，以建立用戶並為用戶分配角色和組。

### 為域啟用即時配置 {#enable-just-in-time-provisioning-for-a-domain}

1. 編寫實現IdentityCreator和AssignmentProvider介面的服務容器。 (請參閱[使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63)。)
1. 將服務容器部署到表單伺服器。
1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。

   選擇現有域或按一下「新建企業域」。

1. 若要建立網域，請按一下「新增企業網域」或「新增混合網域」。 要編輯現有域，請按一下域的名稱。
1. 選擇「Enable Just Time Provisioning（啟用準時預配）」。

   ***注意&#x200B;**:如果缺少「Enable Just In Time Provisioning（啟用準時置備）」複選框，請按一下「Home（首頁）」>「Settings（設定）」>「User Management（用戶管理）」>「Configuration（配置）」>「Advanced System Attributes（高級系統屬性）」，然後按一下「Reload（重新載入）」。*

1. 添加身份驗證提供程式。 添加身份驗證提供程式時，在「新建身份驗證」螢幕上，選擇註冊的身份建立者和分配提供程式。 （請參閱[配置身份驗證提供程式](configuring-authentication-providers.md#configuring-authentication-providers)。）
1. 儲存網域。
