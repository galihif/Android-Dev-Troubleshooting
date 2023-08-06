## Daftar Isi
- [Android Studio](#android-studio)
- [Gradle](#gradle)
- [Jetpack Compose](#jetpack-compose)

## Android Studio

### Change Android Studio Project and Package name

- **Change App/Project Name** :
  - Go to `settings.gradle` and rename `rootProject.name`
  - Go to `strings.xml` and rename `@string/app_name`
  - Change Theme Name in `themes.xml`
  - `Gradle Sync`, Clean and rebuild project
- **Change Package Name** :
  - Go to `build.gradle` module level, rename `namespace` and `applicationId`
  - Run gradle `sync`
  - In the project tab, Tree Appearance > uncheck `Compact Middle Packages`
  - Right click on package name folder > Refactor > Rename > Do Refactor
  - Clean and rebuild project
- **Reference** :
[Stackoverflow Thread](https://stackoverflow.com/questions/16804093/rename-package-in-android-studio/29092698#29092698)

## Gradle

### Error: Execution failed for task ':app:kaptGenerateStubsDebugKotlin'
- **Issue**:
After adding hilt dependencies, it's successfully synced but failed to run and throw error
```
Execution failed for task ':app:kaptGenerateStubsDebugKotlin'.
> 'compileDebugJavaWithJavac' task (current target is 1.8) and 'kaptGenerateStubsDebugKotlin' task (current target is 17) jvm target compatibility should be set to the same Java version.
  Consider using JVM toolchain: https://kotl.in/gradle/jvm/toolchain
```

- **Solution**: 
Ganti `jvmTarget` dan `sourceCompatibility` `targetCompatibility` ke Java 17

- **Reference**: 
[Stackoverflow Thread](https://stackoverflow.com/questions/69079963/how-to-set-compilejava-task-11-and-compilekotlin-task-1-8-jvm-target-com)

## Jetpack Compose

### Layout: A child in row not fill max height to its parent 
- **Issue**:
The card already set to `fillMaxHeight` but not showing on row.
<img width="241" alt="image" src="https://github.com/galihif/Android-Dev-Troubleshooting/assets/61546756/35271203-381b-4513-993a-236844e8db05">

- **Solution**:
In the parent add the `.height(IntrinsicSize.Min)` to its modifier
<img width="243" alt="image" src="https://github.com/galihif/Android-Dev-Troubleshooting/assets/61546756/16d2a0dc-d61a-4201-8f32-a895d112c073">

```
Row(
    modifier = Modifier.fillMaxWidth().height(IntrinsicSize.Min)
) {
    Child1(
        modifier = Modifier
            .fillMaxHeight()
            .width(100.dp),
    ) {}
    Child2(
        modifier = Modifier
            .fillMaxWidth()
            .weight(1f)
    ) {...}
}
```

- **Reference**: 
[Stackoverflow Thread](https://stackoverflow.com/questions/67677125/fill-height-for-child-in-row)

### Navigation : Popbackstack multiple screens

- **Issue**:

In a navigation flow where there are multiple screens (e.g., Screen A > Screen B > Screen C), there may be situations where you want to pop multiple screens off the back stack at once. For example, you might want to navigate directly from Screen C back to Screen A, skipping Screen B. Using the default `NavController.popBackStack()` method will only pop one screen at a time, which may not be sufficient for your use case.

- **Solution**:
  
A solution to this problem is using the overloaded `NavController.popBackStack(route: String, inclusive: Boolean)` method, which pops all destinations up to a specified one.

Here's how you can use this function in your code:

```
val navController = rememberNavController()
Button(onClick = {
    navController.popBackStack(route = "A", inclusive = false)
}) {
    Text(text = "Back to Screen A")
}
```

This code will pop the back stack until it reaches Screen A, but Screen A will remain in the stack, i.e., it will be the current destination after the operation.
If `inclusive` is set to **false** (which is the default), then all destinations up to but not including the one associated with the given route (in this case A) will be popped.
If `inclusive` is set to **true**, then all destinations up to and including the one associated with the given route will be popped.

Remember, `popBackStack()` returns a boolean indicating whether it successfully popped the back stack. You should handle the case where it returns `false`, which indicates that it could not find a destination associated with the given `route` in the back stack.

- **Reference**: 
[Stackoverflow Thread](https://stackoverflow.com/questions/69415996/jetpack-compose-navcontroller-popbackstack-multiple-pages)

### Recomposition : Updating Value Not Reflected in Composable

- **Issue** :

In a Jetpack Compose project, a value updated in the ViewModel might not be reflected in a specific composable. Despite the value being changed and observed within the ViewModel, the composable may still show the initial or default value. This can lead to inconsistencies in the UI where the displayed information does not match the actual data state.

- **Solution** :
A solution to this problem is using the `key` function in Jetpack Compose, which can be used to force recomposition of a specific composable based on a particular value. Whenever the value passed to the `key` function changes, the composable within the key block will recompose, ensuring that the UI correctly reflects the updated value.

Here's how you can use this approach in your code:

```
@Composable
fun MyComposable(user: User) {
    val score = calculateScore(user)

    // This will force recomposition of the inner content whenever the score changes
    key(score) {
        Text("User score: $score")
        // other composables that depend on the score
    }
}
```

By leveraging the key function, developers can ensure that the UI updates in response to specific data changes, resolving the issue where certain composables were not reflecting the updated value when expected. This leads to a more predictable and responsive user experience.

- **References** : ChatGPT4
