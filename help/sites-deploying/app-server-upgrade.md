---
title: 應用程式伺服器安裝的升級步驟
description: 瞭解如何升級透過應用程式伺服器部署的AEM執行個體。
feature: Upgrading
exl-id: 86dd10ae-7f16-40c8-84b6-91ff2973a523
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 應用程式伺服器安裝的升級步驟{#upgrade-steps-for-application-server-installations}

本節說明更新AEM for Application Server安裝所需的程式。

此程式中的所有範例都使用Tomcat作為「應用程式伺服器」，並暗示您已部署AEM的工作版本。 此程式旨在記錄從&#x200B;**AEM 6.4版到6.5**&#x200B;所執行的升級。

1. 首先，啟動TomCat。 在大多數情況下，您可以透過從終端機執行此命令，執行`./catalina.sh`啟動指令碼來執行此動作：

   ```shell
   $CATALINA_HOME/bin/catalina.sh start
   ```

1. 如果已部署AEM 6.4，請存取：

   ```shell
   https://<serveraddress:port>/cq/system/console/bundles
   ```

1. 接下來，取消部署AEM 6.4。這可以從TomCat應用程式管理員(`http://serveraddress:serverport/manager/html`)完成

1. 現在，請使用crx2oak移轉工具移轉存放庫。 若要這麼做，請從[此位置](https://repo1.maven.org/maven2/com/adobe/granite/crx2oak/)下載最新版本的crx2oak。

   ```shell
   SLING_HOME= $AEM-HOME/crx-quickstart java -Xmx4096m -jar crx2oak.jar --load-profile segment-fds
   ```

1. 執行下列操作，刪除sling.properties檔案中的必要屬性：

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

1. 移除不再需要的檔案和資料夾。 您需要明確移除的專案包括：

   * **啟動板/啟動資料夾**。 您可以在終端機中執行以下命令來刪除它： `rm -rf crx-quickstart/launchpad/startup`

   * **base.jar檔案**： `find crx-quickstart/launchpad -type f -name "org.apache.sling.launchpad.base.jar*" -exec rm -f {} \`

   * **BootstrapCommandFile_timestamp.txt檔案**： `rm -f crx-quickstart/launchpad/felix/bundle0/BootstrapCommandFile_timestamp.txt`

   * 執行`find crx-quickstart/launchpad -type f -name "sling.options.file" -exec rm -rf`以移除&#x200B;**sling.options.file**

1. 現在，建立與AEM 6.5搭配使用的節點存放區和資料存放區。您可以在`crx-quickstart\install`下建立兩個名稱如下的檔案，以執行此操作：

   * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg`
   * `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.cfg`

   這兩個檔案會將AEM設定為使用TarMK節點存放區和檔案資料存放區。

1. 編輯組態檔，使其可供使用。 更具體地說：

   * 將下列行新增至`org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`：

     `customBlobStore=true`

   * 然後將下列行新增至`org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`：

     ```
     path=./crx-quickstart/repository/datastore
     minRecordLength=4096
     ```

1. 您現在需要變更AEM 6.5 war檔案中的執行模式。 若要這麼做，請先建立暫存資料夾，以容納AEM 6.5戰爭。 此範例中的資料夾名稱為`temp`。 複製war檔案後，從temp資料夾內執行以擷取其內容：

   ```
   jar xvf aem-quickstart-6.5.0.war
   ```

1. 擷取內容後，請移至&#x200B;**WEB-INF**&#x200B;資料夾並編輯web.xml檔案以變更執行模式。 若要尋找XML中設定它們的位置，請尋找`sling.run.modes`字串。 找到後，請變更下一行程式碼的執行模式（預設為author）：

   ```bash
   <param-value >author</param-value>
   ```

1. 變更上述作者值，並將執行模式設定為： `author,crx3,crx3tar`。 程式碼的最後一個區塊看起來應該像這樣：

   ```
   <init-param>
   <param-name>sling.run.modes</param-name>
   <param-value>author,crx3,crx3tar</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

1. 使用修改後的內容重新建立jar：

   ```bash
   jar cvf aem65.war
   ```

1. 最後，在TomCat中部署新的war檔案。
