---
title: 將字體設為可用
description: 確定表單內使用的字型可用於託管AEM表單的J2EE應用程式伺服器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%
---
# 將字體設為可用 {#make-fonts-available}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

確定表單內使用的字型可用於託管AEM表單的J2EE應用程式伺服器。 例如，請考量下列情況。 表單設計人員將字型新增到Designer使用的字型目錄中，並建立在不同電腦上使用該字型的表單。 為了讓Output服務使用字型，請將其放置在Customer fonts目錄中。 如果Customer fonts目錄不存在，請在裝載AEM表單的J2EE應用程式伺服器上建立目錄。

如需其他字型設定的詳細資訊，請參閱[設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定Customer字型目錄的位置**

1. 在管理控制檯中，按一下設定>核心系統設定>設定。
1. 在「系統字型目錄的位置」方塊中，輸入Customer字型目錄的路徑。 可以新增多個目錄，以分號&#x200B;**；**&#x200B;分隔
1. 按一下「確定」。
1. 重新啟動已安裝AEM表單的系統。

>[!NOTE]
>
>字型是從Windows系統字型快取中挑選的，需要重新啟動系統才能更新快取。 指定Customer字型目錄後，請務必重新啟動安裝AEM表單的系統。
