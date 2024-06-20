---
title: 使用管理員檢視管理組織階層中的任務
description: 經理和組織主管如何在AEM Forms工作區的待辦事項索引標籤中存取和處理其直接和間接報告的任務。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: e50974a7-01ac-4a08-bea2-df9cc975c69e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 使用管理員檢視管理組織階層中的任務{#managing-tasks-in-an-organizational-hierarchy-using-manager-view}

在AEM Forms工作區中，管理員現在可以存取其階層中指派給任何人的任務（直接或間接報告），並對其執行各種動作。 這些任務可在AEM Forms工作區的「待辦事項」索引標籤中使用。 直接下屬工作支援的動作如下：

**前進**  — 將任務從直接下屬轉送給任何使用者。

**索賠**  — 宣告直接下屬的任務。

**索賠與未結**  — 宣告直接下屬的工作，並在經理的待辦事項清單中自動開啟。

**拒絕**  — 拒絕由其他使用者轉送至直接報告的任務。 此選項適用於其他使用者轉送給直接下屬的工作。

AEM Forms限制使用者的存取許可權僅限於使用者擁有存取控制(ACL)的任務。 這類檢查可確保使用者只能擷取其擁有存取許可權的任務。 使用協力廠商Web服務和實作來定義階層，組織可以自訂管理員和直接報表的定義，以符合其需求。

1. 建立DSC。 如需詳細資訊，請參閱以下主題中的「為AEM Forms開發元件」： [使用AEM Forms程式設計](https://www.adobe.com/go/learn_aemforms_programming_63) 指南。
1. 在DSC中，為階層管理定義新的SPI，以在AEM Forms使用者中定義直接報告和階層。 以下是範例Java™程式碼片段。

   ```java
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
       It is functionally equivalent to -
       getDirectReports(principalOid).size()>0
       */
       boolean isManager(String principalOid) {
   
       }
   }
   ```

1. 建立component.xml檔案。 請確定spec-id如下面的程式碼片段中所示相同。 以下是程式碼片段的範例，您可以重新調整用途。

   ```xml
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

1. 透過Workbench部署DSC。 重新啟動 `ProcessManagementTeamTasksService` 服務。
1. 您可能需要重新整理瀏覽器，或再次登出/登入使用者。

以下畫面說明如何存取直接下屬的工作和可用的動作。

![cu_manager_view](assets/cu_manager_view.png)

存取直接下屬的任務並據以進行操作
