---
title: 針對JEE上的AEM Forms，將JBoss EAP叢集從7.4.10升級至7.4.23
description: 針對JEE上的AEM Forms，將JBoss EAP叢集從7.4.10升級至7.4.23的其他步驟。
exl-id: 2c9e7f41-a8d6-4b03-8e5c-1a4f6d9e0b72
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE
role: User, Developer
source-git-commit: dffa92539a8205387d21d3873ab9424508182f19
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 1%

---

# 針對JEE上的AEM Forms，將JBoss EAP叢集從7.4.10升級至7.4.23 {#upgrade-jboss-eap-cluster-from-7-4-10-to-7-4-23}

## 概觀 {#overview}

當您針對JEE版AEM Forms將JBoss EAP叢集從7.4.10版升級至7.4.23版時，除了獨立升級步驟外，還需要額外設定。 在新的JBoss安裝中，必須更新叢集特定的設定，例如快取定位器、主從驗證、主機繫結和網域控制站組態。

## 套用至 {#applies-to}

本文適用於：

* 在叢集環境中於JBoss EAP 7.4.10上執行的JEE上的AEM Forms
* Windows和Linux上的主從式JBoss EAP設定

## 先決條件 {#prerequisites}

完成[在JEE](/help/forms/using/upgrade-jboss-eap-from-7-4-10-to-7-4-23.md)上將AEM Forms的JBoss EAP從7.4.10升級為7.4.23中的所有步驟，包括複製連線URL、使用者名稱和密碼從現有安裝到新的組態檔。

## 步驟 {#steps}

執行下列其他叢集特定步驟：

### 更新domain.conf.bat {#update-domain-conf-bat}

1. 在您的`domain.conf.bat`中，將現有設定中的定位器資訊新增至新檔案：

   ```text
   set "JAVA_OPTS=%JAVA_OPTS% -Doak.documentMK.maxServerTimeDiffMillis=-1"
   set "JAVA_OPTS=%JAVA_OPTS% -Dadobe.cache.cluster-locators=<ip-address-master>[22345],<ip-address-slave>[22345]"
   set "JAVA_OPTS=%JAVA_OPTS% -DentityExpansionLimit=10000"
   ```

### 設定主從式驗證 {#configure-master-slave-authentication}

1. 在主節點上建立主從式驗證的新使用者。
1. 在從屬節點上，更新`host.xml`中的使用者密碼：

   ```xml
   <server-identities>
       <secret value="Y2hhbmdlaXQ="/>
   </server-identities>
   ```

### 更新host.xml中的IP位址 {#update-ip-addresses-in-host-xml}

1. 更新`host.xml`中主要和從屬節點的IP位址：

   ```xml
   <interfaces>
       <interface name="management">
           <inet-address value="${jboss.bind.address.management:<ip-address>}"/>
       </interface>
       <interface name="public">
           <inet-address value="${jboss.bind.address:<ip-address>}"/>
       </interface>
   </interfaces>
   ```

### 從網域設定中移除部署 {#remove-deployments-from-domain-configuration}

1. 確定新的`domain_<db>.xml`檔案中沒有`<deployments>`區段。
1. 請勿從現有設定複製下列區塊：

   ```xml
   <deployments>
       <deployment name="adobe-forms-ivs-jboss.ear" runtime-name="adobe-forms-ivs-jboss.ear"/>
       <deployment name="adobe-livecycle-cq-author.ear" runtime-name="adobe-livecycle-cq-author.ear"/>
       <deployment name="adobe-livecycle-jboss.ear" runtime-name="adobe-livecycle-jboss.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win32.ear" runtime-name="adobe-livecycle-native-jboss-x86_win32.ear"/>
       <deployment name="adobe-livecycle-native-jboss-x86_win64.ear" runtime-name="adobe-livecycle-native-jboss-x86_win64.ear"/>
       <deployment name="adobe-output-ivs-jboss.ear" runtime-name="adobe-output-ivs-jboss.ear"/>
       <deployment name="adobe-workspace-client.ear" runtime-name="adobe-workspace-client.ear"/>
   </deployments>
   ```

### 更新網域組態中的驅動程式類別 {#update-driver-class-in-domain-configuration}

1. 根據您的資料庫引擎更新`domain_<db>.xml`中的驅動程式類別區段：

   **MSSQL：**

   ```xml
   <xa-datasource-class>com.microsoft.sqlserver.jdbc.SQLServerXADataSource</xa-datasource-class>
   ```

   **Oracle：**

   ```xml
   <xa-datasource-class>oracle.jdbc.xa.client.OracleXADataSource</xa-datasource-class>
   ```

### 更新從屬節點上的網域控制站 {#update-domain-controller-on-slave-nodes}

1. 使用主要IP位址、連線埠`9999`、使用者名稱`slave1`以及領域`ManagementRealm`更新`host.xml`中從節點上的網域控制站區塊：

   ```xml
   <remote host="<ip-address>" port="9999" username="slave1" realm="ManagementRealm"/>
   ```

### 更新jboss-cli.xml {#update-jboss-cli-xml}

1. 在主節點和從節點上更新`jboss-cli.xml`中的`<host>`專案。
