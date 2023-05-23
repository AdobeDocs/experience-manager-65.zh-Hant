---
title: 使字型可用
seo-title: Make fonts available
description: 確保表單中使用的字型可在托管表單的J2EE應用程式伺服器上AEM使用。
seo-description: Ensure that the fonts used within a form are available for use on the J2EE application server hosting AEM forms.
uuid: 6588b4b6-f866-4253-91c8-3aa174340e8c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9f58a6c4-3190-49d4-800c-4a55dca7c296
exl-id: e9eae896-b1e4-4caa-b466-ac8c9e7416a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# 使字型可用 {#make-fonts-available}

確保表單中使用的字型可在托管表單的J2EE應用程式伺服器上AEM使用。 例如，請考慮以下方案。 表單設計器將字型添加到設計器使用的字型目錄，並在單獨的電腦上建立使用該字型的表單。 為了使輸出服務使用字型，請將其放在客戶字型目錄中。 如果Customer字型目錄不存在，請在托管表單的J2EE應用程式伺服器上創AEM建目錄。

有關其他字型設定的資訊，請參見 [配置常規AEM表單設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)。

**指定Customer字型目錄的位置**

1. 在管理控制台中，按一下「設定」>「核心繫統設定」>「配置」。
1. 在「System Fonts Directory（系統字型目錄）」框中，鍵入Customer字型目錄的路徑。 可以添加多個目錄，用分號分隔 **;**
1. 按一下「確定」。
1. 重新啟動安裝表AEM單的系統。

>[!NOTE]
>
>從Windows系統字型快取中選取字型，更新快取時需要系統重新啟動。 指定Customer字型目錄後，請確保重新啟動安裝了表單AEM的系統。
