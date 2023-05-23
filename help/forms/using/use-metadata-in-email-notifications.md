---
title: 在電子郵件通知中使用元資料
seo-title: Use metadata in an email notification
description: 使用元資料填充表單工作流電子郵件通知中的資訊
seo-description: Use metadata to populate information in a forms workflow email notification
uuid: 9075b64e-1934-44d5-8b16-aa6e95e93da9
topic-tags: publish
discoiquuid: d48b5137-c866-43cd-925b-7a6a8eac8c0b
docset: aem65
exl-id: 18cfc4be-676d-4f08-afc1-4f11bb48dab6
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---

# 在電子郵件通知中使用元資料 {#use-metadata-in-an-email-notification}

您可以使用分配任務步驟建立任務並將任務分配給用戶或組。 當將任務分配給用戶或組時，將向定義的用戶或定義的組的每個成員發送電子郵件通知。 典型 [電子郵件通知](../../forms/using/use-custom-email-template-assign-task-step.md) 包含已分配任務的連結和與任務相關的資訊。

您可以在電子郵件模板中使用元資料來動態填充電子郵件通知中的資訊。 例如，在運行時（生成電子郵件通知時）動態選擇以下電子郵件通知中的標題、說明、到期日期、優先順序、工作流和最後日期的值。

![預設電子郵件模板](assets/default_email_template_metadata_new.png)

元資料以鍵值對的形式儲存。 您可以在電子郵件模板中指定密鑰，並在運行時（生成電子郵件通知時）將密鑰替換為值。 例如，在下面的代碼示例中，「$ {workitem_title}」是鍵。 在運行時將替換為值「Loan-Request」。

```html
subject=Task Assigned - ${workitem_title}

message=<html><body>\n\
 <table style="width: 480px; font-family: Helvetica, Arial, sans-serif; border: 0; padding: 0; vertical-align: top; text-align: left; word-wrap: break-word; margin: 16px auto; color:#323232; background-color:#FFFCF9; border-collapse: collapse;">\n\
  <tbody>\n\
   <tr>\n\
    <td style="height: 100px; width: 480px; background-color: #FFE0CB; border-top: 5pt solid black; font-family: Helvetica, Arial, sans-serif; font-weight: bold; font-size: 15px; line-height: 20px; padding: 12px; color: #707070;">\n\
      Sample Company\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="font-family: Helvetica, Arial, sans-serif; height: auto; background-color: #FFFCF9; padding: 32px 16px 20px 16px; ">\n\
     <pre style="font-size: 13px; font-family: Helvetica, Arial, sans-serif;  font-weight: normal; color: #323232;"> Hello ${workitem_assignee},\n\
 The following task has been assigned to you:</pre>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="width: 480px;">\n\
     <table style="height: auto; width: 480px; background-color:#FFFBF9; font-family: Helvetica, Arial, sans-serif; border-collapse: collapse;">\n\
      <tbody>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> TITLE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_title}</p>\n\
        </td>\n\
       </tr>\n\
                            <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DESCRIPTION</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_description}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> DUE DATE</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_due_date}</p>\n\
        </td>\n\
       </tr>\n\
       <tr style="border-bottom: solid 2px #FFFCF9;">\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> PRIORITY</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_priority}</p>\n\
        </td>\n\
       </tr>\n\
       <tr>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; width: auto; height: auto; background-color:#FFF5EF; font-weight: bold; font-size: 11px; line-height: 20px; padding: 12px; color: #707070;"> WORKFLOW</td>\n\
        <td style="font-family: Helvetica, Arial, sans-serif; background-color:#FFF5EF; text-align: left; vertical-align: middle; height: auto; font-weight: normal; font-size: 13px; line-height: 20px; padding: 10px 16px 10px 32px; color: #323232;">\n\
         <p>${workitem_workflow}</p>\n\
        </td>\n\
       </tr>\n\
      </tbody>\n\
     </table>\n\
    </td>\n\
   </tr>\n\
   <tr style = "text-align: center; vertical-align: middle;">\n\
    <td style="padding:48px 0 72px 0;"> \n\
     <a href="${workitem_url}" target="_blank" style="background-color: #1EBBBB; font-size: 18px; line-height: 25px; font-weight: bold; color: #FFFFFF; text-decoration: none; padding: 15px 15px 15px 15px;">Open Task</a>\n\
    </td>\n\
   </tr>\n\
   <tr>\n\
    <td style="border-top: solid 1px #EDEAE7; padding: 16px;">\n\
     <p><span style="font-size: 12px; font-weight: normal; font-style: italic; color: #919191;">This is an automatically generated email. Please do not reply to this email.</code></p>\n\
    </td>\n\
   </tr>\n\
  </tbody>\n\
 </table>\n\
</body>\n\
</html>\n\
```

