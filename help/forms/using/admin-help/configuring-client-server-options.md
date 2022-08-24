---
title: 配置客戶端和伺服器選項
seo-title: Configuring client and server optionsn
description: 瞭解如何配置各種客戶端和伺服器選項，如伺服器配置設定、文檔安全形色和事件審核。
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

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「伺服器配置」。
1. 配置設定，然後按一下「確定」。

## 伺服器配置設定 {#server-configuration-settings}

**基本URL:** 包含伺服器名稱和埠的基本文檔安全URL。 附加到基礎的資訊會建立連接URL。 例如，在訪問網頁時會附加/edc/Main.do。 用戶還通過此URL響應外部用戶註冊邀請。

如果使用IPv6，請輸入基本URL作為電腦名稱或DNS名稱。 如果使用數字IP地址，Acrobat將無法開啟受策略保護的檔案。 此外，請為伺服器使用HTTP安全(HTTPS)URL。

>[!NOTE]
>
>基本URL嵌入到受策略保護的檔案中。 客戶端應用程式使用基本URL連接回伺服器。 即使稍後更改了基URL，受保護的檔案仍將繼續包含該URL。 如果更改基本URL，則需要為所有連接的客戶端更新配置資訊。

**預設離線租用期：** 用戶離線使用受保護文檔的預設時間長度。 此設定確定在建立策略時自動離線租用期設定的初始值。 （請參閱建立和編輯策略。） 租用期到期後，收件人必須再次同步文檔以繼續使用它。

有關離線租用和同步工作方式的討論，請參見 [配置離線租用和同步的初級知識](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)。

**預設離線同步期間：** 自文檔初始受保護後離線使用的最長時間。

**客戶端會話超時：** 如果通過客戶端應用程式登錄的用戶不與文檔安全性進行交互，則文檔安全性斷開連接的時間長度（以分鐘為單位）。

**允許匿名用戶訪問：** 選擇此選項可啟用建立允許匿名用戶開啟受策略保護的文檔的共用策略和個人策略的功能。 （沒有帳戶的用戶可以訪問文檔，但無法登錄到文檔安全性或使用其他受策略保護的文檔。）

**禁用對版本7客戶端的訪問：** 指定用戶是否可以使用Acrobat或Reader7.0連接到伺服器。 選擇此選項後，用戶必須使用Acrobat或Reader8.0及更高版本完成對PDF文檔的文檔安全操作。 如果策略要求在開啟受策略保護的文檔時，Acrobat或Reader8.0及更高版本必須以認證模式運行，則應禁用對Acrobat或Reader7的訪問。 （請參閱指定用戶和組的文檔權限。）

**允許每個文檔離線訪問** 選擇此選項可指定每個文檔的離線訪問。 如果啟用此設定，則用戶將只能離線訪問該用戶至少聯機開啟過的那些文檔。

**允許用戶名密碼驗證：** 選擇此選項可使客戶端應用程式在連接到伺服器時使用用戶名/密碼驗證。

**允許Kerberos身份驗證：** 選擇此選項可使客戶端應用程式在連接到伺服器時使用Kerberos身份驗證。

**允許客戶端證書身份驗證：** 選擇此選項可使客戶端應用程式在連接到伺服器時使用證書驗證。

**允許擴展身份驗證** 選擇以啟用擴展驗證，然後輸入擴展驗證登錄URL。

