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
　　实现功能：点击按钮给注解的Bean设置值并弹出
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
　　实现功能：在注解Extra之后打印日志
<br/>
<br/>
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
    
      @AfterExtras
    public void showExtras(){
        Log.d("zttjiangqq", "invoke showExtras...");
    }
}
```

=========================================================
####<a name="AfterInject"/>4、AfterInject
　　实现功能：注入普通类之后的一些初始化之类的。
<br/>
<br/>
TwoActivity的代码:
```Java
　 @EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
    
    @Bean
    PersonBean personBean;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
    @Click(R.id.btn_one)
    public void buttonClick(){
       Log.d("zttjiangqq","测试AfterInject...");
    }
    
    @AfterInject
    public void showAfterInjectThing(){
        Log.d("zttjiangqq","invoke showAfterInjectThing...");
    }
}
```

=========================================================
####<a name="ViewById"/>5、ViewById
　　实现功能：
<br/>
<br/>
　　TwoActivity的代码：
```Java
　 @EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
 
    @ViewById
    TextView afterViews_tv;//这个名字必须与xml中的id是一样的
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    } 
}
```

=========================================================
####<a name="AfterViews"/>6、AfterViews
　　实现功能：在activity_main.xml中有一个TextView，设置有默认值，当注入之后改变上面的值。
<br/>
<br/>
　　activity_main.xml代码就一个Button
```Java
　 <?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="match_parent">
      
    <TextView

        android:id="@+id/afterViews_tv"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="我是默认文本数据框"/>
</LinearLayout>
```
　　TwoActivity代码
```Java
@EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
    
    @ViewById
    TextView afterViews_tv;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
  
    @AfterViews
    public void initViews(){
        afterViews_tv.setText("我已经被注入了...");
    }
}
```
备注：<br/>
为什么要在这个标签里面写而不在onCreate()方法里面写，在AA框架里面执行onCreate()方法时还没有执行@ViewById，对象是空。
 =========================================================
####<a name="RootContext"/>7、RootContext
　　实现功能：在TwoActivity中点击按钮的时候能获取到通过context取出来的值
<br/>
<br/>
　　PersonBean代码
```Java
@EBean
public class PersonBean {
    @RootContext
    Context context;//已经实例化好了
    private String username;
    private String extra;
    public PersonBean() {
    }

    public String getUsername() {
        return username;
    }
public String getExtra() {
        return extra;
    }
    public void setUsername(String username) {
        extra=context.getResources().getString(R.string.string_extra);//随便一个字符串
        this.username = username;
    }
}
```
　　TwoActivity的代码：
```Java
@EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
   
    @ViewById
    Button btn_one;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
    @Click(R.id.btn_one)
    public void buttonClick(){
        personBean.setUsername("江清清");
        Toast.makeText(this,personBean.getUsername()+personBean.getExtra(),Toast.LENGTH_SHORT).show();
    }
}
```
　
=========================================================
####<a name="SystemService"/>8、SystemService
　　实现功能：用注入方法获取系统服务，不再使用之前的方法
<br/>
<br/>
```Java
　 @EActivity(R.layout.two_layout)
public class TwoActivity extends Activity {
    @SystemService
    ConnectivityManager connectivityManager;
   
    @ViewById
    Button btn_one;
  
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
    }
    @Click(R.id.btn_one)
    public void buttonClick(){
        
                // 获取手机所有连接管理对象(包括wi-fi,net等连接的管理)
                // ConnectivityManager connectivityManager = (ConnectivityManager)this.getSystemService(Context.CONNECTIVITY_SERVICE);
                // 获取NetworkInfo对象
                NetworkInfo[] networkInfo = connectivityManager.getAllNetworkInfo();
                if (networkInfo != null && networkInfo.length > 0)
                {
                    for (int i = 0; i < networkInfo.length; i++)
                    {
                        System.out.println(i + "===状态===" + networkInfo[i].getState());
                        System.out.println(i + "===类型===" + networkInfo[i].getTypeName());
                        // 判断当前网络是否为连接状态
                        if (networkInfo[i].getState() == NetworkInfo.State.CONNECTED)
                        {
                            Toast.makeText(this,"当前有网络...",Toast.LENGTH_SHORT).show();
                        }
                    }
                }
            
    }
}
```
