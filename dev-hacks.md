## Add pt/ any language to php storm 

- Download the UNICODE version fo the file (possible source [www.winedt.org](http://www.winedt.org/dict.html))
- Remove the header, if any (just to be sure, because I don't know if it is intepreted as content otherwise)
- Convert it from unicode-16 to utf-8 with iconv, e. g.:
- `$ iconv -f UTF-16 -t UTF-8 pt.dic > pt.utf-8.dic`
- Move the converted file back to its original name (or remove the original, just to avoid confusion).
- Move the file to one of the folders scanned by phpstorm( will be at __settings >> editor >> spelling dictionary tab__ )
- Restart phpStorm
