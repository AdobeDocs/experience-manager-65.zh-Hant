---
title: 讓字型可供使用
seo-title: 讓字型可供使用
description: 請確定表單中使用的字型可用於代管AEM表單的J2EE應用程式伺服器。
seo-description: 請確定表單中使用的字型可用於代管AEM表單的J2EE應用程式伺服器。
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 讓字型可供使用 {#make-fonts-available}

請確定表單中使用的字型可用於代管AEM表單的J2EE應用程式伺服器。 例如，請考慮以下情形。 表單設計人員會將字型新增至Designer使用的字型目錄，並在個別電腦上建立使用該字型的表單。 為了讓「輸出」服務使用字型，請將它放置在「客戶」字型目錄中。 如果Customer字型目錄不存在，請在代管AEM表單的J2EE應用程式伺服器上建立目錄。

如需其他字型設定的詳細資訊，請參閱「 [設定一般AEM表格設定」](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定客戶字型目錄的位置**

1. 在管理控制台中，按一下「設定>核心繫統設定>組態」。
1. 在「系統字型目錄的位置」方塊中，輸入客戶字型目錄的路徑。 可以添加多個目錄，並以分號分隔 **;**
1. 按一下「確定」。
1. 重新啟動安裝AEM表單的系統。

>[!NOTE]
>
>從Windows系統字型快取中挑選字型，而更新快取時需要重新啟動系統。 指定Customer字型目錄後，請確定您重新啟動安裝AEM表單的系統。

