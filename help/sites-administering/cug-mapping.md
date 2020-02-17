---
title: AEM 6.5中的自訂使用者群組對應
seo-title: AEM 6.5中的自訂使用者群組對應
description: 瞭解自訂使用者群組對應在AEM中的運作方式。
seo-description: 瞭解自訂使用者群組對應在AEM中的運作方式。
uuid: 7520351a-ab71-4661-b214-a0ef012c0c93
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 13085dd3-d283-4354-874b-cd837a9db9f9
docset: aem65
translation-type: tm+mt
source-git-commit: a268b7046430cc17c8b59b9306cf3533d73bb4a2

---


# AEM 6.5中的自訂使用者群組對應 {#custom-user-group-mapping-in-aem}

## CUG相關JCR含量比較 {#comparison-of-jcr-content-related-to-cug}

<table>
 <tbody>
  <tr>
   <td><strong>舊版AEM</strong></td>
   <td><strong>AEM 6.5</strong></td>
   <td><strong>評論</strong></td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugEnabled</p> <p>聲明節點類型：N/A，剩餘屬性</p> </td>
   <td><p>授權:</p> <p>節點：rep:cugPolicy of node type rep:CugPolicy</p> <p>聲明節點類型：rep:CugMixin</p> <p> </p> <p> </p> <p> </p> 驗證:</p> <p>混音類型：granite:AuthenticationRequired</p> </td>
   <td><p>為了限制讀訪問，專用的CUG策略被應用到目標節點。</p> <p>注意：策略只能應用於配置的支援路徑。</p> <p>名稱為rep:cugPolicy和type rep:CugPolicy的節點受到保護，無法使用一般的JCR API呼叫寫入；請改用JCR存取控制管理。</p> <p>如需 <a href="https://jackrabbit.apache.org/oak/docs/security/authorization/cug.html">詳細資訊</a> ，請參閱本頁。</p> <p>為了對節點強制執行驗證要求，添加混合類型granite:AuthenticationRequired就足夠了。</p> <p>注意：僅在已配置的支援路徑下方受到尊重。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugPrincipals</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td><p>屬性：rep:principalNames</p> <p>聲明節點類型：rep:CugPolicy</p> </td>
   <td><p>包含允許讀取受限CUG下方內容之承擔者名稱的屬性受到保護，無法使用一般JCR API呼叫寫入；請改用JCR存取控制管理。</p> <p>如需 <a href="https://svn.apache.org/repos/asf/jackrabbit/trunk/jackrabbitapi/src/main/java/org/apache/jackrabbit/api/security/authorization/PrincipalSetPolicy.java">實作的詳細資訊</a> ，請參閱本頁。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugLoginPage</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td><p>屬性：granite:loginPath（可選）</p> <p>聲明節點類型：granite:AuthenticationRequired</p> </td>
   <td><p>具有混合類型granite:AuthenticationRequired定義的JCR節點可以任選地定義替代登錄路徑。</p> <p>注意：僅在已配置的支援路徑下方受到尊重。</p> </td>
  </tr>
  <tr>
   <td><p>屬性：cq:cugRealm</p> <p>聲明節點類型：NA，剩餘財產</p> </td>
   <td>不適用</td>
   <td>新實作不再支援。</td>
  </tr>
 </tbody>
</table>

## OSGi服務比較 {#comparison-of-osgi-services}

**舊版AEM**

標籤：Adobe Granite Closed User Group(CUG)支援

名稱：com.day.cq.auth.impl.CugSupportImpl

**AEM 6.5**

* 標籤：Apache Jackrabbit Oak CUG設定

   名稱：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugConfiguration

   配置策略=必需

* 標籤：Apache Jackrabbit Oak CUG排除清單

   名稱：org.apache.jackrabbit.oak.spi.security.authorization.cug.impl.CugExcludeImpl

   配置策略=必需

* 名稱：com.adobe.granite.auth.requirement.impl.RequirementService
* 標籤：Adobe Granite驗證需求與登入路徑處理常式

   名稱：com.adobe.granite.auth.requirement.impl.DefaultRequirementHandler

   配置策略=必需

**評論**

* 配置CUG授權並啟用／禁用評估。
配置不應受CUG授權影響的承擔者排除清單的服務。

   >[!NOTE] 如果未配置CugExcludeImpl，則CugConfiguration將返回預設值。

   如有特殊需求，可插入自訂的CugExclude實作。

* OSGi元件實施LoginPathProvider ，它向LoginSelectorHandler公開匹配的登錄路徑。 它對RequirementHandler有強制性參考，用來註冊觀察者，該觀察者會監聽透過granite:AuthenticationRequired mixin類型儲存在內容中的已變更驗證要求。
* OSGi元件實作RequirementHandler，通知SlingAuthenticator有關authrequirements的變更。

   由於此元件的配置策略為「需要」，因此只有在指定了一組支援的路徑時才會激活它。

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

