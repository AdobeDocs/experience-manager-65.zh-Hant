---
title: 高容量安全資訊傳遞
seo-title: High-volume secure information delivery
description: 文檔安全性支援將許可證與用戶關聯，而不是與批量生產環境中的文檔關聯。
seo-description: Document security supports the association of licenses to users, rather than to the documents in mass production environments.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 高容量安全資訊傳遞 {#high-volume-secure-information-delivery}

在大規模生產環境中，例如為電信公司生成安全的每月發票的環境中，建立特定於每個文檔的許可證可以成為資源密集型流程。 在這種情況下，文檔安全性支援將許可證與用戶關聯，而不是與文檔關聯。 為用戶生成的許可證用於為該用戶保護的所有文檔。

此方法的一個優點是，文檔安全資料庫的大小不會隨著文檔而線性增長，而是隨著用戶的數量而增長。 另外，由於您只需為用戶建立一次許可證，因此通過這些策略對文檔的後續保護會更快。 所有此類文檔均支援離線訪問、文檔過期和撤銷等功能。

文檔安全性還支援抽象策略。 抽象策略是包含所有策略屬性（如文檔安全設定和使用權限）的策略模板，但不包含主體清單。 管理員可以從抽象策略中建立任意數量的策略，這些策略具有不同的承擔者，他們應該有權訪問文檔。 對抽象策略所做的更改不會影響從抽象策略生成的實際策略。

如果是電信公司的每月發票生成，您可以建立抽象策略、建立用戶，然後為每個用戶生成唯一的許可證。 這些許可證稍後將應用於每個用戶的文檔。

只有透過檔案安全性Java SDK才支援建立抽象原則。 但是，您可以管理從文檔安全網頁的抽象策略中建立的策略。 使用此方法建立的策略在行為上與從文檔安全網頁建立的策略相同。

請參閱 [使用AEM表單進行程式設計](https://www.adobe.com/go/learn_aemforms_programming_63) 以取得更多資訊。
