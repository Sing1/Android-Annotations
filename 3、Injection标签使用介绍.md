###主要知识点
* [1、Extra](#Extra)
* [2、Bean](#Bean)
* [3、AfterExtras](#AfterExtras)
* [4、AfterInject](#AfterInject)
* [5、ViewById](#ViewById)
* [6、AfterViews](#AfterViews)
* [7、RootContext](#RootContext)
* [8、SystemService](#SystemService)

####<a name="Extra"/>1、Extra
　　实现功能：从TwoActivity带一个值跳转到ThreeActivity
<br/>
<br/>
　　TwoActivity的代码
```Java
　 @EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
   
    @Extra("key_value")//可以不写，不写的时候会默认将message作为key
    String message;//注解之后会生成一个message的函数

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }

    @Click(R.id.btn_one)
    public void buttonClick(View view){
        Intent intent=TwoActivity_.intent(this).message("HelloWorld").get();
        intent.setClass(this,ThreeActivity_.class);
        this.startActivity(intent);
    }
}
```
　　ThreeActivity的代码：
```Java
@EActivity(R.layout.three_layout)
public class ThreeActivity  extends Activity {
    @Extra
    String myMessage;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        Intent mIntent=this.getIntent();
        //ThreeActivity_.intent(this).get()
        Bundle bundle=mIntent.getExtras();
        if(bundle!=null) {
            Toast.makeText(this, "获取到的值为:" + bundle.getString("message"), Toast.LENGTH_SHORT).show();
        }
    }
}
```

=========================================================
####<a name="Bean"/>2、Bean
　　实现功能：
<br/>
<br/>
　　TwoActivity代码
```Java
@EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
  
    @Bean
    PersonBean personBean;//必须有个无参的构造函数
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
    @Click(R.id.btn_one)
    public void buttonClick(){ 
        personBean.setUsername("江清清);
        personBean.setPassword("123456");
        Toast.makeText(this,personBean.getUsername()+personBean.getPassword(),Toast.LENGTH_SHORT).show();
    }
}
```

=========================================================
####<a name="AfterExtras"/>3、AfterExtras
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...

=========================================================
####<a name="AfterInject"/>4、AfterInject
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...
=========================================================
####<a name="ViewById"/>5、ViewById
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...
 =========================================================
####<a name="AfterViews"/>6、AfterViews
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...
 =========================================================
####<a name="RootContext"/>7、RootContext
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...
 =========================================================
####<a name="SystemService"/>8、SystemService
　　实现功能：
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 
```
　　MainActivity代码
...
 
