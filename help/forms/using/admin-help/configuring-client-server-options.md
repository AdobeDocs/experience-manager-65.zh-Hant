---
title: 配置客戶端和伺服器選項
seo-title: 配置客戶機和伺服器選項
description: 瞭解如何設定各種用戶端和伺服器選項，例如伺服器組態設定、檔案保全形色和事件稽核。
seo-description: 瞭解如何設定各種用戶端和伺服器選項，例如伺服器組態設定、檔案保全形色和事件稽核。
uuid: 1f9f9886-726e-4fad-9ff8-0ff11eef653e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0f069fbc-10c2-403e-9419-5e9920035d75
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e

---


# 設定檔案安全性伺服器 {#configure-the-document-security-server}

1. 在管理控制台中，按一下「服務>檔案安全性>設定>伺服器設定」。
1. 配置設定並按一下確定。

## 伺服器組態設定 {#server-configuration-settings}

**** 基本URL:基本文檔安全URL，包含伺服器名和埠。 附加到基礎的資訊會建立連接URL。 例如，會附加/edc/Main.do以存取網頁。 使用者也會透過此URL回應外部使用者註冊邀請。

如果您使用IPv6，請輸入基本URL作為電腦名或DNS名稱。 如果您使用數值IP位址，Acrobat將無法開啟受原則保護的檔案。 此外，請為您的伺服器使用HTTP安全(HTTPS)URL。

***注意&#x200B;**:基本URL已內嵌在受原則保護的檔案中。 用戶端應用程式使用基本URL來連線回伺服器。 受保護的檔案將繼續包含基本URL，即使稍後變更亦然。 如果您變更基本URL，則所有連線用戶端的設定資訊都必須更新。*

**** 預設離線租用期：使用者離線使用受保護檔案的預設時間長度。 此設定決定了建立策略時自動離線租用期間設定的初始值。 （請參閱建立和編輯原則。）當租賃期到期時，收件者必須再次同步檔案，才能繼續使用。

