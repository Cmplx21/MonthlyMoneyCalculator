# MonthlyMoneyCalculator

This project uses qmake and is optimized for development in **VSCodium** on Linux, providing full C++ IntelliSense and QML language support.

## **Prerequisites**

Before opening the project, ensure your Linux system has the required build tools and language server dependencies installed.  
**Ubuntu / Debian / Mint:**

```Bash  
sudo apt update  
sudo apt install build-essential qtbase5-dev qtdeclarative5-dev bear clangd libodbc2  
```

*(Note: Use qt6-base-dev and qt6-declarative-dev if using Qt 6)*

**Arch Linux / Manjaro:**

```Bash  
sudo pacman -S base-devel qt5-base qt5-declarative bear clangd unixodbc  
```

## **VSCodium Extensions**

Install the following extensions from the VSCodium marketplace:

1. **clangd** (by LLVM) - *Provides high-performance C++ IntelliSense.*  
2. **Qt** / **QML** (by The Qt Company) - *Provides the qmlls language server.***Note:** If prompted, disable Microsoft's default C/C++ IntelliSense in favor of clangd.

## **Initial Setup**

### **1. Generate the C++ Database**

For clangd to understand Qt headers, we use bear to intercept the compiler and generate a compile_commands.json file.  
Open the integrated terminal (Ctrl + `) and run:

```Bash  
qmake && make clean && bear -- make  
```  
*You must run this command whenever you add new C++ files or Qt modules to your .pro file.*

### **2\. Configure QML Imports**

To enable QML auto-completion, the QML Language Server needs to know where your system stores its QtQuick modules.

1. Run this command in your terminal to find your path:  
```Bash  
qmake -query QT_INSTALL_QML
```

2. Open .vscode/settings.json (create it if it doesn't exist) and add the path to the qmlls arguments:  
```JSON  
{  
    "qt-qml.qmlls.additionalImportPaths": \["/usr/lib/qt/qml"\]
}  
```

3. Restart VSCodium to apply the changes.