## 在電子郵件通知中使用系統生成的元資料 {#using-system-generated-metadata-in-an-email-notification}

一個AEM Forms應用程式提供了一些現成的元資料變數（鍵值對）。 您可以在電子郵件模板中使用這些變數。 變數的值基於關聯的表單應用程式。 下表列出了所有可用的開箱元資料變數：

<table>
 <tbody> 
  <tr> 
   <td>金鑰</td> 
   <td>說明</td> 
  </tr> 
  <tr> 
   <td>工作項目</td> 
   <td>關聯表單應用程式的標題。</td> 
  </tr> 
  <tr> 
   <td>工作項目_url</td> 
   <td>用於訪問關聯表單應用程式的URL。</td> 
  </tr> 
  <tr> 
   <td>工作項目說明</td> 
   <td>關聯的表單應用程式的說明。</td> 
  </tr> 
  <tr> 
   <td>工作項目優先順序</td> 
   <td>為關聯的表單應用程式指定的優先順序。</td> 
  </tr> 
  <tr> 
   <td>工作項到期日</td> 
   <td>對關聯的表單應用程式執行操作的最後日期。</td> 
  </tr> 
  <tr> 
   <td>工作項目_工作流</td> 
   <td>與表單應用程式關聯的工作流的名稱。</td> 
  </tr> 
  <tr> 
   <td>工作項_assign_timestamp</td> 
   <td>將工作流項分配給當前工作負責人的日期和時間。</td> 
  </tr> 
  <tr> 
   <td>workitem_assignee</td> 
   <td>當前受分配人的名稱。</td> 
  </tr> 
  <tr> 
   <td>主機前置詞</td> 
   <td>作者伺服器的URL。 例如，https://10.41.42.66:4502<br /> </td> 
  </tr> 
  <tr> 
   <td>發佈前置詞</td> 
   <td>發佈伺服器的URL。 例如，https://10.41.42.66:4503</td> 
  </tr> 
 </tbody> 
</table>

## 在電子郵件通知中使用自定義元資料 {#using-custom-metadata-in-an-email-notification}

您還可以在電子郵件通知中使用自定義元資料。 自定義元資料除了包含系統生成的元資料之外還包含資訊。 例如，從資料庫檢索到策略詳細資訊。 可以使用ECMAScript或OSGi捆綁包在crx-repository中添加自定義元資料：

### 使用ECMAScript添加自定義元資料  {#use-ecmascript-to-add-custom-metadata}

