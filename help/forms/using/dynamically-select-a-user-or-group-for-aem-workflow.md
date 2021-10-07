---
title: 動態選取以AEM Forms為中心的工作流程步驟的使用者或群組
seo-title: Dynamically select a user or group for AEM Forms-centric workflow steps
description: '了解如何在執行階段為AEM Forms工作流程選取使用者或群組。 '
seo-description: Learn how to select a user or group for an AEM Forms workflow at the runtime.
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
exl-id: 3c48660e-5e4f-4615-82d4-9f1f285c2a39
source-git-commit: 8f0e8b15d2ed8b436594fd2be464b4ace29a8902
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# 動態選取以AEM Forms為中心的工作流程步驟的使用者或群組 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

了解如何在執行階段為AEM Forms工作流程選取使用者或群組。

在大型組織中，需要動態選取流程的使用者。 例如，根據座席與客戶的接近程度選擇要為客戶服務的現場座席。 在這種情況下，動態選擇代理。

在OSGi](/help/forms/using/aem-forms-workflow.md)上指派[以Forms為中心的工作流程的任務和Adobe Sign步驟，提供可動態選取使用者的選項。 您可以使用ECMAScript或OSGi套件組合，以動態方式為「指派任務」步驟選擇受託人，或為「簽署檔案」步驟選擇簽署人。

## 使用ECMAScript動態選擇用戶或組 {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript是一種指令碼語言。 用於用戶端指令碼和伺服器應用程式。 執行下列步驟以使用ECMAScript動態選取使用者或群組：

1. 開啟CRXDE Lite。 URL為`https://'[server]:[port]'/crx/de/index.jsp`
1. 在下列路徑建立副檔名為.ecma的檔案。 如果路徑（節點結構）不存在，請建立它：

   * （分配任務步驟的路徑）`/apps/fd/dashboard/scripts/participantChooser`
   * （簽名步驟的路徑）`/apps/fd/workflow/scripts/adobesign`

1. 將具有動態選取使用者邏輯的ECMAScript新增至.ecma檔案。 按一下「**[!UICONTROL 全部保存]**」。

   有關示例指令碼，請參閱[動態選擇用戶或組](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group)的示例ECMAScript。

1. 新增指令碼的顯示名稱。 此名稱會顯示在工作流程步驟中。 要指定名稱：

   1. 展開指令碼節點，按一下右鍵&#x200B;**[!UICONTROL jcr:content]**&#x200B;節點，然後按一下&#x200B;**[!UICONTROL Mixins]**。
   1. 在「編輯Mixins」對話方塊中新增`mix:title`屬性，然後按一下「**確定**」。
   1. 將下列屬性新增至指令碼的jcr:content節點：

      | 名稱 | 類型 | 值 |
      |--- |--- |--- |
      | jcr:title | 字串 | 指定指令碼的名稱。 例如，選擇最接近的欄位代理。 此名稱顯示在「分配任務」和「簽署文檔」步驟中。 |

   1. 按一下「**全部保存**」。 指令碼可供AEM Workflow的元件中選取。

      ![指令碼](assets/script.png)

### 動態選擇用戶或組的ECMAScript示例 {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

以下示例ECMAScript動態選擇「分配任務」步驟的受託人。 在此指令碼中，會根據裝載的路徑選取使用者。 使用此指令碼之前，請確定指令碼中提及的所有使用者都存在於AEM中。 如果指令碼中提及的使用者不存在於AEM中，則相關程式可能會失敗。

```javascript
function getParticipant() {

var workflowData = graniteWorkItem.getWorkflowData();

if (workflowData.getPayloadType() == "JCR_PATH") { 

var path = workflowData.getPayload().toString(); 
     if (path.indexOf("/content/geometrixx/en") == 0) {
    return "user1";
    } 
   else {
              return "user2";
            }
}
}
```

以下範例ECMAScript會動態選取Adobe Sign步驟的受託人。 使用以下指令碼之前，請確保指令碼中提及的用戶資訊（電子郵件地址和電話號碼）正確。 如果指令碼中提及的使用者資訊不正確，則相關程式可能會失敗。

>[!NOTE]
>
>使用ECMAScript for Adobe Sign時，指令碼必須位於crx-repository（位於/apps/fd/workflow/scripts/adobesign/），且應具有名為getAdobeSignRecipients的函式，才能傳回使用者清單。

```javascript
function getAdobeSignRecipients() {

    var recipientSetInfos = new Packages.java.util.ArrayList();

    var recipientInfoSet = new com.adobe.aem.adobesign.recipient.RecipientSetInfo();
    var recipientInfoList = new Packages.java.util.ArrayList();
    var recipientInfo = new com.adobe.aem.adobesign.recipient.RecipientInfo();

    var email;
    var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.PHONE;  
    //var recipientAuthenticationMethod = com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod.NONE;
    var securityOptions = null;

    var phoneNumber = "123456789";
    var countryCode = "+1";
    var recipientPhoneInfo = new Array();
    recipientPhoneInfo.push(new com.adobe.aem.adobesign.recipient.RecipientPhoneInfo(phoneNumber, countryCode));

     securityOptions = new com.adobe.aem.adobesign.recipient.RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
    
    email = "example@example.com";
    
    recipientInfo.setEmail(email);
    recipientInfo.setSecurityOptions(securityOptions);
    
    recipientInfoList.add(recipientInfo);
    recipientInfoSet.setMemberInfos(recipientInfoList);
    recipientSetInfos.add(recipientInfoSet);

    return recipientSetInfos;

}
```

## 使用Java介面動態選擇用戶或組 {#use-java-interface-to-dynamically-choose-a-user-or-group}

您可以使用[RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面動態選擇用於Adobe Sign的用戶或組並分配任務步驟。 您可以建立使用[RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面的OSGi套件組合，並將其部署至AEM Forms伺服器。 它可讓選項在AEM Workflow的「指派任務」和Adobe Sign元件中供選取。

您需要[AEM Forms用戶端SDK](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) jar和[granite jar](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/)檔案，才能編譯下列程式碼範例。 將這些jar檔案作為外部依賴項添加到OSGi捆綁項目。 您可以使用任何Java IDE來建立OSGi套件組合。 下列程式提供使用Eclipse建立OSGi套件組合的步驟：

1. 開啟Eclipse IDE。 導覽至&#x200B;**[!UICONTROL 檔案]**> **[!UICONTROL 新專案]**。
1. 在「選擇嚮導」螢幕上，選擇&#x200B;**[!UICONTROL Maven項目]**，然後按一下&#x200B;**[!UICONTROL Next]**。
1. 在New Maven專案中，保留預設值，然後按一下&#x200B;**[!UICONTROL Next]**。 選取原型，然後按一下&#x200B;**[!UICONTROL Next]**。 例如， maven-archetype-quickstart。 為項目指定&#x200B;**[!UICONTROL 組Id]**、**[!UICONTROL 工件Id]**、**[!UICONTROL 版本]**&#x200B;和&#x200B;**[!UICONTROL 包]**，然後按一下&#x200B;**[!UICONTROL 完成]**。 專案隨即建立。
1. 開啟pom.xml檔案以進行編輯，並以下列項目取代檔案的所有內容：

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
       <modelVersion>4.0.0</modelVersion>
   
       <groupId>getAgent</groupId>
       <artifactId>assignToAgent</artifactId>
       <version>1.0</version>
       <packaging>bundle</packaging><!-- packaging type bundle is must -->
   
       <name>assignToAgent</name>
       <url>https://maven.apache.org</url>
       <repositories>
           <repository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo1.maven.org/maven2/com/adobe/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk</artifactId>
               <version>6.0.138</version>
           </dependency>
           <dependency>
               <groupId>com.adobe.granite</groupId>
               <artifactId>com.adobe.granite.workflow.api</artifactId>
               <version>1.0.0</version>
           </dependency>
   
           <dependency>
               <groupId>org.osgi</groupId>
               <artifactId>org.osgi.core</artifactId>
               <version>4.2.0</version>
               <scope>provided</scope>
           </dependency>
   
           <dependency>
               <groupId>org.apache.felix</groupId>
               <artifactId>org.apache.felix.scr.annotations</artifactId>
               <version>1.7.0</version>
   
           </dependency>
   
           <dependency>
               <groupId>org.apache.sling</groupId>
               <artifactId>org.apache.sling.api</artifactId>
               <version>2.2.0</version>
   
           </dependency>
   
       </dependencies>
   
       <!-- ====================================================================== -->
       <!-- B U I L D D E F I N I T I O N -->
       <!-- ====================================================================== -->
       <build>
           <plugins>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-bundle-plugin</artifactId>
                   <extensions>true</extensions>
                   <configuration>
                       <instructions>
                           <Bundle-SymbolicName>com.aem.assigntoAgent-bundle</Bundle-SymbolicName>
                       </instructions>
                   </configuration>
               </plugin>
   
               <plugin>
                   <groupId>org.apache.felix</groupId>
                   <artifactId>maven-scr-plugin</artifactId>
                   <version>1.9.0</version>
                   <executions>
                       <execution>
                           <id>generate-scr-descriptor</id>
                           <goals>
                               <goal>scr</goal>
                           </goals>
                       </execution>
                   </executions>
               </plugin>
           </plugins>
       </build>
   
   </project>
   ```

1. 添加使用[RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面的原始碼，以動態地選擇「分配」任務步驟的用戶或組。 如需程式碼範例，請參閱[使用Java介面動態選擇使用者或群組的範例](#-sample-scripts-for)。
1. 開啟命令提示字元，並導覽至包含OSGi套件專案的目錄。 使用以下命令建立OSGi捆綁包：

   `mvn clean install`

1. 將套件組合上傳至AEM Forms伺服器。 您可以使用AEM Package Manager將套件組合匯入AEM Forms伺服器。

匯入套件組合後，可在Adobe Sign和「指派任務」步驟中使用選擇Java介面以動態選取使用者或群組的選項。

### 動態選擇使用者或群組的Java程式碼範例 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

下列范常式式碼會動態選擇Adobe Sign步驟的受託人。 您在OSGi套件中使用程式碼。 使用下列程式碼之前，請確定程式碼中提及的使用者資訊（電子郵件地址和電話號碼）正確無誤。 如果程式碼中提及的使用者資訊不正確，相關程式可能會失敗。

```java
/*************************************************************************

 *
 * ADOBE CONFIDENTIAL
 * __________________
 *
 * Copyright 2016 Adobe Systems Incorporated
 * All Rights Reserved.
 *
 * NOTICE:  All information contained herein is, and remains
 * the property of Adobe Systems Incorporated and its suppliers,
 * if any.  The intellectual and technical concepts contained
 * herein are proprietary to Adobe Systems Incorporated and its
 * suppliers and are protected by trade secret or copyright law.
 * Dissemination of this information or reproduction of this material
 * is strictly forbidden unless prior written permission is obtained
 * from Adobe Systems Incorporated.
 **************************************************************************/
 
package com.aem.impl;

import java.util.ArrayList;
import java.util.List;

import com.adobe.aem.adobesign.recipient.RecipientAuthenticationMethod;
import com.adobe.aem.adobesign.recipient.RecipientInfo;
import com.adobe.aem.adobesign.recipient.RecipientPhoneInfo;
import com.adobe.aem.adobesign.recipient.RecipientSecurityOption;
import com.adobe.aem.adobesign.recipient.RecipientSetInfo;
import com.adobe.fd.workflow.adobesign.api.RecipientInfoSpecifier;
import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

/**
 * <code>DummyRecipientInfoSpecifier implementation. A sample code to write implementation of RecipientInfoSpecifier to choose recipients/code>...
 */
@Service

@Component(metatype = false)
public class DummyRecipientChoser implements RecipientInfoSpecifier {
    public List<RecipientSetInfo> getAdobeSignRecipients(WorkItem workItem, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {

        List<RecipientSetInfo> recipientSetInfos = new ArrayList<RecipientSetInfo>();

                //First Recipient

                RecipientSetInfo recipientInfoSet1 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList = new ArrayList<RecipientInfo>();
                RecipientInfo recipientInfo1 = new RecipientInfo();//Member to first recipient

                String email;

                RecipientAuthenticationMethod recipientAuthenticationMethod = RecipientAuthenticationMethod.WEB_IDENTITY;
                RecipientSecurityOption securityOptions = null;

                String phoneNumber = "123456789";
                String countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo = new RecipientPhoneInfo[1];  //if multiple phone numbers, size>1
                recipientPhoneInfo[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo , null);
                 
                email = "example@example.com";

                recipientInfo1.setEmail(email);
                recipientInfo1.setSecurityOptions(securityOptions);

                recipientInfoList.add(recipientInfo1);  //Add member

                recipientInfoSet1.setMemberInfos(recipientInfoList);

                //Second Recipient

                RecipientSetInfo recipientInfoSet2 = new RecipientSetInfo();
                List<RecipientInfo> recipientInfoList2 = new ArrayList<RecipientInfo>();

                recipientAuthenticationMethod = RecipientAuthenticationMethod.PHONE;
                securityOptions = null;
                 
                phoneNumber = "987654321";//"0123456789";

                countryCode = "+1";
                RecipientPhoneInfo[] recipientPhoneInfo_1 = new RecipientPhoneInfo[1];
                recipientPhoneInfo_1[0] = new RecipientPhoneInfo(phoneNumber, countryCode);
                securityOptions = new RecipientSecurityOption(recipientAuthenticationMethod, recipientPhoneInfo_1 , null);
                 
                email = "example2@example.com";//"dummymail2@domain.com";

                RecipientInfo recipientInfo2  = new RecipientInfo();
                recipientInfo2.setEmail(email);
                recipientInfo2.setSecurityOptions(securityOptions);

                recipientInfoList2.add(recipientInfo2);  //Add member

                recipientInfoSet2.setMemberInfos(recipientInfoList2);

                //*********************************

                recipientSetInfos.add(recipientInfoSet1); 
                recipientSetInfos.add(recipientInfoSet2);

        return recipientSetInfos;

    }

}
```
