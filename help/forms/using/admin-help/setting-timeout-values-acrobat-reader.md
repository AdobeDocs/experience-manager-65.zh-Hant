---
title: 設定與Acrobat Reader DC擴充功能搭配使用的逾時值
seo-title: 設定與Acrobat Reader DC擴充功能搭配使用的逾時值
description: 瞭解如何設定與Acrobat Reader DC擴充功能搭配使用的逾時值。
seo-description: 瞭解如何設定與Acrobat Reader DC擴充功能搭配使用的逾時值。
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 設定與Acrobat Reader DC擴充功能搭配使用的逾時值 {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

在Acrobat Reader DC擴充功能中處理許多PDF檔案時，請確定下列逾時值已適當設定，以防止工作逾時或失敗：

**檔案處理超時**

此值可在管理控制台中設定。 按一下「設定>核心繫統設定>組態」，並指定「預設檔案處理逾時」的值。

**** User Manager AEM Forms逾時：此值可以通過編輯config.xml檔案來設定。 在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔案」，然後按一下「匯出」。 開啟匯出的config.xml檔案並編輯下列行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

儲存並將config.xml檔案匯入管理主控台。

**** 應用程式伺服器會話超時：此值可在應用程式伺服器上設定。 如需詳細資訊，請參閱應用程式伺服器隨附的檔案。
