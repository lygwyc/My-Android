1. 找到**module**的build.grade
2. 在**android{}**中,添加如下代码
      ``` java
        compileOptions {
            sourceCompatibility JavaVersion.VERSION_1_8
            targetCompatibility JavaVersion.VERSION_1_8
        }
	    