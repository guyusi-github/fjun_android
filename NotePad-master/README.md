# 效果展示图
## 一、图一展示标签，增加时间串
-----------------------------------------------------------------------------------------------------------------
### 代码过程：
1.在NOdeEdit.class中528行中增加代码片段，就是在private final void updateNote(String text, String title) ，添加时间撮，增加时间串
```java
    SimpleDateFormat dateformat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String dateStr = dateformat.format(System.currentTimeMillis());
         values.put(NotePad.Notes.COLUMN_NAME_MODIFICATION_DATE, dateStr);
            
```
![image](https://github.com/guyusi-github/fjun_android/blob/master/NotePad-master/image/result1.png)
代码过程：
## 二、图二为搜索界面实现
-----------------------------------------------------------------------------------------------------------------------
## 代码片段：
1.list_context_menu.xml中增加的文件：
'''java
<item android:id="@+id/menu_search"
        android:icon="@drawable/ic_menu_compose"
        android:title="Search"
        android:alphabeticShortcut='p'
        app:showAsAction="always"
        app:actionViewClass="com.example.android.notepad.NoteEditor$LinedEditText"/>
'''
2.在res.layout下建立的布局文件
'''java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:layout_margin="15dp"
    android:orientation="vertical"
    >
<!--tools:context="com.airsaid.searchviewdemo.MainActivity-->
    <SearchView
        android:id="@+id/searchView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:iconifiedByDefault="false"
        android:queryHint="请输入搜索内容" />

    <ListView
        android:id="@+id/listView"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />
</LinearLayout>

'''
![image](https://github.com/guyusi-github/fjun_android/blob/master/NotePad-master/image/result2.png)
