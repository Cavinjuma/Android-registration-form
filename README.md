# Android-registration-form

activity_main

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:padding="16dp"
    android:background="@drawable/background"
    android:orientation="vertical">

    <TextView
        android:id="@+id/titleTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Android Registration Form"
        android:textSize="25sp"
        android:textStyle="bold"
        android:paddingBottom="10dp"/>

    <EditText
        android:id="@+id/firstNameEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="First Name"/>

    <EditText
        android:id="@+id/lastNameEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Last Name"/>

    <EditText
        android:id="@+id/emailEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Email"
        android:inputType="textEmailAddress"/>

    <EditText
        android:id="@+id/phoneEditText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Phone Number"
        android:inputType="phone"/>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Gender:" />

    <RadioGroup
        android:id="@+id/genderRadioGroup"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <RadioButton
            android:id="@+id/maleRadioButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Male"/>

        <RadioButton
            android:id="@+id/femaleRadioButton"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Female"/>
    </RadioGroup>

    <CheckBox
        android:id="@+id/termsCheckBox"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="I accept the Terms and Conditions"/>

    <Button
        android:id="@+id/submitButton"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Register"/>

    <TextView
        android:id="@+id/resultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text=""
        android:paddingTop="10dp"/>
    <TextView
        android:id="@+id/titleTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="BSE-05-0218/2022 (Juma Cavin)"
        android:textSize="15sp"
        android:gravity="bottom"
        android:textColor="@color/white"
        android:paddingBottom="10dp"/>

</LinearLayout>

MainActivity.java

package com.example.formreg;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.EditText;
import android.widget.RadioButton;
import android.widget.RadioGroup;
import android.widget.TextView;
import android.widget.Toast;
import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {

    private EditText firstNameEditText, lastNameEditText, emailEditText, phoneEditText;
    private RadioGroup genderRadioGroup;
    private CheckBox termsCheckBox;
    private Button submitButton;
    private TextView resultTextView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        // Initializing UI elements
        firstNameEditText = findViewById(R.id.firstNameEditText);
        lastNameEditText = findViewById(R.id.lastNameEditText);
        emailEditText = findViewById(R.id.emailEditText);
        phoneEditText = findViewById(R.id.phoneEditText);
        genderRadioGroup = findViewById(R.id.genderRadioGroup);
        termsCheckBox = findViewById(R.id.termsCheckBox);
        submitButton = findViewById(R.id.submitButton);
        resultTextView = findViewById(R.id.resultTextView);

        // Button click listener
        submitButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (!termsCheckBox.isChecked()) {
                    Toast.makeText(MainActivity.this, "Please accept terms and conditions", Toast.LENGTH_SHORT).show();
                    return;
                }

                // Get user input
                String firstName = firstNameEditText.getText().toString().trim();
                String lastName = lastNameEditText.getText().toString().trim();
                String email = emailEditText.getText().toString().trim();
                String phone = phoneEditText.getText().toString().trim();

                // Get selected gender
                int selectedId = genderRadioGroup.getCheckedRadioButtonId();
                RadioButton selectedRadioButton = findViewById(selectedId);
                String gender = selectedRadioButton != null ? selectedRadioButton.getText().toString() : "Not Selected";

                // Display the input details
                String result = "First Name: " + firstName + "\nLast Name: " + lastName +
                        "\nEmail: " + email + "\nPhone: " + phone + "\nGender: " + gender;
                resultTextView.setText(result);
                Toast.makeText(MainActivity.this, "Registration Successful", Toast.LENGTH_SHORT).show();
            }
        });
    }
}


background.xml

<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android">
    <gradient android:type="linear" android:angle="100" android:centerColor="#5CEEF1F4"
        android:startColor="#B2ED070D" android:endColor="#D312161A"/>
</shape>

AndroidManifest.xml

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.FormReg"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER"/>
            </intent-filter>
        </activity>
    </application>

</manifest>
