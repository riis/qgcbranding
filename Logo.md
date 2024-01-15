# Logo

*All changes will be made within the custom folder*

## <a name="setup"></a>Setup
When changing the logo, we will need to edit 3 files:
 1. [custom.qrc](qgroundcontrol/custom/custom.qrc)
 2. [CustomPlugin.h](qgroundcontrol/custom/src/CustomPlugin.h) Found in `/src`
 3. [CustomPlugin.cc](qgroundcontrol/custom/src/CustomPlugin.cc) Found in `/src`

Follow the [previous steps setup](ColorScheme.md#setup) to set up the CustomPlugin.h and CustomPlugin.cc. If you have not edited each of these files from the example, you can skip to [Change The Logo](Logo.md#changethelogo).

 - **CustomPlugin.h**
    - Add to the CustomPlugin class `brandImageIndoor` and `brandImageOutdoor`:
        ```
        class CustomPlugin : public QGCCorePlugin
        {
        public:
            CustomPlugin(QGCApplication* app, QGCToolbox *toolbox);
            ~CustomPlugin();

            void paletteOverride (QString colorName, QGCPalette::PaletteColorInfo_t& colorInfo) final;
            QString brandImageIndoor (void) const final;
            QString brandImageOutdoor (void) const final;
        };
        ```
 - **CustomPlugin.cc**
    - Add both functions `brandImageIndoor` and `brandImageOutdoor`:
        ```
        QString CustomPlugin::brandImageIndoor(void) const
        {
        }

        QString CustomPlugin::brandImageOutdoor(void) const
        {
        }
        ```
 - **custom.qrc**
    - Add the following line under `<qresource prefix="custom/img">`:
        ```
        <file alias="CustomAppIcon.png">res/Images/CustomAppIcon.png</file>
        ```

## <a name="changingthelogo"></a>Changing The Logo
 - **custom.qrc**
    - Within `<qresource prefix="custom/img">`, you may find a line like below. Change `res/Images/CustomAppIcon.png` to point to the new location of your file. In most cases, ***it is usually easier to leave the alias name*** as this will be the name QT will use within your project. If you are leaving the alias name, you can proceed to add the function in `CustomPlugin.cc` in the next step; if not, continue following along.
        ```
        <file alias="CustomAppIcon.png">res/Images/CustomAppIcon.png</file>
        ```
 - **CustomPlugin.cc**
    - In the `brandImageIndoor` and `brandImageOutdoor` functions, add a return command with the string of the logo. The string will be **the location of the logo from the project resource directory**. Find this by viewing `custom.qrc` and locating CustomAppIcon or its new alias. The prefix comes from the `<qresource>` tag and the name is its alias. Each function will be the same, but by changing the string, you can choose which logo to use for each mode.  
        - An example from code above would be:
            ```
            QString CustomPlugin::brandImageIndoor(void) const
            {
                return QStringLiteral("/custom/img/CustomAppIcon.png");
            }
            ``` 
            - `/custom/img` comes from its prefix from the `<qresource>` tag
            - `CustomAppIcon.png` comes from its alias name
 - **custom_deploy.pri**
    - Append this to the end of the file to change the name of the logo. Here, make sure to use the name of the file and not the alias:
        ```
        QMAKE_POST_LINK += && $$QMAKE_COPY $$PWD/res/Images/CustomAppIcon.png $$DESTDIR
        ```

---
[Next: Fonts](Fonts.md) \
[Prev: Color Scheme](GettingStarted.md)