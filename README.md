# Preferences ---设置界面

## 首先给出Preferences.xml文件

```
<?xml version ="1.0" encoding ="utf-8"?><!--  Learn More about how to use App Actions: https://developer.android.com/guide/actions/index.html -->
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">
    <PreferenceCategory
        android:title="@string/In_line"
        android:key="@string/In_line">
        <CheckBoxPreference
            android:title="@string/CheckBoxPreference"
            android:key="@string/CheckBoxPreference"
            android:summary="this is a checkbox..."
            android:defaultValue="false"/>
    </PreferenceCategory>

    <PreferenceCategory
        android:title="@string/Dialog_based"
        android:key="@string/Dialog_based">
        <EditTextPreference
            android:title="@string/EditTextPreference"
            android:key="@string/EditTextPreference"
            android:summary="Edit your name..."
            android:textSize="20dp"
            android:dialogLayout="@layout/dialog"
            android:dialogTitle="Edit your name"
            />
        <ListPreference
            android:title="@string/ListPreference"
            android:key="@string/ListPreference"
            android:summary="select what you want..."
            android:dialogTitle="Select you likes"
            android:entries="@array/entries_muti_select_list_preference"
            android:entryValues="@array/entries_muti_select_list_preference"
            android:defaultValue="青菜"
            />
    </PreferenceCategory>

    <PreferenceCategory
        android:title="@string/Launch"
        android:key="@string/Launch">
        <PreferenceScreen android:title="New PreferenceScreen"
            android:key="New PreferenceScreen"
            android:summary="go to a website...">
            <CheckBoxPreference android:title="New CheckBoxPreference"
            android:key="new_CheckBoxPreference"
            android:summary="this is a new checkbox..."
            android:defaultValue="false"/>
        </PreferenceScreen>
        <PreferenceScreen
            android:title="Net"
            android:key="net"
            android:summary="go to a website...">
            <intent android:action="android.intent.action.VIEW"
                android:data="http://www.baidu.com"/>
        </PreferenceScreen>
    </PreferenceCategory>

    <PreferenceCategory
        android:title="@string/CheckBoxPreference"
        android:key="@string/CheckBoxPreference"
        android:summary="this is ParenCheckbox and Children...">
        <CheckBoxPreference
            android:title="@string/Parent"
            android:key="@string/Parent"
            android:summary="this is parent..."
            />
        <CheckBoxPreference
            android:title="@string/Child"
            android:key="@string/Child"
            android:dependency="@string/Parent"
            android:summary="this is child..."
            />
    </PreferenceCategory>

</PreferenceScreen>

```

## 然后是读取这个文件的SettingsFragment类

```
package com.example.setting;

import android.os.Bundle;
import android.preference.PreferenceFragment;
import android.support.annotation.Nullable;

public class SettingsFragment extends PreferenceFragment {
    @Override
    public void onCreate(@Nullable Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        addPreferencesFromResource(R.xml.preferences);
    }
}

```

## main函数

```
package com.example.setting;

import android.content.Intent;
import android.preference.PreferenceFragment;
import android.support.v7.app.AppCompatActivity;
import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        getFragmentManager().beginTransaction()
                .replace(R.id.fram, new SettingsFragment()).commit();
    }


}


```


## 下面是各个部分的截图
1. In-line preferences 
1.1 CheckBoxPreference

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410134751513.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

2. Dialog-based preferences
2.1 EditTextPreference

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410134828327.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

2.2 ListPreference 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410134849337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
3. Launch preferences
3.1 PreferenceScreen: 跳转到另一个PreferenceScreen 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410135017564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410135044562.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

3.2 PreferenceScreen: 启动一个网页 

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410135017564.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2019041013512964.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

4. Preference attributes 
4.1 CheckBox: 父选项

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410135154656.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)
4.2 CheckBox: 子选项，当父选项勾选时呈现

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190410135224196.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FpbmdmZW5nbG9zZXI=,size_16,color_FFFFFF,t_70)

以上就是本次实验的内容了，略显粗糙。。。。