[ECMAScript](https://en.wikipedia.org/wiki/ECMAScript) 是指令碼語言。 它用於客戶端指令碼和伺服器應用程式。 執行以下步驟以使用ECMAScript為電子郵件模板添加自定義元資料：

1. 使用管理帳戶登錄到CRX DE。 URL為https://&#39;[伺服器]:[埠]/crx/de/index.jsp

1. 導航到/apps/fd/dashboard/scripts/metadataScripts。 建立副檔名為.ecma的檔案。 例如， usermetadata.ecma

   如果上述路徑不存在，請建立它。

1. 將代碼添加到.ecma檔案中，該檔案具有在鍵值對中生成自定義元資料的邏輯。 例如，以下ECMAScript代碼為保險單生成自定義元資料：

   ```javascript
   function getUserMetaData()  {
       //Commented lines below provide an overview on how to set user metadata in map and return it.
       var HashMap = Packages.java.util.HashMap;
       var valuesMap = new HashMap();
       valuesMap.put("policyNumber", "2017568972695");
       valuesMap.put("policyHolder", "Adobe Systems");
   
       return valuesMap;
   }
   ```

1. 按一下「全部保存」。 現在，該指令碼可供在工作流模型中AEM選擇。

   ![分配任務元資料](assets/assigntask-metadata.png)

1. （可選）指定指令碼的標題：

   如果未指定標題，則「自定義元資料」欄位將顯示ECMAScript檔案的完整路徑。 執行以下步驟為指令碼指定有意義的標題：

   1. 展開指令碼節點，按一下右鍵 **[!UICONTROL jcr：內容]** ，然後按一下 **[!UICONTROL 米辛]**。
   1. 在「編輯混音」對話框中鍵入混音：標題，然後按一下 **+**。
   1. 添加具有以下值的屬性。

      | 名稱 | jcr:title |
      |---|---|
      | 類型 | 字串 |
      | 值 | 指定指令碼的標題。 例如，策略持有者的自定義元資料。 指定的值顯示在分配任務步驟中。 |

### 使用OSGi捆綁包和Java介面添加自定義元資料 {#use-an-osgi-bundle-and-java-interface-to-add-custom-metadata}

可以使用WorkitemUserMetadataService Java介面為電子郵件模板添加自定義元資料。 您可以建立使用WorkitemUserMetadataService Java介面的OSGi捆綁包，並將其部署到AEM Forms伺服器。 它使元資料可在「分配任務」步驟中供選擇。

要使用Java介面建立OSGi捆綁包，請添加 [AEM Forms客戶端SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 罐子 [花崗岩](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.workflow.api/1.0.2/) 檔案作為OSGi捆綁項目的外部依賴項。 可以使用任何Java IDE建立OSGi包。 以下過程提供了使用Eclipse建立OSGi捆綁包的步驟：

1. 開啟Eclipse IDE。 導航到「檔案」>「新建項目」。

1. 在「選擇嚮導」螢幕上，選擇「Maven Project」，然後按一下「Next」（下一步）。

1. 在New Maven項目中，保留預設值，然後按一下Next。 選取原型並按一下「下一步」(Next)。 例如， maven-archetype-quickstart。 指定項目的組ID、項目ID、版本和包，然後按一下完成。 將建立項目。

1. 開啟pom.xml檔案進行編輯，並用下列內容替換該檔案的所有內容：

1. 添加使用WorkitemUserMetadataService Java介面為電子郵件模板添加自定義元資料的原始碼。 下面列出了示例代碼：

   ```java
   package com.aem.impl;
   
   import com.adobe.fd.workspace.service.external.WorkitemUserMetadataService;
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Properties;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.osgi.framework.Constants;
   
   import java.util.HashMap;
   import java.util.Map;
   
   @Component
   @Service
   @Properties({
           @Property(name = Constants.SERVICE_DESCRIPTION, value = "A sample implementation of a user metadata service."),
           @Property(name = WorkitemUserMetadataService.SERVICE_PROPERTY_LABEL, value = "Default User Metadata Service")})
   
   public class WorkitemUserMetadataServiceImpl
     implements WorkitemUserMetadataService
   {
     public WorkitemUserMetadataServiceImpl() {}
   
     public Map<String, String> getUserMetadataMap()
     {
       HashMap<String, String> metadataMap = null;
       metadataMap = new HashMap();
       metadataMap.put("test_metadata", "tested-interface implementation");
       return metadataMap;
     }
   }
   ```

1. 開啟命令提示符並導航到包含OSGi捆綁項目的目錄。 使用以下命令建立OSGi捆綁包：

   `mvn clean install`

1. 將捆綁包上載到AEM Forms伺服器。 可以使用包管AEM理器將包導入到AEM Forms伺服器。

導入包後，您可以在「分配任務」步驟中選擇元資料，然後使用電子郵件模板。
