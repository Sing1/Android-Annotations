######从今天起摆脱AsyncTask写法
###主要知识点
* [1、Background(共享线程池,并行) BackgroundExecutor.cancelAll("id") (id,serial,delay)](#Background)
* [2、UiThread](#UiThread)
* [3、SupposeBackground　确保子线陈运行](#SupposeBackground)
* [4、SupposeUiThread　确保主线程运行](#SupposeUiThread)

####<a name="Background"/>1、Background(共享线程池,并行) BackgroundExecutor.cancelAll("id") (id,serial,delay)
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码 

=========================================================
####<a name="UiThread"/>2、UiThread
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...

=========================================================
####<a name="SupposeBackground"/>3、SupposeBackground　确保子线陈运行
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...

=========================================================
####<a name="SupposeUiThread"/>4、SupposeUiThread　确保主线程运行
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...
