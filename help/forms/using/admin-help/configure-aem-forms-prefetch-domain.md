---
title: 配置AEM表單以預取域資訊
seo-title: Configure AEM forms to prefetchdomain information
description: 配置AEM表單以預回遷域資訊（如果由於嵌套較深的組而響應時間較慢），或者您是許多組的成員。
seo-description: Configure AEM forms to prefetch domain information if you experience a slower response time due to deeply nested groups or if you are a member of many groups.
uuid: 53c8995e-3f9d-42e8-9f75-cee7debe6ce1
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f9a3f897-90c6-4942-8a86-aae510298f2a
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 配置AEM表單以預取域資訊 {#configure-aem-forms-to-prefetchdomain-information}

如果用戶屬於多個組（例如，500或更多組），或者這些組深度嵌套（例如，30個級別），則可能會經歷較慢的響應時間。 如果遇到此問題，可以配置表AEM單從某些域預取資訊。

1. 在管理控制台中，按一下 **[!UICONTROL 設定>用戶管理>配置>導入和導出配置檔案]**。
1. 要將當前配置設定導出到檔案，請按一下 **[!UICONTROL 導出]** 並將配置檔案保存到其他位置。
1. 添加以下節點（以粗體標籤）:

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

   在本示例中，為預取配置了多個域。 域名用「/」分隔。 上面的示例中顯示了 *域名1*。 *域名2*, *域名3*。

1. 要導入更新的檔案，請在用戶管理中按一下 **[!UICONTROL 配置>導入和導出配置檔案]**。
1. 按一下 **[!UICONTROL 瀏覽]** 要查找檔案，請按一下「導入」，然後按一下 **[!UICONTROL 確定]**。
