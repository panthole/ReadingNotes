###下载tensorflow

	git clone --recurse-submodules  https://github.com/tensorflow/tensorflow.git

###下载NDK，最好r12b版本
###下载SDK
###下载chocolatey，在cmd中复制下面一段回车
	@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
###下载bazel
	choco install bazel

###配置WORKSPACE文件
	# Uncomment and update the paths in these entries to build the Android demo.
	android_sdk_repository(
    name = "androidsdk",
    api_level = 23,
    # Ensure that you have the build_tools_version below installed in the 
    # SDK manager as it updates periodically.
    build_tools_version = "25.0.2",
    # Replace with path to Android SDK on your system
    path = "D:\Dev\Android-Sdk",
	)

	# Android NDK r12b is recommended (higher may cause issues with Bazel)
	android_ndk_repository(
    name="androidndk",
    path="D:\Dev\Android-Sdk\ndk-bundle",
    # This needs to be 14 or higher to compile TensorFlow. 
    # Note that the NDK version is not the API level.
    api_level=14)

#
	bazel build -c opt //tensorflow/contrib/android:libtensorflow_inference.so --crosstool_top=//external:android/crosstool --host_crosstool_top=@bazel_tools//tools/cpp:toolchain --cpu=armeabi-v7a