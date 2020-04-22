# ViewModel_LiveData_Kotlin_Sample
This Sample aim to understand the concepts of two main Jetpack components - ViewModel and LiveData with Kotlin as Programming language. Please read the ReadMe file for the theoretical description.

<h2>ViewModel</h2>
<p><b> ViewModel is a class responsible for preparing and managing data to UI components(Activity or fragments) and also survives in orientation changes.</b></p>
<p><b> It remains alive until its reference scope is alive.</b></p>
<p><b> It should never access your view hierarchy or hold any reference of UI.</b></p>
<p><b> It was announced in google IO 2017.</b></p>
<p><b> Another important use of ViewModel is that it pcan be used a communication layer between different fragments of activity so that
they nether need to talk to other fragment directly. </b></p>
<p><b> OnCleared() method is last method called inside ViewModel before its destruction.Useful if you want to clear some references in order to prevent memory leak.</p></p>
<p><b> If you want context inside your Viewmodel then use AndroidViewModel inside it as it have default application context inside it. </b></p>

<p><b> * Disadvantage of ViewModel over SavedInstanceState is It do not survice on process kill due to low memory but SavedInstanceState does. </b></p>

<h2> Implementation of ViewModel </h2>
<p><b> Create a class and Extends a ViewModel class inside it. </b></p>
<pre><code>
class MainViewModel : ViewModel() {

}
</pre></code>
<p><b> Create a ViewModelProvider instance inside your UI referencing that class which extends ViewModel class.Earlier it was ViewModelProviders but it is deprecated now. </b></p>
<pre><code>
mainViewModel = ViewModelProvider(this).get(MainViewModel::class.java)
</code></pre>

<h2> ViewModelProvider</h2>
<p><b> An utility class that provides ViewModel for a scope.</p></b>
<p><b> ViewModelProvider.Factory is use to create a custom constructor inside ViewModel.</b></p>
<pre><code>
class MyViewModelFactory(val arg:Int) :ViewModelProvider.Factory
{
    override fun <T : ViewModel?> create(modelClass: Class<T>): T {
        return modelClass.getConstructor(Int::class.java).newInstance(arg)
    }
}

mainViewModel = ViewModelProvider(this,MyViewModelFactory(20)).get(MainViewModel::class.java)
</code></pre>
<h2> How ViewModel survives rotation changes </h2>
<p><b>When you write ViewModelProvider(this).get(MainViewModel::class.java) then ViewModelProvider map the ViewModel instance with "this" referencing
UI component. For the first time it creates an instance of ViewModel then when you rotate the device then it uses the same instance of ViewModel
a Singleton pattern is internally used for saving the state of ViewModel.</b></p>

