---
title: 大量安全資訊傳遞
seo-title: 大量安全資訊傳遞
description: 檔案安全性支援將授權與使用者關聯，而非與大量生產環境中的檔案關聯。
seo-description: 檔案安全性支援將授權與使用者關聯，而非與大量生產環境中的檔案關聯。
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 大量安全資訊傳遞 {#high-volume-secure-information-delivery}

在大量生產環境（例如為電信公司生成安全的月發票）中，建立特定於每個文檔的許可證可以成為資源密集型過程。 在這種情況下，檔案安全性支援將授權與使用者關聯，而非與檔案關聯。 為使用者產生的授權會用於為該使用者提供保護的所有檔案。

此方法的一個優點是，檔案安全性資料庫的大小不會隨著檔案而線性增加，而會隨著使用者人數而增加。 此外，由於您只需為使用者建立授權一次，因此透過這些原則對檔案的後續保護變得更快。 所有此類檔案都支援離線存取、檔案過期和撤銷等功能。

檔案安全性也支援抽象原則。 抽象策略是包含所有策略屬性（如文檔安全設定和使用權限）的策略模板，但不包含承擔者清單。 管理員可以使用不同的承擔者從抽象原則建立任意數量的原則，這些承擔者應該有權存取檔案。 對抽象策略所做的更改不會影響從抽象策略生成的實際策略。

如果是電信公司的月繳型發票，您可以建立抽象原則、建立使用者，然後為每個使用者產生唯一的授權。 這些授權稍後會套用至每位使用者的檔案。

只有檔案安全性Java SDK才支援建立抽象原則。 但是，您可以管理從Document Security網頁的抽象原則建立的原則。 使用此方法建立的原則在行為上與從Document Security網頁建立的原則相同。

如需詳 [細資訊，請參閱「使用AEM表格進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63) 」。
