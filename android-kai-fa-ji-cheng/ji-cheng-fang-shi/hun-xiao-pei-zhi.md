# 混淆配置

## 混淆配置

如果你的apk最终会经过代码混淆，请在proguard配置文件中加入以下代码:

```groovy
-keepclassmembers class * implements java.io.Serializable {
    private static final java.io.ObjectStreamField[] serialPersistentFields;
    private void writeObject(java.io.ObjectOutputStream);
    private void readObject(java.io.ObjectInputStream);
    java.lang.Object writeReplace();
    java.lang.Object readResolve();
}

-keep class com.android.vending.billing.**
```

{% hint style="info" %}
 如果在运行过程中出现异常：ClassNotFoundException，可能造成原因是由于代码混淆。
{% endhint %}



