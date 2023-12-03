---
{"dg-publish":true,"permalink":"/Android异常001/","noteIcon":""}
---

线上bugly报了一个**Could not find Fragment constructor**


看了下默认构造方法如下。
注释中有说明：**强烈建议子类不要有其他带参数的构造函数，因为在重新实例化片段时不会调用这些构造函数**
也就是**重新实例化**的时候只会调用**空参**的构造函数。
```
/**  
 * Default constructor.  <strong>Every</strong> fragment must have an  
 * empty constructor, so it can be instantiated when restoring its * activity's state.  It is strongly recommended that subclasses do not * have other constructors with parameters, since these constructors * will not be called when the fragment is re-instantiated; instead, * arguments can be supplied by the caller with {@link #setArguments}  
 * and later retrieved by the Fragment with {@link #getArguments}.  
 * * <p>Applications should generally not implement a constructor. Prefer  
 * {@link #onAttach(Context)} instead. It is the first place application code can run where  
 * the fragment is ready to be used - the point where the fragment is actually associated with * its context. Some applications may also want to implement {@link #onInflate} to retrieve  
 * attributes from a layout resource, although note this happens when the fragment is attached. */

public Fragment() {  
}
```


看了下Fragment源码，搜到了对应的报错。下面的这个方法被标记位已弃用。

```
/**  
 * Create a new instance of a Fragment with the given class name.  This is * the same as calling its empty constructor, setting the {@link ClassLoader} on the  
 * supplied arguments, then calling {@link #setArguments(Bundle)}.  
 * * @param context The calling context being used to instantiate the fragment.  
 * This is currently just used to get its ClassLoader. * @param fname The class name of the fragment to instantiate.  
 * @param args Bundle of arguments to supply to the fragment, which it  
 * can retrieve with {@link #getArguments()}.  May be null.  
 * @return Returns a new fragment instance.  
 * @throws InstantiationException If there is a failure in instantiating  
 * the given fragment class.  This is a runtime exception; it is not * normally expected to happen. * @deprecated Use {@link FragmentManager#getFragmentFactory()} and  
 * {@link FragmentFactory#instantiate(ClassLoader, String)}, manually calling  
 * {@link #setArguments(Bundle)} on the returned Fragment.  
 */
@Deprecated  
@NonNull
public static Fragment instantiate(@NonNull Context context, @NonNull String fname,  
        @Nullable Bundle args) {  
    try {  
        Class<? extends Fragment> clazz = FragmentFactory.loadFragmentClass(  
                context.getClassLoader(), fname);  
        Fragment f = clazz.getConstructor().newInstance();  
        if (args != null) {  
            args.setClassLoader(f.getClass().getClassLoader());  
            f.setArguments(args);  
        }  
        return f;  
    } catch (java.lang.InstantiationException e) {  
        throw new InstantiationException("Unable to instantiate fragment " + fname  
                + ": make sure class name exists, is public, and has an"  
                + " empty constructor that is public", e);  
    } catch (IllegalAccessException e) {  
        throw new InstantiationException("Unable to instantiate fragment " + fname  
                + ": make sure class name exists, is public, and has an"  
                + " empty constructor that is public", e);  
    } catch (NoSuchMethodException e) {  
        throw new InstantiationException("Unable to instantiate fragment " + fname  
                + ": could not find Fragment constructor", e);  
    } catch (InvocationTargetException e) {  
        throw new InstantiationException("Unable to instantiate fragment " + fname  
                + ": calling Fragment constructor caused an exception", e);  
    }  
}
```


在**try**代码块中可以看到，通过反射，调用了空的构造函数。
```
Fragment f = clazz.getConstructor().newInstance();  
```

## 参考资料
[记一次Could not find Fragment constructor - 简书](https://www.jianshu.com/p/8df58655bfe3)
[android - Could not find Fragment constructor - Stack Overflow](https://stackoverflow.com/questions/51831053/could-not-find-fragment-constructor)