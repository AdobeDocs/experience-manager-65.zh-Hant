---
title: 配置客戶端和伺服器選項
seo-title: Configuring client and server optionsn
description: 了解如何配置各種客戶端和伺服器選項，如伺服器配置設定、文檔安全形色和事件審核。
seo-description: Learn how you can configure the various client and server options, such as server configuration settings, document security roles, and event auditing.
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
feature: Document Security
exl-id: fe132f13-5f9a-4c86-a385-0a0026c812e2
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '10242'
ht-degree: 0%

---

# 配置文檔安全伺服器 {#configure-the-document-security-server}

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「伺服器配置」。
1. 配置設定並按一下「確定」。

## 伺服器配置設定 {#server-configuration-settings}

**基本URL:** 包含伺服器名稱和埠的基本文檔安全URL。 附加至基礎的資訊會建立連線URL。 例如，會附加/edc/Main.do以存取網頁。 使用者也會透過此URL回應外部使用者註冊邀請。

如果您使用IPv6，請輸入基本URL作為電腦名或DNS名。 如果您使用數字IP位址，Acrobat將無法開啟受原則保護的檔案。 此外，請為伺服器使用HTTP安全(HTTPS)URL。

>[!NOTE]
>
>基本URL嵌入到受策略保護的檔案中。 客戶端應用程式使用基本URL連回伺服器。 安全檔案將繼續包含基本URL，即使稍後已變更亦然。 如果您變更基本URL，則需要為所有連接的用戶端更新設定資訊。

**預設離線租用期：** 用戶離線使用受保護文檔的預設時間長度。 建立策略時，此設定將確定「自動離線租賃期」設定的初始值。 （請參閱建立和編輯原則。） 當租賃期過期時，收件人必須再次同步文檔以繼續使用它。

有關離線租賃和同步如何工作的討論，請參見 [配置離線租賃和同步的入門課程](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html).

**預設離線同步期間：** 任何文檔在最初受保護時離線使用的時間上限。

**客戶端會話超時：** 如果通過客戶端應用程式登錄的用戶沒有與文檔安全性交互，則在經過該時間後，文檔安全性將斷開連接（以分鐘為單位）。

**允許匿名用戶訪問：** 選擇此選項以啟用建立共用和個人策略的功能，使匿名用戶能夠開啟受策略保護的文檔。 （沒有帳戶的用戶可以訪問該文檔，但無法登錄到文檔安全性，或使用其他受策略保護的文檔。）

**禁用對第7版客戶端的訪問：** 指定使用者是否可使用Acrobat或Reader7.0連線至伺服器。 選取此選項時，使用者必須使用Acrobat或Reader8.0及更新版本，才能完成PDF檔案的檔案安全作業。 如果策略要求在開啟受策略保護的文檔時，Acrobat或Reader8.0及更高版本必須以認證模式運行，則應禁用對Acrobat或Reader7的訪問。 （請參閱指定使用者和群組的檔案權限）。

**允許對每個文檔進行離線訪問** 選擇此選項以指定每個文檔的離線訪問。 如果啟用此設定，則用戶將只能離線訪問用戶至少聯機開啟過一次的文檔。

**允許用戶名密碼驗證：** 選擇此選項可使客戶端應用程式在連接到伺服器時使用用戶名/密碼驗證。

**允許Kerberos身份驗證：** 選擇此選項可使客戶端應用程式在連接到伺服器時使用Kerberos身份驗證。

**允許客戶端證書驗證：** 選擇此選項可使客戶端應用程式在連接到伺服器時使用證書身份驗證。

**允許擴展身份驗證** 選擇以啟用擴展身份驗證，然後輸入擴展身份驗證登錄URL。

