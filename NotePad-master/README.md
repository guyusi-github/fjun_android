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
## 二、图二为搜索界面实现
---------------------------------------------------------------------------------------------------------
## 代码片段：
1.list_context_menu.xml中增加的文件：
```java
<item android:id="@+id/menu_search"
        android:icon="@drawable/ic_menu_compose"
        android:title="Search"
        android:alphabeticShortcut='p'
        app:showAsAction="always"
        app:actionViewClass="com.example.android.notepad.NoteEditor$LinedEditText"/>
```
2.在res.layout下建立的布局文件
```java
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
```

3.在AndroidManifest.xml建立activity引入

```java
<activity android:name=".SearchActivity"
            android:icon="@drawable/live_folder_notes"
            android:label="@string/live_folder_name">
            <intent-filter>
                <action android:name="android.intent.action.CREATE_LIVE_FOLDER" />

                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
```
4.建立activity（SearchActivity.class）实现逻辑
```java
package com.example.android.notepad;

import android.app.Activity;
import android.os.Bundle;
import android.text.TextUtils;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.SearchView;

public class SearchActivity  extends Activity {
    private SearchView mSearchView;
    private ListView mListView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.search_note);
        mSearchView = (SearchView) findViewById(R.id.searchView);
        mListView = (ListView) findViewById(R.id.listView);
        mListView.setAdapter(new ArrayAdapter<String>(this, android.R.layout.simple_list_item_1, mStrs));
        mListView.setTextFilterEnabled(true);

        // 设置搜索文本监听
        mSearchView.setOnQueryTextListener(new SearchView.OnQueryTextListener() {
            // 当点击搜索按钮时触发该方法
            @Override
            public boolean onQueryTextSubmit(String query) {
                return false;
            }

            // 当搜索内容改变时触发该方法
            @Override
            public boolean onQueryTextChange(String newText) {
                if (!TextUtils.isEmpty(newText)){
                    mListView.setFilterText(newText);
                }else{
                    mListView.clearTextFilter();
                }
                return false;
            }
        });

    }
}
```

![image](https://github.com/guyusi-github/fjun_android/blob/master/NotePad-master/image/result2.png)
