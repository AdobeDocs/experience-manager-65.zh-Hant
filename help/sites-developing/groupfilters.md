---
title: 建立設備組篩選器
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

# 建立設備組篩選器{#creating-device-group-filters}

>[!NOTE]
>
>Adobe建SPA議對需要基於單頁應用程式框架的客戶端呈現（如React）的項目使用編輯器。 [深入了解](/help/sites-developing/spa-overview.md).

建立設備組篩選器以定義一組設備功能要求。 根據需要建立任意數量的篩選器以針對所需的設備功能組。

設計篩選器，以便您可以使用它們的組合來定義權能組。 通常，不同設備組的功能會有重疊。 因此，您可能會將某些篩選器用於多個設備組定義。

建立篩選器後，可在 [組配置。](/help/sites-developing/mobile.md#creating-a-device-group)

## 篩選Java類 {#the-filter-java-class}

設備組篩選器是實現 [com.day.cq.wcm.mobile.api.device.DeviceGroupFilter](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 。 部署後，實現類提供可用於設備組配置的篩選器服務。

本文所介紹的解決方案採用Apache Felix Maven SCR插件，方便了元件和服務的開發。 因此，示例Java類使用 `@Component`和 `@Service` 注釋。 類具有以下結構：

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

您需要為以下方法提供代碼：

* `getDescription`:返回篩選器說明。 說明將出現在「設備組配置」對話框中。
* `getTitle`:返回篩選器的名稱。 為設備組選擇篩選器時，將顯示名稱。
* `matches`:確定設備是否具有所需的功能。

### 提供篩選器名稱和說明 {#providing-the-filter-name-and-description}

的 `getTitle` 和 `getDescription` 方法分別返回篩選器名稱和說明。 以下代碼說明了最簡單的實現：

```java
public String getDescription() {
    return "An example device group filter";
}

public String getTitle() {
 return "myFilter";
}
```

對名稱和說明文本進行硬編碼對於單語言創作環境來說就足夠了。 請考慮將字串外部化以用於多語言使用，或用於在不重新編譯原始碼的情況下啟用字串更改。

### 根據篩選條件評估 {#evaluating-against-filter-criteria}

的 `matches` 函式返回 `true` 如果設備功能滿足所有篩選條件。 評估方法參數中提供的資訊以確定設備是否屬於組。 以下值作為參數提供：

* DeviceGroup對象
* 用戶代理的名稱
* 包含設備功能的映射對象。 Map鍵是WURFL™功能名稱，值是WURFL™資料庫中的相應值。

的 [com.day.cq.wcm.mobile.api.devicespecs.DeviceSpecsConstants](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/wcm/mobile/api/device/DeviceGroupFilter.html) 介麵包含靜態欄位中WURFL™功能名稱的子集。 從設備功能映射中檢索值時，請將這些欄位常數用作鍵。

例如，以下代碼示例確定設備是否支援CSS:

```xml
boolean cssSupport = true;
cssSupport = NumberUtils.toInt(capabilities.get(DeviceSpecsConstants.DSPEC_XHTML_SUPPORT_LEVEL)) > 1;
```

的 `org.apache.commons.lang.math` 包提供 `NumberUtils` 類。

>[!NOTE]
>
>確保部署到的WURFL™資料AEM庫包括用作篩選條件的功能。 (請參閱 [設備檢測](/help/sites-developing/mobile.md#server-side-device-detection)。)

### 螢幕大小的示例篩選器 {#example-filter-for-screen-size}

下面的示例DeviceGroupFilter實現確定設備的物理大小是否符合最低要求。 此篩選器旨在向觸摸設備組添加粒度。 無論物理螢幕大小如何，應用程式UI中按鈕的大小應相同。 其他項目（如文本）的大小可能不同。 該篩選器可以動態選擇控制UI元素大小的特定CSS。

此篩選器將大小條件應用於 `physical_screen_height` 和 `physical_screen_width` WURFL™屬性名稱。

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

getTitle方法返回的字串值顯示在設備組屬性的下拉清單中。

![文檔組](assets/filteraddtogroup.png)

getTitle和getDescription方法返回的字串值包含在設備組摘要頁的底部。

![過濾器描述](assets/filterdescription.png)

### 馬文POM檔案 {#the-maven-pom-file}

如果使用Maven構建應用程式，則以下POM代碼非常有用。 POM引用了幾個必需的插件和依賴項。

**外掛程式:**

* Apache Maven編譯器插件：從原始碼編譯Java類。
* Apache Felix Maven捆綁包插件：建立包和清單
* Apache Felix Maven SCR插件：建立元件描述符檔案並配置服務元件清單頭。

**相依性:**

* `cq-wcm-mobile-api-5.5.2.jar`:提供DeviceGroup和DeviceGroupFilter介面。

* `org.apache.felix.scr.annotations.jar`:提供元件和服務注釋。

DeviceGroup和DeviceGroupFilter介面包含在Day Compules 5 WCM Mobile API捆綁包中。 Felix注釋包含在Apache Felix聲明性服務包中。 可以從公共Adobe庫獲取此JAR檔案。

在創作時， 5.5.2是WCM Mobile API包的最新版本AEM。 使用AdobeWeb控制台([https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles))以確保這是部署在您的環境中的捆綁包版本。

**POM:** （您的POM將使用其他groupId和版本。）

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

添加 [獲取內容包Maven插件](/help/sites-developing/vlt-mavenplugin.md) 部分將提供給您的maven設定檔案以使用公共Adobe儲存庫。
