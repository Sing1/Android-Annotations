###主要知识点
* [1、TextChange](#TextChange)
* [2、AfterTextChange](#AfterTextChange)
* [3、BeforeTextChange](#BeforeTextChange)
* [4、FoucsChange](#FoucsChange)
* [5、CheckedChange](#CheckedChange)
* [6、Touch](#Touch)
* [7、Click](#Click)
* [8、LongClick](#LongClick)
* [9、ItemClick](#ItemClick)

####<a name="TextChange"/>1、TextChange
####<a name="AfterTextChange"/>2、AfterTextChange
####<a name="BeforeTextChange"/>3、BeforeTextChange
　　实现功能：两个输入框分别用两种监听比较区别
<br/>
<br/>
　　EventBindActivity的代码:
```Java
　　@EActivity
　　public class EventBindActivity extends Activity {

　　　　private EditText et_event_bind_one;//原生方法写

　　　　@ViewById
　　　　EditText et_event_bind_two;//注入
   
　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　setContentView(R.layout.event_bind_layout);
　　　　　　et_event_bind_one=(EditText)this.findViewById(R.id.et_event_bind_one);
　　　　　　//给EditText添加文本变化监听--实现三个监听方法
　　　　　　et_event_bind_one.addTextChangedListener(new TextWatcher() {
　　　　　　　　@Override
　　　　　　　　public void beforeTextChanged(CharSequence s, int start, int count, int after) {
　　　　　　　　　　Log.d("zttjiangqq","beforeTextChanged:"+s);
　　　　　　　　}
　　　　　　　　@Override
　　　　　　　　public void onTextChanged(CharSequence s, int start, int before, int count) {
　　　　　　　　　　Log.d("zttjiangqq","onTextChanged:"+s);
　　　　　　　　}
　　　　　　　　@Override
　　　　　　　　public void afterTextChanged(Editable s) {
　　　　　　　　　　Log.d("zttjiangqq","afterTextChanged:"+s.toString());
　　　　　　　　}
　　　　　　});
　　　　}
      
　　　　//第二个EditText中内容发生变化的监听
　　　　@BeforeTextChange(R.id.et_event_bind_two)//绑定id
　　　　public void beforeEd(CharSequence s, int start, int count, int after){//参数直接copy原生方法的参数
　　　　　　Log.d("zttjiangqq","beforeEd:"+s);
　　　　}
　　　　@TextChange(R.id.et_event_bind_two)//绑定id
　　　　public void textEd(CharSequence s, int start, int before, int count){//参数直接copy原生方法的参数
　　　　　　Log.d("zttjiangqq","textEd:"+s);
　　　　}
　　　　@AfterTextChange(R.id.et_event_bind_two)//绑定id
　　　　public void afterEd(Editable s){//参数直接copy原生方法的参数
　　　　　　Log.d("zttjiangqq","afterEd:"+s);
　　　　}
　　}
```

=========================================================
####<a name="FoucsChange"/>4、FoucsChange
　　实现功能：当EditText的焦点发生变化时参看打印日志。
<br/>
<br/>
　　EventBindActivity的代码就：
```Java
　　@EActivity
　　public class EventBindActivity extends Activity {

　　　　@ViewById
　　　　EditText et_event_bind_two;

　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　setContentView(R.layout.event_bind_layout); 
　　　　} 

　　　　@FocusChange(R.id.et_event_bind_two)//绑定id
　　　　public void focusChange(View view,boolean hasFocus){//参数可不写
　　　　　　Log.d("zttjiangqq", "当前EditText Two的焦点发生变化，状态为:"+hasFocus);
　　　　}
　　}
```

=========================================================
####<a name="CheckedChange"/>5、CheckedChange
　　实现功能：RadioButton中是否选中，查看打印日志
<br/>
<br/>
　　EventBindActivity的代码
```Java
　　@EActivity
　　public class EventBindActivity extends Activity {

　　　　@ViewById
　　　　RadioGroup radio_group;
　　　　@ViewById
　　　　RadioButton radio_one,radio_two;

　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　setContentView(R.layout.event_bind_layout);
　　　　}

　　　　@CheckedChange({R.id.radio_one,R.id.radio_two})//注入多个控件的方法
　　　　public void radioChecked(CompoundButton view, boolean isChecked){
　　　　　　if(view.getId()==R.id.radio_one){
　　　　　　　　Log.d("zttjiangqq","Radio_One的选中状态为:"+isChecked);
　　　　　　}else{
　　　　　　　　Log.d("zttjiangqq","Radio_Two的选中状态为:"+isChecked);
　　　　　　}
　　　　}
　　}
```

=========================================================
####<a name="Touch"/>6、Touch
　　实现功能：触摸控件，查看日志打印
<br/>
<br/>
　　EventBindActivity的代码
```Java
　　@EActivity
　　public class EventBindActivity extends Activity {

　　　　@ViewById
　　　　Button btn_four;

　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　setContentView(R.layout.event_bind_layout);
　　　　}
　　　　
　　　　@Touch(R.id.btn_four)
　　　　public void touchButton(){//可以加其他的参数（未试）
　　　　　　Log.d("zttjiangqq", "Button被Touch触摸了...");
　　　　}
　　}
```

=========================================================
####<a name="Click"/>7、Click
　　实现功能：点击不同的按钮区分点击哪个按钮
<br/>
<br/>
　　EventBindActivity的代码
```Java
　　@EActivity
　　public class EventBindActivity extends Activity {

　　　　@ViewById
　　　　Button btn_one,btn_two,btn_three,btn_four,btn_five;

　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　setContentView(R.layout.event_bind_layout);
　　　　}
　　　　
　　　　@Click({R.id.btn_four,R.id.btn_five})//注入多个
　　　　public void clickButton(View view){
　　　　　　switch (view.getId()){//这种方法区分点击的是哪个
　　　　　　　　case R.id.btn_four:
　　　　　　　　　　Log.d("zttjiangqq","...");
　　　　　　　　　　break;
　　　　　　　　case R.id.btn_five:
　　　　　　　　　　Toast.makeText(this,"当前Button被点击了...",Toast.LENGTH_SHORT).show();
　　　　　　　　　　break;
　　　　　　}
　　　　}
　　}
```

=========================================================
####<a name="LongClick"/>8、LongClick
　　实现功能：长按控件查看日志是否触发监听事件
<br/>
<br/>
　　EventBindActivity的代码
```Java
　　@EActivity
　　public class EventBindActivity extends Activity {

　　　　@ViewById
　　　　Button btn_six;

　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　setContentView(R.layout.event_bind_layout);
　　　　}

　　　　@LongClick(R.id.btn_six)
　　　　public void longClickButton(View view){
　　　　　　Toast.makeText(this,"当前Button被长按了...",Toast.LENGTH_SHORT).show();
　　　　} 
　　}
```

=========================================================
####<a name="ItemClick"/>9、ItemClick
　　实现功能：在ItemClickTestActivity中测试点击Item的效果
<br/>
<br/>
　　ItemClickTestActivity的代码
```Java
　　@EActivity(R.layout.item_click_layout)
　　public class ItemClickTestActivity extends Activity {
　　　　
　　　　@ViewById
　　　　ListView lv_itemClick;
　　　　private LayoutInflater mInflater;
　　　　private String[] mTitles;

　　　　@Override
　　　　protected void onCreate(Bundle savedInstanceState) {
　　　　　　super.onCreate(savedInstanceState);
　　　　　　mInflater=LayoutInflater.from(this);
　　　　}

　　　　@AfterViews
　　　　public void initViews(){
　　　　　　mTitles=new String[]{"item1","item2","item3","item4","item5","item6","item7","item8",};
　　　　　　lv_itemClick.setAdapter(new myAdapter());
　　　　}

　　　　@ItemClick(R.id.lv_itemClick)
　　　　public void showItemClick(String str){
　　　　　　Log.d("zttjiangqq",str+"");//这个打印出来是当前点击的String值，可以尝试传View,int等参数试试
　　　　}

　　　　class myAdapter extends BaseAdapter{
　　　　　　
　　　　　　@Override
　　　　　　public int getCount() {
　　　　　　　　return mTitles.length;
　　　　　　}

　　　　　　@Override
　　　　　　public Object getItem(int position) {
　　　　　　　　return mTitles[position];
　　　　　　}
　　　　　　
　　　　　　@Override
　　　　　　public long getItemId(int position) {
　　　　　　　　return position;
　　　　　　}
　　　　　　
　　　　　　@Override
　　　　　　public View getView(int position, View convertView, ViewGroup parent) {
　　　　　　　　Hondler hondler=null;
　　　　　　　　if(convertView==null){
　　　　　　　　　　hondler=new Hondler();
　　　　　　　　　　convertView=mInflater.inflate(R.layout.lv_item_layout,null);
　　　　　　　　　　hondler.lv_item_tv=(TextView)convertView.findViewById(R.id.lv_item_tv);
　　　　　　　　　　convertView.setTag(hondler);
　　　　　　　　}else {
　　　　　　　　　　hondler=(Hondler)convertView.getTag();
　　　　　　　　}
　　　　　　　　hondler.lv_item_tv.setText(mTitles[position]);
　　　　　　　　
　　　　　　　　return convertView;
　　　　　　}
　　　　}

　　　　static class Hondler{
　　　　　　TextView lv_item_tv;
　　　　}
　　}
```
　　item_click_layout.xml的代码
```Java
　　<?xml version="1.0" encoding="utf-8"?>
　　<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
　　　　android:orientation="vertical"
　　　　android:layout_width="match_parent"
　　　　android:layout_height="match_parent">

　　　　<LinearLayout
　　　　　　android:layout_width="fill_parent"
　　　　　　android:layout_height="49dp"
　　　　　　android:orientation="horizontal"
　　　　　　android:background="@android:color/holo_purple"
　　　　　　android:gravity="center">

　　　　　　<TextView
　　　　　　　　android:textColor="@android:color/white"
　　　　　　　　android:textSize="16sp"
　　　　　　　　android:text="ItemClick测试"
　　　　　　　　android:layout_width="wrap_content"
　　　　　　　　android:layout_height="wrap_content"/>
　　　　</LinearLayout>

　　　　<ListView
　　　　　　android:id="@+id/lv_itemClick"
　　　　　　android:layout_width="fill_parent"
　　　　　　android:layout_height="fill_parent"
　　　　　　android:cacheColorHint="@android:color/transparent"/>
　　</LinearLayout>
```
　　lv_item_layout.xml的代码
```Java
　　<?xml version="1.0" encoding="utf-8"?>
　　<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
　　　　android:orientation="vertical"
　　　　android:layout_width="match_parent"
　　　　android:layout_height="45dp"
　　　　android:gravity="center_vertical">

　　　　<TextView
　　　　　　android:gravity="center_vertical"
　　　　　　android:id="@+id/lv_item_tv"
　　　　　　android:paddingLeft="10dp"
　　　　　　android:textSize="16sp"
　　　　　　android:text="ItemClick测试"
　　　　　　android:layout_width="wrap_content"
　　　　　　android:layout_height="45dp"/>
　　</LinearLayout>
```
