---
layout:       post
title:        "Android Studio 3 教程之4-Activities"
subtitle:     " Android Studio 3 - Activities"
date:         2018-03-08 02:30:02
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - 安卓
    -  Android
---

视频教程[Android Studio 3.2 安卓开发起步教程](https://ke.qq.com/course/288985?tuin=ac5537fd) 
[Youtube视频网址](​​​​https://www.youtube.com/channel/UCIJLimsCMSfc3wHmevgj8Ng)

## 内容：

* Task 1. Create the TwoActivities project

* Task 2. Create and launch the second activity

* Task 3. Send data from the main activity to the second activity

* Task 4. Return data back to the main activity

### task1 

1. Define the layout for the main activity

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:paddingBottom="@dimen/activity_vertical_margin"
android:paddingLeft="@dimen/activity_horizontal_margin"
android:paddingRight="@dimen/activity_horizontal_margin"
android:paddingTop="@dimen/activity_vertical_margin"
tools:context="com.example.android.twoactivities.MainActivity">
<Button
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="@string/button_main"
android:id="@+id/button_main"
android:layout_alignParentBottom="true"
android:layout_alignParentRight="true"
android:layout_alignParentEnd="true"
android:onClick="launchSecondActivity"/>
</RelativeLayout>
```

2. Define the button action

Log.d(LOG_TAG, "Button clicked!");

private static final String LOG_TAG =
MainActivity.class.getSimpleName();


### task2: Create and launch the second activity

1. Click the app folder for your project and choose File -> New -> Activity -> Empty Activity.

2. Modify the Android manifest

```
<activity android:name=".SecondActivity"></activity>
```

Add these attributes to the <activity> element:

```
android:label        "Second Activity"
android:parentActivityName     ".MainActivity"
```

Add a <meta-data> element inside the <activity> element for the second activity

```
<activity android:name=".SecondActivity"
   android:label="@string/activity2_name"
   android:parentActivityName=".MainActivity">
     <meta-data
        android:name="android.support.PARENT_ACTIVITY"
        android:value="com.example.android.twoactivities.MainActivity" />
</activity>
```

3. 添加一个TextView,id设为“text_header”

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:paddingBottom="@dimen/activity_vertical_margin"
android:paddingLeft="@dimen/activity_horizontal_margin"
android:paddingRight="@dimen/activity_horizontal_margin"
android:paddingTop="@dimen/activity_vertical_margin"
tools:context=".SecondActivity">
<TextView
android:id="@+id/text_header"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:layout_marginBottom="@dimen/activity_vertical_margin"
android:text="@string/text_header"
android:textAppearance="?android:attr/textAppearanceMedium"
android:textStyle="bold" />
</RelativeLayout>
```

4. 在主activity中添加intent

```
Intent intent = new Intent(this, SecondActivity.class);

tartActivity(intent);

```

### Task 3. Send data from the main activity to the second activity

1. Send data using intent 

```
public static final String EXTRA_MESSAGE =
"com.example.android.twoactivities.extra.MESSAGE";


Intent intent = new Intent(this, SecondActivity.class);
String message = mMessageEditText.getText().toString();
intent.putExtra(EXTRA_MESSAGE, message);
startActivity(intent);
```

2. Add a TextView to the second activity for the message

3. get data from intent

```
Intent intent = getIntent();
String message =
intent.getStringExtra(MainActivity.EXTRA_MESSAGE);
TextView textView = (TextView) findViewById(R.id.text_message);
textView.setText(message);
```

### Task 4. Return data back to the main activity

1. Add an EditText and a Button to the second activity layout

2. Create a response intent in the second activity

```
public static final String EXTRA_REPLY =
"com.example.android.twoactivities.extra.REPLY";
```


```
public void returnReply(View view) {
  String reply = mReply.getText().toString();
  Intent replyIntent = new Intent();
  replyIntent.putExtra(EXTRA_REPLY, reply);
  setResult(RESULT_OK, replyIntent);
  finish();
}
```

3. Add TextViews to the main activity layout to display the reply

4. Get the reply from the intent extra and display it


```
public static final int TEXT_REQUEST = 1;

startActivityForResult(intent, TEXT_REQUEST);
```

```
public void onActivityResult(int requestCode, int resultCode,
Intent data) {
  super.onActivityResult(requestCode, resultCode, data);
  if (requestCode == TEXT_REQUEST) {
    if (resultCode == RESULT_OK) {
      String reply =
      data.getStringExtra(SecondActivity.EXTRA_REPLY);
      mReplyHeadTextView.setVisibility(View.VISIBLE);
      mReplyTextView.setText(reply);
       mReplyTextView.setVisibility(View.VISIBLE);
    }
  }
}
```
