# mainelements

MainActivity.java:

      package com.example.mainelements;

      import androidx.appcompat.app.AppCompatActivity;

      import android.annotation.SuppressLint;
      import android.os.Bundle;
      import android.util.Log;
      import android.view.View;
      import android.widget.AdapterView;
      import android.widget.ArrayAdapter;
      import android.widget.Button;
      import android.widget.EditText;
      import android.widget.ListView;
      import android.widget.TextView;
      import android.widget.Toast;

      import java.util.ArrayList;
      import java.util.Collections;
      import java.util.HashSet;
      import java.util.Set;


      public class MainActivity extends AppCompatActivity implements View.OnClickListener, AdapterView.OnItemClickListener {

          TextView mainTextView;
          Button mainButton;
          EditText mainEditText;
          ListView mainListView;
          ArrayAdapter mArrayAdapter;
          ArrayList mNameList = new ArrayList();
          Button ok_btn, cnc_btn;


          @Override
          protected void onCreate(Bundle savedInstanceState) {
              super.onCreate(savedInstanceState);
              setContentView(R.layout.activity_main);
              mainTextView = findViewById(R.id.main_textview);
              mainTextView.setText("Set in Java!");
              mainButton = findViewById(R.id.main_button);
              mainEditText = (EditText) findViewById(R.id.main_edittext);
              ok_btn = findViewById(R.id.ok_btn);
              cnc_btn = findViewById(R.id.cnc_btn);
              mainButton.setOnClickListener(this);
              mainListView = findViewById(R.id.main_listview);
              mArrayAdapter = new ArrayAdapter(this,
                      android.R.layout.simple_list_item_1,
                      mNameList);
              mainListView.setAdapter(mArrayAdapter);
              mainListView.setOnItemClickListener(this);
              mainListView.setOnItemLongClickListener(Lng);
              ok_btn.setOnClickListener(oclBtn);
              cnc_btn.setOnClickListener(oclBtn);


          }

          @SuppressLint("SetTextI18n")
          @Override
          public void onClick(View v) {
              mainTextView.setText(mainEditText.getText().toString().trim() + " is learning Android development!"); //trim удаляет пробелы
              mNameList.add(mainEditText.getText().toString().trim());
              mainEditText.setText("");
              Collections.sort(mNameList);  //сортирую
              Set<String> set = new HashSet<>(mNameList); //убираю повторы
              mNameList.clear();
              mNameList.addAll(set);
              mArrayAdapter.notifyDataSetChanged();

          }
          ///
          @SuppressLint("SetTextI18n")
          @Override
          public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
              Log.d("omg android", position + ": " + mNameList.get(position));  // это лог!!!
              mainTextView.setText(mNameList.get(position) + " is learning Android development!");
          }

          AdapterView.OnItemLongClickListener Lng = new AdapterView.OnItemLongClickListener() {
              @Override
              public boolean onItemLongClick(AdapterView<?> parent, View view, int position, long id) {
                  String value = (String) mNameList.get(position);
                  Log.d("omg android", position + ": " + value);  // это лог!!!
                  mNameList.remove(position); //удаляю значение по индексу
                  Toast.makeText(getApplicationContext(), "Удалено: " + value, Toast.LENGTH_LONG).show(); //сообщение об удалении
                  mArrayAdapter.notifyDataSetChanged();
                  return true;
              }
          };

          View.OnClickListener oclBtn = new View.OnClickListener() {
              @Override
              public void onClick(View v) {
                  switch (v.getId()) {
                      case R.id.ok_btn:
                          // кнопка ОК
                          mainTextView.setText("Нажата кнопка ОК");
                          Toast.makeText(getApplicationContext(), "Нажата кнопка ОК", Toast.LENGTH_LONG).show();
                          break;
                      case R.id.cnc_btn:
                          // кнопка Выход
                          finish();
                          System.exit(0);
                  }

              }
          };
      }
      
activity_main.xml:

        <?xml version="1.0" encoding="utf-8"?>
        <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
            xmlns:app="http://schemas.android.com/apk/res-auto"
            xmlns:tools="http://schemas.android.com/tools"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:orientation="vertical"
            tools:context=".MainActivity">

            <TextView
                android:id="@+id/main_textview"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="@string/greetings"
                android:layout_marginTop="20dp"
                android:layout_marginLeft="20dp"
                android:textSize="24dp"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintLeft_toLeftOf="parent"
                app:layout_constraintRight_toRightOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <LinearLayout
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:orientation="horizontal">

                <Button
                    android:id="@+id/main_button"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_marginStart="20dp"
                    android:layout_marginLeft="20dp"
                    android:layout_marginTop="20dp"
                    android:text="@string/button" />

                <EditText
                    android:id="@+id/main_edittext"
                    android:layout_width="100dp"
                    android:layout_height="50dp"
                    android:layout_marginLeft="20dp"
                    android:layout_marginTop="20dp"
                    android:hint="@string/hint" />


            </LinearLayout>

            <ListView
                android:id="@+id/main_listview"
                android:layout_width="match_parent"
                android:layout_height="390dp"
                android:layout_marginTop="20dp"
                android:layout_weight="0"/>

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:orientation="horizontal">

                <Button
                    android:id="@+id/ok_btn"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:text="OK" />

                <Button
                    android:id="@+id/cnc_btn"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:text="Выход" />

            </LinearLayout>





        </LinearLayout>
        
![image](https://user-images.githubusercontent.com/76133815/142426738-54447df2-d1af-4592-a4a0-911fb13ec939.png)

![image](https://user-images.githubusercontent.com/76133815/142426894-fff683a5-197f-4a54-91d8-4d94bde3294d.png)

![image](https://user-images.githubusercontent.com/76133815/142426954-caf37d14-b91e-4f97-acec-cd20892eebc9.png)

