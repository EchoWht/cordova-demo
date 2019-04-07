
# Cordava 的使用

## 安装

```bash
npm install -g cordova
```
> 注意：我第一次安装用的cnpm，出现了一些问题，后卸载且删除目录后重新用npm安装的就可以了 

## 创建项目

```bash
cordova create appName org.apache.cordova.myApp appName
```

## 生成android项目

```bash
cordova platform add android
```

## 创建vue项目

直接在./appName下创建，也可以在其他目录下

## 将vue build生成的最终文件指向到./appName/www/

需要修改Vue项目config/index.js文件，内容如下

```javascript
 build: {
    // Template for index.html
    index: path.resolve(__dirname, '../../www/index.html'),//参考此配置，按照路径修改

    // Paths
    assetsRoot: path.resolve(__dirname, '../../www'),//参考此配置，按照路径修改
    assetsSubDirectory: 'static',
    assetsPublicPath: '',//参考此配置，按照路径修改

    /**
     * Source Maps
     */

    productionSourceMap: true,
    // https://webpack.js.org/configuration/devtool/#production
    devtool: '#source-map',

    // Gzip off by default as many popular static hosts such as
    // Surge or Netlify already gzip all static assets for you.
    // Before setting to `true`, make sure to:
    // npm install --save-dev compression-webpack-plugin
    productionGzip: false,
    productionGzipExtensions: ['js', 'css'],

    // Run the build command with an extra argument to
    // View the bundle analyzer report after build finishes:
    // `npm run build --report`
    // Set to `true` or `false` to always turn it on or off
    bundleAnalyzerReport: process.env.npm_config_report
  }
	
```

## build vue 项目

```bash
npm run build
```

## 校验开发环境的完整性

```bash
cordova requirements
```
### 配置Gradle

可能需要配置Gradle，配置方法如下

```bash
## gradle path
export GRADLE_HOME=/Applications/Android\ Studio.app/Contents/gradle/gradle-4.10.1
export PATH=${PATH}:${GRADLE_HOME}/bin
```

配置完成后如果执行gradle命令时提示gradle: Permission denied，需要执行以下命令

```bash
##gradle 的路径
chmod +x /Applications/Android\ Studio.app/Contents/gradle/gradle-4.10.1/gradle
```

## 打包成apk

```bash
cordova build android
```

## 通过模拟器测试

需要手动启动一个模拟器，注意不要通过android studio启动

```bash
/Users/wanghaotian/Library/Android/sdk/emulator/emulator  -netdelay none -netspeed full -avd Nexus_5X_API_28
```

```bash
cordova run android
```



## 参考链接
- [cordova+vue 项目打包成Android（apk）应用](http://www.cnblogs.com/qirui/p/8421372.html)
- [Mac下配置Gradle的路径](https://blog.csdn.net/wj9966/article/details/78144453)
- [【Gradle】Mac上配置gradle环境变量以及gradle: Permission denied解决方案](https://blog.csdn.net/zhichaosong/article/details/81148184)
