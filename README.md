# Android-Emulator-Detection
Emulator detection is a technique used to determine if a software application or operating system is running on an emulator rather than on original hardware


# Code 

```kotlin
private fun checkBuildConfig(): Boolean {
     var isEmulator = (Build.MANUFACTURER.contains("Genymotion")
             || Build.MODEL.contains("google_sdk")
             || Build.MODEL.toLowerCase().contains("droid4x")
             || Build.MODEL.contains("Emulator")
             || Build.MODEL.contains("Android SDK built for x86")
             || Build.HARDWARE == "goldfish"
             || Build.HARDWARE == "vbox86"
             || Build.HARDWARE.toLowerCase().contains("nox")
             || Build.FINGERPRINT.startsWith("generic")
             || Build.PRODUCT == "sdk"
             || Build.PRODUCT == "google_sdk"
             || Build.PRODUCT == "sdk_x86"
             || Build.PRODUCT == "vbox86p"
             || Build.PRODUCT.toLowerCase().contains("nox")
             || Build.BOARD.toLowerCase().contains("nox")
             || (Build.BRAND.startsWith("generic") && Build.DEVICE.startsWith("generic")))
     return isEmulator
}
