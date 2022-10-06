---
title: 配置目錄
seo-title: Configuring directories
description: 了解如何新增、編輯和刪除目錄，以及設定使用者管理以使用虛擬清單檢視。
seo-description: Learn how to add, edit and delete directories and configure user management to use virtual list view.
uuid: 0bf1a8a7-c917-4248-9937-d24e31c5ba17
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 1f15f028-aa81-478e-97eb-f83a4dc0418c
exl-id: 30edcef2-e8fa-403a-9850-b8dfeeb9ac65
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 0%

---

# 配置目錄 {#configuring-directories}

對於您配置的每個企業域，指定身份驗證提供程式查詢用戶資訊的目錄。 可以為域配置多個目錄。

## 添加目錄或自定義SPI {#adding-directories-or-custom-spis}

對於您配置的每個企業域，指定身份驗證提供程式查詢用戶資訊的目錄。 您可以將目錄添加到現有企業域或添加到新企業域。 可以為域配置多個目錄。 您也可以配置域以使用自定義服務提供商介面(SPI)進行同步。

### 添加目錄 {#add-a-directory}

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建企業域」或選擇現有的企業域。
1. 按一下「添加目錄」。
1. 在「配置檔案名稱」框中，鍵入一個名稱以區分此目錄，然後按一下「下一步」。
1. 配置目錄伺服器設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 要驗證是否可以與LDAP伺服器建立連接，請按一下測試。 如果測試失敗，請查看應用程式伺服器日誌檔案中的異常以確定失敗的根本原因。 按一下「關閉」 ，然後按一下「下一步」 。
1. 選取「使用者設定」 ，並視需要配置設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 要驗證基本DN和其他配置的屬性收集了正確的用戶批，請按一下測試。 LDAP會嘗試使用提供的設定（如基本DN、搜索篩選器和所有屬性）來檢索前200條記錄。

   如果傳回使用者，結果會顯示依屬性集指派給每個欄位的值。 如果測試因伺服器名稱不存在、授權資訊不正確或屬性不正確而失敗，則會顯示以下錯誤訊息：&quot;指定的搜索標準未返回任何結果&quot;。 要確定故障的根本原因，請查看應用程式伺服器日誌檔案中的異常。 按一下「關閉」 ，然後按一下「下一步」 。

1. 選取「群組設定」 ，並視需要配置設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 要驗證基本DN和其他配置的屬性是否收集正確的組批，請按一下測試。 如果傳回群組，結果會顯示依屬性集指派給每個欄位的值。 按一下關閉。

### 新增自訂SPI {#add-a-custom-spi}

如需建立自訂SPI的相關資訊，請參閱以下主題中的「開發AEM表單的SPI」： [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63). 要使新部署的自定義SPI可用於與域關聯，請重新啟動伺服器。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下「新建企業域」或選擇現有的企業域。
1. 按一下「添加目錄」。
1. 在「配置檔案名稱」框中鍵入名稱，選擇「自定義SPI提供程式」，然後按一下「下一步」。
1. 從清單中選擇自定義用戶提供程式，然後按一下下一步。
1. 從清單中選擇自定義組提供程式，然後按一下「完成」。

## 編輯目錄 {#edit-a-directory}

