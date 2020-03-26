# NavigationDrawer
How to apply Navigation Drawer in your app

 1.Make a fragment for main activity
 2.Inflate it and return in the same fragment.kt file in onCreateView .
 3. use Data Binding.
 4.Add the those fragments to the navigation graph to show in the drawer.
 5. Create the navDrawer menu with those fragments menu items.
 6.Then, we have to create the navdrawer_menu. Add two menu items by dragging menu items into the component tree.
   The first item should have the id of those Fragment, the @string(title) and &drawable(icon).
7. Add the DrawerLayout into the activity_main layout containing the LinearLayout and navHostFragment

It should be just inside of the Data Binding layout tag.

<layout xmlns:android="http://schemas.android.com/apk/res/android"
   xmlns:app="http://schemas.android.com/apk/res-auto">

   <androidx.drawerlayout.widget.DrawerLayout
       android:id="@+id/drawerLayout"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
   >  
   
8.Add the NavigationView at the bottom of the the DrawerLayout

Now add the NavigationView at the bottom of the DrawerLayout.

<com.google.android.material.navigation.NavigationView
   android:id="@+id/navView"
   android:layout_width="wrap_content"
   android:layout_height="match_parent"
   android:layout_gravity="start"
   app:menu="@menu/navdrawer_menu" />
   
9.Move to MainActivity and add private lateinit vars for drawerLayout and appBarConfiguration.
private lateinit var drawerLayout: DrawerLayout
private lateinit var appBarConfiguration: AppBarConfiguration

10. Initialize the drawerLayout from the binding variable.
drawerLayout = binding.drawerLayout   

11.Add the DrawerLayout as the third parameter to setupActionBarWithNavController

Add the drawerLayout as the third parameter to the setupActionBarWithNavController method. NOTE: If Android Studio displays an error, you may have to rebuild your project before using the binding variable.

drawerLayout = binding.drawerLayout
val navController = this.findNavController(R.id.myNavHostFragment)
NavigationUI.setupActionBarWithNavController(this, navController, drawerLayout)

12.Create an appBarConfiguration with the navController.graph and drawerLayout
appBarConfiguration = AppBarConfiguration(navController.graph, drawerLayout)

13. Hook up the navigation UI up to the navigation view.
And then hook the navigation UI up to the navigation view by calling setupWithNavController.
NavigationUI.setupWithNavController(binding.navView, navController)   

14.In onSupportNavigateUp, replace navController.navigateUp with NavigationUI.navigateUp with drawerLayout as parameter

And, in our onSupportNavigateUp activity method, we need to use NavigationUI.navigateUp with the drawerLayout as a parameter instead of navController.navigateUp.

override fun onSupportNavigateUp(): Boolean {
   val navController = this.findNavController(R.id.myNavHostFragment)
   return NavigationUI.navigateUp(drawerLayout, navController)
}
And that’s it. We have a working app drawer. Let's add the navigation header to finish things.

15.In the NavigationView at the bottom of the DrawerLayout within the main activity layout file, add the nav header as the headerLayout.

<com.google.android.material.navigation.NavigationView
   android:id="@+id/navView"
   android:layout_width="wrap_content"
   android:layout_height="match_parent"
   android:layout_gravity="start"
   app:headerLayout="@layout/nav_header"
   app:menu="@menu/navdrawer_menu" />

