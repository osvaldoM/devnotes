## Add pt/ any language to php storm 

- Download the UNICODE version fo the file (possible source [www.winedt.org](http://www.winedt.org/dict.html))
- Remove the header, if any (just to be sure, because I don't know if it is intepreted as content otherwise)
- Convert it from unicode-16 to utf-8 with iconv, e. g.:
- `$ iconv -f UTF-16 -t UTF-8 pt.dic > pt.utf-8.dic`
- Move the converted file back to its original name (or remove the original, just to avoid confusion).
- Move the file to one of the folders scanned by phpstorm( will be at __settings >> editor >> spelling dictionary tab__ )
- Restart phpStorm

### Start android emulator as _.root._ with writable _.fs._
credits to [answer one](https://stackoverflow.com/a/49427040/4043487) and [answer two](https://stackoverflow.com/a/49511666/4043487) 

- properly setup environemnt variables as described in answer two

list devices

    $ emulator -list-avds
    output: Nexus_5X_API_28_x86
    
    $ emulator -avd @Nexus_5X_API_26_x86 -writable-system 
    $ adb root
    $ adb remount
