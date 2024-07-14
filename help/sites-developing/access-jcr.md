---
title: 如何以程式設計方式存取AEM JCR
description: 您可以利用程式設計方式修改位於AEM存放庫(Adobe Experience Cloud的一部分)中的節點和屬性
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: fe946b9a-b29e-4aa5-b973-e2a652417a55
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 如何以程式設計方式存取AEM JCR{#how-to-programmatically-access-the-aem-jcr}

您可以利用程式設計方式修改位於Adobe CQ存放庫(Adobe Experience Cloud的一部分)中的節點和屬性。 若要存取CQ存放庫，請使用Java™內容存放庫(JCR) API。 您可以使用Java™ JCR API來建立、取代、更新及刪除Adobe CQ存放庫中的(CRUD)內容。 如需Java™ JCR API的詳細資訊，請參閱[https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)。

>[!NOTE]
>
>本文開發文章會修改來自外部Java™應用程式的Adobe CQ JCR。 相反地，您可以使用JCR API從OSGi套件組合中修改JCR。 如需詳細資訊，請參閱[將CQ資料儲存在Java™內容存放庫](https://helpx.adobe.com/experience-manager/using/persisting-cq-data-java-content1.html)。

>[!NOTE]
>
>若要使用JCR API，請將`jackrabbit-standalone-2.4.0.jar`檔案新增至您的Java™應用程式的類別路徑。 您可以從[https://jackrabbit.apache.org/jcr/jcr-api.html](https://jackrabbit.apache.org/jcr/jcr-api.html)的Java™ JCR API網頁取得此JAR檔案。

>[!NOTE]
>
>若要瞭解如何使用JCR Query API查詢Adobe CQ JCR，請參閱[使用JCR API查詢Adobe Experience Manager資料](https://helpx.adobe.com/experience-manager/using/querying-experience-manager-data-using1.html)。

## 建立存放庫執行個體 {#create-a-repository-instance}

雖然有不同的方式可連線到存放庫並建立連線，但此開發文章使用屬於`org.apache.jackrabbit.commons.JcrUtils`類別的靜態方法。 方法的名稱為`getRepository`。 此方法會採用代表Adobe CQ伺服器URL的字串引數。 例如，`http://localhost:4503/crx/server`。

`getRepository`方法傳回`Repository`執行個體，如下列程式碼範例所示。

```java
//Create a connection to the AEM JCR repository running on local host
Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");
```

## 建立工作階段執行個體 {#create-a-session-instance}

`Repository`執行個體代表CRX存放庫。 您使用`Repository`執行個體來建立與存放庫的工作階段。 若要建立工作階段，請叫用`Repository`執行個體的`login`方法並傳遞`javax.jcr.SimpleCredentials`物件。 `login`方法傳回`javax.jcr.Session`例項。

您使用物件的建構函式並傳遞下列字串值來建立`SimpleCredentials`物件：

* 使用者名稱；
* 對應的密碼

傳遞第二個引數時，請呼叫字串物件的`toCharArray`方法。 下列程式碼顯示如何呼叫傳回`javax.jcr.Sessioninstance`的`login`方法。

```java
//Create a Session instance
javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));
```

## 建立節點例項 {#create-a-node-instance}

使用`Session`執行個體來建立`javax.jcr.Node`執行個體。 `Node`執行個體可讓您執行節點作業。 例如，您可以建立節點。 若要建立代表根節點的節點，請叫用`Session`執行個體的`getRootNode`方法，如下列程式碼行所示。

```java
//Create a Node
Node root = session.getRootNode();
```

建立`Node`執行個體後，您可以執行建立其他節點和為其新增值等工作。 例如，下列程式碼會建立兩個節點，並將值新增至第二個節點。

```java
// Store content
Node day = adobe.addNode("day");
day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");
```

## 擷取節點值 {#retrieve-node-values}

若要擷取節點及其值，請叫用`Node`執行個體的`getNode`方法，並傳遞代表節點完整路徑的字串值。 考量在前一個程式碼範例中建立的節點結構。 若要擷取日期節點，請指定adobe/day，如下列程式碼所示：

```java
// Retrieve content
Node node = root.getNode("adobe/day");
System.out.println(node.getPath());
System.out.println(node.getProperty("message").getString());
```

## 在Adobe CQ存放庫中建立節點 {#create-nodes-in-the-adobe-cq-repository}

以下Java™程式碼範例代表連線至Adobe CQ、建立`Session`執行個體及新增節點的Java™類別。 節點會獲派資料值，然後節點的值及其路徑會寫入主控台。 當您完成工作階段時，請務必登出。

```java
/*
 * This Java Quick Start uses the jackrabbit-standalone-2.4.0.jar
 * file. See the previous section for the location of this JAR file
 */

import javax.jcr.Repository;
import javax.jcr.Session;
import javax.jcr.SimpleCredentials;
import javax.jcr.Node;

import org.apache.jackrabbit.commons.JcrUtils;
import org.apache.jackrabbit.core.TransientRepository;

public class GetRepository {

public static void main(String[] args) throws Exception {

try {

    //Create a connection to the CQ repository running on local host
    Repository repository = JcrUtils.getRepository("http://localhost:4503/crx/server");

   //Create a Session
   javax.jcr.Session session = repository.login( new SimpleCredentials("admin", "admin".toCharArray()));

  //Create a node that represents the root node
  Node root = session.getRootNode();

  // Store content
  Node adobe = root.addNode("adobe");
  Node day = adobe.addNode("day");
  day.setProperty("message", "Adobe CQ is part of the Adobe Digital Marketing Suite!");

  // Retrieve content
  Node node = root.getNode("adobe/day");
  System.out.println(node.getPath());
  System.out.println(node.getProperty("message").getString());

  // Save the session changes and log out
  session.save();
  session.logout();
  }
 catch(Exception e){
  e.printStackTrace();
  }
 }
}
```

執行完整的程式碼範例並建立節點後，您就可以檢視&#x200B;**[!UICONTROL CRXDE Lite]**&#x200B;中的新節點，如下圖所示。

![chlimage_1-68](assets/chlimage_1-68a.png)
