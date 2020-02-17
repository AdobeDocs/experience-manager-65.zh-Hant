---
title: 使用管理員視圖管理組織層次結構中的任務
seo-title: 使用管理員視圖管理組織層次結構中的任務
description: 經理和組織主管如何在AEM Forms工作區的「待辦事項」標籤中存取及處理其直接和間接報表的工作。
seo-description: 經理和組織主管如何在AEM Forms工作區的「待辦事項」標籤中存取及處理其直接和間接報表的工作。
uuid: c44c55e6-6cc1-417d-8e89-c8d5c32914c8
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2e60df86-d8ff-4cf9-b801-9559857b5ff4
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# 使用管理員視圖管理組織層次結構中的任務{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

在AEM Forms工作區中，管理員現在可以存取指派給階層中任何人的工作（直接或間接報表），並對他們執行各種動作。 這些工作可在AEM Forms工作區的「待辦事項」標籤中使用。 直接報告任務上支援的操作包括：

**轉發** ：將任務從直接報告轉發給任何用戶。

**報銷申請** ：申請直接報告的任務。

**Claim &amp; Open** Claim a task of a direct report and automatically open it in the To-do list of the manager.

**拒絕** ：拒絕某些其他用戶轉發到直接報告的任務。 此選項可用於其他用戶轉發到直接報告的任務。

AEM Forms僅限使用者存取使用者擁有存取控制(ACL)的工作。 這樣的檢查可確保用戶只能獲取用戶具有訪問權限的任務。 使用協力廠商的web-services和實作來定義階層，組織可以自訂經理的定義並直接報告以符合其需求。

1. 建立DSC。 如需詳細資訊，請參閱「使用AEM Forms進行程式設計」指南中的「開 [發AEM Forms的元件](https://www.adobe.com/go/learn_aemforms_programming_63) 」主題。
1. 在DSC中，為階層管理定義新的SPI，以在AEM Forms使用者中定義直接報表和階層。 以下是範例Java™程式碼片段。

   ```as3
   public class MyHierarchyMgmtService
   {
        /*
       Input : Principal Oid for a livecycle user
       Output : Returns true when the user is either the service invoker OR his direct/indirect report.
       */
       boolean isInHierarchy(String principalOid) {
   
       }
   
       /*
       Input : Principal Oid for a livecycle user
       Output : List of principal Oids for direct reports of the livecycle user
       A user may get direct reports only for himself OR his direct/indirect reports.
       So the API is functionally equivalent to -
       isInHierarchy(principalOid) ? <return direct reports> : <return empty list>
       */
       List<String> getDirectReports(String principalOid) {
   
       }
   
       /*
       Returns whether a livecycle user has direct reports or not.
       It's functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. 建立component.xml檔案。 請確定規格ID必須與下列程式碼片段中所示相同。 以下是您可重複使用的范常式式碼片段。

   ```as3
   <component xmlns="https://adobe.com/idp/dsc/component/document">
       <component-id>com.adobe.sample.SampleDSC</component-id>
       <version>1.1</version>
       <supports-export>false</supports-export>
         <descriptor-class>com.adobe.idp.dsc.component.impl.DefaultPOJODescriptorImpl</descriptor-class>
         <services>
           <service name="MyHierarchyMgmtService" title="My hierarchy management service" orchestrateable="false">
           <auto-deploy service-id="MyHierarchyMgmtService" category-id="Sample DSC" major-version="1" minor-version="0" />
           <description>Service for resolving hierarchy management.</description>
            <specifications>
            <specification spec-id="com.adobe.idp.taskmanager.dsc.enterprise.HierarchyManagementProvider"/>
            </specifications>
           <specification-version>1.0</specification-version>
           <implementation-class>com.adobe.sample.hierarchymanagement.MyHierarchyMgmtService</implementation-class>
           <request-processing-strategy>single_instance</request-processing-strategy>
           <supported-connectors>default</supported-connectors>
           <operation-config>
               <operation-name>*</operation-name>
               <transaction-type>Container</transaction-type>
               <transaction-propagation>supports</transaction-propagation>
               <!--transaction-timeout>3000</transaction-timeout-->
           </operation-config>
           <operations>
               <operation anonymous-access="true" name="isInHierarchy" method="isInHierarchy">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               <operation anonymous-access="true" name="getDirectReports" method="getDirectReports">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.util.List"/>
               </operation>
               <operation anonymous-access="true" name="isManager" method="isManager">
                   <input-parameter name="principalOid" type="java.lang.String" />
                   <output-parameter name="result" type="java.lang.Boolean"/>
               </operation>
               </operations>
               </service>
         </services>
   </component>
   ```

1. 通過Workbench部署DSC。 重新啟動 `ProcessManagementTeamTasksService` 服務。
1. 您可能必須重新整理瀏覽器或再次向使用者登出／登入。

以下螢幕說明了如何訪問直接報告的任務和可用的操作。

![cu_manager_view](assets/cu_manager_view.png)

存取直接報表的工作並處理工作

[聯絡支援](https://www.adobe.com/account/sign-in.supportportal.html)
