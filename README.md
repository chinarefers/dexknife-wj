首先是用法介绍
dependencies {
 	classpath 'com.library.wj:dexknife-wj:1.0.2'//分包
}
使用插件
apply plugin: 'dexknifeWj'
接下来是配置
dexKnife {
    //必选参数
    enabled true //if false,禁用分包插件
    //可选参数/
    //1.如果没有可选参数，将根据enabled决定是否分包。
    //2.如果有可选参数，需满足必选参数和可选参数的条件才允许分包

    /*
    *eg:当前productFlavors = dev，buildType = debug，
    *参数组合1：enabled = true，productFlavor = dev，buildType = debug 分包
    *参数组合2：enabled = true，productFlavor = mock，buildType = debug 不分包
    *参数组合1：enabled = true，buildType = debug 所有buildType = debug分包
    *参数组合1：enabled = true，productFlavor = dev 所有productFlavor = dev分包
    * */
    //=======================加固
    shell true
    packerNgShell false
    apktoolpath 'C://android_work/android_workspace/android_studio_xs/dexknife-wj/src/apktool/apktool.jar'
    jiaguzippath 'C:/android_work/android_workspace/android_studio_xs/dexknife-wj/src/main/java/com/wj/dexknife/shell/jiagu/jiagu.zip'
    //=======================多渠道
    // 指定渠道打包输出目录
    archiveOutput = file(new File(project.buildDir.path, new SimpleDateFormat("yyyy-MM-dd").format(new Date()) + "_apks"))
    // 指定渠道打包输出文件名格式
    // 默认是 `${appPkg}-${flavorName}-${buildType}-v${versionName}-${versionCode}`
    archiveNameFormat = 'qianfandu-${flavorName}-${versionName}'
    // 是否检查Gradle配置中的signingConfig，默认不检查
    // checkSigningConfig = false
    // 是否检查Gradle配置中的zipAlignEnabled，默认不检查
    // checkZipAlign = false
}