---
title: 動態選取使用者或群組，以進行AEM Forms為中心的工作流程步驟
description: 瞭解如何在執行階段為AEM Forms工作流程選取使用者或群組。
content-type: troubleshooting
topic-tags: publish
exl-id: 3c48660e-5e4f-4615-82d4-9f1f285c2a39
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---

# 動態選取使用者或群組，以進行AEM Forms為中心的工作流程步驟 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

瞭解如何在執行階段為AEM Forms工作流程選取使用者或群組。

在大型組織中，需要動態選取流程的使用者。 例如，根據代理商與客戶的鄰近程度，選取欄位代理商以提供客戶服務。 在這種情況下，代理程式會以動態方式選取。

指派任務和Adobe Sign步驟 [OSGi上以Forms為中心的工作流程](/help/forms/using/aem-forms-workflow.md) 提供可動態選取使用者的選項。 您可以使用ECMAScript或OSGi套件組合來動態選取「指派工作」步驟的被指定者，或選取「簽署檔案」步驟的簽署者。

## 使用ECMAScript動態選取使用者或群組 {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript是一種指令碼語言。 用於使用者端指令碼和伺服器應用程式。 執行下列步驟，使用ECMAScript動態選取使用者或群組：

1. 開啟CRXDE Lite。 URL為 `https://'[server]:[port]'/crx/de/index.jsp`
1. 在下列路徑建立副檔名為.ecma的檔案。 如果路徑（節點結構）不存在，請建立它：

   * （指派工作步驟的路徑） `/apps/fd/dashboard/scripts/participantChooser`
   * （簽章步驟的路徑） `/apps/fd/workflow/scripts/adobesign`

1. 將具有動態選取使用者邏輯的ECMAScript新增至.ecma檔案。 按一下&#x200B;**[!UICONTROL 「儲存全部」]**。

   如需範例指令碼，請參閱 [動態選取使用者或群組的ECMAScript範例](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group).

1. 新增指令碼的顯示名稱。 此名稱會顯示在工作流程步驟中。 若要指定名稱，請執行下列動作：

   1. 展開指令碼節點，用滑鼠右鍵按一下 **[!UICONTROL jcr：content]** 節點，然後按一下 **[!UICONTROL Mixin]**.
   1. 新增 `mix:title` 屬性，並按一下 **確定**.
   1. 將以下屬性新增到指令碼的jcr：content節點中：

      | 名稱 | 類型 | 值 |
      |--- |--- |--- |
      | jcr:title | 字串 | 指定指令碼的名稱。 例如，選擇最近的欄位代理。 此名稱會顯示在指派任務和簽署檔案步驟中。 |

   1. 按一下 **全部儲存**. 指令碼將可以在AEM Workflow的元件中選擇。

      ![指令碼](assets/script.png)

### 範例ECMAScripts以動態選擇使用者或群組 {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

下列範例ECMAScript會動態選取「指派工作」步驟的被指派者。 在此指令碼中，會根據裝載的路徑來選取使用者。 使用此指令碼之前，請確定指令碼中提到的所有使用者都存在於AEM中。 如果指令碼中提到的使用者不存在於AEM中，則相關程式可能會失敗。

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

以下範例ECMAScript會動態選取Adobe Sign步驟的被指定者。 使用以下指令碼之前，請確定指令碼中提及的使用者資訊（電子郵件地址和電話號碼）正確無誤。 如果指令碼中提及的使用者資訊不正確，相關程式可能會失敗。

>[!NOTE]
>
>在使用適用於Adobe Sign的ECMAScript時，指令碼必須位於/apps/fd/workflow/scripts/adobesign/的crx-repository中，並且應該有一個名為getAdobeSignRecipients的函式以傳回使用者清單。

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

## 使用Java介面動態選擇使用者或群組 {#use-java-interface-to-dynamically-choose-a-user-or-group}

您可以使用 [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面可動態選擇Adobe Sign的使用者或群組，以及指派工作步驟。 您可以建立一個OSGi套件組合，該套件組合使用 [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面並將其部署至AEM Forms伺服器。 這可讓您在AEM Workflow的指派任務和Adobe Sign元件中選取選項。

您需要 [AEM Forms使用者端SDK](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) jar和 [granite jar](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 編譯下列程式碼範例的檔案。 將這些jar檔案新增為外部相依性至OSGi套件專案。 您可以使用任何Java IDE來建立OSGi套件。 下列程式提供使用Eclipse建立OSGi套件的步驟：

1. 開啟Eclipse IDE。 瀏覽至 **[!UICONTROL 檔案]**> **[!UICONTROL 新增專案]**.
1. 在「選取精靈」畫面上，選取 **[!UICONTROL Maven專案]**，然後按一下 **[!UICONTROL 下一個]**.
1. 在新Maven專案上，保留預設值，然後按一下 **[!UICONTROL 下一個]**. 選取原型並按一下 **[!UICONTROL 下一個]**. 例如，maven-archetype-quickstart。 指定 **[!UICONTROL 群組ID]**， **[!UICONTROL 成品ID]**， **[!UICONTROL 版本]**、和 **[!UICONTROL 封裝]** ，然後按一下 **[!UICONTROL 完成]**. 專案已建立。
1. 開啟pom.xml檔案進行編輯，並將檔案的所有內容取代為下列內容：

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

1. 新增使用的原始程式碼 [RecipientInfoSpecifier](https://www.adobe.io/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面可動態選擇使用者或群組以用於指派工作步驟。 如需程式碼範例，請參閱 [使用Java介面動態選擇使用者或群組的範例](#-sample-scripts-for).
1. 開啟命令提示字元並導覽至包含OSGi套件專案的目錄。 使用以下命令來建立OSGi套件：

   `mvn clean install`

1. 將套件組合上傳至AEM Forms伺服器。 您可以使用AEM封裝管理員將套件組合匯入至AEM Forms伺服器。

匯入束後，即可在Adobe Sign和指派工作步驟中，使用選項來選擇用於動態選取使用者或群組的Java介面。

### 動態選擇使用者或群組的Java程式碼範例 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

下列程式碼範例會動態選擇Adobe Sign步驟的被指定者。 您可以在OSGi套件組合中使用程式碼。 在使用下列程式碼之前，請確定程式碼中提及的使用者資訊（電子郵件地址和電話號碼）正確無誤。 如果程式碼中提到的使用者資訊不正確，相關程式可能會失敗。

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
