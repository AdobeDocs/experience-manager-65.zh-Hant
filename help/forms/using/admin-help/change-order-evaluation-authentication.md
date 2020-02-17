---
title: 更改驗證評估順序
seo-title: 更改驗證評估順序
description: 您可以變更AEM表單評估多個驗證提供者的順序。
seo-description: 您可以變更AEM表單評估多個驗證提供者的順序。
uuid: c2693e5b-cf09-4bb8-815a-2b20ebf6eea0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5434df9c-ecf6-450a-aa7e-d9ab69b66fe6
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 更改驗證評估順序 {#change-the-order-of-evaluation-for-authentication}

如果您設定了多個驗證提供者，您可以變更AEM表單評估驗證的順序。 config.xml檔案中列出的驗證提供者順序會決定驗證評估順序。

1. 在管理控制台中，按一下「設定>使用者管理>設定>匯入和匯出設定檔」。
1. 要將當前配置設定導出到檔案，請按一下「導出」(Export)，然後將配置檔案保存到其他位置。
1. 在檔案中查找以下節點：

   ```as3
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   在 `<entry key="order" value="3" />`中，編輯每個節點的值以設定驗證評估的順序。

1. 若要匯入更新檔案，請在「使用者管理」中按一下「設定>匯入和匯出設定檔」。
1. 按一下「瀏覽」以尋找檔案，按一下「匯入」，然後按一下「確定」。