有關離線租用和同步如何運作的討論，請參 [閱Primer中有關配置離線租用和同步的資訊](https://blogs.adobe.com/security/2009/05/primer_on_configuring_offline.html)。

**** 預設離線同步期間：任何檔案在最初受到保護後離線使用的最長時間。

**** 客戶端會話超時：如果透過用戶端應用程式登入的使用者未與檔案安全性互動，則檔案安全性會在幾分鐘內中斷連線。

**** 允許匿名用戶訪問：選取此選項，可啟用建立共用和個人化原則的能力，讓匿名使用者開啟受原則保護的檔案。 （沒有帳戶的使用者可以存取檔案，但無法登入檔案保全或使用其他受原則保護的檔案。）

**** 禁用對第7版客戶端的訪問：指定使用者是否可使用Acrobat或Reader 7.0連線至伺服器。 當選取此選項時，使用者必須使用Acrobat或Reader 8.0及更新版本，才能完成PDF檔案的檔案保全作業。 如果政策要求在開啟受原則保護的檔案時，Acrobat或Reader 8.0及更新版本必須以認證模式執行，您應停用Acrobat或Reader 7的存取權。 （請參閱指定使用者和群組的檔案權限。）

**允許每份檔案的離線存取** ：選取此選項可指定每份檔案的離線存取。 如果啟用此設定，則使用者將只能離線存取使用者至少已線上開啟過一次的檔案。

**** 允許用戶名密碼驗證：選擇此選項可使客戶端應用程式在連接到伺服器時使用用戶名／口令驗證。

**** 允許Kerberos身份驗證：選擇此選項可使客戶端應用程式在連接到伺服器時使用Kerberos驗證。

**** 允許客戶端證書驗證：選擇此選項可啟用客戶端應用程式在連接到伺服器時使用證書驗證。

**允許擴展驗證** ：選擇以啟用擴展驗證，然後輸入擴展驗證登錄URL。

選擇此選項可讓客戶端應用程式使用擴展身份驗證。 擴充驗證可提供自訂驗證程式，以及AEM Forms伺服器上設定的不同驗證選項。 例如，使用者現在可以從Acrobat和Reader用戶端體驗以SAML為基礎的驗證，而非AEM表單的使用者名稱／密碼。 依預設，「著陸URL」包含 *localhost* 作為伺服器名稱。 以完全限定的主機名替換伺服器名稱。 如果尚未啟用擴充驗證，著陸URL中的主機名稱會自動從基本URL填入。 請參 [閱添加擴展驗證提供程式](configuring-client-server-options.md#add-the-extended-authentication-provider)。

***注意&#x200B;**:Apple Mac OS x搭配Adobe Acrobat 11.0.6版及更新版本支援延伸驗證。*

**延伸驗證的偏好HTML控制寬度** ：指定在Acrobat中開啟以輸入使用者認證的延伸驗證對話方塊的寬度。

**延伸驗證的偏好HTML控制高度** ：指定在Acrobat中開啟以輸入使用者認證的延伸驗證對話方塊的高度。

*****注意&#x200B;*:此對話框的寬度和高度限制如下：寬度：最少= 400，最多= 900

高度：最低= 450;最大值= 800

**** 啟用客戶端憑據快取：選取此選項可讓使用者快取其認證（使用者名稱和密碼）。 當使用者的認證被快取時，他們不必在每次開啟檔案時或按一下Adobe Acrobat「管理保全政策」頁面上的「重新整理」按鈕時輸入認證。 您可以指定使用者必須再次提供其認證的天數。 將天數設為0可無限期快取憑證。

## 設定檔案安全性使用者和管理員 {#configuring-document-security-users-and-administrators}

### 為管理員指派檔案保全形色 {#assigning-document-security-roles-to-administrators}

您的AEM表單環境包含一或多個具有建立使用者和群組適當權限的管理員使用者。 如果貴組織使用檔案安全性，則至少還必須指派一位管理員來管理已邀請的使用者和本機使用者。

管理員還必須具有管理控制台用戶角色，才能訪問管理控制台。 (請參 [閱建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)

### 設定可見的使用者和群組 {#configuring-visible-users-and-groups}

要在策略用戶搜索期間查看選定域中的用戶和組，超級管理員或策略集管理員必須選擇並將域（在用戶管理中建立）添加到每個策略集的可見用戶和組清單中。

可見的用戶和組清單對策略集協調器可見，用於限制最終用戶在選擇要添加到策略的用戶或組時可以瀏覽的域。 如果未執行此任務，則策略集協調器將找不到要添加到策略的任何用戶或組。 任何給定的策略集都可以有一個以上的策略集協調器。

1. 在您安裝並設定AEM表單環境並具備檔案安全性後，請在「使用者管理」中設定所有適當的網域。 <!-- Fix broken link (See Setting up and managing domains) -->

   ***注意&#x200B;**:必須先建立域，才能建立任何策略。*

1. 在管理控制台中，按一下「服務>檔案管理>原則」，然後按一下「原則集」標籤。
1. 選擇全局策略集，然後按一下可見用戶和組頁籤。
1. 按一下「新增網域」，並視需要新增現有網域。
1. 導覽至「服務>檔案安全性>設定>我的原則」，然後按一下「可見的使用者和群組」標籤。
1. 按一下「新增網域」，並視需要新增現有網域。

## 添加擴展身份驗證提供程式 {#add-the-extended-authentication-provider}

AEM表格提供您可針對環境自訂的範例設定。 執行以下步驟：

>[!NOTE]
>
>Apple Mac OS x搭配Adobe Acrobat 11.0.6版及更新版本支援延伸驗證。

1. 獲取WAR檔案部署示例。 請參閱適用於您應用程式伺服器的安裝指南。
1. 請確定表單伺服器具有完全限定的名稱，而非IP位址做為基本URL，且是HTTPS URL。 請參閱 [伺服器組態設定](configuring-client-server-options.md#server-configuration-settings)。
1. 從「伺服器配置」頁啟用擴展驗證。 請參閱 [伺服器組態設定](configuring-client-server-options.md#server-configuration-settings)。
1. 在「使用者管理」設定檔案中新增所需的SSO重新導向URL。 請參 [閱新增SSO重新導向URL以進行延伸驗證](configuring-client-server-options.md#add-sso-redirect-urls-for-extended-authentication)。

### 新增SSO重新導向URL以進行延伸驗證 {#add-sso-redirect-urls-for-extended-authentication}

啟用延伸驗證後，使用者在Acrobat XI或Reader XI中開啟受原則保護的檔案時，會收到驗證對話方塊。 此對話方塊會載入您在Document Security伺服器設定上指定為延伸驗證著陸URL的HTML頁面。 請參閱 [伺服器組態設定](configuring-client-server-options.md#server-configuration-settings)。

>[!NOTE]
>
>Apple Mac OS x搭配Adobe Acrobat 11.0.6版及更新版本支援延伸驗證。

1. 在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔」。
1. 按一下「導出」(Export)，將配置檔案保存到磁碟。
1. 在編輯器中開啟檔案，並找到AllowedUrls節點。
1. 在節 `AllowedUrls` 點中添加以下行： `<entry key="sso-l" value="/ssoexample/login.jsp"/> <entry key="sso-s" value="/ssoexample"/> <entry key="sso-o" value="/ssoexample/logout.jsp"/>`

   ```as3
   <entry key="sso-l" value="/ssoexample/login.jsp"/>
   <entry key="sso-s" value="/ssoexample"/>
   <entry key="sso-o" value="/ssoexample/logout.jsp"/>
   ```

1. 儲存檔案，然後從「手動設定」頁面匯入更新的檔案：在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔」。

## 設定離線安全性 {#configuring-offline-security}

檔案安全性可讓您離線使用受原則保護的檔案，毋需使用網際網路或網路連線。 此功能要求原則允許離線存取，如指定使用者 [和群組的檔案權限中所述](/help/forms/using/admin-help/creating-policies.md#specify-the-document-permissions-for-users-and-groups)。 在離線使用具有此策略的文檔之前，收件人必須在聯機時開啟文檔並啟用離線訪問，方法是在出現提示時按一下「是」。 也可以請求接收者驗證其身份。 然後，收件者可以在原則中指定的離線租用期間離線使用檔案。

離線租用期結束時，收件者必須透過線上開啟檔案或使用Acrobat或Acrobat Reader DC擴充功能表命令進行同步，以再次與檔案安全性同步。 (請參 *閱「Acrobat說明* 」或適當 *的Acrobat Reader DC擴充功能說明*。)

由於允許離線存取的檔案需要離線儲存檔案的電腦上的快取金鑰材料，因此，如果未經授權的使用者可取得該金鑰材料，檔案可能會受到危害。 為彌補這種可能性，您可設定排程和手動的按鍵變換選項，以防止未經授權的人使用按鍵存取檔案。

### 設定預設的離線租用期間 {#set-a-default-offline-lease-period}

受原則保護檔案的收件者可讓檔案離線一段時間，持續在原則中指定的天數。 在將檔案與檔案保全初次同步後，收件者可離線使用，直到離線租用期間到期為止。 當租賃期到期時，收件者必須將檔案連線並登入，以便與檔案安全性同步，才能繼續使用檔案。

您可以設定預設的離線租用期間。 當任何人建立或編輯原則時，可以從預設值變更租用期間。

1. 在檔案安全頁面上，按一下「設定>伺服器設定」。
1. 在「預設離線租用期間」框中，鍵入離線租用期間的天數。
1. 按一下「確定」。

### 管理關鍵變換 {#manage-key-rollovers}

檔案安全性使用加密演算法和授權來保護檔案。 當檔案加密時，檔案安全性會產生並管理一個稱為 *DocKey的解密金鑰* ，並傳遞給用戶端應用程式。 如果保護文檔的策略允許離線訪問，則還會為每個對文檔具有離線訪問權限的用戶生成稱為 *承擔者密鑰* 的離線密鑰。

>[!NOTE]
>
>如果主密鑰不存在，文檔安全性將生成一個密鑰以保護文檔。

若要離線開啟受原則保護的檔案，使用者的電腦必須有適當的主要金鑰。 當使用者與檔案安全性同步時，電腦會取得主密鑰（線上開啟受保護的檔案）。 如果此主密鑰被洩露，則用戶可以離線訪問的任何文檔也可能被洩露。

降低離線檔案威脅的一種方式是避免允許離線存取特別敏感的檔案。 另一種方法是定期地滾動主鍵。 當檔案安全性將金鑰卷過時，任何現有金鑰都無法再存取受原則保護的檔案。 例如，如果犯罪者從被盜筆記型電腦中獲得主密鑰，則該密鑰無法用於訪問在發生翻車後受保護的文檔。 如果您懷疑某個主密鑰已洩露，則可以手動將其滾動到該密鑰上。

不過，您也需要注意到，主鍵變換會影響所有主鍵，而不只是主鍵。 它還降低了系統的可擴充性，因為客戶端必須儲存更多密鑰才能離線訪問。 預設的關鍵字變換頻率為20天。 建議不要將此值設為低於14天，因為可能無法讓使用者檢視離線檔案，而且系統效能可能會受到影響。

在以下示例中，Key1是兩個主鍵中較舊的鍵，Key2是較新的鍵。 當您第一次按一下「立即變換索引鍵」按鈕時，Key1會變成無效，並產生較新的有效主索引鍵(Key3)。 當使用者與檔案安全性同步時，會取得Key3，通常是透過線上開啟受保護的檔案。 不過，除非使用者達到原則中指定的離線租用期間上限，否則不會強制與檔案安全性同步。 在第一次重新啟動金鑰後，仍離線的使用者仍可開啟離線檔案，包括受Key3保護的檔案，直到達到離線租用期限上限為止。 當您再次按一下「立即變換按鍵」按鈕時，Key2會變成無效，而Key4會建立。 在兩個關鍵變換期間仍處於離線狀態的使用者在與檔案安全性同步之前，無法開啟使用Key3或Key4保護的檔案。

**變更主要變換頻率**

為保密目的，當您使用離線檔案時，檔案安全性會提供預設頻率為20天的自動金鑰變換選項。 您可以變更變換頻率；不過，請避免將值設為低於14天，因為可能會防止使用者檢視離線檔案，而且系統效能可能會受到影響。

1. 在檔案安全性頁面上，按一下「設定>金鑰管理」。
1. 在「關鍵變換頻率」框中，鍵入變換期間的天數。
1. 按一下「確定」。

**手動滾動主鍵**

為了維護離線檔案的機密性，您可以手動將滑鼠指向主要金鑰。 您可能會發現必須手動滑鼠指向某個金鑰（例如，如果該金鑰是由某人從快取該金鑰的電腦取得，以便離線存取檔案）。

>[!NOTE]
>
>避免經常使用手動變換，因為它會使所有主鍵都變換，而不只是一個主鍵，而且可能會暫時防止使用者離線檢視新檔案。

主密鑰必須滾轉兩次，客戶端電腦上以前存在的密鑰才失效。 已使主密鑰失效的客戶機必須與文檔安全服務重新同步，以獲取新的主密鑰。

1. 在檔案安全性頁面上，按一下「設定>金鑰管理」。
1. 按一下「立即變換按鍵」，然後按一下「確定」。
1. 等待大約10分鐘。 伺服器日誌中將顯示以下日誌消息： `Done RightsManagement key rollover for`*N *`principals`. 其*&#x200B;中&#x200B;*N是檔案安全系統中的使用者人數。
1. 按一下「立即變換按鍵」，然後按一下「確定」。
1. 等待大約10分鐘。

## 設定事件稽核和隱私權設定 {#configuring-event-auditing-and-privacy-settings}

檔案安全性可以稽核並記錄與受原則保護的檔案、原則、管理員和伺服器互動相關的事件資訊。 您可以設定事件稽核，也可以指定要稽核的事件類型。 要審計特定文檔的事件，還必須啟用策略上的審計選項。

啟用審計後，您可以在「事件」頁面上查看已審計事件的詳細資訊。 檔案安全性使用者也可以檢視與他們使用或建立受原則保護的檔案相關的事件。

您可以選擇以下類型的事件進行審計：

* 受原則保護的檔案事件，例如授權或未經授權的使用者嘗試開啟檔案
* 策略事件，如建立、更改、刪除、啟用和禁用策略
* 使用者事件，例如外部使用者邀請和註冊、啟用和停用的使用者帳戶、使用者密碼的變更，以及描述檔更新
* AEM表單事件，例如版本不符、目錄伺服器和授權提供者無法使用，以及伺服器組態變更

### 啟用或禁用事件審計 {#enable-or-disable-event-auditing}

您可以啟用和停用與伺服器、受原則保護的檔案、原則、原則集和使用者相關的事件稽核。 啟用事件審計時，您可以選擇審計所有可能的事件，也可以選擇要審計的特定事件。

啟用伺服器審計後，您可以在「事件」頁面上查看已審計事件。

1. 在管理主控台中，按一下「服務> Document Security >設定>稽核和隱私權設定」。
1. 要配置伺服器審計，請在「啟用伺服器審計」下，選擇「是」或「否」。
1. 如果您選擇「是」，請在每個事件類別下執行下列其中一個動作，以選取要稽核的選項：

   * 要審計類別中的所有事件，請選擇「全部」。
   * 若要僅審核某些事件，請取消選取「全部」，然後選取您要審核之事件旁的核取方塊。

      (請參 [閱事件審計選項](configuring-client-server-options.md#event-auditing-options)。)

1. 按一下「確定」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，例如上一頁按鈕、重新整理按鈕，以及上一或下一箭頭，因為此動作可能會造成不需要的資料擷取和資料顯示問題。

### 啟用或停用隱私權通知 {#enable-or-disable-privacy-notification}

您可以啟用和停用隱私權通知訊息。 當您啟用隱私權通知時，當收件者嘗試開啟受原則保護的檔案時，會顯示訊息。 此通知會通知使用者檔案使用情況正在檢查中。 您也可以指定URL，讓使用者在隱私權政策頁面可供使用時，用來檢視您的隱私權政策頁面。

1. 在管理控制台中，按一下「服務> Document Security>設定>稽核和隱私權設定」。
1. 若要設定隱私權通知，請在「啟用隱私權通知」下方，選取「是」或「否」。

   如果附加至檔案的原則允許匿名使用者存取，而「啟用隱私權聲明」設定為「否」，則不會提示使用者登入，也不會顯示隱私權通知訊息。

   如果附加至檔案的原則不允許匿名使用者存取，使用者會看到隱私權通知訊息。

1. 如果適用，在「隱私權URL」方塊中，輸入您隱私權政策頁面的URL。 如果「隱私權URL」方塊留空，則會顯示adobe.com的隱私權頁面。
1. 按一下「確定」。

>[!NOTE]
>
>停用隱私權通知並不會停用檔案使用情況稽核。 透過擴充使用追蹤支援的立即可用稽核動作和自訂動作仍可收集使用者行為資訊。

### 匯入自訂稽核事件類型 {#import-a-custom-audit-event-type}

如果您使用支援其他事件（例如特定檔案類型的事件）審核的檔案安全性應用程式，Adobe合作夥伴可以提供您自訂的審核事件，讓您將這些事件匯入檔案安全性。 只有當Adobe合作夥伴已提供自訂事件類型時，才能使用此功能。

1. 在管理控制台中，按一下「服務> Document Security >設定>事件管理」。
1. 按一下「瀏覽」前往要匯入的XML檔案，然後按一下「匯入」。
1. 如果找到相同的事件代碼和命名空間組合，導入將覆寫伺服器上現有的自定義審計事件類型。
1. 按一下「確定」。

### 刪除自訂稽核事件類型 {#delete-a-custom-audit-event-type}

1. 在管理控制台中，按一下「服務>檔案安全性>設定>事件管理」。
1. 選擇要刪除的自定義審計事件類型旁邊的複選框，然後按一下刪除。
1. 按一下「確定」。

### 匯出稽核事件 {#export-audit-events}

您可以將審核事件導出到檔案以用於存檔。

1. 在管理控制台中，按一下「服務> Document Security >設定>事件管理」。
1. 視需要編輯「匯出稽核事件」下的設定。 您可以指定：

   * 要匯出之審核事件的最低年齡
   * 單一檔案中要包含的稽核事件數目上限。 伺服器根據此值生成一個或多個檔案。
   * 將在其中建立檔案的資料夾。 此資料夾位於表單伺服器上。 如果資料夾路徑是相對的，則它是相對於您的應用程式伺服器根目錄的。
   * 用於審計事件檔案的檔案前置詞
   * 檔案的格式，為與Microsoft excel相容的逗號分隔值(CSV)檔案或XML檔案。

1. 按一下「匯出」。 如果要取消導出，請按一下「取消導出」。 如果其他使用者已排程匯出，在匯出完成之前，「取消匯出」按鈕將無法使用。 如果其他使用者已排程匯出，「取消匯出」按鈕將無法使用。 要檢查計畫的「導出」或「刪除」是否已啟動或已完成，請按一下「刷新」。

### 刪除審計事件 {#delete-audit-events}

您可以刪除超過指定天數的審核事件。

1. 在管理控制台中，按一下「服務> Document Security >設定>事件管理」。
1. 在「刪除審計事件」下，在「刪除審計事件早於」框中指定天數。
1. 按一下「刪除」。 按一下「匯出」。 如果要取消刪除，請按一下「取消刪除」。 如果其他使用者已排程刪除，則在匯出完成之前，「取消刪除」按鈕不可用。 如果其他使用者已排程匯出，則「取消刪除」按鈕無法使用。 要檢查已排程的刪除是否已啟動或已完成，請按一下刷新。

### 事件審計選項 {#event-auditing-options}

您可以啟用和停用事件稽核，並指定要稽核的事件類型。

**檔案事件**

**** 檢視檔案：收件者會檢視受原則保護的檔案。

**** 關閉檔案：收件者會關閉受原則保護的檔案。

**列印低解析度** ：收件者會列印具有指定低解析度選項之受原則保護的檔案。

**** 列印高解析度：收件者會列印具有指定高解析度選項之受原則保護檔案。

**** 將注釋添加到文檔：收件者會將註解新增至PDF檔案。

**** 廢止檔案：使用者或管理員廢止受原則保護檔案的存取權。

**** 取消撤銷檔案：使用者或管理員重新設定對受原則保護檔案的存取權。

**** 表單填寫：收件者會將資訊輸入可填寫的PDF檔案。

**** 已移除原則：發行者會從檔案中移除原則，以取消安全性保護。

**** 變更檔案撤銷URL:來自API層級的呼叫會變更指定的撤銷URL，以存取取代已撤銷檔案的新檔案。

**** 修改文檔：收件者會變更受原則保護檔案的內容。

**** 簽署檔案：收件者簽署檔案。

**** 保護新檔案：使用者套用原則以保護檔案。

**** 切換文檔策略：用戶或管理員切換附加到文檔的策略。

**** 將檔案發佈為：在伺服器上註冊的新檔案，其documentName和授權與現有檔案相同，且檔案不具有父子關係。 您可以使用AEM表單SDK觸發此事件。

**** 重複檔案：在伺服器上註冊一份documentName和授權與現有檔案相同的新檔案，且這些檔案具有父子關係。 您可以使用AEM表單SDK觸發此事件。

**政策事件**

**** 已建立策略：用戶或管理員建立策略。

**** 啟用的策略：管理員使策略可用。

**** 變更的政策：用戶或管理員更改策略。

**** 禁用策略：管理員使策略不可用。

**** 已刪除策略：用戶或管理員刪除策略。

**** 更改策略所有者：來自API層級的呼叫會變更原則擁有者。

**使用者事件**

**** 已刪除的用戶：管理員刪除用戶帳戶。

**** 註冊邀請的使用者：外部用戶通過文檔安全註冊。

**** 成功登入：管理員或使用者成功登入嘗試。

**** 受邀的使用者：檔案安全性邀請使用者註冊。

**** 已啟用的使用者：外部使用者使用啟動電子郵件中的URL來啟動其帳戶，或是管理員啟用帳戶。

**** 更改密碼：被邀請的使用者變更其密碼，或管理員重設本機使用者的密碼。

**** 登錄失敗：管理員或用戶登錄嘗試失敗。

**** 停用的使用者：管理員會停用本機使用者帳戶。

**** 描述檔更新：受邀的使用者會變更其名稱、組織名稱和密碼。

**** 帳戶鎖定：管理員鎖定帳戶。

**策略集事件**

**** CreatedPolicy Set:管理員或策略集協調員建立策略集。

**** 已刪除策略集：管理員或策略集協調員刪除策略集。

**** 修改的策略集：管理員或策略集協調員更改策略集。

**系統事件**

**** 目錄同步完成：「事件」頁面無法提供這項資訊。 當前目錄同步資訊（包括上次同步的當前同步狀態和時間）顯示在「域管理」頁上。 若要存取管理控制台中的「網域管理」頁面，請按一下「設定>使用者管理>網域管理」。

**** 客戶端啟用離線訪問：使用者啟用離線存取，以存取使用者電腦上伺服器所保護的檔案。

**同步化Client** Client應用程式必須將資訊與伺服器同步，才允許離線存取。

**** 版本不符：與伺服器不相容的AEM表單SDK版本嘗試連線至伺服器。

**** 目錄同步資訊：「事件」頁面無法提供這項資訊。 當前目錄同步資訊（包括上次同步的當前同步狀態和時間）顯示在「域管理」頁上。 若要存取管理控制台中的「網域管理」頁面，請按一下「設定>使用者管理>網域管理」。

**** 伺服器配置更改：對伺服器組態所做的變更，這些變更會透過網頁或透過匯入config.xml檔案手動完成。 這包括對基本URL、會話超時、登錄鎖定、目錄設定、密鑰變換、外部註冊的SMTP伺服器設定、水印配置、顯示選項等的更改。

## 設定擴充的使用狀況追蹤 {#configuring-extended-usage-tracking}

檔案安全性可追蹤可在受保護檔案上執行的各種自訂事件。 您可以在全域層級或原則層級，啟用從Document Security伺服器追蹤事件的功能。 然後，您可以設定JavaScript來擷取在受保護PDF檔案中執行的特定動作，例如按一下按鈕或儲存檔案。 此使用資料會以XML檔案的形式，以索引鍵值配對傳送，供您進一步分析。 存取受保護檔案的使用者可允許或拒絕用戶端應用程式的此類追蹤。

如果在全域層級啟用追蹤，您可以在原則層級覆寫此設定，並針對特定原則停用此設定。 如果在全域層級停用追蹤，則無法進行原則層級覆寫。 當事件計數達到25或檔案關閉時，追蹤事件清單會自動推送至伺服器。 您也可以設定指令碼，根據您的需求明確推送事件清單。 您可以存取Document Security物件屬性和方法，自訂事件追蹤。

啟用追蹤後，後續建立的所有原則都會依預設開啟追蹤。 在伺服器上啟用追蹤之前建立的原則需要手動更新。

### 啟用或停用擴充的使用狀況追蹤 {#enable-or-disable-extended-usage-tracking}

開始之前，請確定已啟用「伺服器審計」。 有關審 [核的詳細資訊](configuring-client-server-options.md#configuring-event-auditing-and-privacy-settings) ，請參閱配置事件審計和隱私設定。

1. 在管理主控台中，按一下「服務> Document Security >設定>稽核和隱私權設定」。
1. 若要設定擴充的使用追蹤，請在「啟用追蹤」下方，選取「是」或「否」。
1. 若要在登入頁面上設定「允許收集詳細使用資料」核取方塊的選取，請在「啟用追蹤預設值」下方選取「是」或「否」。

若要檢視追蹤的事件，您可以使用「事件」頁面上的「檔案事件」篩選。 使用JavaScript追蹤的事件會標示為「詳細的使用追蹤」。 有關事件 [的詳細資訊](/help/forms/using/admin-help/monitoring-events.md#monitoring-events) ，請參閱監視事件。

## 設定檔案安全性顯示設定 {#configure-document-security-display-settings}

1. 在管理控制台中，按一下「服務>檔案安全性>設定>顯示選項」。
1. 配置設定並按一下確定。

### Display settings {#display-settings}

**** 要顯示搜索結果的行：執行搜索時在頁面上顯示的行數。

**用戶端登入對話框的自訂**

這些設定可控制當使用者透過用戶端應用程式登入檔案保全時，登入提示中顯示的文字。

**** 歡迎文字：歡迎訊息文字，例如「請使用您的使用者名稱和密碼登入」。 歡迎訊息文字應包含如何登入檔案安全性，以及如何聯絡您組織中的管理員或其他指定支援人員以取得協助的資訊。 例如，如果外部使用者忘記密碼或需要註冊或登入程式的協助，則可能需要聯絡管理員。 歡迎文字的最大長度為512個字元。

**** 用戶名文本：用戶名框的文本標籤。

**** 密碼文字：密碼框的文本標籤。

**自訂用戶端認證驗證對話方塊**

這些設定會控制憑證驗證對話方塊中顯示的文字。

**** 選擇驗證類型文本：顯示的文本用於引導用戶選擇驗證類型。

**** 選擇憑證文字：顯示的文本用於引導用戶選擇證書類型。

**** 證書不可用錯誤文本：當選取的憑證無法使用時，最多會顯示512個字元的訊息。

**自訂用戶端憑證顯示**

**** 僅顯示受信任的憑證發行者：選取此選項時，用戶端應用程式只會向使用者提供AEM表單設定為信任的憑證發行者憑證（請參閱管理憑證和憑證）。如果未選取此選項，使用者會收到使用者系統上所有憑證的清單。

## 設定動態浮水印 {#configure-dynamic-watermarks}

使用檔案安全性，您可以設定動態水印選項的預設設定，當您建立原則時可套用此選項。 水 *印* ，是疊加在檔案文字上的影像。 它對於追蹤檔案內容非常有用，而且有助於識別非法使用內容。

動態水印可以由定義的變數（例如使用者ID、日期和自訂文字）組成的文字，或PDF中的豐富式內容組成。 您可以使用多個元素來設定浮水印，每個元素都有自己的定位和格式。

水印是不可編輯的，因此是確保檔案內容機密性的更安全方法。 動態水印也可確保水印顯示足夠的使用者特定資訊，以做為進一步散布檔案的威懾。

當收件者檢視或列印檔案時，原則指定的浮水印會出現在受原則保護的檔案中。 與永久浮水印不同，動態浮水印不會儲存在檔案中，這提供了在內部網路環境中部署檔案時的彈性，以確保檢視應用程式顯示特定使用者的身分。 此外，如果檔案有多位使用者，使用動態水印表示您可以使用一個檔案而非多個版本，每個版本都有不同的水印。 顯示的水印反映當前用戶的身份。

請注意，動態浮水印與使用者可直接在Acrobat中新增至檔案的浮水印不同。 結果是，受原則保護的檔案中可以有兩個浮水印。

### 建立浮水印時的注意事項 {#considerations-when-creating-watermarks}

您可以使用多個水印元素建立動態水印，每個元素都指定為文字或PDF。 在浮水印中最多可包含5個元素。

如果您選擇文字型水印，則可以在水印中指定多個元素並輸入多個文字項目，並指定每個元素的位置。 為這些元素指定有意義的名稱，例如頁首、頁尾等。

例如，如果您想要在頁首、頁尾、邊界和整個檔案中指定不同的文字做為浮水印，則可建立數個浮水印元素並指定其位置。 如果希望用戶的用戶ID和當前訪問文檔的日期顯示在標題中，右邊距中的策略名稱和自定義文本「機密」對角線顯示在文檔上，則可以定義單獨的水印元素，其類型為文本，並指定其格式和位置。 當水印套用至檔案時，水印中的所有元素會同時套用至檔案，依其新增至水印的順序排列。

通常，您會使用PDF浮水印來包含圖形內容，例如標誌或特殊符號，例如版權或註冊商標。

您可以修改檔案安全性設定檔案，以變更浮水印元素數目和PDF檔案大小的限制。 請參 [閱更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。

配置浮水印時，請記住以下事項：

* 您無法使用受密碼保護的PDF檔案做為浮水印元素。 不過，如果您建立的浮水印包含其他未受密碼保護的元素，則這些元素將會套用為浮水印的一部分。
* 您可以變更要用作浮水印元素的PDF檔案大小上限。 不過，當套用浮水印的檔案離線同步化時，大型的PDF檔案會降低效能。 請參 [閱更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)。
* 只有選取的PDF第一頁會當做浮水印使用。 請確定您要顯示為浮水印的資訊可在第一頁本身使用。
* 即使您可以指定PDF檔案的縮放比例，如果您打算將PDF當做頁首、頁尾或邊界中的浮水印使用，請考慮其頁面大小和版面配置。
* 指定字型名稱時，請正確輸入名稱。 AEM表格會取代您指定的字型（如果該字型不存在於開啟檔案的用戶端機器中）。
* 如果您選取文字作為浮水印內容，則將縮放選項指定為「最適頁面大小」(Fit To Page)對寬度不相同的頁面不起作用。
* 當您指定浮水印元素的位置時，請確定最多一個元素具有相同的位置。 如果兩個水印元素具有相同的位置（例如中心），它們會重疊在檔案上，並依順序加入到水印中。
* 指定字型大小和文字時，請確定文字長度在頁面中完全可見。 文字內容會指向新行，因此您原本要出現在邊界中的浮水印內容可能會重疊在頁面上的內容區域。 不過，如果檔案在Acrobat 9中開啟，單行以外的文字會被截斷。

### 動態水印的限制 {#limitations-of-dynamic-watermarks}

有些用戶端應用程式可能不支援動態浮水印。 請參閱適當的Acrobat Reader DC擴充功能說明。 此外，請記住下列支援動態浮水印的Acrobat版本：

* 您無法使用受密碼保護的PDF檔案做為浮水印元素。
* Acrobat和Adobe Reader 10之前的版本不支援下列浮水印功能：

   * PDF浮水印
   * 浮水印中的多個元素（文字/PDF）
   * 進階選項，例如頁面範圍或顯示選項
   * 文字格式選項，例如指定的字型、字型名稱和顏色。 不過，舊版Acrobat和Reader會以預設字型和顏色顯示文字內容。

* Acrobat 9.0及舊版：Acrobat 9.0及舊版不支援動態浮水印的原則名稱。 如果Acrobat 9.0開啟受原則保護的檔案，其中包含原則名稱和其他動態資料的動態水印，則會顯示水印，而不包含原則名稱。 如果動態水印只包含原則名稱，Acrobat會顯示錯誤訊息

### 新增動態水印範本 {#add-a-dynamic-watermark-template}

您可以建立動態水印範本。 這些範本仍可作為管理員或使用者建立之原則的設定選項。

>[!NOTE]
>
>在導出配置檔案時，動態水印配置資訊不會與其他配置資訊一起捕獲。

1. 在管理控制台中，按一下「服務> Document Security >設定>浮水印」。
1. 按一下「新增」。
1. 在「名稱」框中，鍵入新水印的名稱。

   ***注意&#x200B;**:水印或水印元素的名稱或說明中不能使用某些特殊字元。 請參閱「考量事項」中列出的[限制，以編輯原則](/help/forms/using/admin-help/creating-policies.md#considerations-for-editing-policies)。*

1. 在「名稱」下，在加號旁輸入有意義的名稱至浮水印元素，例如「頁首」，然後新增說明，並展開加號以顯示選項。
1. 在「來源」下，選取「文字」或「PDF」的水印類型。
1. 如果您選取「文字」，請執行下列動作：

   * 選擇要包括的水印類型。 如果您選取「自訂文字」，請在相鄰方塊中輸入要顯示浮水印的文字。 請記住將顯示為浮水印的文字長度。
   * 為水印文本的文本內容指定文本格式屬性，如字型名稱、字型大小、前景顏色和背景顏色。 將前景和背景顏色指定為十六進位值。

      ***注意&#x200B;**:如果您選取「調整大小」選項為「最適頁面大小」，則無法編輯字型大小屬性。*

1. 如果您選取PDF做為豐富水印選項，請按一下「選取浮水印PDF」旁的「瀏覽 **** 」，以選取您要當做浮水印的PDF檔案。

   ***注意&#x200B;**:請勿使用受密碼保護的PDF檔案。 如果您指定受密碼保護的PDF做為浮水印元素，則不會套用浮水印。*

1. 在「用作背景」下，選擇「是」或「否」。

   **注意**:目前，水印會出現在前景中，而不考慮此設定。

1. 要控制水印在文檔中的顯示位置，請配置「垂直對齊」和「水準對齊」選項。
1. 選擇「適合頁面大小」或選擇%，然後在方塊中輸入百分比。 值必須是整數，而非分數。 若要設定浮水印大小，您可以使用頁面的百分比值，或設定浮水印以符合頁面大小。
1. 在「旋轉」框中，鍵入要旋轉水印的度。 範圍是-180到180。 使用負值可逆時針旋轉水印。 值必須是整數，而非分數。
1. 在「不透明度」方塊中，輸入百分比。 使用整數，而非零碎。
1. 在「進階選項」下，設定下列項目：

   **頁面範圍選項**

   設定應顯示浮水印的頁面範圍。 將開始頁輸入為1，將結束頁輸入為-1，以使所有頁都標有水印。

   **顯示選項**

   選擇要使水印出現的位置。 預設情況下，水印會同時出現在軟拷貝（聯機）和硬拷貝（打印）上。

1. 如有必 **要** ，按一下「浮水印元素」下方的「新增」，新增更多浮水印元素。
1. 按一下「確定」。

### 編輯動態水印範本 {#edit-a-dynamic-watermark-template}

1. 在管理控制台中，按一下「服務>檔案安全性>設定>浮水印」。
1. 在清單中按一下適當的浮水印。
1. 在「編輯浮水印」頁面上，視需要變更設定。
1. 按一下「確定」。

### 刪除動態水印範本 {#delete-a-dynamic-watermark-template}

刪除動態水印時，它不再可用於添加到新策略中。 但是，水印仍保留在當前使用該水印的現有策略上，並且當前保護該策略的文檔將繼續顯示動態水印，直到您或用戶編輯包含已刪除水印的策略為止。 在編輯原則後，將不再套用浮水印。 出現一條消息，指出策略上已刪除現有水印，用戶可以選擇另一個水印來替換它。

1. 在管理控制台中，按一下「服務> Document Security >設定>浮水印」。
1. 選擇適當水印旁的複選框，然後按一下「刪除」。
1. 按一下「確定」。

## 設定邀請的使用者註冊 {#configuring-invited-user-registration}

您組織外部的使用者可以使用檔案保全進行註冊。 已邀請的使用者註冊並啟動其帳戶後，可以使用其電子郵件地址和在註冊時建立的密碼登入檔案安全性。 已註冊的受邀使用者可以使用他們擁有權限的受原則保護檔案。

當被邀請的使用者啟動後，就會成為本機使用者。 您可使用「已邀請」和「本機使用者」區來設定和管理本機使用者。 (請參 [閱管理已邀請和本機使用者帳戶](/help/forms/using/admin-help/invited-local-user-accounts.md#managing-invited-and-local-user-accounts)。)

視您為受邀使用者啟用的功能而定，他們也可以使用下列檔案保全功能：

* 套用原則至檔案
* 建立原則
* 將邀請的使用者新增至原則

當發生下列事件時，Document Security會自動產生註冊邀請電子郵件，除非使用者已位於來源LDAP目錄中或先前已受邀註冊：

* 現有用戶將被邀請的用戶添加到策略
* 管理員在「邀請的用戶註冊」頁面上添加一個已邀請的用戶帳戶

註冊電子郵件包含「註冊」頁面的連結，以及如何註冊的資訊。 在邀請的使用者註冊後，檔案安全性會發出啟動電子郵件，並附上啟動頁面的連結。 啟用後，帳戶會一直有效，直到您停用或刪除為止。

如果啟用內置註冊，則只需指定一次SMTP伺服器、註冊電子郵件詳細資訊、訪問權能和重設密碼電子郵件資訊。 在啟用內建註冊之前，請確定您已在「使用者管理」中建立本機網域，已將「Document security Invite User」角色指派給貴組織中適當的使用者和群組。 (請參 [閱添加本地域](/help/forms/using/admin-help/adding-domains.md#add-a-local-domain)[和建立和配置角色](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)。)如果您不使用內建註冊，則必須使用AEM表單SDK建立您自己的使用者註冊系統。 請參閱「使用AEM表單進行程式設計」中的「開發AEM表 [單的SPI」說明](https://www.adobe.com/go/learn-aemforms-programming-63)。 如果您不使用內建註冊選項，建議您在啟動電子郵件和用戶端登入畫面中設定訊息，以通知使用者如何聯絡管理員以取得新密碼或取得其他資訊。

**啟用和設定邀請的使用者註冊**

依預設，已邀請的使用者註冊程式會停用。 您可以視需要啟用和停用邀請的使用者註冊，以確保檔案安全。

1. 在管理控制台中，按一下「服務>檔案安全性>設定>已邀請的使用者註冊」。
1. 選擇「啟用邀請的用戶註冊」。
1. （選擇性）視需要更新已邀請的使用者註冊設定：

   * [排除或包含外部使用者或群組](configuring-client-server-options.md#exclude-or-include-an-external-user-or-group)
   * [伺服器與註冊帳戶參數](configuring-client-server-options.md#server-and-registration-account-parameters)
   * [註冊邀請電子郵件設定](configuring-client-server-options.md#registration-invitation-email-settings)
   * [啟動電子郵件設定](configuring-client-server-options.md#activation-email-settings)
   * [設定密碼重設電子郵件](configuring-client-server-options.md#configure-a-password-reset-email)

1. （可選）在「內建註冊」下，選擇「是」以啟用此選項。 如果您未啟用內建註冊，則必須設定您自己的使用者註冊系統。
1. 按一下「確定」。

### 排除或包含外部使用者或群組 {#exclude-or-include-an-external-user-or-group}

您可以限制某些外部使用者或使用者群組的檔案安全性註冊。 例如，此選項對於允許存取特定使用者群組但排除屬於群組之特定個人非常有用。

下列設定位於「已邀請的使用者註冊」頁面的「電子郵件限制篩選」區域。

**** 排除：輸入要排除的使用者或群組的電子郵件地址。 若要排除多個使用者或群組，請在新行上輸入每個電子郵件地址。 要排除屬於特定域的所有用戶，請輸入通配符和域名。 例如，要排除example.com域中的所有用戶，請輸入&amp;ast;.example.com。

**** 包含：輸入要包含的使用者或群組的電子郵件地址。 若要包含多個使用者或群組，請在新行上輸入每個電子郵件地址。 要包括屬於特定域的所有用戶，請輸入通配符和域名。 例如，要將所有用戶包括在example.com域中，請輸入&amp;ast;.example.com。

### 伺服器與註冊帳戶參數 {#server-and-registration-account-parameters}

下列設定位於「已邀請的使用者註冊」頁面的「一般設定」區域。

**** SMTP主機：SMTP伺服器的主機名。 SMTP伺服器管理傳出電子郵件通知，以註冊並激活邀請的用戶帳戶。

如果SMTP主機需要，請在「SMTP伺服器帳戶名」和「SMTP伺服器帳戶密碼」框中鍵入所需資訊以連接到SMTP伺服器。 有些組織不執行此要求。 如果您需要資訊，請咨詢系統管理員。

**** SMTP伺服器套接字類名：SMTP伺服器的套接字類名。 例如，javax.net.ssl.SSLSocketFactory。

**** 電子郵件內容類型：接受的MIME類型，例如text/plain或text/html。

**** 電子郵件編碼：用於傳送電子郵件訊息的編碼格式。 您可以指定任何編碼，例如，Unicode的UTF-8或Latin的ISO-8859-1。 預設值為UTF-8。

**** 重新導向電子郵件地址：當您指定此設定的電子郵件地址時，任何新邀請都會傳送至所提供的地址。 此設定可用於測試用途。

**** 使用本機網域：選擇適當的網域。 在新安裝中，請確定您使用「使用者管理」建立網域。 如果這是升級，則在升級期間會建立外部使用者網域，並可使用。

**** 對SMTP伺服器使用SSL:選擇此選項可為SMTP伺服器啟用SSL。

**** 在註冊頁面上顯示登入連結：在為受邀使用者顯示的註冊頁面上顯示登入連結。

**為SMTP伺服器啟用傳輸層安全(TLS)**

1. 開啟管理控制台。

   管理控制台的預設位置為 `https://<server>:<port>/adminui`。

1. 導覽至「首頁>服務> Document Security >設定>已邀請的使用者註冊」。
1. 在「已邀請的用戶註冊」上，指定所有配置設定，然後按一下「確定」。

   >[!NOTE]
   >
   >如果您使用Microsoft Office 365作為SMTP伺服器來發送用戶註冊邀請，請使用以下設定：
   >
   >**** SMTP主機：smtp.office365.com
   >**** 埠：587

1. 接下來，您需要更新config.xml。 請參 [閱配置以啟用SMTP以實現傳輸層安全(TLS)](configuring-client-server-options.md#configuration-to-enable-smtp-for-transport-layer-security-tls)

>[!NOTE]
>
>如果您對「已邀請的使用者註冊」選項進行任何變更，則會覆寫config.xml檔案，並停用TLS。 如果您覆寫變更，您必須執行上述步驟，才能重新啟用「已邀請的使用者註冊」的TLS支援。

### 註冊邀請電子郵件設定 {#registration-invitation-email-settings}

當您建立新的受邀使用者帳戶，或現有使用者新增先前未註冊或受邀註冊至原則的外部收件者時，檔案安全性會自動發出註冊邀請電子郵件。 電子郵件包含收件者可用來存取註冊頁面並輸入個人帳戶資訊的連結，包括使用者名稱和密碼。 密碼可以是8個字元的任意組合。

當收件者啟動帳戶時，使用者會變成本機使用者。

下列設定位於「已邀請的使用者註冊」頁面的「邀請電子郵件設定」區域。

**** 寄件者：傳送邀請電子郵件的電子郵件地址。 「寄件者」電子郵件地址的預設格式為postmaster@[your_installation_domain].com。

**** 主旨：邀請電子郵件訊息的預設主旨。

**** 逾時：如果外部用戶未註冊，則註冊邀請的過期天數。 預設值為30天。

**** 訊息：在邀請使用者註冊的訊息內文中出現的文字。

### 啟動電子郵件設定 {#activation-email-settings}

在邀請的使用者註冊後，檔案安全性會傳送啟動電子郵件。 啟動電子郵件包含帳戶啟動頁面的連結，使用者可在該頁面啟動其帳戶。 啟用帳戶後，使用者可以使用其電子郵件地址和在註冊時建立的密碼來登入檔案安全性。

當收件者啟動使用者帳戶時，使用者會變成本機使用者。

下列設定位於「邀請的使用者註冊」頁面的「啟動電子郵件設定」區域。

>[!NOTE]
>
>建議您在登入畫面上設定訊息，建議外部使用者如何連絡其管理員以取得新密碼或其他資訊。

**** 寄件者：啟動電子郵件寄出的電子郵件地址。 此電子郵件地址會從註冊者的電子郵件主機收到失敗的傳送通知，以及收件者回覆註冊電子郵件所傳送的任何訊息。 「寄件者」電子郵件地址的預設格式為postmaster@[your_installation_domain].com。

**** 主旨：啟動電子郵件訊息的預設主旨。

**** 逾時：如果使用者未啟用帳戶，啟動邀請的過期天數。 預設值為30天。

**** 訊息：訊息內文中顯示的文字是訊息，指出收件者的使用者帳戶需要啟動。 您也可能想要包含如何聯絡管理員以取得新密碼等資訊。

### 設定密碼重設電子郵件 {#configure-a-password-reset-email}

如果您必須重設受邀使用者的密碼，則會產生確認電子郵件，邀請使用者選擇新密碼。 無法判斷使用者的密碼；如果使用者忘記，您必須重設它。

下列設定位於「已邀請的使用者註冊」頁面的「重設密碼電子郵件」區域。

**** 寄件者：發送密碼重設電子郵件的電子郵件地址。 「寄件者」電子郵件地址的預設格式為postmaster@[your_installation_domain].com。

**** 主旨：重設電子郵件訊息的預設主旨。

**** 訊息：訊息內文中顯示的文字是訊息，指出收件者的外部使用者密碼已重設。

## 讓使用者和群組可建立原則 {#enable-users-and-groups-to-create-policies}

「配置」頁具有指向「我的策略」頁的連結，您可以在此頁中指定哪些最終用戶可以建立策略，以及哪些用戶和組在搜索結果中可見。 「我的策略」頁有兩個頁籤：

**** 建立策略頁籤：用於配置用戶權限以建立自定義策略。

**** 「可見用戶和組」頁籤：用於控制哪些用戶和組在用戶搜索結果中可見。 超級用戶或策略集管理員需要選擇在「用戶管理」中建立的域並將其添加到每個策略集的可見用戶和組。 此清單對策略集協調器可見，用於限制策略集協調器在選擇要添加到策略的用戶時可以瀏覽哪些域。

在授予使用者建立自訂原則的權限之前，請先考慮個別使用者想要擁有多少存取權或控制權。 此外，請考慮在讓使用者和群組顯示在搜尋時，您希望使用者和群組的公開度。

### 指定可建立原則的使用者和群組 {#specify-users-and-groups-who-can-create-policies}

身為管理員，指定哪些使用者和群組可以建立自訂原則。 此權限可在使用者和群組層級設定。 搜尋功能會搜尋使用者管理資料庫中的使用者和群組。

1. 在管理控制台中，按一下「服務> Document Security >設定>我的原則」。
1. 在「我的策略」頁面上，按一下「建立策略」頁籤，然後按一下「添加用戶和組」。
1. 在「尋找」方塊中，輸入您所搜尋之使用者或群組的使用者名稱或電子郵件地址。 如果您沒有此資訊，請將方塊留空。 您也可以輸入部分名稱或電子郵件地址，例如您只知道使用者名稱的前兩個字母。
1. 在「使用」清單中，選擇搜索參數「名稱」或「電子郵件」。
1. 在「類型」清單中，選擇「組」或「用戶」以縮小搜索範圍。
1. 在「在」清單中，選擇要搜索的域。 如果您不知道使用者或群組的網域，請選取「所有網域」。
1. 在「顯示」清單中，指定每個頁面要顯示的搜尋結果數目，然後按一下「尋找」。
1. 要添加「我的策略」用戶和組，請為要添加的每個用戶和組選擇複選框。
1. 按一下「新增」，然後按一下「確定」。

您選取的使用者和群組現在擁有建立自訂原則的權限。

### 從用戶或組中刪除建立自定義策略權限 {#remove-the-create-custom-policies-permission-from-a-user-or-group}

1. 在檔案安全性頁面上，按一下設定>我的原則。
1. 在「我的策略」頁上，按一下「建立策略」頁籤。 將顯示具有建立自定義策略權限的用戶和組。
1. 選取要從此權限移除的使用者和群組旁的核取方塊。
1. 按一下「刪除」，然後按一下「確定」。

### 指定在搜尋中可見的使用者和群組 {#specify-users-and-groups-that-are-visible-in-searches}

當使用者管理其自訂原則時，可搜尋要新增至其原則的使用者和群組。 您必須指定在這些搜尋中可看到使用者和群組的網域。

1. 在檔案安全性頁面上，按一下設定>我的原則。
1. 在「我的策略」頁面上，按一下「可見用戶和組」頁籤。
1. 若要讓網域中的使用者和群組可見，請按一下「新增網域」，選取網域，然後按一下「新增」。 要刪除域，請選擇域名旁的複選框，然後按一下刪除。

## 手動編輯Document Security設定檔案 {#manually-editing-the-document-security-configuration-file}

您可以匯入和匯出儲存在Document Security資料庫中的設定資訊。 例如，當您從測試移至生產環境時，可能想要製作配置資訊的備份副本，或者您想要編輯只能設定為編輯此檔案的進階選項。

您可以使用配置檔案進行以下更改：

[建立和編輯策略時顯示CATIA權限](configuring-client-server-options.md#display-catia-permissions-when-creating-and-editing-policies)

[指定離線同步的逾時期間](configuring-client-server-options.md#specify-a-timeout-period-for-offline-synchronization)

[拒絕特定應用程式的檔案安全性服務](configuring-client-server-options.md#denying-document-security-services-for-specific-applications)

[更改水印配置參數](configuring-client-server-options.md#change-the-watermark-configuration-parameters)

[停用外部連結](configuring-client-server-options.md#disabling-external-links)

>[!NOTE]
>
>導入配置檔案會根據檔案中的資訊重新配置系統。 例外是動態水印設定和自訂事件資訊，這些資訊不會與匯出的設定檔案一起儲存。 您必須在新系統中手動配置此資訊。 只有熟悉檔案安全性和XML的系統管理員或專業服務顧問才應修改配置檔案的內容，例如重新配置損壞的設定或調整特定企業部署方案的參數。

**導出配置檔案**

1. 在管理控制台中，按一下「服務>檔案安全性11 >設定>手動設定」。
1. 按一下「導出」(Export)，將配置檔案保存到其他位置。 預設檔案名稱為config.xml。
1. 按一下「確定」。
1. 在更改配置檔案之前，請建立備份副本，以備需要恢復時使用。

**導入配置檔案**

1. 在管理控制台中，按一下「服務>檔案安全性11 >設定>手動設定」。
1. 按一下「瀏覽」前往設定檔案，然後按一下「匯入」。 不能直接在「檔案名」框中鍵入路徑。
1. 按一下「確定」。

### 指定離線同步的逾時期間 {#specify-a-timeout-period-for-offline-synchronization}

當使用者未連線至Document Security伺服器時，Document security可讓他們開啟並使用受保護的檔案。 使用者的用戶端應用程式必須定期與伺服器同步，以維持離線使用的檔案有效性。 當使用者第一次開啟受保護的檔案時，會詢問其電腦是否應獲得執行定期用戶端同步的授權。

依預設，當使用者連線至Document Security伺服器時，同步會每隔四小時自動進行，而且視需要進行。 如果文檔的離線期間在用戶離線時過期，則用戶必須重新連接到伺服器，以使客戶端應用程式與伺服器同步。

在Document Security設定檔中，您可以指定自動背景同步的預設頻率。 此設定用作預設超時期間客戶端應用程式，除非客戶端明確設定自己的超時值。

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到該 `PolicyServer` 節點。 在該節點下，找到該節 `ServerSettings` 點。
1. 在節 `ServerSettings` 點中，添加以下條目並保存檔案：

   `<entry key="BackgroundSyncFrequency" value="`*時間&#x200B;*`"/>`

   其中 *時間* 是自動背景同步之間的秒數。 如果將此值發送到，則 `0`始終會進行同步。 預設值為 `14400` 秒（每四小時）。

1. 導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

### 拒絕特定應用程式的檔案安全性服務 {#denying-document-security-services-for-specific-applications}

您可以設定檔案安全性，以拒絕符合特定條件之應用程式的服務。 准則可以指定單一屬性，例如平台名稱，也可以指定多組屬性。 此功能可協助您控制檔案安全性必須處理的要求。 以下是此功能的一些應用程式：

* **** 收入保護：您可能想要拒絕任何不支援您收入慣例之用戶端應用程式的存取權。
* **** 應用程式相容性：某些應用程式可能與您的檔案安全伺服器的原則或行為不相容。

當用戶端應用程式嘗試建立具有檔案安全性的連結時，就會提供應用程式、版本和平台資訊。 Document Security會將此資訊與從Document Security設定檔取得的「拒絕」設定進行比較。

「拒絕」設定可包含陣列拒絕條件。 如果任一組屬性的所有屬性都相符，則拒絕請求應用程式存取檔案安全服務。

拒絕服務功能要求用戶端應用程式使用檔案安全性C++用戶端SDK 8.2版或更新版本。 下列Adobe產品在要求檔案保全服務時提供產品資訊：

* Adobe Acrobat 9.0 Professional/Acrobat 9.0 Standard及更新版本
* Adobe Reader 9.0和更新版本
* 適用於Microsoft Office 8.2和更新版本的Acrobat Reader DC擴充功能

用戶端應用程式會使用檔案安全性C++用戶端SDK的用戶端API，向檔案安全性要求服務。 用戶端API要求包括平台和SDK版本資訊（預先編譯至用戶端API），以及從用戶端應用程式取得的產品資訊。

用戶端應用程式或外掛程式在其回呼函式的實施中提供產品資訊。 應用程式提供下列資訊：

* 整合器名稱
* 整合器版本
* 應用程式系列
* 應用程式名稱
* 應用程式版本

如果任何資訊不適用，客戶端應用程式會將相應欄位留空。

數個Adobe應用程式在要求檔案保全服務時會包含產品資訊，包括Acrobat、Adobe Reader和Microsoft office專用的Acrobat Reader DC擴充功能。

**Acrobat和Adobe Reader**

當Acrobat或Adobe Reader向檔案安全性要求服務時，會提供下列產品資訊：

* **** 整合商：Adobe Systems, Inc.
* **** 整合器版本：1.0
* **** 應用程式系列：Acrobat
* **** 應用程式名稱：Acrobat
* **** 應用程式版本：9.0.0

**適用於Microsoft Office的Acrobat Reader DC擴充功能**

適用於Microsoft office的Acrobat Reader DC擴充功能是與Microsoft Word、Microsoft excel和Microsoft powerPoint等Microsoft office產品搭配使用的增效模組。 當它請求服務時，它提供以下資訊：

* **** 整合商：Adobe Systems Incorporated
* **** 整合器版本：8.2
* **** 應用程式系列：適用於Microsoft Office的Acrobat Reader DC擴充功能
* **** 應用程式名稱：Microsoft Word、Microsoft excel或Microsoft powerPoint
* **** 應用程式版本：2003或2007年

**設定檔案安全性以拒絕特定應用程式的服務**

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到該 `PolicyServer` 節點。 添加節 `ClientVersionRules` 點作為節點的直接子 `PolicyServer` 節點（如果不存在）:

   ```as3
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

   `SDKPlatforms` 指定代管用戶端應用程式的平台。 可能的值包括：

   * Microsoft Windows
   * Apple OS X
   * Sun Solaris
   * HP-UX
   `SDKVersions` 指定用戶端應用程式所使用的檔案安全性C++用戶端API版本。 例如， `"8.2"`。

   `APPFamilies` 由用戶端API定義。

   `AppName`指定客戶端應用程式的名稱。 逗號用作名稱分隔符。 若要在名稱中加入逗號，請以反斜線(\)字元逸出逗號。 例如， *「Adobe Systems\, Inc.」*。

   `AppVersions` 指定客戶端應用程式的版本。

   `Integrators` 指定開發外掛程式或整合式應用程式的公司或群組名稱。

   `IntegratorVersions` 是外掛程式或整合式應用程式的版本。

1. 對於每組附加的拒絕資料，添加另一 *個MyEntryName* 元素。
1. 保存配置檔案。
1. 導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

**範例**

在此示例中，所有Windows客戶端都被拒絕訪問。

```as3
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

在此範例中，「我的應用程式3.0版」和「我的其他應用程式2.0版」都被拒絕存取。 無論拒絕的原因為何，都會使用相同的拒絕資訊URL。

```as3
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
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

在此範例中，來自Microsoft powerPoint 2007或Microsoft powerPoint 2010安裝Microsoft Office專用Acrobat Reader DC擴充功能的所有要求均遭拒絕。

```as3
 <node name="ClientVersionRules">
     <map>
         <entry key="infoURL" value=”https://get.a.new/version.html”/>
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

依預設，您最多可以在浮水印中指定五個元素。 此外，您要用作浮水印的PDF檔案檔案大小上限為100KB。 您可以在config.xml檔案中變更這些參數。

***注意&#x200B;**:您應謹慎變更這些參數。*

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到該 `ServerSettings` 節點。
1. 在節 `ServerSettings` 點中，添加以下條目並保存檔案： `<entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/> <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>`

   第一個項目， *最大檔案大小* ，是PDF浮水印元素允許的最大檔案大小（以KB為單位）。 預設值為100KB。

   第二個項目 *，最大元素* ，是浮水印中允許的最大元素數。 預設值為5。

   ```as3
   <entry key="maximumSizeOfWatermarkElement" value="max filesize in KB"/>
   <entry key="maximumWatermarkElementsPerWatermark" value="max elements"/>
   ```

1. 導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

### 停用外部連結 {#disabling-external-links}

許多檔案安全性使用者在使用「正確管理」使用者介面時，無法 **存取** www.adobe.com等外部連結：

* `https://[host]:[port]/adminui`
* `https://[host]:[port]/edc`.

下列對config.xml的變更會停用「Right Management」使用者介面的所有外部連結。

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到該 `DisplaySettings` 節點。
1. 要禁用所有外部連結，請在節 `DisplaySettings` 點中添加以下條目，然後保存檔案： `<entry key="ExternalLinksAllowed" value="false"/>`

   ```as3
   <entry key="ExternalLinksAllowed" value="false"/>
   ```

1. 導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

### 用於啟用SMTP進行傳輸層安全(TLS)的配置 {#configuration-to-enable-smtp-for-transport-layer-security-tls}

對config.xml所做的下列變更可啟用「邀請的使用者註冊」功能的TLS支援。

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到該 `DisplaySettings` 節點。
1. 找到以下節點： `<node name="ExternalUser">`

   ```as3
   <node name="ExternalUser">
   ```

1. 將節點中 `SmtpUseTls` 的鍵值 `ExternalUser` 設定為 **true**。
1. 將節點中的 `SmtpUseSsl` 鍵值設 `ExternalUser` 置為 **false**。
1. 儲存 `config.xml`。
1. 導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

### 停用Document Security檔案的SOAP端點 {#disable-soap-endpoints-for-document-security-documents}

下列對config.xml所做的變更會停用檔案安全性檔案的SOAP端點。

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到以下節點： `<node name="DRM">`

   ```as3
   <node name="DRM">
   ```

1. 在DRM節點中，找到該 `entry` 節點：

   `<entry key="AllowUnencryptedVoucher" value="true"/>`

1. 若要停用檔案安全性檔案的SOAP端點，請將值屬性設 **為false**。

   ```as3
   <node name="DRM">
       <map>
           <entry key="AllowUnencryptedVoucher" value="false"/>
       </map>
   </node>
   ```

1. 儲存 `config.xml`。
1. 導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

### 提高檔案安全性伺服器的可擴充性 {#increasingscalability}

依預設，在同步化檔案以供離線使用時，檔案安全性用戶端會為使用者可存取的所有其他檔案擷取原則、浮水印、授權和撤銷更新資訊。 如果這些更新和資訊未與用戶端同步，則離線模式下開啟的檔案仍可能會開啟舊版原則、浮水印和撤銷資訊。

您可以限制傳送至用戶端的資訊，以提高檔案安全性伺服器的可擴充性。 傳送給用戶端的資訊量減少，可改善擴充性、縮短回應時間，並改善伺服器的效能。 執行下列步驟以提高可擴充性：

1. 匯出檔案保全設定檔。 (請參 [閱手動編輯Document Security設定檔](configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。
1. 在編輯器中開啟配置檔案並找到ServerSettings節點。
1. 在ServerSettings節點中，將屬性的值 `DisableGlobalOfflineSynchronizationData`設定為 `true`。

   `<entry key="DisableGlobalOfflineSynchronizationData" value="true"/>`

   當設定為true時，文檔安全伺服器僅發送當前文檔的資訊，其餘文檔（用戶有權訪問的其他文檔）的資訊不發送到客戶端。

   >[!NOTE]
   >
   >預設情況下，鍵的 `DisableGlobalOfflineSynchronizationData`值設定為 `false`。

1. 保存並導入配置檔案。 (請參 [閱手動編輯Document Security設定檔](/help/forms/using/admin-help/configuring-client-server-options.md#manually-editing-the-document-security-configuration-file))。

