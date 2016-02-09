###介绍
　　AndroidAnnotations是一个开源框架，旨在加快Android开发的效率。通过使用它开放出来的注解api，你几乎可以使用在任何地方， 大大的减少了无关痛痒的代码量，让开发者能够抽身其外，有足够的时间精力关注在真正的业务逻辑上面。而且通过简洁你的代码，也提高了代码的稳定性和后期的维护成本。以下AndroidAnnotations简称为AA。<br/>
　　可能会有人提出异议了，我们移动设备的性能，不比后台服务器拥有充足的内存和运算能力。当大量的使用注解的时候，会不会对APP的造成什么不良的影响，会不会影响到APP的执行性能？在这里先明确的声明，AA不会给APP带来任何副作用，相反它强大易用的api能为你带来前所未有的编程体验。<br/>
　　目前主流的注解框架有xUtils、ButterKnife、Dragger和Roboguice，它们的实现原理都是一致的，都是通过反射机制实现的。通过在Runtime运行期去反射类中带有注解的Field和Method，然后再去执行注解相对应的逻辑代码。大家都知道反射机制是在APP的运行期执行的，会造成执行的效率下降，执行时间变长的缺点。当在我们APP中大量的使用基于反射的注解，会严重影响到性能。但是AA的实现的逻辑并不是基于此。<br/>
　　AA工作的原理其实也很简单，它通过使用jdk 1.6引入的Java Annotation Processing Tool，在编译器中加了一层额外的自动编译步骤，用来生成基于你源码的代码。生成的代码是你源码的直接子类，而且自动生成的类的名称就是父类名称后面加个下划线。比如使用了@EActivity注解的MyActivity，AA都会自动帮你生成一个名为MyActivity_的类。使用AA的注解在编译期间就已经自动生成了对应的子类，运行期运行的其实就是这个子类，所以说AA的使用不会给APP的执行性能造成负面影响。<br/>
<br/>
　　[官网地址](http://androidannotations.org "http://androidannotations.org") 
<br/>
###特点
* 1、使用依赖注入
* 2、简化的线程模型
* 3、事件绑定
* 4、REST
* 5、包不超过159K,并且性能基本不受影响
<br/>

###相似DI框架
* 1、RoboGuice
* 2、Dagger
* 3、ButterKnife
* 4、...

###AndroidStudio集成AndroidAnnotations方法
* 1、全局build.gradle
```Java
    dependencies {
        classpath 'com.android.tools.build:gradle:1.3.0’
        classpath 'com.neenbedankt.gradle.plugins:android-apt:1.4'
    }
```
* 2、Module内部build.gradle
```Java
  apply plugin: 'com.android.application'
  apply plugin: 'android-apt'
  def AAVersion = 'XXX' 这边填写版本号，现在AndroidAnnotations的发布版本已经到了3.3.2
  
  dependencies {
    apt "org.androidannotations:androidannotations:$AAVersion"
    compile "org.androidannotations:androidannotations-api:$AAVersion"
  }
  
  apt {
    arguments {
      androidManifestFile variant.outputs[0].processResources.manifestFile
    }
  }
``` 
