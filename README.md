# yg-react-native-app
It is first react native project of Yuvraj and Ganesh together.

# Create Keystore file
1. Create Keystore file using following command
    ```sh
    keytool -genkey -v -keystore ygapp-release-key.keystore -alias ygapp-key-alias -keyalg RSA -keysize 2048 -validity 10000
    ```
2. Place the ```ygapp-release-key.keystore``` file under the ```android/app directory```.
3. Edit the "android/gradle.properties" and add the following
  ```sh
     MYAPP_RELEASE_STORE_FILE=ygapp-release-key.keystore
     MYAPP_RELEASE_KEY_ALIAS=ygapp-key-alias
     MYAPP_RELEASE_STORE_PASSWORD=ganu123
     MYAPP_RELEASE_KEY_PASSWORD=ganu123
   ```
4. Edit ```android/app/build.gradle``` and ensure the following are there (the sections with signingConfigs may need to be added)
```sh
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                storeFile file(MYAPP_RELEASE_STORE_FILE)
                storePassword MYAPP_RELEASE_STORE_PASSWORD
                keyAlias MYAPP_RELEASE_KEY_ALIAS
                keyPassword MYAPP_RELEASE_KEY_PASSWORD
            }
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```
# APK Generation
* Run command ```cd android``` to navigate to android folder. 
* For Linux run command  ```./gradlew assembleRelease```
* For Windows, run command ```gradlew assembleRelease```
* Find your signed apk (```app-release.apk```) under ```android/app/build/outputs/apk/release```
