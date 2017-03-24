# DrawerLayoutMaterial
这个demo演示，如果使用DrawerLayout创建抽屉式应用，并使用meterial design风格的actionBar/ToolBar按钮。先看下效果吧：

一、使用ActionBar

<image src = "http://upload-images.jianshu.io/upload_images/166866-b59bce0bfede28e3.gif?imageView2/2/w/1240"/>

二、使用ToolBar

<image src = "http://upload-images.jianshu.io/upload_images/166866-956237976519c8b5.gif?imageView2/2/w/1240"/>

下面说说,怎么创建的吧

一、ActionBar + DrawerLayout

1、style.xml:

```
    <style name="DrawerArrowStyle" parent="Widget.AppCompat.DrawerArrowToggle">
        <item name="spinBars">true</item>
        <item name="barLength">18dp</item>
        <item name="gapBetweenBars">3dp</item>
        <item name="drawableSize">24dp</item>
        <item name="color">@android:color/white</item>
    </style>

    <style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="drawerArrowStyle">@style/DrawerArrowStyle</item>
    </style>
```

2、Manifest.xml：

指定Activity或者Application的theme是上面的AppTheme就好了

3、布局文件activity_actionbar.xml

```
<?xml version="1.0" encoding="utf-8"?>
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:openDrawer="start">
    
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent">

        <TextView
            android:id="@+id/tv_name"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:text="actionbar"
            android:textAppearance="@style/TextAppearance.AppCompat.Body1" />
    </LinearLayout>

    <android.support.design.widget.NavigationView
        android:id="@+id/nav_view"
        android:layout_width="wrap_content"
        android:layout_height="match_parent"
        android:layout_gravity="start"
        android:fitsSystemWindows="true"
        app:headerLayout="@layout/nav_header_main" />
        
</android.support.v4.widget.DrawerLayout>
```
4、activity.java文件
```
public class ActionBarActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_actionbar);

        DrawerLayout drawerLayout = (DrawerLayout) findViewById(R.id.drawer_layout);

        getSupportActionBar().setHomeButtonEnabled(true);
        getSupportActionBar().setDisplayHomeAsUpEnabled(true);
        ActionBarDrawerToggle actionBarDrawerToggle = new ActionBarDrawerToggle(this, drawerLayout, R.string.drawer_open, R.string.drawer_close);
        actionBarDrawerToggle.syncState();
        drawerLayout.setDrawerListener(actionBarDrawerToggle);
    }
}

```
二、ToolBar + DrawerLayout
```
1、style.xml:

 <!-- Base application theme. -->
    <style name="NoActionBarAppTheme" parent="Theme.AppCompat.Light.NoActionBar">
        <!-- Customize your theme here. -->
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
        <item name="drawerArrowStyle">@style/DrawerArrowStyle</item>
    </style>

    <style name="DrawerArrowStyle" parent="Widget.AppCompat.DrawerArrowToggle">
        <item name="spinBars">true</item>
        <item name="barLength">18dp</item>
        <item name="gapBetweenBars">3dp</item>
        <item name="drawableSize">24dp</item>
        <item name="color">@android:color/white</item>
    </style>
```
指定Activity或者Application的theme是上面的NoActionBarAppTheme就好了

2、布局文件activity_toolbar.xml:
```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <android.support.v7.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:background="@color/colorPrimary" />

    <android.support.v4.widget.DrawerLayout xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/drawer_layout"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_below="@id/toolbar"
        tools:openDrawer="start">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/tv_name"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:text="toolbar"
                android:textAppearance="@style/TextAppearance.AppCompat.Body1" />
        </LinearLayout>

        <android.support.design.widget.NavigationView
            android:id="@+id/nav_view"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            android:layout_gravity="start"
            android:fitsSystemWindows="true"
            app:headerLayout="@layout/nav_header_main" />

    </android.support.v4.widget.DrawerLayout>
</RelativeLayout>
```

3、activity.java文件：
```
public class ToolBarActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_toolbar);

        Toolbar toolbar = (Toolbar) findViewById(R.id.toolbar);
        setSupportActionBar(toolbar);
        toolbar.setTitleTextColor(Color.WHITE);
        toolbar.setTitle("DrawerLayout-Navi");

        DrawerLayout mDrawer = (DrawerLayout) findViewById(R.id.drawer_layout);

        ActionBarDrawerToggle actionBarDrawerToggle = new ActionBarDrawerToggle(this, mDrawer, toolbar, R.string.drawer_open, R.string.drawer_close);
        actionBarDrawerToggle.syncState();

        mDrawer.setDrawerListener(actionBarDrawerToggle);
    }
}
```
