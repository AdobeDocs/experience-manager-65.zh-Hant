---
title: 註冊為使用者
description: 瞭解如何使用您從Document Security使用者那裡收到的受原則保護檔案，即使您是該使用者組織的外部人員。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
feature: Document Security
exl-id: 320d8fa4-e200-4993-b018-a9718cddc5c1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 3%

---

# 註冊為使用者 {#registering-as-a-user}

您可以使用從Document Security使用者那裡收到的受原則保護的檔案，即使您是該使用者組織的外部人員。 若要使用受原則保護的檔案，您必須向Document Security註冊。 如果您之前未受邀註冊，document security會在下列事件發生時啟動註冊程式：

* 想要向您傳送受原則保護檔案的Document Security使用者會將您新增至原則中。
* Document Security管理員會為您建立帳戶。

  在您註冊並啟用帳戶後，您可以使用您有權透過原則使用的受原則保護檔案。 如果Document Security管理員為受邀使用者啟用這些功能，則您可能有權執行這些任務：

* 使用Document Security原則的Protect檔案。
* 建立您自己的使用者原則，可套用至您的檔案。
* 邀請其他外部使用者將受原則保護的檔案新增至原則，以使用這些受原則保護的檔案。

  此外，當您註冊時，您不需要再次註冊即可使用其他受原則保護的檔案。 您的帳戶會維持使用中，直到原則管理員停用或刪除它為止。

>[!NOTE]
>
>如果您收到受原則保護的檔案，但沒有收到註冊電子郵件邀請，請聯絡向您傳送檔案的人以獲取更多資訊。

## 註冊為受邀使用者 {#register-as-an-invited-user}

如果您是受邀使用者，並且收到來自Document Security的電子郵件註冊訊息，則可以使用訊息中的URL進行註冊，以開啟線上註冊頁面。 註冊後，您將收到關於啟用帳戶的第二次通知。

1. 開啟Document Security註冊電子郵件。 該訊息包含的URL是Document Security中「外部使用者註冊」頁面的連結。
1. 按一下URL或將其複製並貼到瀏覽器中。 將會顯示「外部使用者註冊」頁面。
1. 在適當的方塊中輸入您的姓名、電話號碼、地址、組織和密碼，然後在「確認密碼」方塊中重新輸入您的密碼。 您的密碼可以是八個字元的任意組合。
1. 按一下「儲存」。 系統會顯示感謝訊息，通知您檢視電子郵件中的啟用電子郵件訊息。 現在啟用您的帳戶以完成註冊程式。

## 啟用您的受邀使用者帳戶 {#activate-your-invited-user-account}

註冊後，Document Security會傳送一封啟用電子郵件給您。 使用郵件中的URL啟用您的帳戶。 然後，您可以登入Document Security，以使用您有權存取的受原則保護檔案。 根據管理員為外部使用者啟用的功能，您可能擁有建立原則、將原則套用至檔案以及將其他外部使用者新增至您原則的許可權。

在管理員停用或刪除您的帳戶之前，該帳戶會一直保持活動狀態。

1. 開啟Document Security註冊確認電子郵件。
1. 按一下訊息中顯示的URL。 此時會顯示Document Security啟用頁面。
1. 按一下這裡以移至登入頁面。
1. 在「使用者名稱」方框中，輸入您在Document Security下已註冊的電子郵件地址。 此電子郵件地址是您預設的Document Security使用者名稱。
1. 在「密碼」方塊中，輸入您註冊時建立的密碼，然後按一下「登入」。

## 重設密碼 {#reset-your-password}

如果您忘記密碼，原則管理員可以為您重設密碼。 重設密碼會產生一封電子郵件，邀請您使用臨時密碼登入。 然後，您可以建立另一個密碼。

如需聯絡Document Security管理員以取得新密碼的詳細資訊，請查閱邀請您註冊的組織的啟用電子郵件通知或其他通知。

1. 通知原則管理員您需要新密碼。
1. 當您收到Document Security密碼電子郵件時，請開啟該電子郵件並取得新的臨時密碼。
1. 使用新的臨時密碼登入Document Security。
1. 按一下頁面右上角的「選項」 。 將會顯示「外部使用者」頁面。
1. 選取「變更密碼」，然後在「舊密碼」方塊中輸入臨時密碼。
1. 在「新密碼」方塊中，輸入新密碼，然後在「確認密碼」方塊中重新輸入密碼。
