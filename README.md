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


