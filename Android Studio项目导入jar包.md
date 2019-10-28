# Android Studio项目导入jar包
#github
- - - -
1.  找到**module**的build.grade
2. 在**android{}中**,添加如下代码
```
android {
      compileOptions {
          sourceCompatibility JavaVersion.VERSION_1_8
          targetCompatibility JavaVersion.VERSION_1_8
      }
  } 
```
3. 成功