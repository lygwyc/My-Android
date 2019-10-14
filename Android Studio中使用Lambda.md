1. 找到module的build.grade
2. 在android{}中,添加如下代码
	    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }