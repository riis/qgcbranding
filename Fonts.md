# Fonts

*All changes will be made within the custom folder except if following the [more involved way](Fonts.md#hardermethod)*

## <a name="changingthefont"></a>Changing The Font
To change the font, you will need to edit 2 files:
 1. [custom.qrc](res/example/custom.qrc)
 2. [qgcresources.exclusion](res/example/qgcresources.exclusion)

 - **qgcresources.exclusion**
    - This file excludes any file listed from the project, allowing replacement with `custom.qrc`. Adding the lines below will exclude all current fonts. `opensans` is used for *text in most languages* and `NanumGothic` for *Korean language text*. All fonts and resources can be found within `qgcresources.qrc`, and any line can be copied and pasted into the exclusion file.

    ```
    <file alias="opensans">resources/fonts/OpenSans-Regular.ttf</file>
    <file alias="opensans-demibold">resources/fonts/OpenSans-Semibold.ttf</file>
    <file alias="NanumGothic-Regular">resources/fonts/NanumGothic-Regular.ttf</file>
    <file alias="NanumGothic-Bold">resources/fonts/NanumGothic-Bold.ttf</file>
    ```

**There are 2 ways to edit `custom.qrc`: The [easy way](Fonts.md#easymethod) or the [more involved way](Fonts.md#hardermethod)**
### <a name="easymethod"></a>Easy Method
In this method, we replace the new font with our current font. The project will continue to reference `opensans`, but it will use our new fonts.

 - **custom.qrc**
    - Add the qresource with a prefix "/fonts" and add the file location to each line without changing the alias name. Use the file location within the custom folder.
        ```
        <qresource prefix="/fonts">
            <file alias="opensans">res/fonts/TextFont-Regular.ttf</file>
            <file alias="opensans-demibold">res/fonts/TextFont-Semibold.ttf</file>
            <file alias="NanumGothic-Regular">res/fonts/Korean-Regular.ttf</file>
            <file alias="NanumGothic-Bold">res/fonts/Korean-Bold.ttf</file>
        </qresource>
        ```

### <a name="hardermethod"></a>More Involved Method
In this method, we replace the new font with our current font and change its name. The project will recognize it as its new font name.

 - **custom.qrc**
    - Add the qresource with a prefix "/fonts" and add the file location for each line, changing the alias name as needed. Remember, use the file location within the custom folder.
        ```
	    <qresource prefix="/fonts">
		    <file alias="TextFont">res/fonts/TextFont.ttf</file>
		    <file alias="TextFont-demibold">res/fonts/TextFont-Semibold.ttf</file>
		    <file alias="Korean-Regular">res/fonts/Korean-Regular.ttf</file>
		    <file alias="Korean-Bold">res/fonts/Korean-Bold.ttf</file>
	    </qresource>
        ```

**Make sure to run `updateqrc.py` after making any changes to the exclusion file or custom file to apply changes**

 - **src/QGCApplication.cc**
    - Located in the root directory of QGroundControl and within the src folder, QGCApplication.cc can be found. Change the lines below to your new font names:
  
        ```
        if(QFontDatabase::addApplicationFont(":/fonts/TextFont") < 0) {
            qWarning() << "Could not load /fonts/TextFont font";
        }
        if(QFontDatabase::addApplicationFont(":/fonts/TextFont-demibold") < 0) {
            qWarning() << "Could not load /fonts/TextFont-demibold font";
        }
        ```
        
        ```
        if(_locale == QLocale::Korean) {
            qCDebug(LocalizationLog) << "Loading Korean fonts" << _locale.name();
            if(QFontDatabase::addApplicationFont(":/fonts/Korean-Regular") < 0) {
                qCWarning(LocalizationLog) << "Could not load /fonts/Korean-Regular font";
            }
            if(QFontDatabase::addApplicationFont(":/fonts/Korean-Bold") < 0) {
                qCWarning(LocalizationLog) << "Could not load /fonts/Korean-Bold font";
            }
        }
        ```


---
[Prev: Logo](Logo.md)