選擇此選項可使客戶端應用程式使用擴展身份驗證。 擴充驗證提供自訂驗證程式，以及AEM Forms伺服器上設定的不同驗證選項。 例如，使用者現在可以體驗SAML驗證，而非AEM表單使用者名稱/密碼，從Acrobat和Reader用戶端。 依預設，登陸URL包含 *localhost* 作為伺服器名稱。 用完全限定的主機名替換伺服器名。 如果尚未啟用延伸驗證，則會自動從基礎URL填入登錄URL中的主機名稱。 請參閱 [添加擴展身份驗證提供程式](configuring-client-server-options.md#add-the-extended-authentication-provider).

***附註&#x200B;**:Apple Mac OS X支援Adobe Acrobat 11.0.6版及更新版本的延伸驗證。*

**擴展驗證的首選HTML控制寬度** 指定在Acrobat中開啟以輸入使用者憑證的延伸驗證對話方塊寬度。

**擴展驗證的首選HTML控制高度** 指定在Acrobat中開啟以輸入使用者憑證的延伸驗證對話方塊的高度。

***附註&#x200B;**:此對話框的寬度和高度限制如下：*
寬度：最小= 400，最大= 900

高度：最低= 450;上限= 800

**啟用客戶端憑據快取：** 選擇此選項可允許用戶快取其憑據（用戶名和密碼）。 快取使用者的認證時，他們不必在每次開啟檔案或按一下Adobe Acrobat中「管理安全性原則」頁面上的「重新整理」按鈕時輸入其認證。 您可以指定使用者必須再次提供其憑證的天數。 將天數設為0可無限期快取憑據。

## 配置文檔安全用戶和管理員 {#configuring-document-security-users-and-administrators}

### 為管理員分配文檔安全形色 {#assigning-document-security-roles-to-administrators}

您的AEM表單環境包含一或多個具有建立使用者和群組適當權限的管理員使用者。 如果貴組織正在使用文檔安全性，則至少還必須為一個管理員分配管理受邀用戶和本地用戶的權限。

管理員還必須具有管理控制台用戶角色才能訪問管理控制台。 (請參閱 [建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).)

### 設定可見的使用者和群組 {#configuring-visible-users-and-groups}

要在策略用戶搜索期間查看選定域中的用戶和組，超級管理員或策略集管理員必須選擇域，並將每個策略集的域（在「用戶管理」中建立）添加到可見的用戶和組清單中。

可見的用戶和組清單對策略集協調器可見，用於限制最終用戶在選擇要添加到策略的用戶或組時可以瀏覽的域。 如果未執行此任務，則策略集協調器將找不到要添加到策略的任何用戶或組。 任何給定的策略集都可以有多個策略集協調器。

1. 在您以檔案安全性安裝及設定AEM表單環境後，請在「使用者管理」中設定所有適當的網域。 <!-- Fix broken link (See Setting up and managing domains) -->

   ***附註&#x200B;**:必須先建立域，然後才能建立任何策略。*

1. 在管理控制台中，按一下「服務」>「文檔管理」>「策略」，然後按一下「策略集」頁簽。
1. 選擇「全局策略集」，然後按一下「可見用戶和組」頁簽。
1. 按一下「新增網域」 ，然後視需要新增現有網域。
1. 導覽至「服務>檔案安全性>設定>我的原則」 ，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」 ，然後視需要新增現有網域。

## 添加擴展身份驗證提供程式 {#add-the-extended-authentication-provider}

AEM forms提供您可針對環境自訂的範例設定。 執行下列步驟：

>[!NOTE]
>
>Apple Mac OS X支援Adobe Acrobat 11.0.6版及更新版本的延伸驗證。

1. 獲取部署的示例WAR檔案。 請參閱適合您的應用程式伺服器的安裝指南。
1. 請確定表單伺服器的基本URL是完全限定的名稱，而不是IP位址，且是HTTPS URL。 請參閱 [伺服器配置設定](configuring-client-server-options.md#server-configuration-settings).
1. 從「伺服器配置」頁啟用「擴展身份驗證」。 請參閱 [伺服器配置設定](configuring-client-server-options.md#server-configuration-settings).
1. 在「使用者管理」設定檔案中新增所需的SSO重新導向URL。 請參閱 [新增SSO重新導向URL以進行延伸驗證](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication).

### 新增SSO重新導向URL以進行延伸驗證 {#add-sso-redirect-urls-for-extended-authentication}

啟用擴展身份驗證後，用戶在Acrobat XI或ReaderXI中開啟受策略保護的文檔時，將獲得身份驗證對話框。 此對話框載入您在文檔安全伺服器設定中指定為擴展身份驗證登錄URL的HTML頁。 請參閱 [伺服器配置設定](configuring-client-server-options.md#server-configuration-settings).

>[!NOTE]
>
>Apple Mac OS X支援Adobe Acrobat 11.0.6版及更新版本的延伸驗證。

1. 在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔」。
1. 按一下「導出」，然後將配置檔案保存到磁碟。
1. 在編輯器中開啟檔案，然後找到AllowedUrls節點。
1. 在 `AllowedUrls` 節點，添加以下行： `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 儲存檔案，然後從「手動配置」頁面匯入更新的檔案：在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔」。

## 配置離線安全性 {#configuring-offline-security}

文檔安全性提供了離線使用受策略保護的文檔的能力，而無需連接網際網路或網路。 此功能要求策略允許離線訪問，如 [指定用戶和組的文檔權限](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups). 在離線使用具有此策略的文檔之前，收件人必須在聯機時開啟該文檔並在提示時按一下「是」啟用離線訪問。 還可請求接收者驗證其身份。 然後，在策略中指定的離線租用期間內，收件人可以離線使用文檔。

離線租用期結束時，收件者必須線上開啟檔案，或使用Acrobat或Acrobat Reader DC擴充功能表命令進行同步，才能再次與檔案安全性同步。 (請參閱 *Acrobat說明* 或適當 *Acrobat Reader DC擴充功能說明*.)

由於允許離線訪問的文檔需要在離線儲存檔案的電腦上快取關鍵材料，因此，如果未經授權的用戶能夠獲取關鍵材料，則檔案可能會受到損害。 為了彌補這一可能性，提供了計畫和手動密鑰變換選項，您可以配置這些選項以防止未經授權的人使用密鑰訪問文檔。

### 設定預設的離線租用期 {#set-a-default-offline-lease-period}

受策略保護文檔的接收者可以使文檔在策略中指定的天數內離線。 最初將文檔與文檔安全性同步後，收件者可以離線使用它，直到離線租賃期過期。 租期過期時，收件人必須聯機獲取文檔並登錄以與文檔安全同步，才能繼續使用文檔。

您可以設定預設的離線租用期。 當任何人建立或編輯策略時，可以從預設值更改租用期。

1. 在文檔安全頁上，按一下「配置」>「伺服器配置」。
1. 在「預設離線租賃期」框中，鍵入離線租賃期的天數。
1. 按一下「確定」。

### 管理密鑰滾動 {#manage-key-rollovers}

檔案安全性使用加密演算法和授權來保護檔案。 當它加密文檔時，文檔安全性將生成並管理稱為的解密密鑰 *DocKey* 會傳遞至用戶端應用程式。 如果保護文檔的策略允許離線訪問，則離線密鑰稱為 *主鍵* 也會為每個離線存取檔案的使用者產生。

>[!NOTE]
>
>如果主密鑰不存在，則文檔安全性將生成一個密鑰以保護文檔。

要離線開啟受策略保護的文檔，用戶的電腦必須具有相應的主密鑰。 當用戶與文檔安全性同步時，電腦獲取主密鑰（聯機開啟受保護的文檔）。 如果此主密鑰被洩露，則用戶可以離線訪問的任何文檔也可能被洩露。

減少離線文檔威脅的一種方法是避免允許對特別敏感的文檔進行離線訪問。 另一種方法是定期滾動主鍵。 當文檔安全性將密鑰翻蓋時，任何現有密鑰都無法再訪問受策略保護的文檔。 例如，如果犯罪者從失竊的筆記型電腦獲取主密鑰，則該密鑰無法用於訪問在滾動發生後受保護的文檔。 如果您懷疑某個特定主密鑰已被洩露，則可以手動滾動該密鑰。

不過，您也必須注意，密鑰變換會影響所有主密鑰，而不只是一個密鑰。 它還降低了系統的可擴充性，因為客戶端必須儲存更多密鑰以便離線訪問。 預設的關鍵變換頻率為20天。 建議不要將此值設定為低於14天，因為可能會阻止用戶查看離線文檔，並且系統效能可能會受到影響。

在以下示例中，Key1是兩個主鍵中較舊的，Key2是較新的鍵。 第一次按一下「立即變換密鑰」按鈕時，Key1將變為無效，並生成一個較新的有效主密鑰(Key3)。 當用戶與文檔安全性同步時，他們將獲取Key3，這通常是通過聯機開啟受保護的文檔。 但是，在用戶達到策略中指定的最大離線租用期之前，不強制與文檔安全同步。 在第一個密鑰變換後，保持離線狀態的用戶仍然可以開啟離線文檔，包括受Key3保護的文檔，直到達到最大離線租用期。 第二次按一下「立即變換密鑰」按鈕時，Key2將變為無效，並且Key4已建立。 在兩個密鑰滾動期間保持離線狀態的用戶在與文檔安全同步之前無法開啟受Key3或Key4保護的文檔。

**變更關鍵變換頻率**

為了保密起見，當您使用離線文檔時，文檔安全性提供了自動密鑰變換選項，預設頻率期為20天。 您可以更改變換頻率；但是，請避免將值設定在14天以下，因為可能會阻止人們查看離線文檔，並且系統效能可能會受到影響。

1. 在文檔安全頁上，按一下「配置」>「密鑰管理」。
1. 在「關鍵變換頻率」框中，鍵入變換週期的天數。
1. 按一下「確定」。

**手動滾動主鍵**

要保護離線文檔的機密性，可以手動滾轉主密鑰。 您可能會發現需要手動滾動密鑰（例如，如果某人從快取密鑰的電腦獲取密鑰，從而允許離線訪問文檔，則該密鑰被洩露。）

>[!NOTE]
>
>避免經常使用手動變換，因為它會導致所有主鍵都變換，而不只是一個，並且可能會暫時阻止用戶離線查看新文檔。

主密鑰必須滾動兩次，之後客戶端電腦上以前的現有密鑰才會失效。 已使主密鑰失效的客戶端電腦必須與文檔安全服務重新同步，以獲取新的主密鑰。

1. 在文檔安全頁上，按一下「配置」>「密鑰管理」。
1. 按一下「Rolver Keys Now（立即變換密鑰）」 ，然後按一下「OK（確定）」。
1. 等10分鐘。 伺服器日誌中顯示以下日誌消息： `Done RightsManagement key rollover for`*N* `principals`. 其中 *N* 是文檔安全系統中的用戶數。
1. 按一下「Rolver Keys Now（立即變換密鑰）」 ，然後按一下「OK（確定）」。
1. 等10分鐘。

## 配置事件審核和隱私設定 {#configuring-event-auditing-and-privacy-settings}

文檔安全性可以審核並記錄與與受策略保護的文檔、策略、管理員和伺服器交互相關的事件的資訊。 您可以配置事件審核，也可以指定要審核的事件類型。 要審核特定文檔的事件，還必須啟用策略上的審核選項。

啟用審核後，您可以在「事件」頁上查看審核事件的詳細資訊。 文檔安全用戶還可以查看與他們使用或建立的受策略保護的文檔相關的事件。

您可以選擇以下類型的事件進行審核：

* 受策略保護的文檔事件，例如授權或未經授權的用戶嘗試開啟文檔
* 策略事件，如建立、更改、刪除、啟用和禁用策略
* 使用者事件，例如外部使用者邀請和註冊、啟用和停用的使用者帳戶、使用者密碼的變更，以及設定檔更新
* AEM表單事件，如版本不匹配、不可用的目錄伺服器和授權提供程式以及伺服器配置更改

### 啟用或禁用事件審核 {#enable-or-disable-event-auditing}

您可以啟用和禁用與伺服器、受策略保護的文檔、策略、策略集和用戶相關的事件的審核。 啟用事件審核時，您可以選擇審核所有可能的事件，也可以選擇要審核的特定事件。

啟用伺服器審核時，可以在「事件」頁上查看已審核事件。

1. 在管理控制台中，按一下「服務>檔案安全性>設定>稽核和隱私權設定」 。
1. 要配置伺服器審核，請在「啟用伺服器審核」下，選擇「是」或「否」。
1. 如果您選擇「是」，則在每個事件類別下，執行下列任一操作以選擇要審核的選項：

   * 要審核類別中的所有事件，請選擇「全部」。
   * 要僅審核某些事件，請取消選擇「全部」，然後選中要審核的事件旁邊的複選框。

      (請參閱 [事件審核選項](configuring-client-server-options.md#event-auditing-options).)

1. 按一下「確定」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，例如上一頁按鈕、重新整理按鈕，以及上一頁或下一頁箭頭，因為此動作會造成不想要的資料擷取和資料顯示問題。

### 啟用或停用隱私權通知 {#enable-or-disable-privacy-notification}

您可以啟用和停用隱私權通知訊息。 當您啟用隱私通知時，當收件者嘗試開啟受原則保護的檔案時，會顯示訊息。 通知通知用戶正在審核文檔使用。 您也可以指定URL，使用者可使用該URL來檢視您的隱私權原則頁面（如果有）。

1. 在管理控制台中，按一下「服務>檔案安全性>設定>稽核和隱私權設定」 。
1. 若要設定隱私權通知，請在「啟用隱私權通知」下方選取「是」或「否」。

   如果附加到文檔的策略允許匿名用戶訪問，並且「啟用隱私聲明」設定為「否」，則不會提示用戶登錄，也不會顯示隱私通知消息。

   如果附加到文檔的策略不允許匿名用戶訪問，則用戶將看到隱私通知消息。

1. 若適用，在「隱私權URL」方塊中，輸入您的隱私權政策頁面的URL。 如果「隱私權URL」方塊留空，則會顯示adobe.com的隱私權頁面。
1. 按一下「確定」。

>[!NOTE]
>
>禁用隱私聲明不會禁用文檔使用審核。 透過擴充使用追蹤支援的立即可用稽核動作和自訂動作，仍可收集使用者行為資訊。

### 匯入自訂稽核事件類型 {#import-a-custom-audit-event-type}

如果您使用支援對其他事件（如特定檔案類型的特定事件）進行審計的支援文檔安全的應用程式，則Adobe合作夥伴可以為您提供可導入到文檔安全的自定義審計事件。 只有在Adobe合作夥伴已提供自訂事件類型時，才使用此功能。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「事件管理」。
1. 按一下「瀏覽」以轉到要導入的XML檔案，然後按一下「導入」。
1. 如果找到相同的事件代碼和命名空間組合，則導入會覆寫伺服器上的現有自定義審核事件類型。
1. 按一下「確定」。

### 刪除自訂稽核事件類型 {#delete-a-custom-audit-event-type}

1. 在管理控制台中，按一下「服務>檔案安全性>設定>事件管理」。
1. 選取要刪除的自訂稽核事件類型旁的核取方塊，然後按一下「刪除」。
1. 按一下「確定」。

### 導出審核事件 {#export-audit-events}

您可以將稽核事件匯出至檔案以用於封存。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「事件管理」。
1. 視需要編輯「匯出稽核事件」底下的設定。 您可以指定：

   * 要導出的審計事件的最低年齡
   * 要包含在單一檔案中的稽核事件數上限。 伺服器會根據此值產生一或多個檔案。
   * 建立檔案的資料夾。 此資料夾位於表單伺服器上。 如果資料夾路徑是相對的，則它是相對於應用程式伺服器根目錄的。
   * 用於審計事件檔案的檔案前置詞
   * 檔案的格式，為與Microsoft Excel相容的逗號分隔值(CSV)檔案或XML檔案。

1. 按一下「匯出」。 如果要取消導出，請按一下取消導出。 如果其他用戶已計畫導出，則在導出完成之前，取消導出按鈕不可用。 如果其他用戶已計畫導出，則「取消導出」按鈕不可用。 要檢查計畫的導出或刪除是否已啟動或已完成，請按一下刷新。

### 刪除審計事件 {#delete-audit-events}

您可以刪除早於指定天數的稽核事件。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「事件管理」。
1. 在「刪除審核事件」下，指定「刪除審核事件早於」框中的天數。
1. 按一下刪除。按一下「匯出」。 如果要取消刪除，請按一下取消刪除。 如果其他用戶已計畫刪除，則在導出完成之前，取消刪除按鈕不可用。 如果其他用戶已計畫導出，則「取消刪除」按鈕不可用。 要檢查計畫的刪除是否已開始或已完成，請按一下刷新。

### 事件審核選項 {#event-auditing-options}

您可以啟用和停用事件稽核，並指定要稽核的事件類型。

**檔案事件**

**查看文檔：** 收件人查看受策略保護的文檔。

**關閉文檔：** 收件人將關閉受策略保護的文檔。

**打印低解析度** 收件人打印具有指定的低解析度選項的受策略保護文檔。

**打印高解析度：** 收件人打印具有指定的高解析度選項的受策略保護文檔。

**向文檔添加註釋：** 收件者會將註解新增至PDF檔案。

**撤消文檔：** 用戶或管理員撤消對受策略保護文檔的訪問。

**取消撤消文檔：** 用戶或管理員重新對受策略保護的文檔進行訪問。

**表單填寫：** 收件者將資訊輸入可填寫的PDF檔案中。

**已刪除策略：** 發佈者從文檔中刪除策略以撤消安全保護。

**更改文檔吊銷URL:** 來自API層級的呼叫會變更指定的撤銷URL，以存取取代已撤銷檔案的新檔案。

**修改文檔：** 收件人更改受策略保護文檔的內容。

**簽署文檔：** 收件者簽署檔案。

**保護新文檔：** 用戶應用策略以保護文檔。

**文檔上的切換策略：** 用戶或管理員將切換附加到文檔的策略。

**將文檔發佈為：** 在伺服器上註冊一個文檔，其documentName和許可與現有文檔相同，並且這些文檔沒有父子關係。 可使用AEM Forms SDK觸發此事件。

**迭代文檔：** 在伺服器上註冊一個文檔，其documentName和許可證與現有文檔相同，並且這些文檔具有父子關係。 可使用AEM Forms SDK觸發此事件。

**策略事件**

**已建立策略：** 用戶或管理員建立策略。

**啟用的策略：** 管理員使策略可用。

**更改的策略：** 用戶或管理員更改策略。

**禁用的策略：** 管理員使策略不可用。

**已刪除的策略：** 用戶或管理員刪除策略。

**更改策略所有者：** 來自API層級的呼叫會變更原則擁有者。

**使用者事件**

**已刪除用戶：** 管理員會刪除使用者帳戶。

**註冊受邀用戶：** 外部用戶註冊到文檔安全性。

**成功登入：** 管理員或使用者成功登入嘗試。

**受邀用戶：** 檔案安全性邀請使用者註冊。

**激活的用戶：** 外部使用者透過啟用電子郵件中的URL來啟用其帳戶，或是管理員會啟用帳戶。

**更改密碼：** 被邀請的用戶更改其密碼，或管理員重置本地用戶的密碼。

**登錄失敗：** 管理員或用戶嘗試登錄失敗。

**已停用的使用者：** 管理員禁用本地用戶帳戶。

**配置檔案更新：** 受邀的用戶更改其名稱、組織名稱和密碼。

**帳戶已鎖定：** 管理員鎖定帳戶。

**策略集事件**

**已建立策略集：** 管理員或策略集協調器建立策略集。

**已刪除的策略集：** 管理員或策略集協調器刪除策略集。

**修改的策略集：** 管理員或策略集協調器更改策略集。

**系統事件**

**目錄同步完成：** 「事件」頁面無法取得此資訊。 「域管理」頁上將顯示當前目錄同步資訊，包括當前同步狀態和上次同步的時間。 若要存取管理控制台中的「網域管理」頁面，請按一下「設定>使用者管理>網域管理」 。

**客戶端啟用離線訪問：** 用戶允許離線訪問用戶電腦上的伺服器所保護的文檔。

**同步的客戶端** 客戶端應用程式必須與伺服器同步資訊以允許離線訪問。

**版本不匹配：** 與伺服器不相容的AEM Forms SDK版本嘗試連線至伺服器。

**目錄同步資訊：** 「事件」頁面無法取得此資訊。 「域管理」頁上將顯示當前目錄同步資訊，包括當前同步狀態和上次同步的時間。 若要存取管理控制台中的「網域管理」頁面，請按一下「設定>使用者管理>網域管理」 。

**伺服器配置更改：** 通過網頁或通過導入config.xml檔案手動完成對伺服器配置的更改。 這包括對基本URL、會話超時、登錄鎖定、目錄設定、密鑰滾動、外部註冊的SMTP伺服器設定、水印配置、顯示選項等的更改。

## 配置擴展使用情況跟蹤 {#configuring-extended-usage-tracking}

文檔安全性可以跟蹤可在受保護文檔上執行的各種自定義事件。 您可以在全局級別或策略級別啟用從文檔安全伺服器跟蹤事件。 然後，您可以設定JavaScript來擷取受保護PDF檔案中執行的特定動作，例如按一下按鈕或儲存檔案。 此使用資料會以索引鍵值配對的XML檔案傳送，供您進一步分析。 訪問受保護文檔的最終用戶可以允許或拒絕客戶端應用程式的此類跟蹤。

如果在全局級別啟用了跟蹤，則可以在策略級別覆蓋此設定，並為特定策略禁用它。 如果在全局級別禁用了跟蹤，則無法執行策略級別覆蓋。 當事件計數達到25或檔案關閉時，追蹤事件的清單會自動推送至伺服器。 您也可以設定指令碼，根據您的需求明確推送事件清單。 您可以存取檔案安全性物件屬性和方法，以自訂事件追蹤。

啟用追蹤後，後續建立的所有原則都會預設啟用追蹤。 在伺服器上啟用追蹤之前建立的原則需要手動更新。

### 啟用或停用延伸使用量追蹤 {#enable-or-disable-extended-usage-tracking}

開始之前，請確保已啟用「伺服器審核」。 請參閱 [配置事件審核和隱私設定](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) ，了解有關審核的詳細資訊。

1. 在管理控制台中，按一下「服務>檔案安全性>設定>稽核和隱私權設定」 。
1. 若要設定延伸使用量追蹤，請在「啟用追蹤」下方選取「是」或「否」。
1. 若要在登入頁面上設定「允許收集詳細使用資料」核取方塊的選取，在「啟用追蹤」預設值下，選取「是」或「否」。

要查看跟蹤的事件，可以使用「事件」頁上的「文檔事件」篩選器。 使用JavaScript追蹤的事件會標示為「詳細使用追蹤」。 請參閱 [監控事件](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) 以取得事件的詳細資訊。

## 配置文檔安全顯示設定 {#configure-document-security-display-settings}

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「顯示選項」。
1. 配置設定並按一下「確定」。

### 顯示設定 {#display-settings}

**要針對搜索結果顯示的行：** 執行搜尋時在頁面上顯示的列數。

**用戶端登入對話方塊的自訂**

這些設定控制當用戶通過客戶端應用程式登錄到文檔安全時，在登錄提示中顯示的文本。

**歡迎文字：** 歡迎郵件文本，如「請使用您的用戶名和密碼登錄」。 歡迎郵件文本應包含有關如何登錄文檔安全以及如何聯繫組織中的管理員或其他指定支援人員以獲得幫助的資訊。 例如，如果外部用戶忘記密碼或需要註冊或登錄過程方面的幫助，則可能需要聯繫管理員。 歡迎文字的長度上限為512個字元。

**用戶名文本：** 用戶名框的文本標籤。

**密碼文本：** 密碼框的文本標籤。

**客戶端證書驗證對話框的定製**

這些設定控制證書驗證對話框中顯示的文本。

**選擇驗證類型文本：** 顯示的文字，用於引導用戶選擇驗證類型。

**選擇證書文本：** 顯示的文字，用於引導用戶選擇證書類型。

**證書不可用錯誤文本：** 當選取的憑證無法使用時，最多會顯示512個字元的訊息。

**客戶端證書顯示的定製**

**僅顯示受信任的憑據發行者：** 選中此選項時，客戶端應用程式只向用戶顯示配置為信任的AEM表單的憑據發行商的證書（請參閱管理證書和憑據）。 未選中此選項時，將向用戶顯示用戶系統上所有證書的清單。

## 配置動態水印 {#configure-dynamic-watermarks}

使用文檔安全性，可以配置動態水印選項的預設設定，在建立策略時可以應用該選項。 A *水印* 是疊加在文檔中文本上的影像。 它對於跟蹤文檔的內容非常有用，並有助於識別非法使用該內容。

動態水印可由由定義的變數（如使用者ID、日期和自訂文字）組成的文字，或由PDF內的豐富內容組成。 可以使用多個元素配置水印，每個元素都有自己的定位和格式。

水印不可編輯，因此是確保文檔內容機密性的更安全的方法。 動態水印還確保水印顯示足夠的用戶特定資訊以用作進一步分發文檔的威懾。

當收件人查看或打印文檔時，策略指定的水印將顯示在受策略保護的文檔中。 與永久水印不同，動態水印從不保存在文檔中，這提供了在內部網路環境中部署文檔時所需的靈活性，以確保查看應用程式顯示特定用戶的身份。 另外，如果文檔有多個用戶，使用動態水印意味著可以使用一個文檔，而不是多個版本，每個版本都帶有不同的水印。 顯示的水印反映當前用戶的身份。

請注意，動態水印與使用者可直接新增至Acrobat中檔案的水印不同。 結果是，在受策略保護的文檔中可以有兩個水印。

### 建立水印時的注意事項 {#considerations-when-creating-watermarks}

您可以使用多個水印元素建立動態水印，每個元素都指定為文本或PDF。 您可以在浮水印中加入最多五個元素。

如果選擇基於文本的水印，則可以指定水印內的多個元素以及多個文本條目，並指定每個元素的位置。 為這些元素指派有意義的名稱，例如頁首、頁尾等。

例如，如果要在頁首、頁尾、邊距和文檔中指定不同的文本作為水印，則可建立多個水印元素並指定其位置。 如果希望用戶的用戶ID和當前訪問文檔的日期顯示在標題中，則右邊距中的策略名稱，以及自定義文本「CONFIDENTIAL」在文檔上對角顯示，則可以定義單獨的水印元素，並將文本作為類型，並指定其格式和定位。 當將水印應用到文檔時，水印中的所有元素將按添加到水印的順序同時應用到文檔。

通常，您使用基於PDF的水印來包括圖形內容，如徽標或特殊符號，如版權或註冊商標。

可以通過修改文檔安全配置檔案來更改水印元素數和PDF檔案大小的限制。 請參閱 [更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters).

配置水印時，請記住以下事項：

* 不能將受密碼保護的PDF文檔用作水印元素。 但是，如果您建立的水印包含其他不受密碼保護的元素，則這些元素將作為水印的一部分應用。
* 您可以更改要用作水印元素的最大PDF檔案大小。 但是，用作水印的大型PDF文檔在離線同步應用了此類水印的文檔期間會降低效能。 請參閱 [更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters).
* 僅將所選PDF的第一頁用作水印。 請確定您要顯示為浮水印的資訊在第一頁本身上可用。
* 即使可以指定PDF文檔的縮放比例，如果您打算在頁首、頁尾或邊距中將PDF用作水印，請考慮頁面大小和佈局。
* 指定字型名稱時，請正確輸入名稱。 AEM forms會替換您指定的字型（如果該字型不存在於開啟文檔的客戶端電腦中）。
* 如果選擇文本作為水印內容，則將縮放選項指定為適合頁面大小對寬度不同的頁面無效。
* 當指定水印元素的位置時，請確保沒有多個元素具有相同的位置。 如果兩個水印元素具有相同的位置，如中心，則它們在文檔上會重疊，並按添加到水印的順序顯示。
* 指定字型大小和類型時，請確定頁面內已完全顯示文字長度。 文字內容會滾動到新行中，因此您打算出現在邊界中的浮水印內容可能會與頁面上的內容區域重疊。 不過，如果在Acrobat 9中開啟檔案，單行以外的文字會遭到截斷。

### 動態水印的限制 {#limitations-of-dynamic-watermarks}

某些客戶端應用程式可能不支援動態水印。 請參閱適當的Acrobat Reader DC擴充功能說明。 此外，請記住以下支援動態水印的Acrobat版本：

* 不能將受密碼保護的PDF文檔用作水印元素。
* Acrobat和Adobe Reader 10之前的版本不支援下列浮水印功能：

   * PDF水印
   * 浮水印中的多個元素(文字/PDF)
   * 進階選項，例如頁面範圍或顯示選項
   * 文本格式選項，如指定的字型、字型名稱和顏色。 不過，舊版Acrobat和Reader會以預設字型和顏色顯示文字內容。

* Acrobat 9.0及舊版：Acrobat 9.0及更舊版本不支援動態水印中的策略名稱。 如果Acrobat 9.0開啟了受策略保護的文檔，其中包含策略名稱和其他動態資料的動態水印，則顯示水印時不包含策略名稱。 如果動態水印僅包含策略名稱，Acrobat將顯示一條錯誤消息

### 添加動態水印模板 {#add-a-dynamic-watermark-template}

您可以建立動態水印範本。 這些模板仍可作為管理員或用戶建立的策略的配置選項。

>[!NOTE]
>
>導出配置檔案時，不會用其他配置資訊捕獲動態水印配置資訊。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「水印」。
1. 按一下新增。
1. 在「名稱」框中，鍵入新水印的名稱。

   ***附註&#x200B;**:水印或水印元素的名稱或說明中不能使用某些特殊字元。 請參閱 [編輯原則的考量事項](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies).*

1. 在「名稱」(Name)下，在加號旁，為水印元素（如Header）輸入有意義的名稱，然後添加說明，然後展開加號以顯示選項。
1. 在「源」下，選擇「文本」或「PDF」的水印類型。
1. 如果選擇了「文本」，請執行以下操作：

   * 選擇要包括的水印類型。 如果選擇「自定義文本」，請在相鄰框中鍵入要為水印顯示的文本。 請記住將作為浮水印顯示的文本長度。
   * 為水印文本的文本內容指定文本格式屬性，如字型名稱、字型大小、前景顏色和背景顏色。 將前景和背景顏色指定為十六進位值。

      ***附註&#x200B;**:如果選擇「適合頁面大小」縮放選項，則字型大小屬性不可用於編輯。*

1. 如果您選擇了富水印選項的PDF，請按一下 **瀏覽** 選擇水印PDF旁邊的，以選擇要用作水印的PDF文檔。

   ***附註&#x200B;**:請勿使用受密碼保護的PDF檔案。 如果指定受密碼保護的PDF作為水印元素，則不會應用水印。*

1. 在「用作背景」下，選擇「是」或「否」。

   **附註**:目前，水印會出現在前景中，而與此設定無關。

1. 要控制文檔上顯示水印的位置，請配置「垂直對齊」和「水準對齊」選項。
1. 選擇適合頁面大小，或選擇%並在框中鍵入百分比。 值必須是整數，而非分數。 要配置水印大小，可以使用頁的百分比值或設定水印以適合頁的大小。
1. 在「旋轉」(Rotation)框中，鍵入要旋轉水印的度。 範圍是–180到180。 使用負值逆時針旋轉水印。 值必須是整數，而非分數。
1. 在「不透明度」框中，鍵入百分比。 使用整數，而非小數。
1. 在「進階選項」下，設定下列項目：

   **頁面範圍選項**

   設定應顯示浮水印的頁面範圍。 將起始頁輸入為1，將結束頁輸入為–1，以使所有頁都標籤有水印。

   **顯示選項**

   選擇要讓浮水印出現的位置。 預設情況下，水印會同時出現在軟拷貝（聯機）和硬拷貝（打印）上。

1. 按一下 **新增** 在「浮水印元素」下添加更多水印元素（如有必要）。
1. 按一下「確定」。

### 編輯動態水印模板 {#edit-a-dynamic-watermark-template}

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「水印」。
1. 按一下清單中適當的浮水印。
1. 在「編輯水印」頁上，根據需要更改設定。
1. 按一下「確定」。

### 刪除動態水印模板 {#delete-a-dynamic-watermark-template}

刪除動態水印時，它不再可用於添加到新策略。 但是，水印仍保留在當前使用的現有策略上，並且當前保護的文檔繼續顯示動態水印，直到您或用戶編輯包含已刪除水印的策略為止。 編輯策略後，將不再應用水印。 此時將出現一條消息，指出策略上已刪除現有水印，用戶可以選擇另一個水印來替換它。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「水印」。
1. 選取適當浮水印旁的核取方塊，然後按一下「刪除」。
1. 按一下「確定」。

## 配置邀請的用戶註冊 {#configuring-invited-user-registration}

您組織外部的使用者可透過檔案安全性進行註冊。 已邀請的註冊和激活其帳戶的用戶可以使用其電子郵件地址和註冊時建立的密碼登錄到文檔安全。 已註冊的受邀用戶可以使用他們具有權限的受策略保護的文檔。

當受邀的使用者啟動後，就會成為本機使用者。 可使用「受邀」和「本地用戶」區域來配置和管理本地用戶。 (請參閱 [管理受邀和本機使用者帳戶](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts).)

根據您為受邀用戶啟用的功能，他們還可以使用以下文檔安全功能：

* 將策略應用於文檔
* 建立原則
* 將受邀的用戶添加到策略

當發生以下事件時，文檔安全性會自動生成註冊邀請電子郵件，除非用戶已在源LDAP目錄中或先前已被邀請註冊：

* 現有用戶將受邀用戶添加到策略
* 管理員在「邀請的用戶註冊」頁面上添加一個受邀用戶帳戶

註冊電子郵件包含註冊頁面的連結，以及如何註冊的資訊。 在受邀的使用者註冊後，檔案安全性會發出包含啟動頁面連結的啟動電子郵件。 啟用後，帳戶會維持有效，直到您停用或刪除為止。

如果啟用內置註冊，則只需指定一次SMTP伺服器、註冊電子郵件詳細資訊、訪問功能，以及重置密碼電子郵件資訊。 在啟用內置註冊之前，請確保已在「用戶管理」中建立本地域，並已將「文檔安全邀請用戶」角色分配給組織中的相應用戶和組。 (請參閱 [新增本機網域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) 和 [建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles).) 如果您未使用內建註冊，則必須使用AEM Forms SDK建立自己的使用者註冊系統。 請參閱「開發AEM表單的SPI」相關說明，位於 [使用AEM表單進行程式設計](/help/forms/developing/introducing-java-api-soap-quick.md). 如果不使用內置註冊選項，建議您在激活電子郵件和客戶端登錄螢幕中配置一條消息，以通知用戶如何聯繫管理員以獲取新密碼或其他資訊。

**啟用和配置邀請的用戶註冊**

預設情況下，已邀請的用戶註冊過程將被禁用。 您可以視需要啟用和停用邀請的使用者註冊，以確保檔案安全。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「邀請的用戶註冊」。
1. 選擇「啟用邀請的用戶註冊」。
1. （選用）視需要更新受邀的使用者註冊設定：

   * [排除或包含外部使用者或群組](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [伺服器和註冊帳戶參數](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [註冊邀請電子郵件設定](configuring-client-server-options.md#registration-invitation-email-settings)
   * [啟用電子郵件設定](configuring-client-server-options.md#activation-email-settings)
   * [設定密碼重設電子郵件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （可選）在內置註冊下，選擇是以啟用此選項。 如果未啟用內置註冊，則必須設定自己的用戶註冊系統。
1. 按一下「確定」。

### 排除或包含外部使用者或群組 {#exclude-or-include-an-external-user-or-group}

您可以限制某些外部用戶或用戶組的註冊與文檔安全性。 例如，此選項對於允許存取特定使用者群組但排除屬於該群組的特定個人非常有用。

下列設定位於「邀請的用戶註冊」頁面的「電子郵件限制篩選器」區域中。

**排除：** 輸入要排除的使用者或群組的電子郵件地址。 若要排除多個使用者或群組，請在新行上輸入每個電子郵件地址。 要排除屬於特定域的所有用戶，請輸入通配符和域名。 例如，要排除example.com域中的所有用戶，請輸入&amp;ast;.example.com。

**包含：** 輸入要包含的使用者或群組的電子郵件地址。 若要包含多個使用者或群組，請在新行上輸入每個電子郵件地址。 要包括屬於特定域的所有用戶，請輸入通配符和域名。 例如，要將所有用戶包括在example.com域中，請輸入&amp;ast;.example.com。

### 伺服器和註冊帳戶參數 {#server-and-registration-account-parameters}

下列設定位於「受邀用戶註冊」頁面的「常規設定」區域中。

**SMTP主機：** SMTP伺服器的主機名。 SMTP伺服器管理傳出的電子郵件通知，以註冊並啟用受邀的使用者帳戶。

如果SMTP主機需要，請在「SMTP伺服器帳戶名」和「SMTP伺服器帳戶密碼」框中鍵入所需資訊，以連接到SMTP伺服器。 有些組織沒有執行此要求。 如果需要資訊，請咨詢系統管理員。

**SMTP伺服器套接字類名：** SMTP伺服器的套接字類名。 例如， javax.net.ssl.SSLSocketFactory。

**電子郵件內容類型：** 接受的MIME類型，如text/plain或text/html。

**電子郵件編碼：** 傳送電子郵件訊息時要使用的編碼格式。 您可以指定任何編碼，例如Unicode的UTF-8，拉丁文的ISO-8859-1。 預設為UTF-8。

**重新導向電子郵件地址：** 當您指定此設定的電子郵件地址時，會將任何新邀請傳送至提供的地址。 此設定可用於測試用途。

**使用本機網域：** 選取適當的網域。 在新安裝時，請確定您是使用「使用者管理」建立網域。 如果這是升級，則在升級期間會建立外部使用者網域，可供使用。

**對SMTP伺服器使用SSL:** 選擇此選項可為SMTP伺服器啟用SSL。

**在註冊頁面上顯示登錄連結：** 在為受邀使用者顯示的註冊頁面上顯示登入連結。

**為SMTP伺服器啟用傳輸層安全性(TLS)**

1. 開啟管理主控台。

   管理控制台的預設位置為 `https://<server>:<port>/adminui`.

1. 導覽至「首頁>服務>檔案安全性>設定>受邀的使用者註冊」 。
1. 在「邀請的用戶註冊」中，指定所有配置設定，然後按一下「確定」。

   >[!NOTE]
   >
   >如果您使用Microsoft Office 365作為SMTP伺服器來發送用於用戶註冊的邀請，請使用以下設定：
   >
   >**SMTP主機：** smtp.office365.com
   >**埠：** 587

1. 接下來，您需要更新config.xml。 請參閱 [為傳輸層安全(TLS)啟用SMTP的配置](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果您對「受邀的使用者註冊」選項進行任何變更，則會覆寫config.xml檔案並停用TLS。 如果您覆寫變更，您必須執行上述步驟，重新啟用「受邀使用者註冊」的TLS支援。

### 註冊邀請電子郵件設定 {#registration-invitation-email-settings}

當您建立新的受邀用戶帳戶，或當現有用戶添加以前未註冊或被邀請註冊到策略的外部收件人時，文檔安全性會自動發出註冊邀請電子郵件。 該電子郵件包含一個連結，收件人可用於訪問註冊頁面並輸入個人帳戶資訊，包括用戶名和密碼。 密碼可以是八個字元的任意組合。

當收件者啟用帳戶時，使用者會變成本機使用者。

下列設定位於「邀請的用戶註冊」頁面的「邀請電子郵件配置」區域中。

**開始日期：** 傳送邀請電子郵件的來源電子郵件地址。 「寄件者」電子郵件地址的預設格式為postmaster@[your_installation_domain].com。

**主題：** 邀請電子郵件訊息的預設主旨。

**逾時：** 如果外部用戶未註冊，則註冊邀請過期的天數。 預設值為30天。

**訊息：** 邀請使用者註冊之訊息內文中顯示的文字。

### 啟用電子郵件設定 {#activation-email-settings}

邀請的使用者註冊後，檔案安全性會傳送啟動電子郵件。 啟動電子郵件包含帳戶啟動頁面的連結，使用者可在此啟動其帳戶。 啟用帳戶後，使用者可以使用其電子郵件地址和在註冊時建立的密碼來登入檔案安全性。

當收件者啟用使用者帳戶時，該使用者會變成本機使用者。

以下設定位於「邀請的用戶註冊」頁面的「激活電子郵件配置」區域中。

>[!NOTE]
>
>此外，建議您在登入畫面上設定訊息，以建議外部使用者如何聯絡其管理員以取得新密碼或其他資訊。

**開始日期：** 從中傳送啟動電子郵件的電子郵件地址。 此電子郵件地址從註冊者的電子郵件主機接收失敗的傳送通知，以及收件者回覆註冊電子郵件而傳送的任何訊息。 「寄件者」電子郵件地址的預設格式為postmaster@[your_installation_domain].com。

**主題：** 啟動電子郵件訊息的預設主旨。

**逾時：** 如果使用者未啟用帳戶，則啟動邀請過期的天數。 預設值為30天。

**訊息：** 在郵件正文中顯示的文本，用於指明需要激活收件人的用戶帳戶。 您可能還想要包括一些資訊，如如何聯繫管理員以獲取新密碼。

### 設定密碼重設電子郵件 {#configure-a-password-reset-email}

如果您必須重設受邀使用者的密碼，則會產生確認電子郵件，邀請使用者選擇新密碼。 無法確定用戶的密碼；如果使用者忘記，您必須重設。

下列設定位於「受邀用戶註冊」頁的「重置密碼電子郵件」區域中。

**開始日期：** 從中發送密碼重置電子郵件的電子郵件地址。 「寄件者」電子郵件地址的預設格式為postmaster@[your_installation_domain].com。

**主題：** 重設電子郵件訊息的預設主旨。

**訊息：** 在消息正文中顯示的文本是一條消息，指示收件人的外部用戶密碼被重置。

## 使用戶和組能夠建立策略 {#enable-users-and-groups-to-create-policies}

「配置」頁具有指向「我的策略」頁的連結，可在該頁中指定哪些最終用戶可以建立我的策略，以及哪些用戶和組在搜索結果中可見。 「我的策略」頁有兩個頁簽：

**「建立策略」頁簽：** 用於配置用戶權限以建立自定義策略。

**「可見用戶和組」頁簽：** 用於控制哪些用戶和組在用戶搜索結果中可見。 超級用戶或策略集管理員需要選擇在「用戶管理」中建立的域，並將其添加到每個策略集的可見用戶和組中。 此清單對策略集協調器是可見的，用於在選擇將用戶添加到策略時設定策略集協調器可以瀏覽的域的限制。

在授予使用者建立自訂原則的權限之前，請先考量您希望個別使用者擁有多少存取或控制權。 此外，請考慮讓使用者和群組在搜尋中可見時的公開程度。

### 指定可以建立策略的用戶和組 {#specify-users-and-groups-who-can-create-policies}

以管理員身分，指定哪些使用者和群組可以建立自訂原則。 可在使用者和群組層級設定此權限。 搜索功能將搜索用戶和組的用戶管理資料庫。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「我的策略」。
1. 在「我的策略」頁上，按一下「建立策略」頁簽，然後按一下「添加用戶和組」。
1. 在「查找」框中，鍵入要搜索的用戶或組的用戶名或電子郵件地址。 如果您沒有此資訊，請將方塊留空。 您也可以輸入部分名稱或電子郵件地址，例如只知道使用者名稱的前兩個字母時。
1. 在使用清單中，選擇搜索參數名稱或電子郵件。
1. 在「類型」清單中，選擇「組」或「用戶」以縮小搜索範圍。
1. 在「在」清單中，選擇要搜索的域。 如果您不知道使用者或群組的網域，請選取「所有網域」 。
1. 在「顯示」清單中，指定每頁要顯示的搜索結果數，然後按一下「查找」。
1. 要添加「我的策略」用戶和組，請為要添加的每個用戶和組選擇複選框。
1. 按一下「添加」，然後按一下「確定」。

您選取的使用者和群組現在擁有建立自訂原則的權限。

### 從用戶或組中刪除建立自定義策略權限 {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. 在文檔安全頁上，按一下配置>我的策略。
1. 在「我的策略」頁上，按一下「建立策略」頁簽。 將顯示具有建立自定義策略權限的用戶和組。
1. 選取要從此權限中移除的使用者和群組旁的核取方塊。
1. 按一下「刪除」，然後按一下「確定」。

### 指定在搜尋中可見的使用者和群組 {#specify-users-and-groups-that-are-visible-in-searches}

當用戶管理其自定義策略時，他們可以搜索要添加到其策略中的用戶和組。 您必須指定在這些搜尋中可看到使用者和群組的網域。

1. 在文檔安全頁上，按一下配置>我的策略。
1. 在「我的策略」頁上，按一下「可見的用戶和組」頁簽。
1. 要使域中的用戶和組可見，請按一下「添加域」，選擇域，然後按一下「添加」。 要刪除域，請選中域名旁的複選框，然後按一下刪除。

## 手動編輯文檔安全配置檔案 {#manually-editing-the-document-security-configuration-file}

可以導入和導出儲存在文檔安全資料庫中的配置資訊。 例如，當您從測試環境移至生產環境時，您可能想要製作設定資訊的備份副本，或者您想要編輯只能設定為編輯此檔案的進階選項。

您可以使用設定檔案進行下列變更：

[建立和編輯策略時顯示CATIA權限](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[指定離線同步的逾時期](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒絕特定應用程式的文檔安全服務](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[停用外部連結](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>匯入設定檔案會根據檔案中的資訊重新設定您的系統。 除了動態水印配置和自定義事件資訊，這些資訊不會隨導出的配置檔案一起保存。 您必須在新系統中手動配置此資訊。 只有熟悉文檔安全性和XML的系統管理員或專業服務顧問才應修改配置檔案的內容，例如重新配置損壞的設定或為特定企業部署方案調整參數。

**匯出設定檔案**

1. 在管理控制台中，按一下「服務」>「文檔安全」11 >「配置」>「手動配置」。
1. 按一下「匯出」 ，並將設定檔案儲存在其他位置。 預設檔案名為config.xml。
1. 按一下「確定」。
1. 在更改配置檔案之前，請製作備份副本，以備需要恢復時使用。

**匯入設定檔案**

1. 在管理控制台中，按一下「服務」>「文檔安全」11 >「配置」>「手動配置」。
1. 按一下「瀏覽」 ，前往設定檔案，然後按一下「匯入」 。 不能直接在「檔案名」(File Name)框中鍵入路徑。
1. 按一下「確定」。

### 指定離線同步的逾時期 {#specify-a-timeout-period-for-offline-synchronization}

文檔安全性允許用戶在未連接到文檔安全伺服器時開啟和使用受保護的文檔。 用戶的客戶端應用程式必須定期與伺服器同步，以保留離線使用的有效文檔。 第一次開啟受保護的文檔時，系統會詢問用戶是否應授權其電腦執行定期客戶端同步。

預設情況下，當用戶連接到文檔安全伺服器時，每四小時自動進行同步，並根據需要進行同步。 如果文檔的離線期間在用戶離線時過期，則用戶必須重新連接到伺服器以使客戶端應用程式與伺服器同步。

在文檔安全配置檔案中，可以指定自動背景同步的預設頻率。 此設定用作預設超時期客戶端應用程式，除非客戶端顯式設定自己的超時值。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，然後找出 `PolicyServer` 節點。 在該節點下，找出 `ServerSettings` 節點。
1. 在 `ServerSettings` 節點，添加以下條目，然後保存檔案：

   `<entry key="BackgroundSyncFrequency" value="`*時間* `"/>`

   where *時間* 是自動背景同步之間的秒數。 如果您將此值傳送至 `0`，則一律會進行同步。 預設值為 `14400` 秒（每四小時）。

1. 匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 拒絕特定應用程式的文檔安全服務 {#denying-document-security-services-for-specific-applications}

您可以配置文檔安全性以拒絕對符合特定條件的應用程式提供服務。 條件可以指定單一屬性，例如平台名稱，也可以指定多組屬性。 此功能可協助您控制檔案安全性必須處理的要求。 此功能的部分應用程式如下：

* **收入保護：** 您可能會想要拒絕任何不支援您收入慣例之用戶端應用程式的存取權。
* **應用程式相容性：** 某些應用程式可能與文檔安全伺服器的策略或行為不相容。

當客戶端應用程式嘗試建立與文檔安全性的連結時，它們會提供應用程式、版本和平台資訊。 文檔安全性將此資訊與從文檔安全配置檔案獲取的拒絕設定進行比較。

拒絕設定可包含陣列拒絕條件。 如果任何一組的所有屬性都匹配，則請求應用程式被拒絕訪問文檔安全服務。

拒絕服務功能要求客戶端應用程式使用文檔安全性C++客戶端SDK 8.2版或更新版本。 以下Adobe產品在請求文檔安全服務時提供產品資訊：

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard和更新版本
* Adobe Reader 9.0和更新版本
* Acrobat Reader DC Microsoft Office 8.2及更新版本的擴充功能

用戶端應用程式會使用檔案安全性C++用戶端SDK中的用戶端API，從檔案安全性要求服務。 用戶端API請求包括平台和SDK版本資訊（預編譯至用戶端API），以及從用戶端應用程式取得的產品資訊。

用戶端應用程式或外掛程式在其回呼函式的實施中提供產品資訊。 應用程式提供下列資訊：

* Integrator名稱
* Integrator版本
* 應用程式系列
* 應用程式名稱
* 應用程式版本

如果有任何資訊不適用，客戶端應用程式將相應欄位留空。

數個Adobe應用程式在請求檔案安全服務時都包含產品資訊，包括Acrobat、Adobe Reader和Microsoft Office的Acrobat Reader DC擴充功能。

**Acrobat和Adobe Reader**

當Acrobat或Adobe Reader向檔案安全性要求服務時，會提供下列產品資訊：

* **整合商：** Adobe Systems公司
* **Integrator版本：** 1.0
* **應用程式系列：** Acrobat
* **應用程式名稱：** Acrobat
* **應用程式版本：** 9.0.0

**Acrobat Reader DC Microsoft Office擴充功能**

Acrobat Reader DC Extensions for Microsoft Office是與Microsoft Office產品Microsoft Word、Microsoft Excel和Microsoft PowerPoint搭配使用的外掛程式。 當它請求服務時，它提供以下資訊：

* **整合商：** Adobe Systems Incorporated
* **Integrator版本：** 8.2
* **應用程式系列：** Acrobat Reader DC Microsoft Office擴充功能
* **應用程式名稱：** Microsoft Word、Microsoft Excel或Microsoft PowerPoint
* **應用程式版本：** 2003年或2007年

**配置文檔安全性以拒絕特定應用程式的服務**

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，然後找出 `PolicyServer` 節點。 新增 `ClientVersionRules` 節點作為的直接子節點 `PolicyServer` 節點，如果其中一個不存在，則：

   ```xml
    <node name="ClientVersionRules">
        <map>
            <entry key="infoURL" value="URL"/>
        </map>
        <node name="Denials">
            <map/>
            <node name="MyEntryName">
                <map>
                    <entry key="SDKPlatforms" value="platforms"/>
                    <entry key="SDKVersions" value="versions"/>
                    <entry key="AppFamilies" value="families"/>
                    <entry key="AppNames" value="names"/>
                    <entry key="AppVersions" value="versions"/>
                    <entry key="Integrators" value="integrators"/>
                    <entry key="IntegratorVersions" value="versions"/>
                </map>
            </node>
            <node name="MyOtherEntryName"
                <map>
                    [...]
                </map>
            </node>
            [...]
        </node>
    </node>
   ```

   其中：

   `SDKPlatforms` 指定托管客戶端應用程式的平台。 可能的值包括：

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX

   `SDKVersions` 指定客戶端應用程式使用的文檔安全性C++客戶端API的版本。 例如, `"8.2"`.

   `APPFamilies` 由用戶端API定義。

   `AppName`指定客戶端應用程式的名稱。 逗號是名稱分隔符號。 若要在名稱中加入逗號，請以反斜線(\)字元逸出。 例如， *&quot;Adobe Systems\，公司&quot;*.

   `AppVersions` 指定客戶端應用程式的版本。

   `Integrators` 指定開發插件或整合應用程式的公司或組的名稱。

   `IntegratorVersions` 是外掛程式或整合應用程式的版本。

1. 對於每一組附加的拒絕資料，添加另一組 *MyEntryName* 元素。
1. 儲存設定檔案。
1. 匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

**範例**

在此示例中，所有Windows客戶端都被拒絕訪問。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://www.dont.use/windows.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="SDKPlatforms" value="Microsoft Windows"/>
             </map>
         </node>
     </node>
 </node>
```

在此示例中，My Application 3.0版和My Other Application 2.0版被拒絕訪問。 無論拒絕的原因為何，都會使用相同的拒絕資訊URL。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="FirstDenialSettings">
             <map>
                 <entry key="AppNames" value="My Application"/>
                 <entry key="AppVersions" value="3.0"/>
             </map>
         </node>
         <node name="SecondDenialSettings">
             <map>
                 <entry key="AppNames" value="My Other Application"/>
                 <entry key="AppVersions" value="2.0"/>
             </map>
         </node>
     </node>
 </node>
```

在此範例中，來自Microsoft PowerPoint 2007或Microsoft PowerPoint 2010安裝Microsoft Office適用的Acrobat Reader DC擴充功能的所有請求皆遭拒絕。

```xml
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value="https://get.a.new/version.html"/>
     </map>
     <node name="Denials">
         <map/>
         <node name="Entry_1">
             <map>
                 <entry key="AppFamilies" value=
     "document security Extension for Microsoft Office"/>
                 <entry key="AppNames" value= "Microsoft PowerPoint"/>
                 <entry key="AppVersions" value="2007,2010"/>
             </map>
         </node>
     </node>
 </node
```

### 更改水印配置參數 {#change-the-watermark-configuration-parameters}

預設情況下，您最多可以在水印中指定五個元素。 此外，要用作水印的PDF文檔的檔案大小上限為100KB。 您可以在config.xml檔案中變更這些參數。

***附註&#x200B;**:您應謹慎變更這些參數。*

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，然後找出 `ServerSettings` 節點。
1. 在 `ServerSettings` 節點，添加以下條目，然後保存檔案： `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一條， *最大檔案大小* 是PDF水印元素允許的最大檔案大小（以KB為單位）。 預設為100KB。

   第二條， *最大元素* 是浮水印中允許的最大元素數。 預設為5。

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 停用外部連結 {#disabling-external-links}

許多檔案安全性使用者無法存取外部連結，例如 **www.adobe.com** 當他們使用正確的管理用戶介面時：

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`。

對config.xml所做的以下更改將禁用Right Management用戶介面中的所有外部連結。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，然後找出 `DisplaySettings` 節點。
1. 若要停用所有外部連結，請在 `DisplaySettings` 節點，添加以下條目，然後保存檔案： `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 為傳輸層安全(TLS)啟用SMTP的配置 {#configuration-to-enable-smtp-for-transport-layer-security-tls}

下列config.xml變更為「邀請的使用者註冊」功能啟用TLS支援。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，然後找出 `DisplaySettings` 節點。
1. 找出下列節點： `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. 設定 `SmtpUseTls` 鍵 `ExternalUser` 節點到 **true**.
1. 設定 `SmtpUseSsl` 鍵 `ExternalUser` 節點到 **false**.
1. 儲存 `config.xml`.
1. 匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 禁用文檔安全文檔的SOAP端點 {#disable-soap-endpoints-for-document-security-documents}

對config.xml所做的以下更改將禁用文檔安全文檔的SOAP端點。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟設定檔案，並找到下列節點： `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. 在DRM節點中，找到 `entry` 節點：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 要禁用文檔安全文檔的SOAP端點，請將值屬性設定為 **false**.

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 儲存 `config.xml`.
1. 匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)

### 提高文檔安全伺服器的可擴充性 {#increasingscalability}

預設情況下，在同步文檔以供離線使用時，文檔安全客戶端將獲取用戶有權訪問的所有其它文檔的策略、水印、許可證和吊銷更新資訊。 如果這些更新和資訊未與客戶端同步，則離線模式下開啟的文檔仍可能使用舊的策略、水印和撤銷資訊開啟。

通過限制發送到客戶端的資訊，可以提高文檔安全伺服器的可擴充性。 向客戶端發送的資訊量減少，從而提高了可擴充性、縮短了響應時間，並且提高了伺服器的效能。 執行下列步驟以提高可擴充性：

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
1. 在編輯器中開啟配置檔案，並找到「伺服器設定」節點。
1. 在ServerSettings節點中，設定 `DisableGlobalOfflineSynchronizationData`屬性 `true`.

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   當設定為true時，文檔安全伺服器僅發送當前文檔的資訊，其餘文檔（用戶有權訪問的其他文檔）的資訊不會發送到客戶端。

   >[!NOTE]
   >
   >依預設， `DisableGlobalOfflineSynchronizationData`鍵設為 `false`.

1. 儲存並匯入設定檔案。 (請參閱 [手動編輯文檔安全配置檔案](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file).)