您可以編輯先前配置的目錄的詳細資訊。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 按一下清單中的適當網域，然後在顯示的頁面上，從清單中選取適當的目錄。
1. 視需要配置目錄、用戶和組設定。 (請參閱 [目錄設定](configuring-directories.md#directory-settings).)
1. 按一下「確定」。

## 刪除目錄 {#delete-a-directory}

在刪除目錄後同步域時，該目錄中的所有用戶和組在資料庫中都標籤為過時。 不會從管理控制台的任何搜尋中傳回這些值。

>[!NOTE]
>
>企業域至少需要一個身份驗證提供程式和目錄提供程式。

1. 在管理控制台中，按一下「設定>使用者管理>網域管理」。
1. 在清單中按一下適當的網域。
1. 選擇相應目錄的複選框，然後按一下「刪除」。
1. 在顯示的確認頁上按一下「確定」，然後再次按一下「確定」。

## 目錄設定 {#directory-settings}

將目錄添加到域時，請指定以下目錄設定。

**伺服器：** （強制）目錄伺服器的完全限定域名(FQDN)。 例如，對於adobe.com網路上名為x的電腦，FQDN為x.adobe.com。 可以使用IP地址來取代FQDN伺服器名稱。

**埠：** （強制）目錄伺服器使用的埠。 如果使用安全套接字層(SSL)協定通過網路發送身份驗證資訊，則通常為389或636。

**SSL:** （必要）指定在通過網路發送資料時目錄伺服器是否使用SSL。 預設為「否」。 當設定為「是」時，應用程式伺服器的Java™運行時環境(JRE)必須信任相應的LDAP伺服器證書。

**綁定** （強制）指定如何訪問目錄。

**匿名：** 不需要用戶名或密碼。 匿名用戶只能獲取有限的資料量。 此選項對於初始測試可能很有用。

**用戶：** 需要驗證。 在「名稱」框中，指定可訪問目錄的用戶記錄的名稱。 最好輸入用戶帳戶的完整可分辨名稱(DN)，如cn=Jane Doe、ou=user、dc=can、dc=com。 在「密碼」框中，指定關聯的密碼。 選擇「用戶」作為「綁定」選項時，需要這些設定。

**名稱：** 未啟用匿名訪問時可用於連接到LDAP資料庫的名稱。 對於Active Directory 2003，請指定 `[domain name]\[userid]`. 對於Sun™ One、eDirectory或IBM Tivoli Directory Server，請指定用戶的完全限定名稱，如uid=lcuser、ou=it、o=company.com。

**密碼：** 在未啟用匿名訪問時，與您指定的連接到LDAP資料庫的名稱相對應的密碼。

**在頁面中填入：** 選中後，使用相應的預設LDAP值填充「用戶」和「組」設定頁上的屬性。

**檢索基本DN:** 擷取基本DN，並在下拉式清單中顯示。 當您有多個基本DN且需要選取值時，此設定很實用。

**啟用轉介：** 當您的組織使用以層次結構組織的多個Active Directory域，並且您僅為父域指定了目錄設定時，此設定適用。 在此情況下，當您選取此選項時，「使用者管理」可從子網域存取使用者和群組詳細資訊。

>[!NOTE]
>
>按一下「測試」以驗證是否可以與LDAP伺服器建立連接。 要確定任何失敗的根本原因，請查看應用程式伺服器日誌檔案中的異常。

### 使用者設定 {#user-settings}

**唯一識別碼：** （必要）用於識別使用者的不重複常數屬性。 使用非DN屬性作為唯一識別碼，因為如果使用者移至組織的其他部分，其DN可能會變更。 此設定取決於目錄伺服器。 該值是Active Directory 2003的objectGUID、Sun™ One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>請確定您輸入的屬性保證在組織中是唯一的。 輸入錯誤的值可能會導致嚴重的系統問題。

**基本DN:** 將設定為從LDAP層次結構同步用戶和組的起始點。 最好在層次結構的最低級別指定基本DN，該DN包含所有需要同步服務的用戶和組。

如果在「目錄」設定中選擇了「啟用引用」選項，請將「基本DN」選項設定為 *dc* DN的一部分。 為了讓反向連結運作，搜尋範圍必須同時包含父網域和子網域。

>[!NOTE]
>
>請勿在此設定中加入使用者的DN。 要同步特定用戶，請使用「搜索篩選器」設定。

雖然Base DN是管理控制台中的強制設定，但某些目錄伺服器(如IBM Domino Enterprise Server)可能需要空的BaseDN。 要指定空的基本DN，請導出config.xml檔案，在config.xml檔案中編輯設定，然後重新導入它。 (請參閱 [匯入和匯出設定檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**搜尋篩選器：** （必要）用於查找與用戶關聯的記錄的搜索篩選器。 您可以執行單級搜索或子級搜索。 （請參閱搜尋篩選器語法或RFC 2254）。 有關Microsoft AD架構的其他資訊，請參閱Active Directory架構。

**說明：** 用戶說明的架構屬性

**全名：** （必要）用戶全名的架構屬性

**登入ID:** （必要）使用者登入ID的結構屬性

**姓氏：** （必要）使用者姓氏的結構屬性

**指定名稱：** （必要）使用者名字的結構屬性

**縮寫：** 用戶首字母的架構屬性

**業務日曆：** 使您可以根據此設定的值（業務日曆鍵）將業務日曆映射到用戶。 業務日曆定義業務日和非業務日。 AEM表單可在計算提醒、截止日期和呈報等事件的未來日期和時間時使用商業日曆。 將業務日曆密鑰分配給用戶的方式取決於您使用的是企業、本地還是混合域。 （請參閱配置業務日曆。）

如果使用企業域，可將「業務日曆」設定映射到LDAP目錄中的欄位。 例如，如果目錄中的每個使用者記錄包含 *國家* 欄位，並要根據用戶所在的國家/地區分配業務日曆，請指定 *國家* 欄位名稱作為「業務日曆」設定的值。 然後，您可以映射業務日曆鍵(為 *國家* 欄位（位於LDAP目錄中），以在表單工作流程中執行業務日曆。

用於在表單工作流頁面中顯示業務日曆鍵名稱的空間量有限。 將商務日曆索引鍵的名稱限制為少於53個字元，以免在這些頁面上截斷。

**修改時間戳：** 要啟用增量目錄同步，請設定此值以修改TimeStamp。 （請參閱啟用增量目錄同步。）

**組織：** 用戶所屬組織的名稱的結構屬性。

**主要電子郵件：** 使用者主要電子郵件地址的結構屬性。

**次要電子郵件：** 使用者次要電子郵件地址的結構屬性。

**電話：** 用戶電話號碼的架構屬性。

**郵遞區號：** 用戶郵件地址的結構屬性。

**地區：** 包含ISO地區設定資訊的架構屬性。 值是雙字母語言代碼或語言和國家/地區代碼。

**時區：** 包含用戶所在時區的架構屬性。 值是字串，例如「城市/國家」。

**啟用虛擬清單視圖(VLV)控制項：** 一種LDAP控制項，使AEM表單能夠從目錄伺服器批量檢索資料。 如果您使用Sun One作為LDAP目錄，且該目錄包含許多用戶，則啟用VLV將建立一個索引，用戶管理在搜索用戶時可以使用該索引。 使用只能同步有限資料量的一般使用者帳戶時，此功能相當實用。 您也可以為組啟用VLV。 如果選擇「啟用虛擬清單視圖(VLV)控制項」，請在「排序欄位」框中指定名稱。

>[!NOTE]
>
>要啟用VLV，請配置Sun One。 請參閱 [配置用戶管理以使用虛擬清單視圖(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**排序欄位：** 如果選擇了啟用虛擬清單視圖(VLV)控制項，請指定用於排序索引的屬性名稱。 在目錄伺服器上為VLV建立索引時，此屬性名（如uid）是指定的名稱。

### 群組設定 {#group-settings}

**唯一識別碼：** （必要）用於識別群組的唯一常數屬性。 使用非DN屬性作為唯一識別碼。 此設定取決於目錄伺服器。 該值是Active Directory 2003的objectGUID、Sun One的nsuniqueID和eDirectory的guid。

>[!NOTE]
>
>請確定您輸入的屬性保證在組織中是唯一的。 輸入錯誤的值可能會導致嚴重的系統問題。

**基本DN:** （強制）目錄的基本可分辨名稱。

雖然Base DN是管理控制台中的強制設定，但某些目錄伺服器(如IBM Domino Enterprise Server)需要空的BaseDN。 要指定空的基本DN，請導出config.xml檔案，在config.xml檔案中編輯設定，然後重新導入它。 (請參閱 [匯入和匯出設定檔](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

**搜尋篩選器：** （必填）用於查找與組關聯的記錄的搜索篩選器。 您可以執行單級搜索或子級搜索。

**說明：** 組說明的架構屬性

**全名：** （強制）群組完整名稱的結構屬性

**成員DN:** （強制）組內成員的可分辨名稱的架構屬性

**成員唯一標識符：** 作為所選組成員的用戶或組的唯一標識符。 此值取決於目錄伺服器。 該值是AD2003的objectSID、Sun One的nsuniqueID和eDirectory的guid。

如果使用非DN屬性指定成員DN，則用戶管理使用成員唯一標識符來查詢LDAP，以收集與唯一標識符值對應的用戶DN。

如果將DN指定為唯一標識符，則無需配置成員唯一標識符。

**組織：** 組所屬組織名稱的架構屬性

**主要電子郵件：** 群組主要電子郵件地址的結構屬性

**次要電子郵件：** 組的輔助電子郵件地址的架構屬性

**修改時間戳：** 要啟用增量目錄同步，請設定此值以修改TimeStamp。 （請參閱啟用增量目錄同步。）

**啟用虛擬清單視圖(VLV)控制項：** 一種LDAP控制項，使AEM表單能夠從目錄伺服器批量檢索資料。 如果您使用Sun One作為LDAP目錄，且該目錄包含許多組，則啟用VLV將建立一個索引，用戶管理在搜索組時可以使用該索引。 使用只能同步有限資料量的一般使用者帳戶時，此功能相當實用。 您還可以為用戶啟用VLV。 如果選擇啟用虛擬清單視圖(VLV)控制項，請指定排序欄位名稱。

>[!NOTE]
>
>要啟用VLV，請配置Sun One。 請參閱 [配置用戶管理以使用虛擬清單視圖(VLV)](configuring-directories.md#configure-user-management-to-use-virtual-list-view-vlv).

**排序欄位名稱：** 如果選擇了啟用虛擬清單視圖(VLV)控制項，請指定用於排序索引的屬性名稱。 此屬性名稱是在目錄伺服器上為VLV建立索引時指定的名稱。

>[!NOTE]
>
>按一下「測試」 ，確認系統已根據基本DN和搜尋准則收集使用者和群組設定。

如果傳回使用者和群組，結果會顯示依屬性集指派給每個欄位的值。

>[!NOTE]
>
>「使用者管理」不支援網域內重複的使用者ID;只會同步一個具有使用者ID的使用者。

## 配置用戶管理以使用虛擬清單視圖(VLV) {#configure-user-management-to-use-virtual-list-view-vlv}

目錄同步是用戶管理的一項重要要求。 使用者和群組會從企業目錄同步至AEM表單資料庫，以指派角色和權限。 用戶數量因需求而異，從100到100000+，因此，高效同步資料是一項工程難題。

LDAP通訊協定提供一種機制，可使用請求控制以編頁方式查詢大型資料集。 使用Microsoft Active Directory時，LDAP到AEM表單資料庫同步使用PagedResultsControl以批次檢索特定大小的資料。 Sun ONE目錄伺服器不支援此控制項。 要對Sun ONE Directory Server完成編頁查詢，請使用「虛擬清單視圖」(VLV)控制項。 此控制項涉及目錄伺服器端配置和客戶端實施。

>[!NOTE]
>
>本節介紹如何使用Sun ONE Directory Server的VLV控制項。 但是，可以對支援VLV控制的任何目錄伺服器使用此控制項。

1. 配置目錄時，在「用戶設定」頁和「組設定」頁上選擇「啟用虛擬清單視圖(VLV)控制」。 選中複選框時，還必須在「排序欄位」框中指定排序名稱。 預設值為uid。 (請參閱 [添加目錄或自定義SPI](configuring-directories.md#adding-directories-or-custom-spis) 或 [編輯目錄](configuring-directories.md#edit-a-directory).)
1. 使用Sun ONE管理控制台或命令行指令碼為用戶和組建立LDAP VLV項。 如果使用命令行指令碼，則可以使用示例用戶和組LDIF檔案。 (請參閱 [為VLV配置Sun ONE目錄伺服器](configuring-directories.md#configuring-the-sun-one-directory-server-for-vlv).)
1. 停止伺服器並建立所需的索引。 (請參閱 [為VLV建立目錄伺服器索引](configuring-directories.md#create-the-directory-server-index-for-vlv).)

### 為VLV配置Sun ONE目錄伺服器 {#configuring-the-sun-one-directory-server-for-vlv}

建立VLV需要一對包含 `vlvSearch` 和 `vlvIndex` 對象類。 vlvSearch條目包括搜索基和 `vlvFilter` 屬性，指定包含要排序的屬性的對象類。 此 `vlvIndex` 對象類包括 `vlvSort` 屬性，它指定要排序的一個或多個屬性以及要排序的順序。 (減號(-)表示反字母順序)。 將VLV與AEM表單搭配使用時，使用者和群組需要個別的項目。

>[!NOTE]
>
>可使用Sun ONE圖形用戶介面(GUI)或通過命令行指令碼建立對象條目。 有關使用GUI建立對象條目的說明，請參見Sun ONE文檔。

以下是用戶的VLV項的示例指令碼LDIF:

```text
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

1. 示例指令碼有一個名為 `lcuser`. 此條目用於與VLV相關的配置，以便在AEM表單中進行用戶同步。 相應地修改以下屬性：

   **條目名稱：** 此範例中的項目名稱為 `lcuser`. 若 `lcuser` 已變更，則必須在範例指令碼的所有區域中加以變更。

   **vlvBase:** 在「用戶設定」頁上指定的基DN。

   **vlvFilter:** 在「用戶設定」頁上指定的搜索篩選器。

   **vlvSort:** 在「用戶設定」頁的VLV設定部分中指定的排序欄位。 VLV控制項要求您指定排序控制項。 此欄位用作所建立vlv索引的排序參數。

   **aci:** 示例指令碼中指定的訪問控制授予任何已驗證用戶訪問VLV索引以執行讀取、搜索和比較操作的權利。 管理員可以限制對綁定用戶的訪問，該用戶在「用戶管理」用戶介面中指定的「目錄伺服器設定」頁中配置。 如果未提供權限，則用戶搜索將無法使用VLV，而LDAP伺服器將擲回權限異常。

   >[!NOTE]
   >
   >作為慣例， vlvIndex條目名稱也設定為 `lcuser`，但您可以指定不同的名稱。 在vlvindex工具中使用相同的名稱。 (請參閱 [為VLV建立目錄伺服器索引&#x200B;](configuring-directories.md#create-the-directory-server-index-for-vlv)*.)*

1. 使用 `ldapmodify` 工具，請分別使用組的基本DN、搜索篩選器和排序欄位為組建立類似的條目：

   `server directory\shared\bin>ldapmodify -v -a -h host -p port -D "admin user" -w "password" -f "LDIF file location"`

   例如，輸入下列文字：

   `D:\tools\ldap\sun\shared\bin> -v -a -h localhost -p 55850 -D "uid=admin,ou=administrators,ou=topologymanagement,o=netscaperoot" -w "admin" -f "D:\tools\ldap\data\vlv feature\users.ldif"`

### 為VLV建立目錄伺服器索引 {#create-the-directory-server-index-for-vlv}

配置目錄設定並為用戶和組建立LDAP VLV項後，請停止伺服器並建立所需的索引。

1. 建立對象條目後，停止Sun ONE Server。
1. 使用vlvindex工具，通過鍵入以下文本生成索引：

   *目錄伺服器實例* `\vlvindex.bat -n userRoot -T lcuser`

   將生成以下輸出：

   ```shell
    D:\tools\ldap\sun\shared\bin>..\..\slapd-chetanmeh-xp3\vlvindex.bat -n userRoot -T livecycle
    [21/Nov/2007:16:47:26 +051800] - userRoot: Indexing VLV: livecycle
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 1000 entries (5%).
    [21/Nov/2007:16:47:27 +051800] - userRoot: Indexed 2000 entries (9%).
    ...
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 20000 entries (94%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Indexed 21000 entries (99%).
    [21/Nov/2007:16:47:29 +051800] - userRoot: Finished indexing.
   ```

   vlvindex工具存在於目錄伺服器實例目錄中。 如果Sun ONE Server有兩個運行server1和server2的實例，則vlvindex工具位於 *Sun ONE伺服器目錄*\server1目錄。 參數的值 `-T` 是 `cn` 先前在示例LDIF中建立的vlvindex條目的屬性。 在這種情況下， `lcuser`.

1. 如果還為組啟用了VLV，請為組建立相應的索引。 通過運行以下命令來驗證是否建立索引：

   *sun one server directory* `\shared\bin>ldapsearch -h`*主機名* `-p`*埠否* `-s base -b "" objectclass=*`

   產生如下列範例資料之類的輸出：

   ```shell
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
