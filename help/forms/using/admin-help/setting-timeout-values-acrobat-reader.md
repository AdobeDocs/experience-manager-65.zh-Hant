---
title: 設定超時值以用於Acrobat Reader DC擴展
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: 瞭解如何設定超時值以用於Acrobat Reader DC擴展。
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# 設定超時值以用於Acrobat Reader DC擴展  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

在處理Acrobat Reader DC擴展中的許多PDF檔案時，請確保正確設定以下超時值以防止作業超時和失敗：

**文檔處理超時**

可以在管理控制台中設定此值。 按一下「設定」>「核心繫統設定」>「配置」，然後為「預設文檔處理超時」指定值。

**用戶管理AEM器表單超時：** 可以通過編輯config.xml檔案來設定此值。 在管理控制台中，按一下「設定」>「用戶管理」>「配置」>「導入和導出配置檔案」，然後按一下「導出」。 開啟導出的config.xml檔案並編輯以下行：

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

保存並將config.xml檔案導入到管理控制台。

**應用程式伺服器會話超時：** 可以在應用程式伺服器上設定此值。 有關詳細資訊，請參閱應用程式伺服器附帶的文檔。
