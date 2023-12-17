---
{"dg-publish":true,"permalink":"/200-计算机/260-Android/apk文件命名/","tags":["Android/APK"],"noteIcon":""}
---

## 

```
//修改生成的apk名字  
buildTypes {  
    release {
	    android.applicationVariants.all { variant ->  
	    variant.outputs.all {  
        outputFileName = "Demo_${getGitBranch()}_V${variant.versionName}.${variant.versionCode}_${variant.buildType.name}.apk"  
		    }  
		}
    }
}

```


## 在gradle中获取分支名
```
def getGitBranch() {  
    def stdout = new ByteArrayOutputStream()  
    exec {  
        commandLine 'git', 'rev-parse', '--abbrev-ref', 'HEAD'  
        standardOutput = stdout  
    }  
    return stdout.toString().trim()  
}
```

>[!info]
>`getGitBranch`方法放在app目录下gradle文件中的最外层即可，在需要使用的位置调用即可
## 参考资料