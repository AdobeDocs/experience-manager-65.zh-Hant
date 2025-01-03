---
title: 設定AEM表單以預先擷取網域資訊
description: 如果您因為深度巢狀化群組或是許多群組的成員，而導致回應時間變慢，請設定AEM表單以預先擷取網域資訊。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cf5283a5-dbfb-460d-a8bd-11cd15ab8640
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# 設定AEM表單以預先擷取網域資訊 {#configure-aem-forms-to-prefetchdomain-information}

>[!NOTE]
> 
> 確保使用者具有存取管理員控制檯的管理員許可權。

如果使用者屬於許多群組（例如500個或更多）或群組巢狀結構較深（例如30個層級），回應時間可能會變慢。 如果您遇到此問題，可以設定AEM表單以從特定網域預先擷取資訊。

1. 在管理控制檯中，按一下&#x200B;**[!UICONTROL 設定>使用者管理>設定>匯入及匯出設定檔]**。
1. 若要將目前的組態設定匯出至檔案，請按一下[匯出] ****，並將組態檔案儲存在其他位置。
1. 新增下列節點（以粗體標籤）：

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

   在此範例中，有多個網域設定為預先擷取。 網域名稱以「/」分隔。 以上範例顯示&#x200B;*Domain_Name1*、*Domain_Name2*&#x200B;和&#x200B;*Domain_Name3*。

1. 若要匯入更新的檔案，請在[使用者管理]中按一下[組態] > [匯入及匯出組態檔] ]**。**[!UICONTROL 
1. 按一下&#x200B;**[!UICONTROL 瀏覽]**&#x200B;尋找檔案，按一下[匯入]，然後按一下&#x200B;**[!UICONTROL 確定]**。
