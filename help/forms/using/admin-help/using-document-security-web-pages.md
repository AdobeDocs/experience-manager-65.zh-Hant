---
title: 使用Document Security網頁
seo-title: 使用Document Security網頁
description: 瞭解如何登入、導覽及使用Document Security網頁。
seo-description: 瞭解如何登入、導覽及使用Document Security網頁。
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 使用Document Security網頁 {#using-the-document-security-webpages}

使用者和管理員可使用Document Security網頁來建立和管理原則、管理受原則保護的檔案，以及監控與受原則保護的檔案相關的事件。 管理員也使用網頁來建立原則集並指定原則集協調者、設定檔案安全性預設設定、管理受邀的使用者註冊和帳戶，以及監控和管理伺服器、原則、使用者和檔案相關事件。

>[!NOTE]
>
>您也可以透過Acrobat和其他用戶端應用程式，使用您的使用者登入帳戶登入檔案安全性。 (請參 [閱設定用戶端應用程式對檔案安全性的存取](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)。)

若要開啟網頁，您需要瀏覽器、URL和登入資訊，才能確保檔案安全。 使用者的URL與管理員的URL不同。

由於檔案安全性會參照貴組織現有的目錄以取得使用者資訊，因此您的檔案安全性登入資訊可能與您用來登入網路和其他應用程式的資訊相同。 如需您的帳戶資訊，請洽詢您的系統管理員或管理員。

要以管理員身份登錄，您需要為您分配管理員角色。 您可以使用安裝過程中建立的預設超級管理員帳戶。

## 登入網頁 {#log-in-to-the-web-pages}

若要使用瀏覽器登入網頁，您需要檔案安全性URL和帳戶。 使用者的URL與管理員的URL不同。 管理員也可以登入使用者頁面以建立原則。

如果您可存取多個檔案保全安裝，則需要要存取之檔案保全實例的URL。 如果您沒有此資訊，請洽詢您的管理員。 使用者頁面的預設URL為https://*[host]*:*[port]*/edc。 在某些情況下，可能不需要埠號。 請洽詢您的管理員以取得詳細資訊。

管理員的預設URL為https://*[host]*:*[port]*/adminui。

對於管理員，在安裝期間會建立預設的超級管理員帳戶。 當首次安裝Document Security時，您可以使用這個帳戶登入。

>[!NOTE]
>
>您也可以從Acrobat和其他用戶端應用程式存取網頁。 如需詳細資訊，請參閱Acrobat說明或適當的Acrobat Reader DC擴充功能說明。

1. 在瀏覽器中輸入URL:

   檔案安全性URL:主 `https://`*[機&#x200B;]*`:`*[埠]*`/edc`

   或管理控制台URL:主 `https://`*[機&#x200B;]*`:`*[埠]*`/adminui`

1. 在登入視窗中，輸入您的使用者名稱和密碼，然後按一下「確定」。
1. 在「管理控制台」中，按一下「服務>檔案安全性」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，例如上一頁按鈕、重新整理按鈕以及上一頁和下一頁和下一頁箭頭，因為此動作可能會造成不需要的資料擷取和資料顯示問題。

## 導覽網頁 {#navigating-the-web-pages}

當您登入使用者網頁時，您會看到「原則」、「檔案」和「事件」使用者頁面的連結。

當您登入管理控制台並導覽至檔案安全性首頁時，您可能會看到一或兩個其他連結，一個用於「設定」頁面，另一個用於「已邀請」和「本機使用者」頁面。 只有在啟用邀請的使用者註冊時，才會顯示「已邀請的使用者」和「本機使用者」頁面。

使用這些連結可存取各種頁面，您可在其中建立及管理原則和受原則保護的檔案。

**顯示頁面**

1. 按一下頁面名稱；例如，按一下策略。

**返回上一頁**

1. 按一下您要返回之頁面頁面頂端的導覽連結。

**重新整理頁面上的資料清單**

1. 在首頁面上，按一下您要重新整理之頁面的連結。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，例如上一頁按鈕、重新整理按鈕以及上一頁和下一頁和下一頁箭頭，因為此動作可能會造成不需要的資料擷取和資料顯示問題。

## 從用戶端應用程式設定對檔案安全性的存取 {#setting-up-access-to-document-security-from-client-applications}

用戶端應用程式必須設定為連接至檔案保全，以保護檔案、開啟受原則保護的檔案，以及連接至檔案保全網頁。 如需 *在用戶端應用程式中設定連線* 的詳細資訊，請參閱Acrobat說明或適當的 ** RightsManagementExtension說明。

檔案安全性可透過安全通訊端層(SSL)存取。 您必須將網站的憑證安裝在憑證存放區中，才能透過用戶端應用程式存取檔案安全性。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

這些說明是Internet explorer專用的，但您可以使用任何支援的網頁瀏覽器來安裝憑證。 如需詳細資訊，請參閱您瀏覽器的說明。

**使用Internet explorer安裝伺服器證書**

1. 開啟您的網頁瀏覽器，並在「位址」方塊中輸入檔案安全性的基本URL。 例如，鍵入 `https://[host]:[port]`。 出現「Security Alert（安全警報）」對話框。
1. 按一下「檢視憑證」，然後按一下「安裝憑證」，並選取預設值以進行安裝。 憑證必須安裝在受信任的根認證授權機構中。
1. 關閉瀏覽器作業。
1. 開啟另一個瀏覽器視窗，並在「位址」方塊中輸入相同的URL。 不應出現「安全警報」對話框。 此測試會確認憑證已正確安裝。

## 登出網頁 {#log-out-of-the-web-pages}

當您使用完網頁後登出，如此您就可安全地將網頁瀏覽器用於其他用途。 視檔案安全性的設定而定，您可能需要關閉瀏覽器才能完全登出。

1. 在頁面的右上角，按一下「登出」。
1. 如果「註銷」頁面上出現消息，請關閉瀏覽器窗口以完全註銷。 否則，您可以繼續將瀏覽器用於其他用途。

