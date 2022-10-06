---
title: 使用文檔安全網頁
seo-title: Using the document security webpages
description: 了解如何登入、導覽及使用檔案安全性網頁。
seo-description: Learn how you can login, navigate and use the document security web pages.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 使用文檔安全網頁 {#using-the-document-security-webpages}

用戶和管理員使用文檔安全網頁來建立和管理策略、管理受策略保護的文檔，以及監視與受策略保護的文檔關聯的事件。 管理員還使用網頁建立策略集並指定策略集協調員、配置文檔安全預設設定、管理受邀用戶註冊和帳戶，以及監視和管理伺服器、策略、用戶和文檔相關事件。

>[!NOTE]
>
>您也可以使用使用者登入帳戶，透過Acrobat和其他用戶端應用程式登入檔案安全性。 (請參閱 [設定客戶端應用程式對文檔安全的訪問](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

要開啟網頁，您需要瀏覽器、URL和登錄資訊以確保文檔安全。 使用者的URL與管理員的URL不同。

由於文檔安全引用了貴組織現有目錄中的用戶資訊，因此您的文檔安全登錄資訊可能與您用來登錄網路和其他應用程式的資訊相同。 請咨詢您的系統管理員或管理員以了解您的帳戶資訊。

若要以管理員身分登入，您必須指派管理員角色給您。 您可以使用在安裝過程中建立的預設超級管理員帳戶。

## 登入網頁 {#log-in-to-the-web-pages}

若要使用瀏覽器登入網頁，您需要檔案安全性URL和帳戶。 使用者的URL與管理員的URL不同。 管理員也可以登入使用者頁面以建立原則。

如果您可以訪問多個文檔安全安裝，則需要要訪問的文檔安全實例的URL。 如果您沒有此資訊，請洽詢您的管理員。 使用者頁面的預設URL為 `https://[host]:[port]/edc`. 某些情況下可能不需要埠號。 請向管理員詢問詳細資訊。

管理員的預設URL為 `https://[host]:[port]/adminui`.

對於管理員，在安裝期間會建立預設的超級管理員帳戶。 首次安裝檔案安全性時，可使用此帳戶登入。

>[!NOTE]
>
>您也可以從Acrobat和其他用戶端應用程式存取網頁。 如需詳細資訊，請參閱Acrobat說明或適當的Acrobat Reader DC擴充功能說明。

1. 在瀏覽器中輸入URL:

   文檔安全URL: `https://[host]:[port]/edc`

   或管理控制台URL: `https://[host]:[port]/adminui`

1. 在登錄窗口中，鍵入您的用戶名和密碼，然後按一下確定。
1. 在管理控制台中，按一下「服務>檔案安全性」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，例如上一頁按鈕、重新整理按鈕以及上一頁和下一頁箭頭，因為此動作會造成不想要的資料擷取和資料顯示問題。

## 導覽網頁 {#navigating-the-web-pages}

當您登錄到用戶網頁時，您會看到指向「策略」、「文檔」和「事件」用戶頁的連結。

當您登錄到管理控制台並導航到文檔安全首頁時，您還可能會看到一或兩個附加連結，一個用於「配置」頁，一個用於「已邀請」頁和「本地用戶」頁。 只有在啟用邀請的用戶註冊時，才會顯示「已邀請」和「本地用戶」頁。

使用這些連結可以訪問各個頁面，在這些頁面中建立和管理策略和受策略保護的文檔。

**顯示頁面**

1. 按一下頁面名稱；例如按一下「策略」。

**返回上一頁**

1. 針對您要返回的頁面，按一下頁面頂端的導覽連結。

**重新整理頁面上的資料清單**

1. 在主要頁面上，按一下您要重新整理之頁面的連結。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，例如上一頁按鈕、重新整理按鈕以及上一頁和下一頁箭頭，因為此動作可能會造成不需要的資料擷取和資料顯示問題。

## 設定客戶端應用程式對文檔安全的訪問 {#setting-up-access-to-document-security-from-client-applications}

必須設定客戶端應用程式以連接到文檔安全性以保護文檔、開啟受策略保護的文檔，以及連接到文檔安全網頁。 請參閱 *Acrobat說明* 或適當 *RightsManagementExtension說明* ，了解有關在客戶端應用程式內配置連接的資訊。

檔案安全性可透過安全通訊端層(SSL)存取。 您必須在憑證存放區中安裝網站的憑證，以便透過用戶端應用程式存取檔案安全性。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

這些指示是Internet Explorer專屬的，但您可以使用任何支援的網頁瀏覽器來安裝憑證。 如需詳細資訊，請參閱瀏覽器的說明。

**使用Internet Explorer安裝伺服器憑證**

1. 開啟Web瀏覽器，並在「地址」框中鍵入文檔安全的基本URL。 例如，輸入 `https://[host]:[port]`. 出現「安全警報」對話框。
1. 按一下「查看證書」，然後按一下「安裝證書」並選擇預設值以進行安裝。 憑證必須安裝在受信任的根憑證授權單位中。
1. 關閉瀏覽器工作階段。
1. 開啟另一個瀏覽器視窗，並在「位址」方塊中輸入相同的URL。 不應出現「安全警報」對話框。 此測試會確認憑證已正確安裝。

## 登出網頁 {#log-out-of-the-web-pages}

使用完網頁後登出，以便安全地將網頁瀏覽器用於其他用途。 根據文檔安全配置方式，您可能需要關閉瀏覽器才能完全註銷。

1. 在頁面的右上角，按一下「登出」。
1. 如果「登出」頁面上出現訊息，請關閉瀏覽器視窗以完全登出。 否則，您可以繼續將瀏覽器用於其他用途。
