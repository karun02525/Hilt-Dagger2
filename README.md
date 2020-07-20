# Hilt-Dagger2

#Hilt — A New Dependency Injection Library for Android

#Hilt the standard way of DI on Android

1. History of DI in Android
2. Introducing Hilt—A Native DI Solution for object creation
3. Terminology 
4. Integration
5. Hilt Setup
6. Hilt With Third-Party Dependencies for mvvm,retrofit,etc
7. Hilt With ViewModels application class esay @

Step: 1 
 build.gradle file  add
 classpath 'com.google.dagger:hilt-android-gradle-plugin:2.28-alpha'

step:2 
app build.gradle
apply plugin: 'dagger.hilt.android.plugin'
kapt 'com.google.dagger:hilt-android-compiler:2.28-alpha'


step:3
Finally,add the required hilt dependencies also inside of this app level build.gradle file.
implementation 'com.google.dagger:hilt-android:2.28-alpha'


step:4 
 Di hilt is now ready to use. We’ll need to start by adding an annotation based to our Application class:
 
 @HiltAndroidApp
 class ABCDemoApp : Application()
 
step:5
now also inject dependencies into your application class.
class SomesClass @Inject constructor() {

    fun doSomething() {
        Log.i("Hilt", "Do something right")
    }
}
Inject  app level class -----------------------
@HiltAndroidApp
class HiltDemoApp : Application() {

    @Inject
    lateinit var somesClass: SomeClass

}

------------------------AndroidEntryPoint ---------------

@AndroidEntryPoint
class MainActivity : AppCompatActivity() {

    @Inject lateinit var someClass: SomesClass

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        somesClass.doSomething()
    }
}

---------------------------Module-----------------------
@Module
@InstallIn(ActivityComponent::class)
object SomeModule {

    @Provides
    fun provideAnotherClass(somessClass: SomeClass) = AnotherClass(someClass)
}

Than @InstallIn
------------------------------------------
The @InstallIn annotation is used by hilt to determine the component that the module is to be installed into. 
In the case here, the ActivityComponent is a part of the hilt APIs and means that our AnotherClass will only be injectable into activity classes.

@InstallIn(ApplicationComponent::class)



thank you!!
 
