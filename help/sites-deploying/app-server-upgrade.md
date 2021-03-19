---
title: 應用程式伺服器安裝的升級步驟
seo-title: 應用程式伺服器安裝的升級步驟
description: 瞭解如何升級透過應用程AEM式伺服器部署的例項。
seo-description: 瞭解如何升級透過應用程AEM式伺服器部署的例項。
uuid: e4020966-737c-40ea-bfaa-c63ab9a29cee
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: 1876d8d6-bffa-4a1c-99c0-f6001acea825
docset: aem65
feature: 升級
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# 應用程式伺服器安裝的升級步驟{#upgrade-steps-for-application-server-installations}

本節介紹為了更新應用程式伺服器安裝而需AEM要遵循的過程。

此過程中的所有示例都使用Tomcat作為應用程式伺服器，並暗示您已部署了工作AEM版本。 此程式旨在記錄從&#x200B;**版本6.4AEM到6.5**&#x200B;執行的升級。

1. 首先，啟動TomCat。 在大多數情況下，您可以通過從終端運行以下命令來運行`./catalina.sh`啟動指令碼：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如AEM果已部署6.4，請存取：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下來，取AEM消部署6.4。這可從TomCat App Manager(`http://serveraddress:serverport/manager/html`)完成

1. 現在，請使用crx2oak移轉工具移轉儲存庫。 若要這麼做，請從[這個位置](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/crx2oak)下載最新版crx2oak。

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -XX:MaxPermSize=2048M -jar crx2oak.jar --load-profile segment-fds
   ```

1. 請執行下列動作，刪除sling.properties檔案中的必要屬性：

   1. 開啟位於`crx-quickstart/launchpad/sling.properties`的檔案
   1. 步驟文字移除下列屬性並儲存檔案：

      1. `sling.installer.dir`

      1. `felix.cm.dir`

      1. `granite.product.version`

      1. `org.osgi.framework.system.packages`

      1. `osgi-core-packages`

      1. `osgi-compendium-services`

      1. `jre-*`

      1. `sling.run.mode.install.options`

1. 移除不再需要的檔案和檔案夾。 您需要特別移除的項目包括：

   * **launchpad/startup資料夾**。 通過在終端機中運行以下命令可以刪除它：`rm -rf crx-quickstart/launchpad/startup`

   * **base.jar檔案**:`find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txt檔案**:`rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 執行以下動作以移除&#x200B;**sling.options.file**:`find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`

1. 現在，請建立將與6.5搭配使用的節點AEM儲存區和資料儲存區。您可以通過在`crx-quickstart\install`下建立兩個具有以下名稱的檔案來執行此操作：

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   這兩個檔案將配AEM置為使用TarMK節點儲存和檔案資料儲存。

1. 編輯配置檔案以使其可供使用。 更具體地說：

   * 將以下行添加到`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`:

      ```customBlobStore=true```

   * 然後，將以下行添加到`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`:

      ```
      path=./crx-quickstart/repository/datastore
      minRecordLength=4096
      ```

1. 您現在需要變更6.5 war檔案AEM中的執行模式。 為了做到這一點，首先建立一個臨時資料夾來容納6.AEM5戰爭。 此示例中資料夾的名稱為`temp`。 複製war檔案後，從temp資料夾內運行以提取其內容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 提取內容後，移至&#x200B;**WEB-INF**&#x200B;資料夾並編輯web.xml檔案以變更執行模式。 要查找它們在XML中設定的位置，請查找`sling.run.modes`字串。 找到後，請變更下一行程式碼中的執行模式，依預設會設為編寫：

   ```bash
   <param-value >author</param-value>
   ```

1. 將上述作者值變更，並將執行模式設為：`author,crx3,crx3tar`。 最後一個程式碼區塊應如下所示：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用已修改的內容重新建立jar:

   ```bash
   jar cvf aem65.war
   ```

1. 最後，在TomCat中部署新的戰爭檔案。
