---
title: 使用文檔安全網頁
seo-title: Using the document security webpages
description: 瞭解如何登錄、導航和使用文檔安全網頁。
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

用戶和管理員使用文檔安全網頁建立和管理策略、管理受策略保護的文檔，以及監視與受策略保護的文檔關聯的事件。 管理員還使用網頁建立策略集並指定策略集協調員、配置文檔安全預設設定、管理邀請的用戶註冊和帳戶，以及監控和管理伺服器、策略、用戶和文檔相關事件。

>[!NOTE]
>
>您還可以使用用戶登錄帳戶通過Acrobat和其他客戶端應用程式登錄以記錄安全性。 (請參閱 [設定從客戶端應用程式對文檔安全性的訪問](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)。)

要開啟網頁，您需要瀏覽器、URL和登錄資訊來確保文檔安全。 用戶的URL與管理員的URL不同。

由於文檔安全性引用您組織的現有目錄獲取用戶資訊，因此文檔安全登錄資訊可能與您用於登錄到網路和其他應用程式的資訊相同。 有關帳戶資訊，請咨詢系統管理員或管理員。

要以管理員身份登錄，需要為您分配管理員角色。 可以使用在安裝過程中建立的預設超級管理員帳戶。

## 登錄到網頁 {#log-in-to-the-web-pages}

要使用瀏覽器登錄到網頁，需要文檔安全URL和帳戶。 用戶的URL與管理員的URL不同。 管理員還可以登錄用戶頁以建立策略。

如果您有權訪問多個文檔安全性安裝，則需要要訪問的文檔安全性實例的URL。 如果您沒有此資訊，請與管理員聯繫。 用戶頁的預設URL是 `https://[host]:[port]/edc`。 在某些情況下可能不需要埠號。 請向管理員咨詢詳細資訊。

管理員的預設URL為 `https://[host]:[port]/adminui`。

對於管理員，在安裝期間建立預設超級管理員帳戶。 首次安裝文檔安全性時，可使用此帳戶登錄。

>[!NOTE]
>
>您還可以從Acrobat和其他客戶端應用程式訪問網頁。 有關詳細資訊，請參閱Acrobat幫助或相應的Acrobat Reader DC擴展幫助。

1. 在瀏覽器中鍵入URL:

   文檔安全URL: `https://[host]:[port]/edc`

   或管理控制台URL: `https://[host]:[port]/adminui`

1. 在登錄窗口中，鍵入用戶名和密碼，然後按一下「確定」。
1. 在Administration Console中，按一下「服務」>「文檔安全性」。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，如「後退」按鈕、「刷新」按鈕以及「後退」和「前進」箭頭，因為此操作可能導致不需要的資料捕獲和資料顯示問題。

## 導航網頁 {#navigating-the-web-pages}

登錄到用戶網頁時，將看到指向「策略」、「文檔」和「事件」用戶頁的連結。

當您登錄到管理控制台並導航到文檔安全首頁時，您還可能會看到一兩個附加連結，一個用於「配置」頁，另一個用於「已邀請」和「本地用戶」頁。 僅當啟用邀請的用戶註冊時，才會顯示「邀請的用戶」和「本地用戶」頁。

使用這些連結可訪問各個頁面，在這些頁面中可以建立和管理策略和受策略保護的文檔。

**顯示頁面**

1. 按一下頁面名稱；如按一下「策略」。

**返回上一頁**

1. 按一下頁面頂部要返回的頁面的導航連結。

**刷新頁面上的資料清單**

1. 在首頁上，按一下要刷新的頁面的連結。

>[!NOTE]
>
>使用網頁時，請避免使用瀏覽器按鈕，如後退按鈕、刷新按鈕以及後向和前向箭頭，因為此操作可能會導致不需要的資料捕獲和資料顯示問題。

## 設定從客戶端應用程式對文檔安全性的訪問 {#setting-up-access-to-document-security-from-client-applications}

必須設定客戶端應用程式以連接到文檔安全性以保護文檔、開啟受策略保護的文檔以及連接到文檔安全性網頁。 請參閱 *Acrobat幫助* 或適當 *RightsManagementExtension幫助* 有關在客戶端應用程式內配置連接的資訊。

通過安全套接字層(SSL)訪問文檔安全性。 您必須在證書儲存中安裝網站的證書，以便您可以通過客戶端應用程式訪問文檔安全性。

<!-- Fix broken link See Configuring SSL for information on SSL.-->

這些說明特定於Internet Explorer，但您可以使用任何受支援的Web瀏覽器安裝證書。 有關詳細資訊，請參閱瀏覽器的幫助。

**使用Internet Explorer安裝伺服器證書**

1. 開啟Web瀏覽器，在「地址」框中鍵入文檔安全性的基URL。 例如，鍵入 `https://[host]:[port]`。 出現「Security Alert（安全警報）」對話框。
1. 按一下查看證書，然後按一下安裝證書並選擇預設安裝。 證書需要安裝在受信任的根證書頒發機構中。
1. 關閉瀏覽器會話。
1. 開啟另一個瀏覽器窗口，並在「地址」框中鍵入相同的URL。 不應出現「安全警報」對話框。 此test確認證書已正確安裝。

## 註銷網頁 {#log-out-of-the-web-pages}

使用完網頁後註銷，以便您可以安全地將Web瀏覽器用於其他目的。 根據文檔安全性的配置方式，您可能需要關閉瀏覽器以完全註銷。

1. 在頁面右上角，按一下註銷。
1. 如果「註銷」頁上出現消息，請關閉瀏覽器窗口以完全註銷。 否則，您可以繼續將瀏覽器用於其他目的。
