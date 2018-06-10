# Android 2D Game Development Notes 6

## How to load DEX files

```java
import java.io.File;
import dalvik.system.DexClassLoader;

File dexPath = new File(getCacheDir(), "lib.dex");
File dexOptimizedPath = new File(getCacheDir(), "dex");
// delete dirs to reload
dexOptimizedPath.mkdirs();
DexClassLoader loader = new DexClassLoader(
    dexPath.getAbsolutePath(),
    dexOptimizedPath.getAbsolutePath(),
    null,
    getClassLoader()
  );
System.out.println(loader.loadClass("com.lib.TheLib").newInstance());
```

## How to delete a directory recursively

```java
import java.io.File;

void delete(File file) {
  File[] contents = file.listFiles();
  if (contents != null) {
    for (File f : contents) {
      delete(f);
    }
  }
  file.delete();
}
```
