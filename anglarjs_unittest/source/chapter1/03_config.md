# 配置
---

### 生成配置文件

直接运行如下命令：

```sh
$ karma init
```
然后根据交互提示，会在项目的根目录下自动生成 karma.conf.js 文件, 文件内容如下：


```javascript

// Karma configuration
// Generated on Wed Nov 19 2014 14:37:02 GMT+0800 (CST)

module.exports = function(config) {
  config.set({

    // base path that will be used to resolve all patterns (eg. files, exclude)
    basePath: '',


    // frameworks to use
    // available frameworks: https://npmjs.org/browse/keyword/karma-adapter
        frameworks: ['jasmine'],


    // list of files / patterns to load in the browser
    // 这里配置需要测试的具体js，具体例子如下
    // 为tableCtrl.js 写了 tableCtrl_test.js 测试文件
    files: [
        'src/main/webapp/lib/angular.min.js',
        'src/main/webapp/lib/angular-route.min.js',
        'src/main/webapp/lib/angular-sanitize.min.js',
        'src/main/webapp/lib/angular-resource.min.js',
        'src/main/webapp/lib/checklist-model.js',
        'src/main/webapp/lib/ng-table.js',
        'src/main/webapp/lib/angular-mocks.js',
        'src/main/webapp/app/js/main/mainApp.js',
        'src/main/webapp/app/js/controller/tableCtrl.js',
        'src/test/webapp/appSpec/tableCtrl_test.js'
    ],


    // list of files to exclude
    exclude: [
    ],


    // preprocess matching files before serving them to the browser
    // available preprocessors: https://npmjs.org/browse/keyword/karma-preprocessor
    preprocessors: {
    },


    // test results reporter to use
    // possible values: 'dots', 'progress'
    // available reporters: https://npmjs.org/browse/keyword/karma-reporter
    reporters: ['progress'],


    // web server port
    // 指定启动的端口
    port: 8080,


    // enable / disable colors in the output (reporters and logs)
    colors: true,


    // level of logging
    // possible values: config.LOG_DISABLE || config.LOG_ERROR || config.LOG_WARN || config.LOG_INFO || config.LOG_DEBUG
    logLevel: config.LOG_INFO,


    // enable / disable watching file and executing tests whenever any file changes
    autoWatch: true,


    // start these browsers
    // available browser launchers: https://npmjs.org/browse/keyword/karma-launcher
    // 指定具体的浏览器
    // 可以配置成IE, Firefox, Opera, Safari
    browsers: ['Chrome'],


    // Continuous Integration mode
    // if true, Karma captures browsers, runs the tests and exits
    singleRun: false
  });
};


```

<font color=red>这里只需要修改我中文注释的地方即可。</font>


