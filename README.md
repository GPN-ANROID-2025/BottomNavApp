# DAY 19 : BottomNavApp
# Bottom Navigation in Android using Navigation Component (Java)

## Features
- Bottom Navigation with multiple fragments
- Navigation Component for seamless navigation
- Safe Args for argument passing (optional)
- Back stack management

## Prerequisites
- Android Studio
- Minimum SDK: 21 (Lollipop)
- Gradle configured with AndroidX

## Setup Instructions

### 1. Add Dependencies
Ensure you have the necessary dependencies in your `build.gradle` (Module: app):

```gradle
dependencies {
    implementation 'androidx.navigation:navigation-fragment:2.7.7'
    implementation 'androidx.navigation:navigation-ui:2.7.7'
    implementation 'com.google.android.material:material:1.9.0'
}
```

### 2. Define Navigation Graph
Create a navigation graph (`res/navigation/nav_graph.xml`):

```xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    app:startDestination="@id/homeFragment">

    <fragment
        android:id="@+id/homeFragment"
        android:name="com.example.app.ui.HomeFragment"
        android:label="Home" />

    <fragment
        android:id="@+id/dashboardFragment"
        android:name="com.example.app.ui.DashboardFragment"
        android:label="Dashboard" />

    <fragment
        android:id="@+id/profileFragment"
        android:name="com.example.app.ui.ProfileFragment"
        android:label="Profile" />
</navigation>
```

### 3. Create Bottom Navigation in `activity_main.xml`

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <androidx.fragment.app.FragmentContainerView
        android:id="@+id/nav_host_fragment"
        android:name="androidx.navigation.fragment.NavHostFragment"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:defaultNavHost="true"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toTopOf="@id/bottomNavigationView"
        app:navGraph="@navigation/nav_graph" />

    <com.google.android.material.bottomnavigation.BottomNavigationView
        android:id="@+id/bottomNavigationView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:background="?android:attr/windowBackground"
        app:menu="@menu/bottom_nav_menu"
        app:layout_constraintBottom_toBottomOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

### 4. Define Bottom Navigation Menu (`res/menu/bottom_nav_menu.xml`)

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/homeFragment"
        android:icon="@drawable/ic_home"
        android:title="Home" />
    <item
        android:id="@+id/dashboardFragment"
        android:icon="@drawable/ic_dashboard"
        android:title="Dashboard" />
    <item
        android:id="@+id/profileFragment"
        android:icon="@drawable/ic_profile"
        android:title="Profile" />
</menu>
```

### 5. Setup Navigation in `MainActivity.java`

```java
package com.example.app;

import android.os.Bundle;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.navigation.NavController;
import androidx.navigation.Navigation;
import androidx.navigation.ui.NavigationUI;
import com.google.android.material.bottomnavigation.BottomNavigationView;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        BottomNavigationView bottomNavigationView = findViewById(R.id.bottomNavigationView);
        NavController navController = Navigation.findNavController(this, R.id.nav_host_fragment);
        NavigationUI.setupWithNavController(bottomNavigationView, navController);
    }
}
```



