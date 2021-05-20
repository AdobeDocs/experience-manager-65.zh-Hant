---
title: 設定AEM表單以預先擷取網域資訊
seo-title: 設定AEM表單以預先擷取網域資訊
description: 如果您因深度巢狀群組或您是許多群組的成員而遇到回應時間較慢，請設定AEM表單以預先擷取網域資訊。
seo-description: 如果您因深度巢狀群組或您是許多群組的成員而遇到回應時間較慢，請設定AEM表單以預先擷取網域資訊。
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# 配置AEM表單以預取域資訊{#configure-aem-forms-to-prefetchdomain-information}

如果使用者屬於許多群組（例如500或更多），或者群組深度巢狀化（例如30個層級），則可能會遇到較慢的回應時間。 如果您遇到此問題，可以設定AEM表單以從特定網域預先擷取資訊。

1. 在管理控制台中，按一下「**[!UICONTROL 設定>使用者管理>設定>匯入和匯出設定檔]**」。
1. 要將當前配置設定導出到檔案，請按一下&#x200B;**[!UICONTROL Export]**&#x200B;並將配置檔案保存到其他位置。
1. 新增下列節點（以粗體標示）:

   ```xml
    <node name="UM">
    <map/>
    <node name="PrincipalCache">
        <map>
            <entry key="principalCacheSize" value="1000"/>
            <entry key="principalCacheBatchFetchSize" value="10"/>
            <entry key="rebuildCacheAfterSync" value="true />
            <entry key="enableFullPrefetch" value="false"/>
            <entry key="principalCacheDomains" value="Domain_Name1/Domain_Name2/Domain_Name3"/>
        <map>
    </node>
    <node name="APSAuditService">
   ```

   在此範例中，會設定多個網域以進行預先擷取。 網域名稱以「/」分隔。 以上範例中以&#x200B;*Domain_Name1*、*Domain_Name2*&#x200B;和&#x200B;*Domain_Name3*&#x200B;顯示。

1. 若要匯入更新的檔案，請在「使用者管理」中按一下「**[!UICONTROL 設定>匯入和匯出設定檔」]**。
1. 按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;以查找檔案，按一下導入，然後按一下&#x200B;**[!UICONTROL 確定]**。
