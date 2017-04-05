2017.4.5
##### 1.更新Nexus远程库本地无法同步更新aar依赖包
#######原因：
由于gradle的缓存，比如更新gradle版本就解决这个问题
######解决方法：
* 在Windows删除"C:\Users\*****\.gradle\caches\modules-2\files-2.1"下的相对应包
* 在Mac上删除.gradle文件夹

##### 2.导入新的远程包，导致Android Studio编译报错，Manifest merger failed with multiple errors,see logs
######原因：
由于Gradle插件默认会启用Manifest Merger Tool，若Library项目中manifest也定义了与主项目相同属性（例如默认生成的android:icon和android:theme）,则此时会合并失败，并报上面的错误

######解决方法：
在Manifest.xml的application标签下添加tools:replace="android:icon,android:theme"(多个属性用,隔开，并且记住在manifest根标签上加入xmlns:tools="http://schemas.android.com/tools"，否则会找不到namespace)