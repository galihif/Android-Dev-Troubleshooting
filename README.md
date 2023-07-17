## Daftar Isi
- [Gradle](#gradle)
- [Kotlin](#kotlin-errors)


## Gradle

### Error: Execution failed for task ':app:kaptGenerateStubsDebugKotlin'
- **Detail**:
```
Execution failed for task ':app:kaptGenerateStubsDebugKotlin'.
> 'compileDebugJavaWithJavac' task (current target is 1.8) and 'kaptGenerateStubsDebugKotlin' task (current target is 17) jvm target compatibility should be set to the same Java version.
  Consider using JVM toolchain: https://kotl.in/gradle/jvm/toolchain
```

- **Deskripsi**:
Error saat aplikasi dirun setelah menambahkan dependensi dagger hilt

- **Solusi**: 
Ganti `jvmTarget` dan `sourceCompatibility` `targetCompatibility` ke Java 17

- **Referensi**: 
[Stackoverflow Thread](https://stackoverflow.com/questions/69079963/how-to-set-compilejava-task-11-and-compilekotlin-task-1-8-jvm-target-com)


