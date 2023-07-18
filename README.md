## Daftar Isi
- [Gradle](#gradle)
- [Jetpack Compose](#jetpack-compose)


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



