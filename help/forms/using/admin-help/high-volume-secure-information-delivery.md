---
title: 大容量安全資訊傳遞
seo-title: High-volume secure information delivery
description: 文檔安全性支援許可證與用戶的關聯，而不是與大規模生產環境中的文檔的關聯。
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

# 大容量安全資訊傳遞 {#high-volume-secure-information-delivery}

在大規模生產環境中，建立特定於每個文檔的許可證可以成為資源密集型流程。 在這種情況下，文檔安全性支援將許可證與用戶而不是文檔相關聯。 為用戶生成的許可證用於為該用戶保護的所有文檔。

這種方法的一個優點是，文檔安全資料庫的大小不會隨文檔而線性增長，而會隨用戶數量而增長。 此外，由於您只需為用戶建立一次許可證，因此通過這些策略對文檔的後續保護會更快。 所有此類文檔都支援離線訪問、文檔過期和吊銷等功能。

文檔安全性還支援抽象策略。 抽象策略是包含所有策略屬性（如文檔安全設定和使用權限）但不包含承擔者清單的策略模板。 管理員可以從抽象策略中建立任意數量的策略，這些策略具有不同的承擔者，這些承擔者應有權訪問文檔。 對抽象策略所做的更改不會影響從抽象策略生成的實際策略。

在為電信公司每月生成發票的情況下，您可以建立抽象策略，建立用戶，然後為每個用戶生成唯一的許可證。 這些許可證稍後將應用於每個用戶的文檔。

只有通過文檔安全性Java SDK才支援建立抽象策略。 但是，您可以從文檔安全網頁管理從抽象策略建立的策略。 使用此方法建立的策略與從文檔安全網頁建立的策略的行為相同。

請參閱 [用表格編AEM程](https://www.adobe.com/go/learn_aemforms_programming_63) 的子菜單。
