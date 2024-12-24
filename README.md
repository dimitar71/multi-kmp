# multi-kmp
Using multiple KMP library modules to add them as dependencies

## Structure
- `library-base` - library module
    - contains just `com.example.library.base.Base` interface
    - `library:library-base:1.0.0`
- `library-data` - library module
  - contains `com.example.library.data.DataBase` which extends `Base`
  - adds `library-base` via `api(projects.libraryBase)`
  - `library:library-data:1.0.0`
- `library-multi` - library module
  - contains `com.example.library.multi.MultiBase` which extends `DataBase`
  - adds `library-data` via `api(projects.libraryData)`
  - `library:library-multi:1.0.0`
- `refapp` - Android app
    - uses `library:library-multi:1.0.0` dependency

## Problems:
- albeit `api()` is used, code is not embed
- when starting `refapp`, the error below is shown

```kotlin
Execution failed for task ':refapp:checkDebugAarMetadata'.
> Could not resolve all files for configuration ':refapp:debugRuntimeClasspath'.
   > Could not resolve all dependencies for configuration ':refapp:debugRuntimeClasspath'.
      > Could not find library:library-data:1.0.0.
        Searched in the following locations:
          - https://dl.google.com/dl/android/maven2/library/library-data/1.0.0/library-data-1.0.0.pom
          - file:/Users/T936672/.m2/repository/library/library-data/1.0.0/library-data-1.0.0.pom
          - https://repo.maven.apache.org/maven2/library/library-data/1.0.0/library-data-1.0.0.pom
        Required by:
            project :refapp > library:library-multi-android:1.0.0


```