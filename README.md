# AndroidStudio

<h2>Main Activity Java</h2>

    package com.vibonasi;

    import androidx.appcompat.app.AppCompatActivity;

    import android.os.Bundle;

    import android.os.Bundle;
    import android.widget.TextView;
    import android.view.View;
    import android.widget.Toast;
    import android.widget.EditText;

    import androidx.appcompat.app.AppCompatActivity;
    import androidx.core.content.ContextCompat;

    public class MainActivity extends AppCompatActivity {

        private long fibMinus1 = 0;
        private long fibMinus2 = 1;
        private long currentFib = 0;
        private TextView mShowFibonacci;
        private long i = 0;

        private long n = 0;
        private long limit = 0; // Menyimpan batas Fibonacci yang diinginkan

        private EditText mLimitInput;

                @Override
                protected void onCreate(Bundle savedInstanceState) {
                    super.onCreate(savedInstanceState);
                    setContentView(R.layout.activity_main);
                    mShowFibonacci = (TextView) findViewById(R.id.show_count);
                    mLimitInput = (EditText) findViewById(R.id.limit_input);
                    updateFibonacciDisplay();
                }

                public void countUp(View view) {
                    if (mLimitInput.getText().toString().isEmpty()) {
                        Toast.makeText(this, "Enter the limit first", Toast.LENGTH_SHORT).show();
                        return;
                    }

                    limit = Long.parseLong(mLimitInput.getText().toString());

                    if (n >= limit) {
                        Toast.makeText(this, "Fibonacci limit reached", Toast.LENGTH_SHORT).show();
                        return; // Hentikan perhitungan jika jumlah baris Fibonacci mencapai batas
                    }

                    long newFib = fibMinus1 + fibMinus2;
                    fibMinus2 = fibMinus1;
                    fibMinus1 = newFib;
                    currentFib = newFib;
                    n++; // Inkrementasi jumlah baris Fibonacci

                    updateFibonacciDisplay();
                }



                public void showFibonacci(View view) {
                    Toast toast = Toast.makeText(this, R.string.fibonacci_message, Toast.LENGTH_SHORT);
                    toast.show();
                }

                public void reset(View view) {
                    currentFib = 0;
                    fibMinus2 = 1;
                    fibMinus1 = 0;
                    limit = 0;
                    n = 0;
                    mLimitInput.setText(""); // Mengosongkan input
                    updateFibonacciDisplay();
                }

                private void updateFibonacciDisplay() {
                    if (mShowFibonacci != null) {
                        mShowFibonacci.setText(Long.toString(currentFib));
                        mShowFibonacci.setTextColor(getFibonacciColor());
                    }
                }

                private int getFibonacciColor() {
                    // Gantilah warna berdasarkan nilai Fibonacci
                    i++;
                    if (i % 2 == 0) {
                        return ContextCompat.getColor(this, R.color.colorFibonacciBlue);
                    } else {
                        return ContextCompat.getColor(this, R.color.colorFibonacciGreen);
                    }
                }
            }


<h2>Activity Main XML</h2>

    <?xml version="1.0" encoding="utf-8"?>
    <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".MainActivity">


        <Button
            android:id="@+id/button_fibonacci"
            android:layout_width="242dp"
            android:layout_height="50dp"
            android:layout_marginEnd="8dp"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:background="@color/colorPrimary"
            android:onClick="showFibonacci"
            android:text="@string/button_label_fibonacci"
            android:textColor="@android:color/white"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintHorizontal_bias="0.0"
            app:layout_constraintTop_toTopOf="parent"
            tools:ignore="OnClick" />

        <EditText
            android:id="@+id/limit_input"
            android:layout_width="242dp"
            android:layout_height="50dp"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="8dp"
            android:background="@color/colorPrimary"
            android:textAlignment="center"
            android:textColor="@color/white"
            android:hint="Enter limit"
            android:textColorHint="@color/white"
            android:inputType="number"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="1.0"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />

        <Button
            android:id="@+id/button_count"
            android:layout_width="242dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginEnd="8dp"
            android:layout_marginBottom="4dp"
            android:background="@color/colorPrimary"
            android:onClick="countUp"
            android:text="@string/button_label_count"
            android:textColor="@android:color/white"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="0.0"
            app:layout_constraintStart_toStartOf="parent" />

        <Button
            android:id="@+id/button_reset"
            android:layout_width="242dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginEnd="8dp"
            android:layout_marginBottom="4dp"
            android:background="@color/colorPrimary"
            android:onClick="reset"
            android:text="Reset"
            android:textColor="@android:color/white"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="1.0"
            app:layout_constraintStart_toStartOf="parent"
            tools:ignore="OnClick" />

        <TextView
            android:id="@+id/show_count"
            android:layout_width="0dp"
            android:layout_height="0dp"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="8dp"
            android:layout_marginBottom="8dp"
            android:background="#FFFF00"
            android:gravity="center_vertical"
            android:text="0"
            android:textAlignment="center"
            android:textColor="@color/colorPrimary"
            android:textSize="160sp"
            android:textStyle="bold"
            app:layout_constraintBottom_toTopOf="@+id/button_count"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="0.0"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/button_fibonacci"
            app:layout_constraintVertical_bias="0.0"
            tools:ignore="RtlCompat" />


    </androidx.constraintlayout.widget.ConstraintLayout>

<h2>Color XML</h2>

    <?xml version="1.0" encoding="utf-8"?>
    <resources>
            <color name="black">#FF000000</color>
            <color name="white">#FFFFFFFF</color>
            <color name="blue">#0000FF</color>
            <color name="colorPrimary">#3F51B5</color>
            <color name="colorPrimaryDark">#303F9F</color>
            <color name="colorAccent">#FF4081</color>
            <color name="colorNumber">#69BE28</color>
            <color name="colorFibonacciBlue">#0000FF</color> <!-- Biru -->
            <color name="colorFibonacciGreen">#008000</color> <!-- Hijau -->
    </resources>

<h2>String XML</h2>

    <resources>
            <string name="app_name">FibonacciApp</string>
            <string name="button_label_count">Count</string>
            <string name="button_label_fibonacci">Fibonacci</string>
            <string name="fibonacci_message">Program Fibonacci</string>
    </resources>

Tampilan Web nya

![Screenshot 2023-11-07 092036](https://github.com/zidanperdana/AndroidStudio/assets/116040175/4577c253-9931-407c-b516-ea1fb4798271)
