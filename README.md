# ListViewTest
目录

一、ListView用法

二、定制ListView界面

三、提升ListView的运行效率

四、设置ListView点击事件

一、ListView用法
1.新建项目

2.修改activity——main.xml代码

3.修改MainActivity.java代码

二、定制ListView界面
在上面的基础上

4.定义一个实体类Fruit.java，为ListView适配器的适配类型。

5.为ListView的子项指定一个我们自定义的布局。在layout目录下新建fruit_item.xml

6.自定义适配器，继承自ArrayAdapter,并将泛型指定为Fruit类，名为FruitAdapter

7.修改修改MainActivity.java代码，添加intiFruits()方法，来初始化所有水果数据。

一、ListView用法

1.新建项目

2.修改activity——main.xml代码

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
 
    <ListView
        android:id="@+id/list_view"
        android:layout_width="match_parent"
        android:layout_height="match_parent">
 
    </ListView>
 
</LinearLayout>
3.修改MainActivity.java代码

 

二、定制ListView界面

在上面的基础上

4.定义一个实体类Fruit.java，为ListView适配器的适配类型。

package com.example.listviewtest;
 
public class Fruit {
    private String name;
    private int imageId;
 
    public Fruit(String name, int imageId) {
        this.name = name;
        this.imageId = imageId;
    }
 
    public String getName() {
        return name;
    }
 
    public int getImageId() {
        return imageId;
    }
}
 
5.为ListView的子项指定一个我们自定义的布局。在layout目录下新建fruit_item.xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
 
    <ImageView
        android:id="@+id/fruit_image"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"></ImageView>
 
    <TextView
        android:id="@+id/fruit_name"
        android:gravity="center_vertical"
        android:layout_marginLeft="10dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"></TextView>
</LinearLayout>
6.自定义适配器，继承自ArrayAdapter,并将泛型指定为Fruit类，名为FruitAdapter

public class FruitAdapter extends ArrayAdapter<Fruit> {
 
    private  int resourceId;
 
    public FruitAdapter(@NonNull Context context, int textViewResourceId, @NonNull List<Fruit> objects) {
        super(context, textViewResourceId, objects);
        resourceId = textViewResourceId;
    }
 
    @Override
    public View getView(int position,  View convertView,  ViewGroup parent) {
        Fruit fruit = getItem(position);
        View view = LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
     
        ImageView fruitImage = (ImageView)view.findViewById(R.id.fruit_image);
        TextView fruitName = view.findViewById(R.id.fruit_name);
        fruitImage.setImageResource(fruit.getImageId());
        fruitName.setText(fruit.getName());
        return view;
    }  
7.修改修改MainActivity.java代码，添加intiFruits()方法，来初始化所有水果数据。

public class MainActivity extends AppCompatActivity {
 
    private List<Fruit> fruitList = new ArrayList<Fruit>();
	@Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initFruits();//初始化
        FruitAdapter adapter = new FruitAdapter(MainActivity.this, R.layout.fruit_item, fruitList);
        ListView listView = (ListView)findViewById(R.id.list_view);
        listView.setAdapter(adapter);
    } 
     private void initFruits() {
        for (int i = 0; i < 2; i++) {
            Fruit apple = new Fruit("Apple", R.drawable.apple_pic);
            fruitList.add(apple);
            Fruit banana = new Fruit("Banana", R.drawable.banana_pic);
            fruitList.add(banana);
            Fruit orange = new Fruit("Orange", R.drawable.orange_pic);
            fruitList.add(orange);
            Fruit watermelon = new Fruit("Watermelon", R.drawable.watermelon_pic);
            fruitList.add(watermelon);
            Fruit pear = new Fruit("Pear", R.drawable.pear_pic);
            fruitList.add(pear);
            Fruit grape = new Fruit("Grape", R.drawable.grape_pic);
            fruitList.add(grape);
            Fruit pineapple = new Fruit("Pineapple", R.drawable.pineapple_pic);
            fruitList.add(pineapple);
            Fruit strawberry = new Fruit("Strawberry", R.drawable.strawberry_pic);
            fruitList.add(strawberry);
            Fruit cherry = new Fruit("Cherry", R.drawable.cherry_pic);
            fruitList.add(cherry);
            Fruit mango = new Fruit("Mango", R.drawable.mango_pic);
            fruitList.add(mango);
        }
    }
 
}
三、提升ListView的运行效率
 @Override
    public View getView(int position,  View convertView,  ViewGroup parent) {
        Fruit fruit = getItem(position);
        View view;
        if(convertView == null){
            LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
        }else{
            view = convertView;
        }
        ImageView fruitImage = (ImageView)view.findViewById(R.id.fruit_image);
        TextView fruitName = view.findViewById(R.id.fruit_name);
        fruitImage.setImageResource(fruit.getImageId());
        fruitName.setText(fruit.getName());
        return view;
    }
进一步优化

 
 @Override
 public View getView(int position, View convertView, ViewGroup parent) {
     Fruit fruit = getItem(position);
     View view;
     ViewHolder viewHolder;
     if(convertView == null){
        view =  LayoutInflater.from(getContext()).inflate(resourceId,parent,false);
         viewHolder = new ViewHolder();
         viewHolder.fruitImage = (ImageView) view.findViewById(R.id.fruit_image);
         viewHolder.fruitName = view.findViewById(R.id.fruit_name);
         view.setTag(viewHolder);
     }else{
         view = convertView;
         viewHolder = (ViewHolder)view.getTag();
     }
     viewHolder.fruitImage.setImageResource(fruit.getImageId());
     viewHolder.fruitName.setText(fruit.getName());
     return view;
 }
    class ViewHolder{
        ImageView fruitImage;
        TextView fruitName;
    }
四、设置ListView点击事件
public class MainActivity extends AppCompatActivity {
 
    private List<Fruit> fruitList = new ArrayList<Fruit>();
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        initFruits(); // 初始化水果数据
        FruitAdapter adapter = new FruitAdapter(MainActivity.this, R.layout.fruit_item, fruitList);
        ListView listView = (ListView) findViewById(R.id.list_view);
        listView.setAdapter(adapter);
        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view,
                                    int position, long id) {
                Fruit fruit = fruitList.get(position);
                Toast.makeText(MainActivity.this, fruit.getName(), Toast.LENGTH_SHORT).show();
            }
        });
    }
