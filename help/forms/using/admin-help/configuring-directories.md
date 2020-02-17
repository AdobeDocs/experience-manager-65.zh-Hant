---
title: 配置目錄
seo-title: 配置目錄
description: 瞭解如何添加、編輯和刪除目錄，以及如何配置用戶管理以使用虛擬清單視圖。
seo-description: 瞭解如何添加、編輯和刪除目錄，以及如何配置用戶管理以使用虛擬清單視圖。
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 配置目錄 {#configuring-directories}

針對您配置的每個企業域，指定驗證提供者查詢用戶資訊的目錄。 可以為域配置多個目錄。

## 添加目錄或自定義SPI {#adding-directories-or-custom-spis}

針對您配置的每個企業域，指定驗證提供者查詢用戶資訊的目錄。 您可以將目錄添加到現有企業域或要添加的新企業域。 可以為域配置多個目錄。 您還可以配置域以使用自定義服務提供商介面(SPI)進行同步。

### 添加目錄 {#add-a-directory}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建企業網域」或選取現有的企業網域。
1. 按一下「新增目錄」。
1. 在「描述檔名稱」方塊中，輸入要區分此目錄的名稱，然後按一下「下一步」。
1. 配置目錄伺服器設定。 (請參 [閱目錄設定](configuring-directories.md#directory-settings)。)
1. 要驗證是否可以與LDAP伺服器建立連接，請按一下「測試」。 如果測試失敗，請查看應用程式伺服器日誌檔案中的異常，以確定故障的根本原因。 按一下「關閉」，然後按「下一步」。
1. 選取「使用者設定」並視需要設定設定。 (請參 [閱目錄設定](configuring-directories.md#directory-settings)。)
1. 要驗證基本DN和其他配置的屬性是否收集了正確的用戶批，請按一下「測試」。 LDAP會嘗試使用提供的設定（如基本DN、搜索篩選器和所有屬性）來檢索前200條記錄。

   如果傳回使用者，結果會依屬性集顯示指派給每個欄位的值。 如果測試因為不存在的伺服器名稱、不正確的授權資訊或屬性而失敗，則會出現下列錯誤訊息：&quot;指定的搜索條件未返回任何結果&quot;。 要確定故障的根本原因，請查看應用程式伺服器日誌檔案中的異常。 按一下「關閉」，然後按「下一步」。

1. 選取「群組設定」並視需要設定設定。 (請參 [閱目錄設定](configuring-directories.md#directory-settings)。)
1. 要驗證基本DN和其他配置的屬性是否收集正確的組批，請按一下「測試」。 如果傳回群組，結果會顯示依屬性集指派給每個欄位的值。 按一下「關閉」。

### 添加自定義SPI {#add-a-custom-spi}

如需建立自訂SPI的詳細資訊，請參閱「使用AEM表單進行程式設計」中的「開發AEM [表單的SPI](https://www.adobe.com/go/learn_aemforms_programming_63)」。 要使新部署的自定義SPI可與域關聯，請重新啟動伺服器。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建企業網域」或選取現有的企業網域。
1. 按一下「新增目錄」。
1. 在「配置檔案名稱」框中鍵入名稱，選擇「自定義SPI提供程式」，然後按一下「下一步」。
1. 從清單中選擇自定義用戶提供程式，然後按一下「下一步」。
1. 從清單中選取自訂群組提供者，然後按一下「完成」。

## 編輯目錄 {#edit-a-directory}

您可以編輯先前配置的目錄的詳細資訊。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中的相應域，然後在顯示的頁上，從清單中選擇相應的目錄。
1. 視需要設定目錄、使用者和群組設定。 (請參 [閱目錄設定](configuring-directories.md#directory-settings)。)
1. 按一下「確定」。

## 刪除目錄 {#delete-a-directory}

在刪除目錄後同步域時，該目錄中的所有用戶和組在資料庫中都被標籤為過時。 在「管理控制台」的任何搜尋中，都不會傳回這些檔案。

>[!NOTE]
>
>企業網域至少需要一個驗證提供者和目錄提供者。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在清單中按一下適當的網域。
1. 選中相應目錄的複選框，然後按一下「刪除」。
1. 在顯示的確認頁面上按一下「確定」，然後再按一下「確定」。

## 目錄設定 {#directory-settings}

將目錄添加到域時，請指定以下目錄設定。

**** 伺服器：（強制）目錄伺服器的完全限定域名(FQDN)。 例如，對於corp.adobe.com網路上名為x的電腦，FQDN為x.corp.adobe.com。 IP地址可用來代替FQDN伺服器名。

**** 埠：（必要）目錄伺服器使用的埠。 通常為389或636(如果安全通訊端層(SSL)通訊協定用於透過網路傳送驗證資訊)。

**** SSL:（必要）指定目錄伺服器在通過網路發送資料時是否使用SSL。 預設值為「否」。 當設定為「是」時，應用程式伺服器的Java™運行時環境(JRE)必須信任相應的LDAP伺服器證書。

**綁定** （強制）指定如何訪問目錄。

**** 匿名：不需要用戶名或密碼。 匿名用戶只能獲取有限數量的資料。 這個選項可用於初始測試。

**** 使用者：需要驗證。 在「名稱」框中，指定可以訪問目錄的用戶記錄的名稱。 最好輸入用戶帳戶的完整唯一判別名(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」方塊中，指定相關的密碼。 當您選取「使用者」作為「系結」選項時，就需要這些設定。

**** 名稱：未啟用匿名訪問時可用於連接到LDAP資料庫的名稱。 對於Active Directory 2003，請指定 `[domain name]\[userid]`。 對於Sun™ One、eDirectory或IBM Tivoli Directory Server，請指定用戶的完全限定名稱，如uid=lcuser,ou=it,o=company.com。

**** 密碼：在未啟用匿名訪問時，與您指定連接到LDAP資料庫的名稱相對應的口令。

**** 填入頁面的方式：選中後，使用相應的預設LDAP值填充「用戶」和「組」設定頁上的屬性。

**** 檢索基本DN:檢索基本DN並在下拉清單中顯示它們。 當您有多個基本DN且需要選擇值時，此設定非常有用。

**** 啟用反向連結：當您的組織使用以分層結構組織的多個Active Directory域且您僅為父域指定了目錄設定時，此設定即適用。 在這種情況下，當您選取此選項時，使用者管理可從子網域存取使用者和群組詳細資訊。

***注意&#x200B;**:按一下「測試」以驗證是否可以與LDAP伺服器建立連接。 要確定任何故障的根本原因，請查看應用程式伺服器日誌檔案中的異常。*

### User settings {#user-settings}

**** 唯一識別碼：（必要）用來識別使用者的唯一常數屬性。 使用非DN屬性作為唯一識別碼，因為使用者的DN可能會在移至組織的其他部分時變更。 此設定取決於目錄伺服器。 該值是Active Directory 2003的objectGUID、Sun™ one的nsuniqueID和eDirectory的guid。

**注意**:請確定您輸入的屬性保證在組織中是唯一的。 輸入錯誤值可能導致嚴重的系統問題。*

**** 基本DN:設定為從LDAP分層結構同步用戶和組的起點。 最好在層次結構的最低級別指定基本DN，該DN包括所有需要同步服務的用戶和組。

如果在「目錄」設定中選擇了「啟用轉接」選項，請將「基本DN」選項設定為 *DN* 的dc部分。 若要讓反向連結運作，搜尋範圍必須同時包含父網域和子網域。

***注意&#x200B;**:請勿在此設定中包含使用者的DN。 若要同步特定使用者，請使用「搜尋篩選」設定。*

雖然基本DN是管理控制台中的必備設定，但某些目錄伺服器（如IBM Domino Enterprise Server）可能需要空的BaseDN。 若要指定空的基本DN，請匯出config.xml檔案，在config.xml檔案中編輯設定，然後重新匯入。 (請參 [閱導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。)

**** 搜尋篩選：（必要）用於查找與用戶關聯的記錄的搜索篩選器。 您可以執行單級搜尋或子級搜尋。 （請參閱搜索過濾器語法或RFC 2254。）有關Microsoft AD架構的其他資訊，請參見Active Directory架構。

**** 說明：用戶說明的架構屬性

**** 全名：（必要）用戶全名的方案屬性

**** 登入ID:（必要）使用者登入ID的架構屬性

**** 姓氏：（必要）使用者姓氏的結構屬性

**** 指定名稱：（必要）使用者名稱的架構屬性

**** 縮寫：使用者縮寫簽名的架構屬性

**** 業務日曆：使您能夠根據此設定的值（業務日曆鍵）將業務日曆映射到用戶。 業務日曆定義業務日和非業務日。 AEM表格可在計算事件（例如提醒、期限和呈報）的未來日期和時間時，使用商業日曆。 您為使用者指派商業行事歷金鑰的方式，取決於您是使用企業、本機或混合網域。 （請參閱配置業務日曆。）

如果您使用企業域，可以將「業務日曆」設定映射到LDAP目錄中的欄位。 例如，如果目錄中的每個用戶記錄都包含一個 *country* （國家／地區）欄位，並且您想根據用戶所在的國家／地區分配業務日曆，請指定 *country* （國家／地區）欄位名稱作為「業務日曆」設定的值。 然後，您可以將業務日曆鍵(為LDAP目錄中的 *country* 欄位定義的值)映射到表單工作流中的業務日曆。

用於在表單工作流頁面中顯示業務日曆鍵名稱的空間量是有限的。 將商業日曆索引鍵的名稱限制為少於53個字元，以避免在這些頁面上遭到截斷。

**** 修改時間戳：要啟用增量目錄同步，請設定此值以修改TimeStamp。 （請參閱啟用增量目錄同步。）

**** 組織：用戶所屬組織名稱的方案屬性。

**** 主要電子郵件：用戶主要電子郵件地址的架構屬性。

**** 次要電子郵件：用戶的次要電子郵件地址的方案屬性。

**** 電話：使用者電話號碼的架構屬性。

**** 郵遞區號：使用者郵寄地址的結構屬性。

**** 地區設定：包含ISO地區資訊的架構屬性。 值是雙字母語言代碼或語言和國家代碼。

**** 時區：包含用戶所在時區的方案屬性。 值是字串，例如「城市／國家」。

**** 啟用虛擬清單視圖(VLV)控制：一種LDAP控制項，可讓AEM表單從目錄伺服器以批次擷取資料。 如果您使用Sun one作為LDAP目錄，且該目錄包含許多用戶，則啟用VLV將建立一個索引，用戶管理在搜索用戶時可以使用該索引。 當使用一般使用者帳戶時，此功能很有用，只能同步有限的資料量。 您也可以為組啟用VLV。 如果選擇「啟用虛擬清單視圖(VLV)控制」，請在「排序欄位」框中指定名稱。

***注意&#x200B;**:要啟用VLV，請配置Sun One。 (請參[閱配置用戶管理以使用虛擬清單視圖(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)。)*

**** 排序欄位：如果選擇了「啟用虛擬清單視圖(VLV)控制」，請指定用於排序索引的屬性名。 此屬性名稱（如uid）是您在目錄伺服器上為VLV建立索引時指定的名稱。

### 群組設定 {#group-settings}

**** 唯一識別碼：（必要）用於識別群組的唯一和常數屬性。 使用非DN屬性作為唯一標識符。 此設定取決於目錄伺服器。 該值是Active Directory 2003的objectGUID、Sun one的nsuniqueID和eDirectory的guid。

*注&#x200B;**意**:請確定您輸入的屬性保證在組織中是唯一的。 輸入錯誤值可能導致嚴重的系統問題。*

**** 基本DN:（必要）目錄的基本唯一判別名。

雖然基本DN是管理控制台中的必備設定，但某些目錄伺服器（如IBM Domino Enterprise Server）需要空的BaseDN。 若要指定空的基本DN，請匯出config.xml檔案，在config.xml檔案中編輯設定，然後重新匯入。 (請參 [閱導入和導出配置檔案](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file)。)

**** 搜尋篩選：（必要）用於查找與組關聯的記錄的搜索篩選器。 您可以執行單級搜尋或子級搜尋。

**** 說明：組說明的架構屬性

**** 全名：（必要）群組完整名稱的架構屬性

**** 成員DN:（強制）組內成員的可分辨名稱的方案屬性

**** 成員唯一標識符：屬於所選群組成員的使用者或群組的唯一識別碼。 此值取決於目錄伺服器。 該值是AD2003的objectSID、Sun one的nsuniqueID和eDirectory的guid。

如果使用非DN屬性指定成員DN，使用者管理會使用成員唯一識別碼來查詢LDAP，以收集與唯一識別碼值對應的使用者DN。

如果DN被指定為唯一標識符，則無需配置成員唯一標識符。

**** 組織：組所屬的組織名稱的方案屬性

**** 主要電子郵件：群組主要電子郵件地址的結構屬性

**** 次要電子郵件：群組的次要電子郵件地址的結構屬性

**** 修改時間戳：要啟用增量目錄同步，請設定此值以修改TimeStamp。 （請參閱啟用增量目錄同步。）

**** 啟用虛擬清單視圖(VLV)控制：一種LDAP控制項，可讓AEM表單從目錄伺服器以批次擷取資料。 如果您使用Sun one作為LDAP目錄，且該目錄包含許多組，則啟用VLV將建立一個索引，用戶管理在搜索組時可以使用該索引。 當使用一般使用者帳戶時，此功能很有用，只能同步有限的資料量。 您也可以為用戶啟用VLV。 如果選擇「啟用虛擬清單視圖(VLV)控制」，請指定「排序欄位名稱」。

***注意&#x200B;**:要啟用VLV，請配置Sun One。 (請參[閱配置用戶管理以使用虛擬清單視圖(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv)。)*

**** 排序欄位名稱：如果選擇了「啟用虛擬清單視圖(VLV)控制」，請指定用於排序索引的屬性名。 此屬性名是在目錄伺服器上為VLV建立索引時指定的名稱。

***注意&#x200B;**:按一下「測試」，確認是否已根據基本DN和搜尋准則收集使用者和群組設定。 如果傳回使用者和群組，結果會依屬性集顯示指派給每個欄位的值。*

***注意&#x200B;**:使用者管理不支援網域中重複的使用者ID;只有一個使用者ID的使用者會同步。*

## 配置用戶管理以使用虛擬清單視圖(VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

目錄同步是用戶管理的重要要求。 使用者和群組會從企業目錄同步到AEM表單資料庫，以指派角色和權限。 用戶數量依需求而異，從100到1000000個以上，因此，如何有效地同步資料是一項工程難題。

LDAP協定提供一種機制，可通過使用請求控制以分頁方式查詢大型資料集。 當使用Microsoft Active Directory時，LDAP到AEM表單資料庫同步會使用PagedResultsControl以特定大小的批次擷取資料。 Sun ONE目錄伺服器不支援此控制。 要對Sun ONE Directory server完成編頁查詢，請使用虛擬清單視圖(VLV)控制項。 此控制項包括目錄伺服器端組態和用戶端實作。

>[!NOTE]
>
>本節介紹如何使用Sun ONE Directory Server的VLV控制項。 但是，您可以對支援VLV控制的任何目錄伺服器使用此控制。

1. 配置目錄時，在「用戶設定」頁和「組設定」頁上選擇「啟用虛擬清單視圖(VLV)控制」。 選中此複選框時，還必須在「排序欄位」框中指定排序名稱。 預設值為uid。 (請參 [閱添加目錄或自定義SPI](configuring-directories.md#adding-directories-or-custom-spis)[或編輯目錄](configuring-directories.md#edit-a-directory)。)
1. 使用Sun ONE管理控制台或命令行指令碼為用戶和組建立LDAP VLV條目。 如果您使用命令行指令碼，則可以使用示例用戶和組LDIF檔案。 (請參 [閱為VLV配置Sun ONE目錄伺服器](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv)。)
1. 停止伺服器並建立所需的索引。 (請參 [閱建立VLV的目錄伺服器索引](configuring-directories.md#create-the-directory-server-index-for-vlv)。)

### 為VLV配置Sun ONE目錄伺服器 {#configuring-the-sun-one-directory-server-for-vlv}

建立VLV需要一對包含該類和對象類 `vlvSearch` 的 `vlvIndex` 條目。 vlvSearch條目包括搜索基 `vlvFilter` 礎和屬性，該屬性指定包含要排序的屬性的對象類。 對 `vlvIndex` 像類包括屬性，該屬 `vlvSort` 性指定要排序的一個或多個屬性以及要排序的順序。 (減號(-)表示反向字母順序)。 搭配使用VLV和AEM表單時，使用者和群組需要個別的項目。

>[!NOTE]
>
>可使用Sun ONE圖形用戶介面(GUI)或通過命令行指令碼建立對象條目。 有關使用GUI建立對象條目的說明，請參見Sun ONE文檔。

以下是用戶適用於VLV條目的示例指令碼LDIF:

```as3
 dn: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 objectclass: top
 objectclass: vlvSearch
 cn: lcuser
 vlvBase: dc=corp,dc=adobe,dc=com
 vlvScope: 2
 vlvFilter: (&(objectclass=inetOrgPerson))
 aci: (target="ldap:///cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config")(targetattr="*")(version 3.0; acl "Config"
 ;allow(read,search,compare) userdn="ldap:///all"; )
 dn: cn=lcuser,cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
 cn: lcuser
 vlvSort: cn
 objectclass: top
 objectclass: vlvIndex
```

**使用指令碼建立對象條目**

1. 示例指令碼具有名為的LDAP條目 `lcuser`。 此項目適用於AEM表單中使用者同步的VLV相關設定。 相應地修改以下屬性：

   **** 項目名稱：此示例中的條目名稱為 `lcuser`。 如果 `lcuser` 已變更，則必須在範例指令碼的所有區域進行變更。

   **** vlvBase:在「用戶設定」頁上指定的基本DN。

   **** vlvFilter:在「使用者設定」頁面上指定的搜尋篩選。

   **** vlvSort:在「用戶設定」頁的VLV設定部分中指定的排序欄位。 VLV控制項要求您指定排序控制項。 此欄位用作建立的vlv索引的排序參數。

   **** aci:示例指令碼中指定的訪問控制授予任何已驗證用戶訪問VLV索引以進行讀取、搜索和比較操作的權利。 管理員可以限制對綁定用戶的訪問，該用戶在「用戶管理」用戶介面中指定的「目錄伺服器設定」頁中配置。 如果未授予權限，則用戶搜索不能使用VLV，而LDAP伺服器會拋出權限異常。

   >[!NOTE]
   >
   >作為慣例，vlvIndex條目名稱也設定為， `lcuser`但可以為其指定不同的名稱。 在vlvindex工具中使用相同的名稱。 (請參 [閱建立VLV的目錄伺服器索引](configuring-directories.md#create-the-directory-server-index-for-vlv)*。)*

1. 使用Sun `ldapmodify` ONE Server附帶的工具，分別使用組的基本DN、搜索篩選器和排序欄位為組建立類似條目：

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例如，鍵入以下文本：

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### 為VLV建立目錄伺服器索引 {#create-the-directory-server-index-for-vlv}

配置目錄設定並為用戶和組建立LDAP VLV條目後，請停止伺服器並建立所需的索引。

1. 建立對象項後，停止Sun ONE Server。
1. 使用vlvindex工具，通過鍵入以下文本來生成索引：

   *目錄伺服器實例*`\vlvindex.bat -n userRoot -T lcuser`

   將生成以下輸出：

   ```as3
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex工具存在於目錄伺服器實例目錄中。 如果Sun ONE server有兩個運行server1和server2的實例，則vlvindex工具位於 *Sun ONE伺服器目錄*\server1目錄中。 參數的值是 `-T` 先前在示例LDIF中 `cn` 建立的vlvindex條目的屬性值。 在這個例子中，是的 `lcuser`。

1. 如果也為組啟用了VLV，請為組建立相應的索引。 通過運行以下命令來驗證是否建立了索引：

   *sun一個伺服器目錄*`\shared\bin>ldapsearch -h`*主機名&#x200B;*`-p`*埠no*`-s base -b "" objectclass=*`

   產生如下範例資料的輸出：

   ```as3
    D:\tools\ldap\sun\shared\bin>ldapsearch.exe -h localhost -p 55850 -s base -b "" objectclass=*
    ldapsearch.exe: started Tue Nov 27 16:34:20 2007
    version: 1
    dn:
    objectClass: top
    namingContexts: dc=corp,dc=adobe,dc=com
    supportedExtension: 2.16.840.1.113730.3.5.7
    ...
    vlvsearch: cn=MCC ou=testdata dc=corp dc=adobe dc=com, cn=userRoot,cn=ldbm dat
        abase,cn=plugins,cn=config
    vlvsearch: cn=lcuser,cn=userRoot,cn=ldbm database,cn=plugins,cn=config
    vlvsearch: cn=Browsing ou=testdata,cn=userRoot,cn=ldbm database,cn=plugins,cn=
        config
    1 matches
   ```

