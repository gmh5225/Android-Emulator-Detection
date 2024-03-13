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
private val GENY_FILES = arrayOf(
        "/dev/socket/genyd",
        "/dev/socket/baseband_genyd"
)
private val PIPES = arrayOf(
        "/dev/socket/qemud",
        "/dev/qemu_pipe"
)
private val X86_FILES = arrayOf(
        "ueventd.android_x86.rc",
        "x86.prop",
        "ueventd.ttVM_x86.rc",
        "init.ttVM_x86.rc",
        "fstab.ttVM_x86",
        "fstab.vbox86",
        "init.vbox86.rc",
        "ueventd.vbox86.rc"
)
private val ANDY_FILES = arrayOf(
        "fstab.andy",
        "ueventd.andy.rc"
)
private val NOX_FILES = arrayOf(
        "fstab.nox",
        "init.nox.rc",
        "ueventd.nox.rc"
)
fun checkFiles(targets: Array<String>): Boolean {
    for (pipe in targets) {
        val file = File(pipe)
        if (file.exists()) {
            return true
        }
    }
    return false
}
fun checkEmulatorFiles():Boolean {
    return (checkFiles(GENY_FILES)
            || checkFiles(ANDY_FILES)
            || checkFiles(NOX_FILES)
            || checkFiles(X86_FILES)
            || checkFiles(PIPES))
}
