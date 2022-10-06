---
title: 建立裝置群組篩選器
seo-title: Creating Device Group Filters
description: 建立設備組篩選器以定義一組設備功能要求
seo-description: Create a device group filter to define a set of device capability requirements
uuid: 30c0699d-2388-41b5-a062-f5ea9d6f08bc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 9fef1f91-a222-424a-8e20-3599bedb8b41
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/groupfilters
exl-id: 419d2e19-1198-4ab5-9aa0-02ad18fe171d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# 建立裝置群組篩選器{#creating-device-group-filters}

>[!NOTE]
>
>Adobe建議針對需要單頁應用程式架構用戶端轉譯（例如React）的專案使用SPA編輯器。 [了解更多](/help/sites-developing/spa-overview.md).

建立設備組篩選器以定義一組設備功能需求。 建立您所需的篩選器，以鎖定所需的裝置功能群組。

設計您的篩選器，以便使用篩選器的組合來定義功能群組。 通常，不同裝置群組的功能會有重疊之處。 因此，您可能會對多個裝置群組定義使用某些篩選器。

建立篩選器後，可在 [群組設定。](/help/sites-developing/mobile.md#creating-a-device-group)

## 篩選Java類 {#the-filter-java-class}

裝置群組篩選器是實施 [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 介面。 部署後，實施類別會提供可用於裝置群組設定的篩選服務。

本文所述的解決方案使用Apache Felix Maven SCR外掛程式來促進元件和服務的開發。 因此，示例Java類使用 `@Component`和 `@Service` 註解。 類具有以下結構：

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
public class myDeviceGroupFilter implements DeviceGroupFilter {

       public String getDescription() {
  return null;
 }

 public String getTitle() {
  return null;
 }

 public boolean matches(DeviceGroup arg0, String arg1, Map arg2) {
  return false;
 }

}
```

您必須提供下列方法的程式碼：

* `getDescription`:傳回篩選器說明。 說明會顯示在「設備組配置」對話框中。
* `getTitle`:傳回篩選器的名稱。 為設備組選擇篩選器時，將顯示名稱。
* `matches`:判斷裝置是否具備所需功能。

### 提供篩選器名稱和說明 {#providing-the-filter-name-and-description}

此 `getTitle` 和 `getDescription` 方法會分別傳回篩選器名稱和說明。 下列程式碼說明最簡單的實作：

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

對名稱和說明文字進行硬式編碼，就足以滿足單語言編寫環境的需求。 請考慮將字串外部化以供多語言使用，或啟用字串的更改而不重新編譯原始碼。

### 根據篩選條件評估 {#evaluating-against-filter-criteria}

此 `matches` 函式返回 `true` 如果裝置功能符合所有篩選條件。 評估方法參數中提供的資訊以確定設備是否屬於組。 以下值提供為引數：

* DeviceGroup對象
* 使用者代理的名稱
* 包含裝置功能的地圖物件。 Map鍵是WURFL™功能名稱，值是來自WURFL™資料庫的相應值。

此 [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 介麵包含靜態欄位中WURFL™功能名稱的子集。 從裝置功能圖中擷取值時，請使用這些欄位常數作為索引鍵。

例如，下列程式碼範例會判斷裝置是否支援CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

此 `org.apache.commons.lang.math` 套件提供 `NumberUtils` 類別。

>[!NOTE]
>
>確保部署到AEM的WURFL™資料庫包含用作篩選條件的功能。 (請參閱 [裝置偵測](/help/sites-developing/mobile.md#server-side-device-detection).)

### 螢幕大小的範例篩選 {#example-filter-for-screen-size}

下面的示例DeviceGroupFilter實現確定設備的物理大小是否滿足最低要求。 此篩選器的用途為將粒度新增至觸控裝置群組。 無論螢幕大小為何，應用程式UI中按鈕的大小應相同。 其他項目（如文字）的大小可能有所不同。 篩選器可啟用動態選取控制UI元素大小的特定CSS。

此篩選器會將大小條件套用至 `physical_screen_height` 和 `physical_screen_width` WURFL™屬性名稱。

```java
package com.adobe.example.myapp;

import java.util.Map;

import com.day.cq.wcm.mobile.api.device.DeviceGroup;
import com.day.cq.wcm.mobile.api.device.DeviceGroupFilter;

import org.apache.commons.lang.math.NumberUtils;
import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Service;

@Component(metatype = false)
@Service
@SuppressWarnings("unused")
public class ScreenSizeLarge implements DeviceGroupFilter {
    private int len=400;
    private int wid=200;
    public String getDescription() {

        return "Requires the physical size of the screen to have minimum dimensions " + len + "x" + wid+".";
    }

    public String getTitle() {
        return "Screen Size Large ("+len + "x" + wid+")";
    }

    public boolean matches(DeviceGroup deviceGroup, String userAgent,
            Map<String, String> deviceCapabilities) {

        boolean longEnough=true;
        boolean wideEnough=false;
        int dimension1=NumberUtils.toInt(deviceCapabilities.get("physical_screen_height"));
        int dimension2=NumberUtils.toInt(deviceCapabilities.get("physical_screen_width"));
        if(dimension1>dimension2){
            longEnough=dimension1>=len;
            wideEnough=dimension2>=wid;
        }else{
            longEnough=dimension2>=len;
            wideEnough=dimension1>=wid;
        }

        return longEnough && wideEnough;
    }
}
```

getTitle方法傳回的字串值會出現在裝置群組屬性的下拉式清單中。

![filteraddtogroup](assets/filteraddtogroup.png)

getTitle和getDescription方法傳回的字串值包含在裝置群組摘要頁面底部。

![篩選器描述](assets/filterdescription.png)

### Maven POM檔案 {#the-maven-pom-file}

如果您使用Maven來建置應用程式，下列POM程式碼就十分實用。 POM會參考數個必要的外掛程式和相依性。

**外掛程式:**

* Apache Maven編譯器插件：從原始碼編譯Java類。
* Apache Felix Maven套件組合外掛程式：建立套件和資訊清單
* Apache Felix Maven SCR外掛程式：建立元件描述符檔案並配置服務元件清單標頭。

**相依性:**

* `cq-wcm-mobile-api-5.5.2.jar`:提供DeviceGroup和DeviceGroupFilter介面。

* `org.apache.felix.scr.annotations.jar`:提供元件和服務注釋。

DeviceGroup和DeviceGroupFilter介面包含在Day Commulate 5 WCM Mobile API套件中。 Felix註解包含在Apache Felix Declational Services套件中。 您可以從公用Adobe存放庫取得此JAR檔案。

編寫時，5.5.2是AEM最新版本中的WCM Mobile API套件組合版本。 使用AdobeWeb控制台([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles))，以確保這是您環境中部署的套件組合版本。

**POM:** （您的POM將使用不同的groupId和版本。）

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
        xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
      <modelVersion>4.0.0</modelVersion>
      <groupId>com.adobe.example.myapp</groupId>
      <artifactId>devicefilter</artifactId>
      <version>0.0.1-SNAPSHOT</version>
      <name>my app device filter</name>
      <url>https://dev.day.com/docs/en/cq/current.html</url>
  <packaging>bundle</packaging>
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-scr-plugin</artifactId>
            <executions>
                  <execution>
                    <id>generate-scr-scrdescriptor</id>
                    <goals>
                          <goal>scr</goal>
                    </goals>
                  </execution>
            </executions>
          </plugin>
        <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
    </plugins>
</build>
<dependencies>
     <dependency>
         <groupId>com.day.cq.wcm</groupId>
         <artifactId>cq-wcm-mobile-api</artifactId>
         <version>5.5.2</version>
         <scope>provided</scope>
     </dependency>
     <dependency>
        <groupId>org.apache.felix</groupId>
        <artifactId>org.apache.felix.scr.annotations</artifactId>
        <version>1.6.0</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
</project>
```

新增設定檔 [取得內容套件Maven外掛程式](/help/sites-developing/vlt-mavenplugin.md) 區段會提供給您的maven設定檔案，以使用公用Adobe存放庫。
