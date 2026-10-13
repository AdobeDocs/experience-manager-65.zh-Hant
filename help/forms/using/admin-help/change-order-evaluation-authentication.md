---
title: 變更驗證的評估順序
description: 您可以變更AEM表單評估多個驗證提供者的順序。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
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
source-wordcount: '159'
ht-degree: 0%
---
# 變更驗證的評估順序 {#change-the-order-of-evaluation-for-authentication}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

如果您已設定多個驗證服務提供者，您可以變更AEM表單評估其驗證順序。 在config.xml檔案中列出的驗證提供者順序，決定了驗證的評估順序。

1. 在管理控制檯中，按一下「設定」>「使用者管理」>「組態」>「匯入和匯出組態檔」。
1. 若要將目前的組態設定匯出至檔案，請按一下「匯出」並將組態檔案儲存在其他位置。
1. 在檔案中找到下列節點：

   ```xml
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

   在`<entry key="order" value="3" />`中，編輯每個節點的值，以設定驗證評估的順序。

1. 若要匯入更新的檔案，請在「使用者管理」中按一下「組態」>「匯入及匯出組態檔」。
1. 按一下「瀏覽」尋找檔案，按一下「匯入」，然後按一下「確定」。
