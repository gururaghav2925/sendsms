# Ex.No: 3 – Send SMS using Intent (Android)
 
## Aim
To create and design an Android application that sends an SMS using an Intent, using Android Studio.
 
## Description
This app takes a phone number and a message from the user. On tapping **Send SMS**, it fires an implicit `ACTION_SENDTO` intent with the `smsto:` URI. The device's default messaging app opens with the number and message already filled in, and the user confirms the send there.
 
Because the SMS is handed off to the default messaging app, the app itself does not need runtime SMS permission.
 
## Equipment Required
- Android Studio (latest version)
- Android emulator with a messaging app, or a real Android device
## Project Details
| Item | Value |
|------|-------|
| Project name | smsintent |
| Template | Empty Views Activity |
| Language | Java |
| Min SDK | As selected during project setup |
 
## Algorithm
1. Open Android Studio and click **File → New → New Project**.
2. Type the application name as `smsintent` and click **Next**.
3. Select the Minimum SDK and click **Next**.
4. Select **Empty Activity**, click **Next**, then **Finish**.
5. Design the layout in `activity_main.xml`.
6. Write the logic to read the number and message and send the SMS intent in `MainActivity.java`.
7. Add the permission and `<queries>` block in `AndroidManifest.xml`.
8. Save and run the application.
## Project Structure
```
smsintent/
└── app/src/main/
    ├── AndroidManifest.xml
    ├── java/com/example/smsintent/MainActivity.java
    └── res/layout/activity_main.xml
```

## Manifest
- `<uses-permission android:name="android.permission.SEND_SMS" />` is declared.
- A `<queries>` block for `android.intent.action.SENDTO` with scheme `smsto` is required for package visibility on Android 11 and above. Without it, `resolveActivity` can return `null`.
- `MainActivity` is the launcher activity with `android:exported="true"`.
```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="24dp"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Send SMS using Intent"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="32dp" />

    <EditText
        android:id="@+id/etPhoneNumber"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter phone number"
        android:inputType="phone"
        android:layout_marginBottom="16dp" />

    <EditText
        android:id="@+id/etMessage"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter your message"
        android:inputType="textMultiLine"
        android:minLines="3"
        android:gravity="top|start"
        android:layout_marginBottom="24dp" />

    <Button
        android:id="@+id/btnSendSms"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Send SMS" />

</LinearLayout>
```

## MainActivity.java
```java
/*
 * Program to create and design an android application Send SMS using Intent.
 * Developed by: <name>, Register Number: <reg no>
 */
package com.example.myapplication;

import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.graphics.Insets;
import androidx.core.view.ViewCompat;
import androidx.core.view.WindowInsetsCompat;

public class MainActivity extends AppCompatActivity {

    private EditText etPhoneNumber;
    private EditText etMessage;
    private Button btnSendSms;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
        
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);
            return insets;
        });

        etPhoneNumber = findViewById(R.id.etPhoneNumber);
        etMessage = findViewById(R.id.etMessage);
        btnSendSms = findViewById(R.id.btnSendSms);

        btnSendSms.setOnClickListener(v -> {
            String phoneNumber = etPhoneNumber.getText().toString().trim();
            String message = etMessage.getText().toString().trim();

            if (phoneNumber.isEmpty()) {
                Toast.makeText(MainActivity.this, "Please enter a phone number", Toast.LENGTH_SHORT).show();
            } else {
                Intent intent = new Intent(Intent.ACTION_SENDTO);
                intent.setData(Uri.parse("smsto:" + phoneNumber));
                intent.putExtra("sms_body", message);

                if (intent.resolveActivity(getPackageManager()) != null) {
                    startActivity(intent);
                } else {
                    Toast.makeText(MainActivity.this, "No SMS app found", Toast.LENGTH_SHORT).show();
                }
            }
        });
    }
}


```
 


 
## Output Screenshots

<img width="1535" height="863" alt="image" src="https://github.com/user-attachments/assets/8118e7c1-99d4-4b27-b754-2116cef004f2" />




<img width="1535" height="863" alt="image" src="https://github.com/user-attachments/assets/c11b9c7d-7359-42f4-90bf-cde1b95abdb9" />


## Result
Thus a simple Android application to send an SMS using Intent was created, designed and executed successfully using Android Studio.
 
