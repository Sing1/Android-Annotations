#介绍
　　AndroidAnnotations是一个能够让你快速进行Android开发的开源框架，它可以让我更加专注于业务功能开发。并且使代码更加精简，使项目更加容易维护(例如:findViewById(),setOnClickListener())，它的目标就是“Fast Android Development.Easy maintainance”(Android快速开发,简单维护)。<br/>
<br/>
[官网地址](http://androidannotations.org "http://androidannotations.org") 
<br/>
####特点
* 1、使用依赖注入
* 2、简化的线程模型
* 3、事件绑定
* 4、REST
* 5、包不超过159K,并且性能基本不受影响
<br/>
#### 相似DI框架
* 1、RoboGuice
* 2、Dagger
* 3、ButterKnife
* 4、...
<br/>


AndroidStudio集成AndroidAnnotations方法
1.全局build.gradle
    dependencies {
        classpath 'com.android.tools.build:gradle:1.3.0’
        classpath 'com.neenbedankt.gradle.plugins:android-apt:1.4'
    }
