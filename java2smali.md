If you only have `MainActivity.java` or `MainActivity.class` and want to convert it to `.smali`, follow these steps:  

---

### **🔹 Method 1: Using `dx` + `baksmali` (Recommended)**
#### **Step 1: Compile `MainActivity.java` to `.class`**  
If you have the Java file (`MainActivity.java`), first compile it into a `.class` file:  
```sh
javac -cp android.jar MainActivity.java
```
👉 **Note:** `android.jar` is required for Android-related imports. You can find it in the Android SDK under:
```
$ANDROID_HOME/platforms/android-<VERSION>/android.jar
```

#### **Step 2: Convert `.class` to `.dex`**  
Use the **dx** tool (included in the Android SDK):
```sh
dx --dex --output=classes.dex MainActivity.class
```

#### **Step 3: Convert `.dex` to `.smali` using Baksmali**  
Download [Baksmali](https://github.com/JesusFreke/smali) and run:
```sh
java -jar baksmali.jar d classes.dex -o smali_output
```
Your `.smali` file will be inside `smali_output/your/package/name/MainActivity.smali`.

---

### **🔹 Method 2: Using D8 (Alternative to dx)**
If `dx` is deprecated, use `d8` (from Android SDK):
```sh
d8 --output=classes.dex MainActivity.class
java -jar baksmali.jar d classes.dex -o smali_output
```

---

### **💡 Summary**
1. **Compile** `MainActivity.java` → `MainActivity.class`
2. **Convert** `MainActivity.class` → `classes.dex`
3. **Disassemble** `classes.dex` → `MainActivity.smali`

Now you have your `.smali` file! 🚀 Let me know if you need more help.