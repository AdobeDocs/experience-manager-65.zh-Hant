---
title: 動態選取AEM Forms導向工作流程步驟的使用者或群組
seo-title: 動態選取AEM Forms導向工作流程步驟的使用者或群組
description: '瞭解如何在執行時期為AEM Forms工作流程選取使用者或群組。 '
seo-description: '瞭解如何在執行時期為AEM Forms工作流程選取使用者或群組。 '
uuid: 19dcbda4-61af-40b3-b10b-68a341373410
content-type: troubleshooting
topic-tags: publish
discoiquuid: e6c9f3bb-8f20-4889-86f4-d30578fb1c51
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# 動態選取AEM Forms導向工作流程步驟的使用者或群組 {#dynamically-select-a-user-or-group-for-aem-forms-centric-workflow-steps}

瞭解如何在執行時期為AEM Forms工作流程選取使用者或群組。

在大型組織中，需要動態選擇流程的使用者。 例如，根據座席與客戶的接近程度選擇現場座席以服務客戶。 在這種情況下，會動態選擇代理。

在OSGi上指派工作和Adobe Sign [工作流程的步驟](/help/forms/using/aem-forms-workflow.md) ，提供動態選擇使用者的選項。 您可以使用ECMAScript或OSGi bundles來動態選取「指派工作」步驟的受託人，或選取「簽署檔案」步驟的簽署者。

## 使用ECMAScript動態選取使用者或群組 {#use-ecmascript-to-dynamically-select-a-user-or-group}

ECMAScript是一種指令碼語言。 它用於用戶端指令碼和伺服器應用程式。 執行以下步驟，使用ECMAScript動態選擇用戶或組：

1. 開啟CRXDE Lite。 URL是 `https://[server]:[port]/crx/de/index.jsp`
1. 在以下路徑中建立副檔名為。ecma的檔案。 如果路徑（節點結構）不存在，請建立路徑：

   * （分配任務步驟的路徑） `/apps/fd/dashboard/scripts/participantChooser`
   * （簽名步驟的路徑） `/apps/fd/workflow/scripts/adobesign`

1. 將具有動態選取使用者邏輯的ECMAScript新增至。ecma檔案。 按一下「 **[!UICONTROL 全部儲存]**」。

   如需範例指令碼，請參 [閱動態選擇使用者或群組的範例ECMAScript](/help/forms/using/dynamically-select-a-user-or-group-for-aem-workflow.md#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group)。

1. 添加指令碼的顯示名稱。 此名稱顯示在工作流步驟中。 要指定名稱：

   1. 展開指令碼節點，按一下右鍵 **[!UICONTROL jcr:content]** 節點，然後按一下 **[!UICONTROL Mixins]**。
   1. 在「編輯混 `mix:title` 合」對話方塊中新增屬性，然後按一下「 **確定」**。
   1. 將下列屬性新增至指令碼的jcr:content節點：

      | 名稱 | 類型 | 值 |
      |--- |--- |--- |
      | jcr:title | 字串 | 指定指令碼的名稱。 例如，選擇最接近的欄位代理。 此名稱會顯示在「指派工作」和「簽署檔案」步驟中。 |

   1. 按一下「 **全部儲存**」。 此指令碼可供AEM workflow的元件中選取。

      ![指令碼](assets/script.png)

### ECMAScript範例，可動態選擇使用者或群組 {#sample-ecmascripts-to-dynamically-choose-a-user-or-a-group}

以下示例ECMAScript動態選擇「指派任務」步驟的受託人。 在此指令碼中，根據裝載路徑選擇用戶。 使用此指令碼之前，請確定指令碼中提及的所有使用者都存在於AEM中。 如果指令檔中提及的使用者不存在於AEM中，則相關程式可能會失敗。

```
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

下列範例ECMAScript會動態選取Adobe Sign步驟的受託人。 使用下列指令碼之前，請確定指令碼中提及的使用者資訊（電子郵件地址和電話號碼）正確無誤。 如果指令碼中提及的用戶資訊不正確，則相關進程可能失敗。

>[!NOTE]
>
>使用ECMAScript for Adobe Sign時，指令碼必須位於crx-repository的/apps/fd/workflow/scripts/adobesign/，且應具有名為getAdobeSignRecipients的函式，以傳回使用者清單。

```
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

您可以使用 [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面，動態選擇Adobe Sign和指派工作步驟的使用者或群組。 您可以建立使用 [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面的OSGi套件，並將它部署至AEM Forms伺服器。 它可讓AEM Workflow的「指派工作」和「Adobe Sign」元件中的選項可供選取。

您需要 [AEM Forms Client SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) jar和 [granite jar](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) files才能編譯下列程式碼範例。 將這些jar檔案作為外部依賴項添加到OSGi捆綁項目。 您可以使用任何Java IDE來建立OSGi套件。 下列程式提供使用Eclipse建立OSGi套件的步驟：

1. 開啟Eclipse IDE。 導覽至「 **[!UICONTROL 檔案]**>新 **[!UICONTROL 增專案」]**。
1. 在「選擇嚮導」螢幕上，選擇「 **[!UICONTROL Maven Project]**」，然後按一下「 **[!UICONTROL Next」]**。
1. 在New Maven專案中，保留預設值，然後按一下 **[!UICONTROL 下一步]**。 選擇原型並按一下「下 **[!UICONTROL 一步]**」。 例如，maven-archetype-quickstart。 指定 **[!UICONTROL 項目的Id]**、Artifact Id **[!UICONTROL 、]** version **[!UICONTROL ，以及]********** PackageGroup For Project、Click Finish（完成）。 將建立項目。
1. 開啟pom.xml檔案進行編輯，並用以下內容替換檔案的所有內容：

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
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </repository>
       </repositories>
       <pluginRepositories>
           <pluginRepository>
               <id>adobe</id>
               <name>Adobe Public Repository</name>
               <url>https://repo.adobe.com/nexus/content/groups/public/</url>
               <layout>default</layout>
           </pluginRepository>
       </pluginRepositories>
   
       <dependencies>
           <dependency>
               <groupId>com.adobe.aemfd</groupId>
               <artifactId>aemfd-client-sdk-test</artifactId>
               <version>4.0.70</version>
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

1. 新增使用 [RecipientInfoSpecifier](https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/workflow/adobesign/api/RecipientInfoSpecifier.html) Java介面的原始碼，以動態選擇「指派」工作步驟的使用者或群組。 如需范常式式碼，請 [參閱範例以使用Java介面動態選擇使用者或群組](#-sample-scripts-for)。
1. 開啟命令提示，並導覽至包含OSGi搭售專案的目錄。 使用以下命令建立OSGi包：

   `mvn clean install`

1. 將套件上傳至AEM Forms伺服器。 您可以使用AEM Package manager將搭售匯入AEM Forms伺服器。

匯入套件後，Adobe Sign和「指派工作」步驟中便可使用選擇動態選取使用者或群組的Java介面選項。

### 動態選擇使用者或群組的範例Java程式碼 {#sample-java-code-to-dynamically-choose-a-user-or-a-group}

下列范常式式碼會動態選擇Adobe Sign步驟的受託人。 您可在OSGi套件中使用程式碼。 使用下列程式碼之前，請確定程式碼中提及的使用者資訊（電子郵件地址和電話號碼）正確無誤。 如果程式碼中提及的使用者資訊不正確，相關程式可能會失敗。

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

