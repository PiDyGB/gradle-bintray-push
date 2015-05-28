gradle-bintray-push
===============

## Usage

### 1. Have a working Gradle build
This is upto you.

### 2. Have a working Bintray repository
This is also upto you and remender to setup you GPG sign if you want to sync with maven central (you can use Bintray's public /private key pair).

### 3. Create project root gradle.properties
You may already have this file, in which case just edit the original. This file should contain the POM values which are common to all of your sub-project (if you have any). For instance, here's [android-gestureutilities's](https://github.com/PiDyGB/android-gestureutilities):

```properties
POM_DESCRIPTION=An implementation of swipe to dismiss gesture for any Android View and a touch listener for hide view when a RecyclerView scroll
LICENSE_NAME=The Apache Software License, Version 2.0
LICENSE_URL=http://www.apache.org/licenses/LICENSE-2.0.txt
POM_URL=https://github.com/PiDyGB/android-gestureutilities
SCM_URL=https://github.com/PiDyGB/android-gestureutilities
SCM_CONNECTION=scm:git@github.com:PiDyGB/android-gestureutilities.git
SCM_DEV_CONNECTION=scm:git@github.com:PiDyGB/android-gestureutilities.git
SCM_ISSUETRACKER=https://github.com/PiDyGB/android-gestureutilities/issues
DEVELOPER_ID=PiDyGB
DEVELOPER_NAME=Giuseppe Buzzanca
DEVELOPER_EMAIL=giuseppebuzzanca@gmail.com
```

### 4. Create gradle.properties in each sub-project
The values in this file are specific to the sub-project (and override those in the root `gradle.properties`). In this example, this is just the name, artifactId and packaging type:

```properties
VERSION_NAME=v1.0.0
GROUP=com.github.pidygb.gestureutilities
PACKAGE_NAME=android-gestureutilities
POM_PACKAGING=aar
BINTRAY_REPOSITORY=android
LABELS=['aar', 'android']
```

The `PACKAGE_NAME` and `BINTRAY_REPOSITORY` are important, the first one represent the name of the package that "must exist" into the second one.

### 5. Add dependencies

Add the following dependencies to the project root build.gradle

```properties
classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.1'
classpath 'com.github.dcendents:android-maven-plugin:1.2'
```

### 6. Call the script from each sub-modules build.gradle

Add the following at the end of each `build.gradle` that you wish to upload:

```groovy
apply from: 'https://raw.githubusercontent.com/PiDyGB/gradle-bintray-push/master/gradle-bintray-push.gradle'
```

### 7. Build and Push

You can now build and push:

```bash
$ gradlew bintrayUpload
```

## License

    Copyright 2015 Giuseppe Buzzanca

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