選擇此選項可使客戶端應用程式使用擴展身份驗證。 擴展身份驗證提供了自定義身份驗證進程和在表單伺服器上配置的AEM不同身份驗證選項。 例如，用戶現在可以體驗基於SAML的身份驗證，而AEM不是來自Acrobat和Reader客戶端的表單用戶名/密碼。 預設情況下，登錄URL包含 *本地主機* 作為伺服器名。 將伺服器名稱替換為完全限定的主機名。 如果尚未啟用擴展驗證，則登錄URL中的主機名將自動從基本URL填充。 請參閱 [添加擴展身份驗證提供程式](configuring-client-server-options.md#add-the-extended-authentication-provider)。

***附註&#x200B;**:在AppleMacOS X上支援擴展身份驗證，Adobe Acrobat11.0.6及更高版本。*

**擴展HTML的首選驗證控制寬度** 指定在Acrobat開啟以輸入用戶憑據的擴展身份驗證對話框的寬度。

**擴展HTML的首選驗證控制高度** 指定在Acrobat開啟以輸入用戶憑據的擴展身份驗證對話框的高度。

***附註&#x200B;**:此對話框的寬度和高度限制如下：*
寬度：最小= 400，最大= 900

高度：最少= 450;最大= 800

**啟用客戶端憑據快取：** 選擇此選項可允許用戶快取其憑據（用戶名和密碼）。 快取用戶的憑據時，他們不必在每次開啟文檔或按一下Adobe Acrobat「管理安全策略」頁面上的「刷新」按鈕時輸入其憑據。 您可以指定用戶必須再次提供其憑據的天數。 將天數設定為0允許無限期快取憑據。

## 配置文檔安全用戶和管理員 {#configuring-document-security-users-and-administrators}

### 為管理員分配文檔安全形色 {#assigning-document-security-roles-to-administrators}

您的AEM表單環境包含一個或多個具有建立用戶和組的適當權限的管理員用戶。 如果您的組織正在使用文檔安全性，則還必須至少為一名管理員分配管理已邀請和本地用戶的權限。

管理員還必須具有管理控制台用戶角色才能訪問管理控制台。 (請參閱 [建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)

### 配置可見用戶和組 {#configuring-visible-users-and-groups}

要在策略用戶搜索期間查看選定域中的用戶和組，超級管理員或策略集管理員必須選擇並將域（在用戶管理中建立）添加到每個策略集的可見用戶和組清單中。

可見用戶和組清單對策略集協調器可見，用於限制最終用戶在選擇要添加到策略的用戶或組時可以瀏覽的域。 如果未執行此任務，則策略集協調器將找不到要添加到策略的任何用戶或組。 任何給定策略集都可以有多個策略集協調器。

1. 安裝並配置具有文檔AEM安全性的表單環境後，請在「用戶管理」中設定所有相應的域。 <!-- Fix broken link (See Setting up and managing domains) -->

   ***附註&#x200B;**:必須先建立域，然後才能建立任何策略。*

1. 在管理控制台中，按一下「服務」>「文檔管理」>「策略」，然後按一下「策略集」頁籤。
1. 選擇全局策略集，然後按一下可見用戶和組頁籤。
1. 按一下「添加域」(Add Domain)，然後根據需要添加現有域。
1. 導航到「服務」>「文檔安全性」>「配置」>「我的策略」，然後按一下「可見用戶和組」頁籤。
1. 按一下「添加域」(Add Domain)，然後根據需要添加現有域。

## 添加擴展身份驗證提供程式 {#add-the-extended-authentication-provider}

表AEM單提供了一個示例配置，您可以為環境自定義該配置。 執行以下步驟：

>[!NOTE]
>
>在AppleMacOS X上支援擴展身份驗證，Adobe Acrobat11.0.6及更高版本。

1. 獲取部署WAR檔案的示例。 請參閱適用於您的應用程式伺服器的安裝指南。
1. 確保表單伺服器具有完全限定的名稱，而不是IP地址作為基本URL，並且它是HTTPS URL。 請參閱 [伺服器配置設定](configuring-client-server-options.md#server-configuration-settings)。
1. 從「伺服器配置」頁啟用擴展身份驗證。 請參閱 [伺服器配置設定](configuring-client-server-options.md#server-configuration-settings)。
1. 在「用戶管理」配置檔案中添加所需的SSO重定向URL。 請參閱 [添加SSO重定向URL以進行擴展驗證](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)。

### 添加SSO重定向URL以進行擴展驗證 {#add-sso-redirect-urls-for-extended-authentication}

啟用擴展驗證後，在AcrobatXI或ReaderXI中開啟策略保護文檔的用戶將獲得用於驗證的對話框。 此對話框將載入您在文檔安全伺服器設定上指定為擴展HTML登錄URL的驗證頁。 請參閱 [伺服器配置設定](configuring-client-server-options.md#server-configuration-settings)。

>[!NOTE]
>
>在AppleMacOS X上支援擴展身份驗證，Adobe Acrobat11.0.6及更高版本。

1. 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「導入和導出配置檔案」。
1. 按一下導出，將配置檔案保存到磁碟。
1. 在編輯器中開啟檔案，並找到AllowedUrls節點。
1. 在 `AllowedUrls` ，添加以下行： `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```xml
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 保存檔案，然後從「手動配置」頁導入更新的檔案：在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「導入和導出配置檔案」。

## 配置離線安全性 {#configuring-offline-security}

文檔安全提供了離線使用受策略保護的文檔而無需連接網際網路或網路連接的能力。 此功能要求策略允許離線訪問，如中所述 [指定用戶和組的文檔權限](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups)。 在離線使用具有此策略的文檔之前，收件人必須在聯機時開啟文檔，並在出現提示時按一下「是」啟用離線訪問。 還可請求接收者驗證其身份。 然後，收件人可以在策略中指定的離線租用期間內離線使用文檔。

離線租用期結束時，收件人必須通過聯機開啟文檔或使用Acrobat或Acrobat Reader DC擴展菜單命令進行同步來再次與文檔安全性同步。 (請參閱 *Acrobat幫助* 或適當 *Acrobat Reader DC擴展幫助*。)

由於允許離線訪問的文檔要求在離線儲存檔案的電腦上快取密鑰材料，因此如果未經授權的用戶能夠獲取密鑰材料，則檔案可能會受到損害。 為了彌補這一可能性，提供了計畫和手動密鑰滾動更新選項，您可以配置這些選項來防止未經授權的人使用密鑰訪問文檔。

### 設定預設離線租用期 {#set-a-default-offline-lease-period}

受策略保護文檔的接收者可以使文檔在策略中指定的天數內離線。 最初將文檔與文檔安全性同步後，收件人可以離線使用文檔，直到離線租用期到期。 租用期到期後，收件人必須聯機並登錄以與文檔安全性同步，以繼續使用文檔。

您可以配置預設離線租用期。 當任何人建立或編輯策略時，可以從預設值更改租用期。

1. 在文檔安全頁上，按一下「配置」>「伺服器配置」。
1. 在「預設離線租用期間」框中，鍵入離線租用期間的天數。
1. 按一下「確定」。

### 管理密鑰轉換 {#manage-key-rollovers}

文檔安全使用加密算法和許可證來保護文檔。 當對文檔進行加密時，文檔安全性生成並管理稱為 *文檔密鑰* 它傳遞給客戶端應用程式。 如果保護文檔的策略允許離線訪問，則離線密鑰稱為 *主鍵* 也為每個對文檔具有離線訪問權限的用戶生成。

>[!NOTE]
>
>如果主密鑰不存在，文檔安全性將生成一個密鑰以保護文檔。

要離線開啟受策略保護的文檔，用戶的電腦必須具有相應的主密鑰。 當用戶與文檔安全性同步（聯機開啟受保護的文檔）時，電腦獲取主密鑰。 如果此主密鑰被洩露，則用戶具有離線訪問權限的任何文檔都可能被洩露。

減少離線文檔威脅的一種方法是避免允許離線訪問特別敏感的文檔。 另一種方法是週期性地滾動主鍵。 當文檔安全性將密鑰滾動時，任何現有密鑰都無法再訪問受策略保護的文檔。 例如，如果犯罪者從失竊的筆記型電腦中獲得主密鑰，則該密鑰無法用於訪問滾動更新後受保護的文檔。 如果您懷疑某個特定主密鑰已被洩露，則可以手動將該密鑰滾過。

但是，您還需要注意，密鑰滾動更新會影響所有主密鑰，而不僅影響一個。 它還降低了系統的可擴充性，因為客戶端必須儲存更多密鑰才能進行離線訪問。 預設密鑰滾動更新頻率為20天。 建議不要將此值設定為低於14天，因為可能會阻止人員查看離線文檔，並且可能會影響系統效能。

在以下示例中，Key1是兩個主鍵中較舊的鍵，Key2是較新的鍵。 當您第一次按一下「立即滾動更新密鑰」按鈕時，Key1將變為無效，並生成一個較新的有效主密鑰(Key3)。 當用戶與文檔安全性同步時，他們將獲得Key3，這通常是通過線上開啟受保護的文檔。 但是，在用戶達到策略中指定的最大離線租用期之前，不會強制用戶與文檔安全性同步。 在第一次密鑰滾動更新後，保持離線狀態的用戶仍然可以開啟離線文檔，包括受Key3保護的文檔，直到達到最大離線租用期。 當您再次按一下「立即滾動更新密鑰」按鈕時，Key2將變為無效，並建立Key4。 在兩個密鑰滾動過程中保持離線狀態的用戶在與文檔安全性同步之前無法開啟受Key3或Key4保護的文檔。

**更改關鍵滾動頻率**

為保密起見，當您使用離線文檔時，文檔安全性提供了自動密鑰滾動更新選項，預設頻率為20天。 可以更改滾動頻率；但是，請避免將值設定為低於14天，因為可能會阻止人們查看離線文檔，並且可能會影響系統效能。

1. 在文檔安全頁面上，按一下配置>密鑰管理。
1. 在「關鍵滾動更新頻率」框中，鍵入滾動更新期間的天數。
1. 按一下「確定」。

**手動滾動主鍵**

要保持離線文檔的機密性，可以手動滾動主鍵。 您可能會發現必須手動滾動一個密鑰（例如，如果某個人從電腦獲取了該密鑰，而該密鑰在電腦中被快取，以便離線訪問文檔）。

>[!NOTE]
>
>避免經常使用手動滾動更新，因為它會導致所有主鍵滾動，而不是只滾動一個主鍵，並且可能會暫時阻止用戶離線查看新文檔。

必須先對主密鑰進行兩次滾動，然後才能使客戶端電腦上以前存在的密鑰無效。 已使主密鑰失效的客戶端電腦必須與文檔安全服務重新同步以獲取新的主密鑰。

1. 在文檔安全頁面上，按一下配置>密鑰管理。
1. 按一下「Rovel Keys Now（立即更新滑鼠指針）」 ，然後按一下「OK（確定）」。
1. 等大約10分鐘。 伺服器日誌中顯示以下日誌消息： `Done RightsManagement key rollover for`*N* `principals`。 位置 *N* 是文檔安全系統中的用戶數。
1. 按一下「Rovel Keys Now（立即更新滑鼠指針）」 ，然後按一下「OK（確定）」。
1. 等大約10分鐘。

## 配置事件審核和隱私設定 {#configuring-event-auditing-and-privacy-settings}

文檔安全性可以審核和記錄與與受策略保護的文檔、策略、管理員和伺服器交互相關的事件的資訊。 您可以配置事件審計，也可以指定要審計的事件類型。 要審計特定文檔的事件，還必須啟用策略上的審計選項。

啟用審計後，您可以在「事件」頁上查看審計事件的詳細資訊。 文檔安全用戶還可以查看與他們使用或建立的受策略保護的文檔有關的事件。

您可以選擇以下類型的事件進行審計：

* 受策略保護的文檔事件，如授權或未授權用戶嘗試開啟文檔
* 策略事件，如策略的建立、更改、刪除、啟用和禁用
* 用戶事件，如外部用戶邀請和註冊、激活和停用的用戶帳戶、對用戶密碼的更改以及配置檔案更新
* 表AEM單事件，如版本不匹配、目錄伺服器和授權提供程式不可用以及伺服器配置更改

### 啟用或禁用事件審計 {#enable-or-disable-event-auditing}

可以啟用和禁用與伺服器、受策略保護的文檔、策略、策略集和用戶相關的事件的審核。 啟用事件審計後，您可以選擇審計所有可能的事件，也可以選擇要審計的特定事件。

啟用伺服器審核後，可以在「事件」頁上查看審核事件。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「審核和隱私設定」。
1. 要配置伺服器審核，請在啟用伺服器審核下，選擇是或否。
1. 如果選擇「是」，則在每個事件類別下執行以下操作之一以選擇要審核的選項：

   * 要審核類別中的所有事件，請選擇「全部」。
   * 要僅審核某些事件，請取消選擇「全部」，然後選擇要審核的事件旁邊的複選框。

      (請參閱 [事件審計選項](configuring-client-server-options.md#event-auditing-options)。)

1. 按一下「確定」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，如「後退」按鈕、「刷新」按鈕和「後退」或「前進」箭頭，因為此操作可能導致不需要的資料捕獲和資料顯示問題。

### 啟用或禁用隱私通知 {#enable-or-disable-privacy-notification}

您可以啟用和禁用隱私通知消息。 啟用隱私通知時，當收件人嘗試開啟受策略保護的文檔時，會顯示一條消息。 通知通知用戶文檔使用正在被審計。 您還可以指定用戶可用於查看隱私策略頁的URL（如果該頁可用）。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「審核和隱私設定」。
1. 要配置隱私通知，請在啟用隱私通知下，選擇是或否。

   如果附加到文檔的策略允許匿名用戶訪問，並且「啟用隱私通知」設定為「否」，則不會提示用戶登錄，並且不顯示隱私通知消息。

   如果附加到文檔的策略不允許匿名用戶訪問，用戶將看到隱私通知消息。

1. 如果適用，在「隱私URL」框中，鍵入隱私策略頁的URL。 如果「隱私URL」框留空，則顯示adobe.com的隱私頁。
1. 按一下「確定」。

>[!NOTE]
>
>禁用隱私聲明不會禁用文檔使用情況審核。 通過擴展使用情況跟蹤支援的現成審計操作和自定義操作仍然可以收集用戶行為資訊。

### 導入自定義審核事件類型 {#import-a-custom-audit-event-type}

如果您使用的是支援審核其他事件（如特定於某種檔案類型的事件）的啟用文檔安全的應用程式，則Adobe合作夥伴可以為您提供自定義審核事件，您可以將這些事件導入文檔安全性中。 僅當Adobe夥伴為您提供了自定義事件類型時，才使用此功能。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「事件管理」。
1. 按一下「瀏覽」轉到要導入的XML檔案，然後按一下「導入」。
1. 如果發現相同的事件代碼和命名空間組合，則導入會覆蓋伺服器上的現有自定義審計事件類型。
1. 按一下「確定」。

### 刪除自定義審核事件類型 {#delete-a-custom-audit-event-type}

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「事件管理」。
1. 選中要刪除的自定義審計事件類型旁邊的複選框，然後按一下刪除。
1. 按一下「確定」。

### 導出審核事件 {#export-audit-events}

您可以將審核事件導出到檔案以便存檔。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「事件管理」。
1. 根據需要編輯「導出審計事件」下的設定。 可以指定：

   * 要導出的審核事件的最低年齡
   * 單個檔案中要包含的最大審計事件數。 伺服器根據此值生成一個或多個檔案。
   * 建立檔案的資料夾。 此資料夾位於表單伺服器上。 如果資料夾路徑是相對的，則它是相對於應用程式伺服器根目錄的。
   * 用於審計事件檔案的檔案前置詞
   * 檔案的格式，即與MicrosoftExcel相容的逗號分隔值(CSV)檔案或XML檔案。

1. 按一下「導出」。 如果要取消導出，請按一下「取消導出」。 如果其他用戶已計畫導出，則在導出完成之前「取消導出」按鈕不可用。 如果其他用戶已計畫導出，則「取消導出」按鈕不可用。 要檢查計畫的「導出」或「刪除」是否已啟動或完成，請按一下「刷新」。

### 刪除審計事件 {#delete-audit-events}

您可以刪除超過指定天數的審計事件。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「事件管理」。
1. 在刪除審計事件下，在刪除審計事件早於的框中指定天數。
1. 按一下刪除。按一下「導出」。 如果要取消刪除，請按一下「取消刪除」。 如果其他用戶已計畫刪除，則在導出完成之前，「取消刪除」按鈕不可用。 如果其他用戶已計畫導出，則「取消刪除」按鈕不可用。 要檢查計畫的刪除是否已啟動或完成，請按一下刷新。

### 事件審計選項 {#event-auditing-options}

可以啟用和禁用事件審計並指定要審計的事件類型。

**文檔事件**

**查看文檔：** 收件人查看受策略保護的文檔。

**關閉文檔：** 收件人關閉受策略保護的文檔。

**打印低解析度** 收件人打印具有指定低解析度選項的受策略保護的文檔。

**打印高解析度：** 收件人打印具有指定高解析度選項的受策略保護的文檔。

**將注釋添加到文檔：** 收件人將注釋添加到PDF文檔。

**撤消文檔：** 用戶或管理員撤消對受策略保護的文檔的訪問權限。

**取消撤消文檔：** 用戶或管理員重新授予對受策略保護的文檔的訪問權限。

**表單填充：** 接收者將資訊輸入到可填充的PDF文檔中。

**已刪除策略：** 發佈者從文檔中刪除策略以撤消安全保護。

**更改文檔吊銷URL:** 來自API級別的調用更改指定的撤消URL，以便訪問替換撤消文檔的新文檔。

**修改文檔：** 收件人更改受策略保護文檔的內容。

**簽名文檔：** 收件人簽署文檔。

**保護新文檔：** 用戶應用策略來保護文檔。

**切換文檔策略：** 用戶或管理員切換附加到文檔的策略。

**將文檔發佈為：** 在伺服器上註冊一個文檔，其documentName和許可證與現有文檔相同，且這些文檔沒有父子關係。 可以使用表單SDK觸AEM發此事件。

**迭代文檔：** 在伺服器上註冊一個文檔，其documentName和許可證與現有文檔相同，並且這些文檔具有父子關係。 可以使用表單SDK觸AEM發此事件。

**策略事件**

**已建立策略：** 用戶或管理員建立策略。

**已啟用策略：** 管理員使策略可用。

**更改的策略：** 用戶或管理員更改策略。

**禁用的策略：** 管理員使策略不可用。

**已刪除策略：** 用戶或管理員刪除策略。

**更改策略所有者：** 來自API級別的調用會更改策略所有者。

**用戶事件**

**已刪除用戶：** 管理員刪除用戶帳戶。

**註冊邀請的用戶：** 外部用戶註冊文檔安全性。

**成功登錄：** 管理員或用戶成功登錄嘗試。

**邀請的用戶：** 文檔安全性邀請用戶註冊。

**激活的用戶：** 外部用戶通過使用激活電子郵件中的URL激活其帳戶，或管理員啟用帳戶。

**更改密碼：** 被邀請的用戶更改其密碼或管理員重置本地用戶的密碼。

**登錄失敗：** 管理員或用戶登錄嘗試失敗。

**已停用的用戶：** 管理員禁用本地用戶帳戶。

**配置檔案更新：** 邀請的用戶更改其名稱、組織名稱和密碼。

**帳戶已鎖定：** 管理員鎖定帳戶。

**策略集事件**

**已建立策略集：** 管理員或策略集協調器建立策略集。

**已刪除策略集：** 管理員或策略集協調器刪除策略集。

**修改的策略集：** 管理員或策略集協調員更改策略集。

**系統事件**

**目錄同步完成：** 「事件」頁面中不提供此資訊。 「域管理」頁上顯示當前目錄同步資訊，包括上次同步的當前同步狀態和時間。 要訪問管理控制台中的「域管理」頁，請按一下「設定」>「用戶管理」>「域管理」。

**客戶端啟用離線訪問：** 用戶允許離線訪問針對用戶電腦上的伺服器進行保護的文檔。

**同步客戶端** 客戶端應用程式必須將資訊與伺服器同步，以允許離線訪問。

**版本不匹配：** 與伺服器AEM不相容的表單SDK版本嘗試連接到伺服器。

**目錄同步資訊：** 「事件」頁面中不提供此資訊。 「域管理」頁上顯示當前目錄同步資訊，包括上次同步的當前同步狀態和時間。 要訪問管理控制台中的「域管理」頁，請按一下「設定」>「用戶管理」>「域管理」。

**伺服器配置更改：** 通過網頁或通過導入config.xml檔案手動完成對伺服器配置的更改。 這包括對基本URL、會話超時、登錄鎖定、目錄設定、密鑰滾轉、外部註冊的SMTP伺服器設定、水印配置、顯示選項等的更改。

## 配置擴展的使用情況跟蹤 {#configuring-extended-usage-tracking}

文檔安全性可以跟蹤可在受保護文檔上執行的各種自定義事件。 您可以在全局級別或策略級別上從文檔安全伺服器啟用事件跟蹤。 然後，可以設定JavaScript以捕獲在受保護PDF文檔中執行的特定操作，如按一下按鈕或保存文檔。 此使用資料以鍵值對形式作為XML檔案發送，您可以使用它進行進一步分析。 訪問受保護文檔的最終用戶可以允許或拒絕從客戶端應用程式進行此類跟蹤。

如果在全局級別啟用了跟蹤，則可以在策略級別覆蓋此設定，並對特定策略禁用它。 如果在全局級別禁用跟蹤，則不能執行策略級別覆蓋。 當事件計數達到25或文檔關閉時，跟蹤事件清單會自動推送到伺服器。 您還可以配置指令碼，根據您的要求顯式推送事件清單。 可以通過訪問文檔安全對象屬性和方法來自定義事件跟蹤。

啟用跟蹤後，隨後建立的所有策略將預設啟用跟蹤。 在伺服器上啟用跟蹤之前建立的策略需要手動更新。

### 啟用或禁用擴展使用情況跟蹤 {#enable-or-disable-extended-usage-tracking}

在開始之前，請確保已啟用「伺服器審核」。 請參閱 [配置事件審核和隱私設定](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) 的子菜單。

1. 在管理控制台中，按一下「服務」>「文檔安全」>「配置」>「審核和隱私設定」。
1. 要配置擴展的使用情況跟蹤，請在啟用跟蹤下，選擇是或否。
1. 要設定登錄頁上的「允許收集詳細使用情況資料」複選框的選擇，請在「啟用跟蹤」預設值下，選擇「是」或「否」。

要查看跟蹤的事件，可以使用「事件」頁上的「文檔事件」過濾器。 使用JavaScript跟蹤的事件被標籤為詳細使用情況跟蹤。 請參閱 [監視事件](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) 的子菜單。

## 配置文檔安全顯示設定 {#configure-document-security-display-settings}

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「顯示選項」。
1. 配置設定，然後按一下「確定」。

### 顯示設定 {#display-settings}

**要顯示搜索結果的行：** 執行搜索時在頁面上顯示的行數。

**客戶端登錄對話框的自定義**

這些設定控制用戶通過客戶端應用程式登錄文檔安全性時出現的登錄提示中顯示的文本。

**歡迎文本：** 歡迎消息文本，如「請使用您的用戶名和密碼登錄」。 歡迎消息文本應包含有關如何登錄到文檔安全性以及如何聯繫組織中的管理員或其他指定支援人員尋求幫助的資訊。 例如，外部用戶在忘記密碼或需要註冊或登錄過程幫助時可能需要與管理員聯繫。 歡迎文本的最大長度為512個字元。

**用戶名文本：** 用戶名框的文本標籤。

**密碼文本：** 密碼框的文本標籤。

**客戶端證書驗證對話框的自定義**

這些設定控制證書驗證對話框中顯示的文本。

**選擇驗證類型文本：** 顯示的文本，用於指示用戶選擇驗證類型。

**選擇證書文本：** 為指示用戶選擇證書類型而顯示的文本。

**證書不可用錯誤文本：** 當所選證書不可用時，最多顯示512個字元的消息。

**客戶端證書顯示的自定義**

**僅顯示受信任的憑據發行者：** 選擇此選項後，客戶端應用程式將僅向用戶提供配置為信任的表單的憑據發AEM行方的證書（請參閱管理證書和憑據）。 如果未選擇此選項，則向用戶顯示用戶系統上所有證書的清單。

## 配置動態水印 {#configure-dynamic-watermarks}

使用文檔安全性，可以為建立策略時可以應用的動態水印選項配置預設設定。 A *水印* 是疊加在文檔中文本上的影像。 它對跟蹤文檔內容非常有用，並有助於識別非法使用內容。

動態水印可以由定義的變數（如用戶ID和日期和自定義文本）組成的文本或PDF中的豐富內容組成。 可以使用多個元素配置水印，每個元素都有其自己的定位和格式設定。

水印是不可編輯的，因此它們是確保文檔內容機密性的更安全方法。 動態水印還確保水印顯示足夠的用戶特定資訊，以作為對進一步分發文檔的威懾。

當收件人查看或打印文檔時，策略指定的水印將出現在受策略保護的文檔中。 與永久水印不同，動態水印從不保存在文檔中，這提供了在內部網環境中部署文檔以確保查看應用程式顯示特定用戶身份時所需的靈活性。 此外，如果文檔具有多個用戶，則使用動態水印意味著您可以使用一個文檔而不是多個版本，每個版本都具有不同的水印。 顯示的水印反映當前用戶的身份。

請注意，動態水印與用戶可以直接添加到Acrobat文檔的水印不同。 結果是，在受策略保護的文檔中可以有兩個水印。

### 建立水印時的注意事項 {#considerations-when-creating-watermarks}

可以建立具有多個水印元素的動態水印，每個元素都指定為文本或PDF。 在水印中最多可以包含五個元素。

如果選擇基於文本的水印，則可以指定水印中具有多個文本條目的多個元素，並指定每個元素的位置。 為這些元素指定有意義的名稱，如頁眉、頁腳等。

例如，如果要在頁眉、頁腳、邊距上和跨文檔指定不同的文本作為水印，可建立多個水印元素並指定其位置。 如果希望用戶的用戶ID和當前訪問文檔的日期出現在標題中，策略名稱在右邊距中，自定義文本「CONFIDENTIAL」在文檔中以對角線顯示，則可以定義單獨的水印元素，並將文本作為類型，並指定其格式和定位。 當水印被應用到文檔時，水印中的所有元素都同時被應用到文檔中，按它們被添加到水印的順序。

通常，您使用基於PDF的水印來包括圖形內容（如徽標）或特殊符號（如版權或註冊商標）。

通過修改文檔安全配置檔案，可以更改水印元素數和PDF檔案大小的限制。 請參閱 [更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。

配置水印時，請記住以下內容：

* 不能將受密碼保護的PDF文檔用作水印元素。 但是，如果您建立的水印包含其他未受密碼保護的元素，則這些元素將作為水印的一部分應用。
* 可以更改要用作水印元素的最大PDF檔案大小。 但是，作為水印的大型PDF文檔在應用此類水印的文檔的離線同步期間降低了效能。 請參閱 [更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。
* 只將所選PDF的第一頁用作水印。 確保要作為水印顯示的資訊在第一頁本身上可用。
* 即使可以指定PDF文檔的縮放比例，如果計畫將PDF用作頁眉、頁腳或邊距中的水印，請考慮其頁面大小和佈局。
* 指定字型名稱時，請正確輸入名稱。 表AEM單替換您指定的字型（如果該字型不在開啟文檔的客戶端電腦中）。
* 如果選擇文本作為水印內容，則將縮放選項指定為「適合頁面」對於寬度不相同的頁面不起作用。
* 指定水印元素的定位時，請確保沒有多個元素具有相同的定位。 如果兩個水印元素具有相同的位置，如中心，則它們會在文檔上重疊，並按添加到水印的順序顯示。
* 指定字型大小和類型時，請確保文本長度在頁面中完全可見。 文本內容將滾動到新行中，因此您希望在頁邊距中顯示的水印內容可能會重疊到頁面上的內容區域。 但是，如果文檔在Acrobat 9開啟，則單行以外的文本將被截斷。

### 動態水印的局限性 {#limitations-of-dynamic-watermarks}

某些客戶端應用程式可能不支援動態水印。 請參閱相應的Acrobat Reader DC擴展幫助。 此外，請記住以下關於支援動態水印的Acrobat版本的資訊：

* 不能將受密碼保護的PDF文檔用作水印元素。
* Acrobat和Adobe Reader早於10的版本不支援以下水印功能：

   * PDF水印
   * 水印中的多個元素(文本/PDF)
   * 高級選項，如頁面範圍或顯示選項
   * 文本格式設定選項，如指定的字型、字型名稱和顏色。 但是，早期版本的Acrobat和Reader將以預設字型和顏色顯示文本內容。

* Acrobat 9.0和早期版本：Acrobat 9.0和更早版本不支援動態水印中的策略名稱。 如果Acrobat 9.0開啟一個包含策略名稱和其他動態資料的動態水印的受策略保護文檔，則該水印將不顯示策略名稱。 如果動態水印僅包含策略名稱，則Acrobat將顯示錯誤消息

### 添加動態水印模板 {#add-a-dynamic-watermark-template}

可以建立動態水印模板。 這些模板仍可用作管理員或用戶建立的策略的配置選項。

>[!NOTE]
>
>在導出配置檔案時，動態水印配置資訊不會與其他配置資訊一起捕獲。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「水印」。
1. 按一下「新建」。
1. 在「名稱」(Name)框中，鍵入新水印的名稱。

   ***附註&#x200B;**:不能在水印或水印元素的名稱或說明中使用某些特殊字元。 請參閱中列出的限制 [編輯策略的注意事項](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies)。*

1. 在「名稱」下，在加號旁邊，為水印元素（如「標題」）輸入有意義的名稱，然後添加說明，然後展開加號以顯示選項。
1. 在「源」下，選擇水印類型為「文本」或「PDF」。
1. 如果選擇了「文本」(Text)，請執行以下操作：

   * 選擇要包括的水印類型。 如果選擇「自定義文本」(Custom Text)，請在相鄰框中鍵入要顯示水印的文本。 請記住將作為水印出現的文本長度。
   * 為水印文本的文本內容指定文本格式屬性，如字型名稱、字型大小、前景顏色和背景顏色。 將前景色和背景色指定為十六進位值。

      ***附註&#x200B;**:如果選擇縮放選項為「適合頁面」，則字型大小屬性不可用於編輯。*

1. 如果為富水印選項選擇了PDF，請按一下 **瀏覽** 選擇水印PDF旁邊，選擇要用作水印的PDF文檔。

   ***附註&#x200B;**:請勿使用受密碼保護的PDF文檔。 如果指定受密碼保護的PDF作為水印元素，則不應用水印。*

1. 在用作背景下，選擇是或否。

   **附註**:當前，無論此設定如何，水印都會出現在前景中。

1. 要控制水印在文檔上的顯示位置，請配置「垂直對齊」和「水準對齊」選項。
1. 選擇「適合頁面」或選擇「%」，然後在框中鍵入百分比。 值必須是整數，而不是分數。 要配置水印大小，可以使用一個值（該值是頁面的百分比）或設定水印以適合頁面大小。
1. 在「旋轉」(Rotation)框中，鍵入水印旋轉所依據的度。 範圍是–180到180。 使用負值逆時針旋轉水印。 值必須是整數，而不是分數。
1. 在「不透明度」框中，鍵入一個百分比。 用整數，不用分數。
1. 在「高級選項」(Advanced Options)下，設定以下選項：

   **頁面範圍選項**

   設定應顯示水印的頁面範圍。 將起始頁輸入為1，將結束頁輸入為–1，以使所有頁面都用水印標籤。

   **顯示選項**

   選擇要顯示水印的位置。 預設情況下，水印會同時出現在軟拷貝（聯機）和硬拷貝（打印）上。

1. 按一下 **新建** 在「水印元素」下添加更多水印元素。
1. 按一下「確定」。

### 編輯動態水印模板 {#edit-a-dynamic-watermark-template}

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「水印」。
1. 按一下清單中的相應水印。
1. 在「編輯水印」頁上，根據需要更改設定。
1. 按一下「確定」。

### 刪除動態水印模板 {#delete-a-dynamic-watermark-template}

刪除動態水印時，它不再可用於添加到新策略中。 但是，水印仍保留在當前使用它的現有策略上，並且當前保護的文檔繼續顯示動態水印，直到您或用戶編輯包含已刪除水印的策略。 編輯策略後，不再應用水印。 出現一條消息，指出策略上的現有水印已被刪除，用戶可以選擇另一個水印來替換它。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「水印」。
1. 選中相應水印旁邊的複選框，然後按一下「刪除」。
1. 按一下「確定」。

## 配置邀請的用戶註冊 {#configuring-invited-user-registration}

您組織外部的用戶可以使用文檔安全性進行註冊。 註冊並激活其帳戶的受邀用戶可以使用其電子郵件地址和他們在註冊時建立的密碼登錄文檔安全性。 已註冊的受邀用戶可以使用他們具有權限的受策略保護的文檔。

當被邀請的用戶被激活時，他們將成為本地用戶。 可以使用「邀請的」和「本地用戶」區域配置和管理本地用戶。 (請參閱 [管理已邀請和本地用戶帳戶](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)。)

根據您為受邀用戶啟用的功能，他們還可以使用以下文檔安全功能：

* 將策略應用於文檔
* 建立策略
* 將邀請的用戶添加到策略

當發生以下事件時，文檔安全性會自動生成註冊邀請電子郵件，除非用戶已在源LDAP目錄中或先前已被邀請註冊：

* 現有用戶將被邀請的用戶添加到策略
* 管理員在「邀請的用戶註冊」頁上添加邀請的用戶帳戶

註冊電子郵件包含指向註冊頁面的連結和有關如何註冊的資訊。 在被邀請的用戶註冊後，文檔安全性發出帶有到激活頁的連結的激活電子郵件。 激活後，帳戶將一直有效，直到您停用或刪除它。

如果啟用內置註冊，則只指定一次SMTP伺服器、註冊電子郵件詳細資訊、訪問權能和重置密碼電子郵件資訊。 在啟用內置註冊之前，請確保已在「用戶管理」中建立本地域，並已將「文檔安全邀請用戶」角色分配給您組織中的相應用戶和組。 (請參閱 [添加本地域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain) 和 [建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。) 如果不使用內置註冊，則必須使用表單SDK建立自己的用戶注AEM冊系統。 請參閱中有關「為表單開發SPIAEM」的幫助 [用表格編AEM程](/help/forms/developing/introducing-java-api-soap-quick.md)。 如果不使用「內置註冊」選項，建議您在激活電子郵件和客戶端登錄螢幕中配置一條消息，以通知用戶如何與管理員聯繫以獲取新密碼或其他資訊。

**啟用和配置邀請的用戶註冊**

預設情況下，禁用邀請的用戶註冊進程。 您可以根據需要啟用和禁用邀請的用戶註冊以確保文檔安全。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「邀請的用戶註冊」。
1. 選擇啟用邀請的用戶註冊。
1. （可選）根據需要更新邀請的用戶註冊設定：

   * [排除或包括外部用戶或組](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [伺服器和註冊帳戶參數](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [註冊邀請電子郵件設定](configuring-client-server-options.md#registration-invitation-email-settings)
   * [激活電子郵件設定](configuring-client-server-options.md#activation-email-settings)
   * [配置密碼重置電子郵件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （可選）在內置註冊下，選擇是以啟用此選項。 如果未啟用內置註冊，則必須設定自己的用戶註冊系統。
1. 按一下「確定」。

### 排除或包括外部用戶或組 {#exclude-or-include-an-external-user-or-group}

您可以限制某些外部用戶或用戶組使用文檔安全性進行註冊。 例如，此選項對允許訪問某個用戶組但排除屬於該組的特定個人非常有用。

以下設定位於「已邀請用戶註冊」頁的「電子郵件限制篩選器」區域。

**排除：** 鍵入要排除的用戶或組的電子郵件地址。 要排除多個用戶或組，請在新行上鍵入每個電子郵件地址。 要排除屬於特定域的所有用戶，請輸入通配符和域名。 例如，要排除example.com域中的所有用戶，請輸入&amp;ast;.example.com。

**包括：** 鍵入要包括的用戶或組的電子郵件地址。 要包括多個用戶或組，請在新行上鍵入每個電子郵件地址。 要包括屬於特定域的所有用戶，請輸入通配符和域名。 例如，要在example.com域中包括所有用戶，請輸入&amp;ast;.example.com。

### 伺服器和註冊帳戶參數 {#server-and-registration-account-parameters}

以下設定位於「已邀請用戶註冊」頁的「常規設定」區域。

**SMTP主機：** SMTP伺服器的主機名。 SMTP伺服器管理傳出電子郵件通知以註冊和激活邀請的用戶帳戶。

如果SMTP主機需要，請在SMTP伺服器帳戶名和SMTP伺服器帳戶密碼框中鍵入所需資訊以連接到SMTP伺服器。 有些組織不執行此要求。 如果需要資訊，請咨詢系統管理員。

**SMTP伺服器套接字類名：** SMTP伺服器的套接字類名。 例如， javax.net.ssl.SSLSocketFactory。

**電子郵件內容類型：** 接受的MIME類型，如text/plain或text/html。

**電子郵件編碼：** 發送電子郵件時使用的編碼格式。 可以指定任何編碼，例如，UTF-8用於Unicode,ISO-8859-1用於拉丁語。 預設值為UTF-8。

**重定向電子郵件地址：** 指定此設定的電子郵件地址時，任何新邀請都將發送到提供的地址。 此設定可用於測試。

**使用本地域：** 選擇相應的域。 在新安裝中，確保使用「用戶管理」建立了域。 如果這是升級，則在升級過程中建立了外部用戶域，可以使用。

**將SSL用於SMTP伺服器：** 選擇此選項可為SMTP伺服器啟用SSL。

**在註冊頁上顯示登錄連結：** 在為邀請的用戶顯示的註冊頁上顯示登錄連結。

**為SMTP伺服器啟用傳輸層安全性(TLS)**

1. 開啟管理控制台。

   管理控制台的預設位置是 `https://<server>:<port>/adminui`。

1. 定位至「首頁」>「服務」>「文檔安全性」>「配置」>「邀請的用戶註冊」。
1. 在「已邀請用戶註冊」中，指定所有配置設定，然後按一下「確定」。

   >[!NOTE]
   >
   >如果您使用MicrosoftOffice 365作為SMTP伺服器來發送用戶註冊邀請，請使用以下設定：
   >
   >**SMTP主機：** smtp.office365.com
   >**埠：** 587

1. 接下來，需要更新config.xml。 請參閱 [為傳輸層安全性(TLS)啟用SMTP的配置](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果對「邀請的用戶註冊」選項進行任何更改，則config.xml檔案將被覆蓋，TLS將被停用。 如果覆蓋更改，則需要執行上述步驟以重新激活「已邀請用戶註冊」的TLS支援。

### 註冊邀請電子郵件設定 {#registration-invitation-email-settings}

當您建立新的受邀用戶帳戶或現有用戶添加以前未註冊或被邀請註冊到策略的外部收件人時，文檔安全性會自動發出註冊邀請電子郵件。 該電子郵件包含一個連結，收件人可以使用該連結訪問註冊頁並輸入個人帳戶資訊，包括用戶名和密碼。 密碼可以是八個字元的任意組合。

當收件者激活該帳戶時，該用戶成為本地用戶。

以下設定位於「已邀請用戶註冊」頁的「邀請電子郵件配置」區域。

**發件人：** 發送邀請電子郵件的電子郵件地址。 「發件人」電子郵件地址的預設格式為postmaster@[您的安裝域].com。

**主題：** 邀請電子郵件的預設主題。

**超時：** 如果外部用戶未註冊，則註冊邀請到期的天數。 預設值為30天。

**消息：** 邀請用戶註冊的消息正文中顯示的文本。

### 激活電子郵件設定 {#activation-email-settings}

在被邀請的用戶註冊後，文檔安全性會發送激活電子郵件。 激活電子郵件包含指向帳戶激活頁的連結，用戶可以在該頁激活其帳戶。 激活帳戶後，用戶可以使用其電子郵件地址和在註冊時建立的密碼登錄文檔安全性。

當接收者激活該用戶帳戶時，該用戶成為本地用戶。

以下設定位於「已邀請用戶註冊」頁的「激活電子郵件配置」區域。

>[!NOTE]
>
>還建議您在登錄螢幕上配置一條消息，告知外部用戶如何聯繫其管理員以獲取新密碼或其他資訊。

**發件人：** 從中發送激活電子郵件的電子郵件地址。 此電子郵件地址從註冊者的電子郵件主機接收失敗的傳遞通知，以及收件人回復註冊電子郵件所發送的任何消息。 「發件人」電子郵件地址的預設格式為postmaster@[您的安裝域].com。

**主題：** 激活電子郵件的預設主題。

**超時：** 如果用戶未激活帳戶，則激活邀請將過期的天數。 預設值為30天。

**消息：** 消息正文中顯示一條消息，指示需要激活收件人的用戶帳戶。 您可能還希望包括如何聯繫管理員以獲取新密碼等資訊。

### 配置密碼重置電子郵件 {#configure-a-password-reset-email}

如果您必須重置被邀請用戶的密碼，則會生成一封確認電子郵件，邀請用戶選擇新密碼。 無法確定用戶的密碼；如果用戶忘記了它，則必須重置它。

以下設定位於「已邀請用戶註冊」頁的「重置密碼電子郵件」區域。

**發件人：** 從中發送密碼重置電子郵件的電子郵件地址。 「發件人」電子郵件地址的預設格式為postmaster@[您的安裝域].com。

**主題：** 重置電子郵件的預設主題。

**消息：** 消息正文中顯示一條消息，表明收件人的外部用戶密碼已重置。

## 允許用戶和組建立策略 {#enable-users-and-groups-to-create-policies}

「配置」頁具有指向「我的策略」頁的連結，在該頁中可以指定哪些最終用戶可以建立我的策略，以及哪些用戶和組在搜索結果中可見。 「我的策略」頁有兩個頁籤：

**「建立策略」頁籤：** 用於配置用戶權限以建立自定義策略。

**「可見用戶和組」頁籤：** 用於控制在用戶搜索結果中可見的用戶和組。 需要超級用戶或策略集管理員來為每個策略集選擇和添加在「用戶管理」中建立的域到可見用戶和組。 此清單對策略集協調器可見，用於限制策略集協調器在選擇要添加到策略的用戶時可以瀏覽哪些域。

在授予用戶建立自定義策略的權限之前，請考慮您希望單個用戶擁有多少訪問或控制權。 此外，在使用戶和組對搜索可見時，請考慮希望它們暴露到何種程度。

### 指定可以建立策略的用戶和組 {#specify-users-and-groups-who-can-create-policies}

作為管理員，指定哪些用戶和組可以建立自定義策略。 可以在用戶和組級別設定此權限。 搜索功能將搜索用戶管理資料庫中的用戶和組。

1. 在管理控制台中，按一下「服務」>「文檔安全性」>「配置」>「我的策略」。
1. 在「我的策略」頁上，按一下「建立策略」頁籤，然後按一下「添加用戶和組」。
1. 在「查找」框中，鍵入要搜索的用戶或組的用戶名或電子郵件地址。 如果您沒有此資訊，請將框留空。 您還可以鍵入部分名稱或電子郵件地址，例如只知道用戶名的前兩個字母。
1. 在「使用」清單中，選擇搜索參數「名稱」或「電子郵件」。
1. 在「類型」清單中，選擇「組」或「用戶」以縮小搜索範圍。
1. 在「在」清單中，選擇要搜索的域。 如果不知道用戶或組的域，請選擇「所有域」。
1. 在「顯示」清單中，指定每頁要顯示的搜索結果數，然後按一下「查找」。
1. 要添加「我的策略」用戶和組，請為要添加的每個用戶和組選擇複選框。
1. 按一下「Add（添加）」 ，然後按一下「OK（確定）」。

您選定的用戶和組現在具有建立自定義策略的權限。

### 從用戶或組中刪除建立自定義策略權限 {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. 在文檔安全頁面上，按一下「配置」>「我的策略」。
1. 在「我的策略」頁上，按一下「建立策略」頁籤。 將顯示具有建立自定義策略權限的用戶和組。
1. 選中要從此權限中刪除的用戶和組旁邊的複選框。
1. 按一下「刪除」，然後按一下「確定」。

### 指定在搜索中可見的用戶和組 {#specify-users-and-groups-that-are-visible-in-searches}

當用戶管理其自定義策略時，他們可以搜索要添加到其策略中的用戶和組。 必須指定在這些搜索中可看到用戶和組的域。

1. 在文檔安全頁面上，按一下「配置」>「我的策略」。
1. 在「我的策略」頁上，按一下「可見用戶和組」頁籤。
1. 要使域中的用戶和組可見，請按一下添加域，選擇域，然後按一下添加。 要刪除域，請選中域名旁邊的複選框，然後按一下刪除。

## 手動編輯文檔安全配置檔案 {#manually-editing-the-document-security-configuration-file}

您可以導入和導出儲存在文檔安全資料庫中的配置資訊。 例如，您可能希望在從暫存移動到生產環境時製作配置資訊的備份副本，或者您可能希望編輯只能在編輯此檔案時進行配置的高級選項。

可以使用配置檔案進行以下更改：

[建立和編輯策略時顯示CATIA權限](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[指定離線同步的超時時間](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒絕特定應用程式的文檔安全服務](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[禁用外部連結](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>導入配置檔案會根據檔案中的資訊重新配置系統。 例外是動態水印配置和自定義事件資訊，這些資訊不會與導出的配置檔案一起保存。 必須在新系統中手動配置此資訊。 只有熟悉文檔安全性和XML的系統管理員或專業服務顧問才應修改配置檔案的內容，例如重新配置損壞的設定或調整特定企業部署方案的參數。

**導出配置檔案**

1. 在管理控制台中，按一下「服務」>「文檔安全性」11 >「配置」>「手動配置」。
1. 按一下「導出」(Export)，將配置檔案保存到其他位置。 預設檔案名為config.xml。
1. 按一下「確定」。
1. 在更改配置檔案之前，請製作備份副本，以備需要還原時使用。

**導入配置檔案**

1. 在管理控制台中，按一下「服務」>「文檔安全性」11 >「配置」>「手動配置」。
1. 按一下「瀏覽」(Browse)轉到配置檔案，然後按一下「導入」(Import)。 不能直接在「檔案名」(File Name)框中鍵入路徑。
1. 按一下「確定」。

### 指定離線同步的超時時間 {#specify-a-timeout-period-for-offline-synchronization}

文檔安全性允許用戶在未連接到文檔安全伺服器時開啟和使用受保護的文檔。 用戶的客戶端應用程式必須定期與伺服器同步，以保持文檔在離線使用時有效。 用戶第一次開啟受保護的文檔時，會詢問是否應授權其電腦執行定期客戶端同步。

預設情況下，當用戶連接到文檔安全伺服器時，同步將每四小時自動進行一次，並根據需要進行。 如果文檔的離線期間在用戶離線時過期，則用戶必須重新連接到伺服器以使客戶端應用程式與伺服器同步。

在文檔安全配置檔案中，可以指定自動後台同步的預設頻率。 此設定用作預設超時期客戶端應用程式，除非客戶端顯式設定其自己的超時值。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到 `PolicyServer` 的下界。 在該節點下，找到 `ServerSettings` 的下界。
1. 在 `ServerSettings` 節點，添加以下條目，然後保存檔案：

   `<entry key="BackgroundSyncFrequency" value="`*時間* `"/>`

   何處 *時間* 是自動後台同步之間的秒數。 如果您將此值發送到 `0`，始終進行同步。 預設值為 `14400` 秒（每四小時）。

1. 導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 拒絕特定應用程式的文檔安全服務 {#denying-document-security-services-for-specific-applications}

您可以配置文檔安全性，以拒絕滿足特定條件的應用程式的服務。 條件可以指定單個屬性，如平台名稱，也可以指定多組屬性。 此功能可以幫助您控制必須處理的請求文檔安全性。 以下是此功能的一些應用：

* **收入保護：** 您可能希望拒絕對不支援收入約定的任何客戶端應用程式的訪問權限。
* **應用程式相容性：** 某些應用程式可能與文檔安全伺服器的策略或行為不相容。

當客戶端應用程式試圖建立具有文檔安全性的連結時，它們會提供應用程式、版本和平台資訊。 文檔安全性將此資訊與從文檔安全配置檔案獲取的拒絕設定進行比較。

拒絕設定可以包含幾組拒絕條件。 如果任何一個集合的所有屬性都匹配，則拒絕請求應用程式對文檔安全服務的訪問。

拒絕服務功能要求客戶端應用程式使用文檔安全性C++客戶端SDK 8.2版或更高版本。 以下Adobe產品在請求文檔安全服務時提供產品資訊：

* Adobe Acrobat9.0專業版/Acrobat 9.0標準版及更高版本
* Adobe Reader9.0及更高版本
* Acrobat Reader DCMicrosoftOffice 8.2及更高版本的擴展

客戶端應用程式使用文檔安全性C++客戶端SDK中的客戶端API從文檔安全性請求服務。 客戶端API請求包括平台和SDK版本資訊（預編譯到客戶端API中）以及從客戶端應用程式獲得的產品資訊。

客戶端應用程式或插件在實現回調函式時提供產品資訊。 應用程式提供以下資訊：

* 整合商名稱
* 整合商版本
* 應用程式系列
* 應用程式名稱
* 應用程式版本

如果任何資訊不適用，客戶端應用程式將相應欄位留空。

一些Adobe應用程式在請求文檔安全服務時包括產品資訊，包括Acrobat、Adobe Reader和Acrobat Reader DCMicrosoft辦事處的擴展。

**Acrobat和Adobe Reader**

當Acrobat或Adobe Reader從文檔安全性請求服務時，它提供以下產品資訊：

* **整合商：** Adobe Systems公司
* **整合商版本：** 1.0
* **應用程式系列：** Acrobat
* **應用程式名稱：** Acrobat
* **應用程式版本：** 9.0.0

**Acrobat Reader DCMicrosoft辦事處**

Acrobat Reader DCMicrosoft辦公室的擴展插件是Microsoft辦公室產品MicrosoftWord、MicrosoftExcel和MicrosoftPowerPoint的插件。 當它請求服務時，它提供以下資訊：

* **整合商：** Adobe Systems Incorporated
* **整合商版本：** 8.2
* **應用程式系列：** Acrobat Reader DCMicrosoft辦事處
* **應用程式名稱：** MicrosoftWord、MicrosoftExcel或MicrosoftPowerPoint
* **應用程式版本：** 2003或2007

**配置文檔安全性以拒絕特定應用程式的服務**

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到 `PolicyServer` 的下界。 添加 `ClientVersionRules` 節點作為節點的直接子級 `PolicyServer` 節點，如果不存在：

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

   `SDKPlatforms` 指定承載客戶端應用程式的平台。 可能的值為：

   * Microsoft窗
   * AppleOS X
   * 太陽Solaris
   * HP-UX

   `SDKVersions` 指定客戶端應用程式使用的文檔安全性C++客戶端API的版本。 比如說， `"8.2"`。

   `APPFamilies` 由客戶端API定義。

   `AppName`指定客戶端應用程式的名稱。 逗號用作名稱分隔符。 要在名稱中包含逗號，請使用反斜線(\)字元轉義它。 比如說， *&quot;Adobe Systems&quot;*。

   `AppVersions` 指定客戶端應用程式的版本。

   `Integrators` 指定開發插件或整合應用程式的公司或組的名稱。

   `IntegratorVersions` 是插件或整合應用程式的版本。

1. 對於每組附加的拒絕資料，添加另一組 *我的條目名稱* 的子菜單。
1. 保存配置檔案。
1. 導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

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

在此示例中，My Application 3.0版和My Other Application 2.0版被拒絕訪問。 無論拒絕原因如何，都使用相同的拒絕資訊URL。

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

在本示例中，來自MicrosoftPowerPoint 2007或MicrosoftPowerPoint 2010的為Microsoft辦事處安裝Acrobat Reader DC擴展的所有請求均被拒絕。

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

預設情況下，可以在水印中指定最多五個元素。 此外，您要用作水印的PDF文檔的最大檔案大小限制為100KB。 可以在config.xml檔案中更改這些參數。

***附註&#x200B;**:您應謹慎更改這些參數。*

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到 `ServerSettings` 的下界。
1. 在 `ServerSettings` 節點，添加以下條目，然後保存檔案： `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一個條目， *最大檔案大小* 是PDF水印元素允許的最大檔案大小(KB)。 預設值為100KB。

   第二條， *最大元素* 是水印中允許的最大元素數。 預設值為5。

   ```xml
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 禁用外部連結 {#disabling-external-links}

許多文檔安全用戶無權訪問外部連結，如 **www.adobe.com** 使用「Right Management（正確管理）」用戶介面時：

* `https://[host]:'port'/adminui`
* `https://[host]:'port'/edc`。

以下對config.xml的更改將禁用「Right Management」用戶介面中的所有外部連結。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到 `DisplaySettings` 的下界。
1. 禁用所有外部連結，在 `DisplaySettings` 節點，添加以下條目，然後保存檔案： `<entry key="ExternalLinksAllowed" value="false"/>`

   ```xml
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 為傳輸層安全性(TLS)啟用SMTP的配置 {#configuration-to-enable-smtp-for-transport-layer-security-tls}

以下對config.xml的更改啟用了「邀請的用戶註冊」功能的TLS支援。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到 `DisplaySettings` 的下界。
1. 找到以下節點： `<node name="ExternalUser">`

   ```xml
   <node name="ExternalUser">
   ```

1. 設定 `SmtpUseTls` 的 `ExternalUser` 節點到 **真**。
1. 設定 `SmtpUseSsl` 的 `ExternalUser` 節點到 **假**。
1. 保存 `config.xml`。
1. 導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 禁用文檔安全文檔的SOAP終結點 {#disable-soap-endpoints-for-document-security-documents}

以下對config.xml的更改可禁用文檔安全文檔的SOAP終結點。

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到以下節點： `<node name="DRM">`

   ```xml
   <node name="DRM">
   ```

1. 在DRM節點中，找到 `entry` 節點：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 要禁用文檔安全文檔的SOAP終結點，請將value屬性設定為 **假**。

   ```xml
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 保存 `config.xml`。
1. 導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)

### 提高文檔安全伺服器的可擴充性 {#increasingscalability}

預設情況下，在同步文檔以供離線使用時，文檔安全客戶端會獲取用戶有權訪問的所有其他文檔的策略、水印、許可證和吊銷更新資訊。 如果這些更新和資訊未與客戶端同步，則以離線模式開啟的文檔仍可能與舊策略、水印和吊銷資訊一起開啟。

通過限制發送到客戶端的資訊，可以提高文檔安全伺服器的可擴充性。 向客戶端發送的資訊量減少導致改進的可擴充性、縮短的響應時間以及更好的伺服器效能。 執行以下步驟以提高可擴充性：

1. 導出文檔安全配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
1. 在編輯器中開啟配置檔案並找到ServerSettings節點。
1. 在「伺服器設定」節點中，設定 `DisableGlobalOfflineSynchronizationData`屬性 `true`。

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   當設定為true時，文檔安全伺服器僅發送當前文檔的資訊，並且不將其他文檔（用戶有權訪問的其他文檔）的資訊發送給客戶端。

   >[!NOTE]
   >
   >預設情況下， `DisableGlobalOfflineSynchronizationData`鍵設定為 `false`。

1. 保存並導入配置檔案。 (請參閱 [手動編輯文檔安全配置檔案](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file)。)
