---
title: AEM 6.5中的自訂使用者群組對應
seo-title: Custom User Group Mapping in AEM 6.5
description: 了解自訂使用者群組對應在AEM中的運作方式。
seo-description: Lear how Custom User Group Mapping works in AEM.
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
exl-id: 661602eb-a117-454d-93d3-a079584f7a5d
feature: Security
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# AEM 6.5中的自訂使用者群組對應 {#custom-user-group-mapping-in-aem}

## CUG中JCR含量的比較 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>舊版AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugEnabled</p> <p>聲明節點類型：不適用，剩餘財產</p> </td>
   <td><p>授權:</p> <p>節點：rep:cugPolicy的節點類型rep:CugPolicy</p> <p>聲明節點類型：rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 驗證:</p> <p>Mixin類型：granite:AuthenticationRequired</p> </td>
   <td><p>為了限制讀訪問，將專用的CUG策略應用到目標節點。</p> <p>注意：只能在配置的支援路徑上應用策略。</p> <p>名稱為rep:cugPolicy和rep:CugPolicy的節點受保護，無法使用常規JCR API調用寫入；請改用JCR存取控制管理。</p> <p>請參閱 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">本頁</a> 以取得詳細資訊。</p> <p>為了對節點強制執行驗證要求，只需新增mixin類型granite:AuthenticationRequired即可。</p> <p>注意：僅在已設定的支援路徑之下接受。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugPrincipals</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td><p>屬性：rep:principalNames</p> <p>聲明節點類型：rep:CugPolicy</p> </td>
   <td><p>包含允許讀取受限CUG下方內容的主體名稱的屬性受保護，無法使用常規JCR API調用寫入；請改用JCR存取控制管理。</p> <p>請參閱 <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">本頁</a> 以取得實作的詳細資訊。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugLoginPage</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td><p>屬性：granite:loginPath（可選）</p> <p>聲明節點類型：granite:AuthenticationRequired</p> </td>
   <td><p>定義了混合類型granite:AuthenticationRequired的JCR節點可以選擇性地定義替代登錄路徑。</p> <p>注意：僅在已設定的支援路徑之下接受。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugRealm</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td>不適用</td>
   <td>不再支援新實作。</td>
  </tr>
 </tbody>
</table>

## OSGi服務比較 {#comparison-of-osgi-services}

**舊版AEM**

標籤：AdobeGranite封閉使用者群組(CUG)支援

名稱：com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 標籤：Apache Jackrabbit Oak CUG設定

   名稱：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   ConfigurationPolicy = REQUIRED

* 標籤：Apache Jackrabbit Oak CUG排除清單

   名稱：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   ConfigurationPolicy = REQUIRED

* 名稱：com.adobe.granite.auth.requirement.impl.RequirementService
* 標籤：AdobeGranite驗證需求和登入路徑處理常式

   名稱：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   ConfigurationPolicy = REQUIRED

**評論**

* 配置CUG授權並啟用/禁用評估。
設定不應受CUG授權影響之主體的排除清單的服務。

   >[!NOTE]
   > 
   >若 `CugExcludeImpl` 未設定， `CugConfiguration` 會回到預設值。

   如有特殊需求，可插入自訂CugExclude實作。

* OSGi元件實作LoginPathProvider ，此元件會向LoginSelectorHandler顯示相符的登入路徑。 它具有對RequirementHandler的強制引用，該RequirementHandler用於通過granite:AuthenticationRequired mixin類型註冊偵聽儲存在內容中的更改的驗證要求的觀察器。
* OSGi元件實作RequirementHandler，此元件會通知SlingAuthenticator有關對authremendations的變更。

   由於此元件的配置策略為「需要」，因此只有在指定了一組受支援的路徑時才激活它。

   啟用服務將啟動RequirementService。

<!-- nested tables not supported - text above is the table>
<table>
 <tbody>
  <tr>
   <td><strong>Older AEM Versions</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>Comments</strong></td>
  </tr>
  <tr>
   <td><p>Label: Adobe Granite Closed User Group (CUG) Support</p> <p>Name: com.day.cq.auth.impl.CugSupportImpl</p> </td>
   <td><p>Label: Apache Jackrabbit Oak CUG Configuration</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
    <td><p>Label: Apache Jackrabbit Oak CUG Exclude List</p> <p>Name: org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl</p> <p>ConfigurationPolicy = REQUIRED</p> <p> </p> <p> </p> <p> </p> <p> </p> </td>
      </tr>
      <tr>
       <td>Name: com.adobe.granite.auth.requirement.impl.RequirementService</td>
      </tr>
      <tr>
       <td><p>Label: Adobe Granite Authentication Requirement and Login Path Handler</p> <p>Name: com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler</p> <p>ConfigurationPolicy = REQUIRED</p> </td>
      </tr>
     </tbody>
    </table> </td>
   <td>
     <tbody>
      <tr>
       <td>Configuration of the CUG authorization and enable/disable the evaluation.</td>
      </tr>
      <tr>
       <td><p>Service to configure exclusion list of principals which should not be affected by the CUG authorization.</p> <p>NOTE: If the CugExcludeImpl is not configured, the CugConfiguration will fall back to the default.</p> <p>It is possible to plug a custom CugExclude implementation in case of special needs.</p> </td>
      </tr>
      <tr>
       <td>OSGi component implementing LoginPathProvider that exposes a matching login path to the LoginSelectorHandler. It has a mandatory reference to a RequirementHandler which is used to register the observer that listens to changed auth requirements stored in the content by the means of the granite:AuthenticationRequired mixin type. </td>
      </tr>
      <tr>
       <td><p>OSGi component implementing RequirementHandler that notifies the SlingAuthenticator about changes to authrequirements.</p> <p>As configuration policy for this component is REQUIRE it will only be activated if a set of supported paths is specified.</p> <p>Enabling the service will launch the RequirementService.</p> </td>
      </tr>
     </tbody>
     </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->
