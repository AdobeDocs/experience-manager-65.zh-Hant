---
title: 如何使用Eclipse開發AEM專案
seo-title: 如何使用Eclipse開發AEM專案
description: 本指南說明如何使用Eclipse來開發AEM專案
seo-description: 本指南說明如何使用Eclipse來開發AEM專案
uuid: 79fee76f-6bcc-498f-af46-530816b41bbe
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: aa58cfb8-ec15-4698-a8f0-97683b0de51c
translation-type: tm+mt
source-git-commit: 06f1f753b9bb7f7336454f166e03f753e3735a16

---


# 如何使用Eclipse開發AEM專案{#how-to-develop-aem-projects-using-eclipse}

本指南說明如何使用Eclipse來開發AEM專案。

>[!NOTE]
>
>Adobe現在提供 [AEM Development Tools for Eclipse](/help/sites-developing/aem-eclipse.md) ，協助您使用Eclipse開發AEM解決方案。

## 概覽 {#overview}

若要開始使用Eclipse上的AEM開發，請執行下列步驟。

每個How-To在本How-To的其餘部分中都有更詳細的說明。

* 安裝Eclipse 4.3(Kepler)
* 根據Maven設定您的AEM專案
* 在Maven POM中準備Eclipse的JSP支援
* 將Maven專案匯入Eclipse

>[!NOTE]
>
>本指南以Eclipse 4.3(Kepler)和AEM 5.6.1為基礎。

## 安裝Eclipse {#install-eclipse}

從 [Eclipse下載頁面下載「Eclipse IDE for Java EE Developers」](https://www.eclipse.org/downloads/)。

依照安裝指示 [安裝Eclipse](https://wiki.eclipse.org/Eclipse/Installation)。

## 根據Maven設定您的AEM專案 {#set-up-your-aem-project-based-on-maven}

接著，使用Maven設定專案，如使用Apache Maven [建立AEM專案中所述](/help/sites-developing/ht-projects-maven.md)。

## 準備Eclipse的JSP支援 {#prepare-jsp-support-for-eclipse}

此外，Eclipse也可以提供使用JSP的支援，例如

* 自動完成標籤庫
* 由&lt;cq:defineObjects />和&lt;sling:defineObjects />定義的物件的Eclipse-ackension

為了讓這項功能發揮作用：

1. 請依照「使 [用Apache Maven建立AEM專案](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps) 」 [中「使用JSP的方式」的指示進行](/help/sites-developing/ht-projects-maven.md)。
1. 將以下內容添加到內容模組的POM中的&lt;build />部分。

   Eclipse的Maven支援外掛程式m2e不支援maven-jspc-plugin，而此組態會告訴m2e忽略外掛程式，以及清除暫存編譯結果的相關工作。

   這不是問題：如 [How-To Work with JSPs](/help/sites-developing/ht-projects-maven.md#how-to-work-with-jsps)，此設定中的maven-jspc-plugin僅用於驗證JSP是否在生成過程中編譯。 Eclipse已報告JSP中的任何問題，不依賴此Maven增效模組。

   **myproject/content/pom.xml**

   ```xml
   <build>
     <!-- ... -->
     <pluginManagement>
       <plugins>
         <!--This plugin's configuration is used to store Eclipse m2e settings only. It has no influence on the Maven build itself.-->
         <plugin>
           <groupId>org.eclipse.m2e</groupId>
           <artifactId>lifecycle-mapping</artifactId>
           <version>1.0.0</version>
           <configuration>
             <lifecycleMappingMetadata>
               <pluginExecutions>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.sling</groupId>
                     <artifactId>maven-jspc-plugin</artifactId>
                     <versionRange>[2.0.6,)</versionRange>
                     <goals>
                       <goal>jspc</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
                 <pluginExecution>
                   <pluginExecutionFilter>
                     <groupId>org.apache.maven.plugins</groupId>
                     <artifactId>maven-clean-plugin</artifactId>
                     <versionRange>[2.4.1,)</versionRange>
                     <goals>
                       <goal>clean</goal>
                     </goals>
                   </pluginExecutionFilter>
                   <action>
                     <ignore/>
                   </action>
                 </pluginExecution>
               </pluginExecutions>
             </lifecycleMappingMetadata>
           </configuration>
         </plugin>
       </plugins>
     </pluginManagement>
   </build>
   ```

### 將Maven專案匯入Eclipse {#import-the-maven-project-into-eclipse}

1. 在Eclipse中，選擇「檔案>匯入……」
1. 在「匯入」對話方塊中，選擇「Maven >現有Maven專案」，然後按一下「下一步」。

   ![chlimage_1-41](assets/chlimage_1-41a.png)

1. 輸入專案頂層檔案夾的路徑，然後按一下「全選」和「完成」。

   ![chlimage_1-42](assets/chlimage_1-42a.png)

1. 您現在已準備好使用Eclipse來開發AEM專案，包括JSP自動完成。

   ![chlimage_1-43](assets/chlimage_1-43a.png)

   >[!NOTE]
   >
   >如果您在 `/libs/foundation/global.jsp` 中包含或其 `/libs`他JSP，則需要將其複製到項目中，以便Eclipse能夠解決包含問題。 同時，您需要確定Maven未將它整合在您的內容套件中。 如何達成此目標，請參閱 [How to Build AEM Projects using Apache Maven](/help/sites-developing/ht-projects-maven.md)。

