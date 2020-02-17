---
title: 新增網域
seo-title: 新增網域
description: 瞭解如何使用「網域管理」設定和網域名稱和ID的一般考量，新增企業、本機或混合網域。
seo-description: 瞭解如何使用「網域管理」設定和網域名稱和ID的一般考量，新增企業、本機或混合網域。
uuid: 3ae1e5d4-ea5b-4e0b-be97-3957c3702d5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4004ffe-c981-487d-b803-dc4492ae5998
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 新增網域 {#adding-domains}

## 新增企業網域 {#add-an-enterprise-domain}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建企業網域」。
1. 在ID方塊中，輸入網域的唯一識別碼，並在「名稱」方塊中，輸入網域的描述性名稱。 (請參 [閱網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids)。)
1. 指定是否啟用帳戶鎖定。 (請參 [閱設定帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings))。依預設，會選取「啟用帳戶鎖定」。
1. 按一下「新增驗證」，然後在「驗證提供者」清單中，根據貴組織使用的驗證機制，選取提供者。 可能的值是LDAP、Kerberos、SAML或自定義驗證提供程式。

   如果選擇LDAP，則可以使用在目錄配置中指定的LDAP伺服器，也可以選擇不同的LDAP伺服器以用於驗證。 如果您選擇不同的伺服器，則用戶必須同時存在於兩個LDAP伺服器上。

1. 提供頁面所需的其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。)
1. 添加目錄或自定義服務提供程式介面(SPI)。 (請參 [閱添加目錄或自定義SPI](/help/forms/using/admin-help/configuring-directories.md#adding-directories-or-custom-spis)。)
1. 按一下「完成」，然後按一下「確定」。

建立企業域後，請手動同步目錄或建立觸發器以在用戶管理可以使用該目錄之前執行同步。 然後，您可以設定目錄同步調度並根據需要執行手動同步。 (請參 [閱同步目錄](/help/forms/using/admin-help/synchronizing-directories.md#synchronizing-directories)。)

## 新增本機網域 {#add-a-local-domain}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新增本機網域」。
1. 在ID方塊中，輸入網域的唯一識別碼，並在「名稱」方塊中，輸入網域的描述性名稱。 (請參 [閱網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids)。)
1. 指定是否啟用帳戶鎖定，然後按一下「確定」。 (請參 [閱設定帳戶鎖定設定](/help/forms/using/admin-help/configure-account-locking-settings.md#configure-account-locking-settings))。依預設，會選取「啟用帳戶鎖定」。

## 新增混合網域 {#add-a-hybrid-domain}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建混合網域」。
1. 在ID方塊中，輸入網域的唯一識別碼，並在「名稱」方塊中，輸入網域的描述性名稱。 (請參 [閱網域名稱和ID的重要考量](adding-domains.md#important-considerations-for-domain-names-and-ids)。)
1. 按一下「新增驗證」，然後在「驗證提供者」清單中，根據貴組織使用的驗證機制，選取提供者。 可能的值是LDAP、Kerberos、SAML或自定義驗證提供程式。
1. 提供頁面所需的其他資訊。 (請參閱 [驗證設定](/help/forms/using/admin-help/configuring-authentication-providers.md#authentication-settings)。)
1. 按一下「OK（確定）」 ，然後再次按一下「OK（確定）」。

## 域名和ID的重要注意事項 {#important-considerations-for-domain-names-and-ids}

選擇網域名稱和ID時，請記住下列事項：

### 一般考量 {#general-considerations}

* 使用DB2以外的資料庫提供程式時，域ID最多可包含50個位元組。 如果您使用單位元組ASCII字元，限制為50個字元。 如果網域識別碼包含多位元組字元，此限制會降低。 例如，如果您建立的網域的識別碼包含3位元組字元，則限制為16個字元。 此外，您不能建立包含4位元組字元的網域。 如果您建立的網域ID超過此限制，AEM表單將處於不穩定狀態。 要從此不穩定狀態中恢復，請參閱本頁的「 [Remove a domain that contains extended or multi-byte characters](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」（刪除包含擴展字元或多位元組字元的域）。
* 在AEM表單中可建立的企業網域和本機網域數目，視每個網域ID的長度而定。 當您新增企業或混合網域時，「使用者管理」會更新AEM表單設定檔(config.xml)的「AuthProviders」節點中的configInstance字串。 configInstance字串包含以冒號分隔的清單，列出與授權提供者相關聯之所有網域的絕對路徑。 此字串的大小限制為8192個字元。 達到此限制時，您無法建立其他網域。

### 使用DB2時的注意事項 {#considerations-when-using-db2}

在AEM表單資料庫中使用DB2時，網域ID的允許長度上限取決於使用的字元類型：

* 100個單位元組(ASCII)（例如，英文、法文或德文的字元）
* 50個雙位元組（例如，中文、日文或韓文使用的字元）
* 25個四位元組（例如，繁體中文使用的字元）

### 使用MySQL時的注意事項 {#considerations-when-using-mysql}

將MySQL用作AEM表單資料庫時，會套用下列限制：

* 網域ID和網域名稱僅使用單位元組(ASCII)字元。 如果您使用延伸ASCII字元，AEM表單將會處於不穩定狀態，如果您嘗試刪除網域，可能會擲回例外。 要從此不穩定狀態中恢復，請參閱本頁的「 [Remove a domain that contains extended or multi-byte characters](adding-domains.md#remove-a-domain-that-contains-extended-or-multi-byte-characters)」主題。
* 您無法建立兩個名稱相同但大小寫的網域。 例如，嘗試建立名為 *Adobe* 的網域時， *Adobe* 已存在，會導致錯誤。
* 「使用者管理」無法區分兩個網域名稱，這兩個網域名稱僅在使用擴充字元時不同。 例如，如果您建立名為 *abcde的網域* ，和名為 *âbcdè的網域*，則會視為相同。

### 移除包含擴充或多位元組字元的網域 {#remove-a-domain-that-contains-extended-or-multi-byte-characters}

1. 導出配置檔案，如導入和導 [出配置檔案中所述](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。
1. 開啟配置檔案，在「域」節點下，找到名稱屬性與使用擴展或多位元組字元建立的域名稱匹配的節點。 刪除與該域相關的整個節點。
1. 在資料庫中，在edcprincipaldomainentity表中搜索域：

   * 從edcprincipaldomainentity `*` 中選取。
   * 查找包含擴展字元或多位元組字元的域名，並將其狀態設定為OBSOLETE。

1. 導入更新的配置檔案，如導入和導 [出配置檔案中所述](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。

