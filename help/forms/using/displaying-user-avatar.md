---
title: 顯示用戶虛擬形象
seo-title: Displaying the user avatar
description: 如何自定義AEM Forms工作區以顯示登錄用戶的影像。
seo-description: How to customize the AEM Forms workspace to display the image of a logged-in user.
uuid: 2961dc93-f0d0-4842-80f1-3c239a20e348
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: aec03ea5-17a6-4775-92cb-2ad361895fdf
exl-id: ee0708b0-b630-4a2b-84b6-3c0b92dd7777
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# 顯示用戶虛擬形象 {#displaying-the-user-avatar}

登錄用戶的虛擬形象顯示在AEM Forms工作區的右上角。 此外，組織層次結構中直接報告的化身也顯示在「經理視圖」中。 您可以配置AEM Forms工作區，從資料庫（如LDAP伺服器）中選擇用戶映像。

>[!NOTE]
>
>用戶影像的支援長寬比為1:1。

1. 使用下一步中提到的詳細資訊建立DSC。 有關詳細資訊，請參閱中的「開發AEM表單的元件」主題 [與AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63) 的子菜單。
1. 在DSC中，定義一個新的SPI，該SPI公開getCurrentUserImageUrl和getUserImageUrl方法，以獲取AEM Forms用戶的影像URL。 以下是示例Java™代碼段：

   ```java
   public class DemoUserImageURLProviderService {
     public String getCurrentUserImageUrl()
     {
        // return the URL for profile Image of logged in user
     }
     public String getUserImageUrl(String principalOid)
     {
         // return the URL for profile Image for user represented by this principal Oid
      }
   }
   ```

1. 建立component.xml檔案。 確保spec-id如下面的代碼段所示。

   以下代碼段是示例。 根據您的特定要求定制它。

   ```java
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.DemoUsersComponent</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
       <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
       <services>
           <service name="DemoUserImageURLProviderService" title="Demo User ImageURL provider service" orchestrateable="false">
           <auto-deploy service-id="DemoUserImageURLProviderService" category-id="Demo Users Component DSC" major-version="1" minor-version="0" />
           <description>Service for resolving user image url.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.UserImageUrlProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.demousers.DemoUserImageURLProviderService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="false" name="getCurrentUserImageUrl" method="getCurrentUserImageUrl">
                   <output-parameter name="result" type="java.lang.String"/>
               </operation>
               <operation anonymous-access="false" name="getUserImageUrl"
   method="getUserImageUrl">
               <input-parameter name="principalOid" type="java.lang.String"/>
               <output-parameter name="result" type="java.lang.String"/>
               </operation>
           </operations>
           </service>
       </services>
   </component>
   ```

1. 通過Workbench部署DSC。 重新啟動 `ProcessManagementClientSessionService` 服務。
1. 您可能必須刷新瀏覽器或再次與用戶註銷/登錄。
