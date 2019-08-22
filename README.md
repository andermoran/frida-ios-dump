**python 3 please checkout 3.x branch**

# frida-ios-dump
Pull a decrypted IPA from a jailbroken device. Many times in iOS reverse engineering, we only need the decrypted binary, so why dump the entire decrypted .ipa? The primary feature of this fork is that we have the option to only get the decrypted binary instead of the whole decrypted .ipa. Also, do not modify dump.py to put your password in like you do on the master branch of frida-ios-dump, simply pass your password in through the command line with the `-pass` flag.

## Usage

 1. Install [frida](http://www.frida.re/) on device
 2. `sudo pip install -r requirements.txt --upgrade` (Python 2.7)
 3. Run usbmuxd/iproxy SSH forwarding over USB (Default 2222 -> 22). e.g. `iproxy 2222 22`
 4. Run ./dump.py `Display name` or `Bundle identifier`
 5. There are also other flags to specify the preferred file returned, user, password, port, host, and output path
   * `-b` if you only want the decrypted binary, do not use this flag if you want the entire decrypted .ipa
   * `-n` or `--output-path` where we are dumping the decrypted .ipa or binary
     * If no flag is provided, the output path will be the current working directory
   * `-u` or `--user` the user used for SSH/SCP
     * If no flag is provided, the user will be `root`
   * `-pass` or `--password` the password used for SSH/SCP
     * If no flag is provided, the password will be `alpine`
   * `-p` or `--port` the port used for SSH/SCP
     * If no flag is provided, the port will be `2222`
   * `-host` or `--host` the host used for SSH/SCP
      * If no flag is provided, the user will be `localhost`
   * Example: `./dump.py Aftenposten -b --user root --password alpine --host localhost --port 2222 --output-path /Users/johndoe/Downloads`

For SSH/SCP make sure you have your public key added to the target device's ~/.ssh/authorized_keys file.

```
./dump.py Aftenposten
Start the target app Aftenposten
Dumping Aftenposten to /var/folders/wn/9v1hs8ds6nv_xj7g95zxyl140000gn/T
start dump /var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/AftenpostenApp
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/AFNetworking.framework/AFNetworking
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/ATInternet_iOS_ObjC_SDK.framework/ATInternet_iOS_ObjC_SDK
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/SPTEventCollector.framework/SPTEventCollector
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/SPiDSDK.framework/SPiDSDK
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCore.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreData.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreGraphics.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreImage.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftCoreLocation.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftDarwin.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftDispatch.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftFoundation.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftObjectiveC.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftQuartzCore.dylib
start dump /private/var/containers/Bundle/Application/66423A80-0AFE-471C-BC9B-B571107D3C27/AftenpostenApp.app/Frameworks/libswiftUIKit.dylib
Generating Aftenposten.ipa

Done.
```

Congratulations!!! You've got a decrypted IPA file.

Drag to [MonkeyDev](https://github.com/AloneMonkey/MonkeyDev), Happy hacking!

### issues

If the following error occurs:

* causes device to reboot
* lost connection
* unexpected error while probing dyld of target process

please open the application before dumping.


