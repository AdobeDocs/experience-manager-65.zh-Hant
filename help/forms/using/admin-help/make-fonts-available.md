---
title: 讓字型可供使用
description: 請確定表單內使用的字型可用於裝載AEM表單的J2EE應用程式伺服器。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 讓字型可供使用 {#make-fonts-available}

請確定表單內使用的字型可用於裝載AEM表單的J2EE應用程式伺服器。 例如，請考量下列情況。 表單設計人員將字型新增到Designer使用的字型目錄中，並建立在不同電腦上使用該字型的表單。 為了讓Output服務使用字型，請將其放置在Customer fonts目錄中。 如果Customer fonts目錄不存在，請在主控AEM表單的J2EE應用程式伺服器上建立目錄。

如需其他字型設定的詳細資訊，請參閱 [設定一般AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings).

**指定客戶字型目錄的位置**

1. 在管理控制檯中，按一下設定>核心系統設定>設定。
1. 在「系統字型目錄的位置」方塊中，輸入Customer字型目錄的路徑。 可以新增多個目錄，以分號分隔 **；**
1. 按一下「確定」。
1. 重新啟動已安裝AEM表單的系統。

>[!NOTE]
>
>字型是從Windows系統字型快取中挑選的，需要重新啟動系統才能更新快取。 指定Customer字型目錄後，請確定重新啟動安裝AEM表單的系統。
