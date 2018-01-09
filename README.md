# GitTestGreedDao
GreedDao
mysqltwo中的model为此项目，走了一些弯路，兜兜转转又回来
1.再as中导入相对应的包
compile'org.greenrobot:greendao:3.0.1'
compile'org.greenrobot:greendao-generator:3.0.0'
2.再主项目中在build.gradle中进行配置：添加
apply plugin: 'org.greenrobot.greendao'
buildscript { 
    repositories { 
        mavenCentral()    
}    
dependencies {
    classpath 'org.greenrobot:greendao-gradle-plugin:3.0.0'    
    }
}
然后注意在Model中添加
apply plugin: 'org.greenrobot.greendao'
在项目中才不会报错


3.就是配置路径自定义路径（自动生成代码的路径）
再这里注意有个坑，下面代码是放在Model中的build，而不是放在主项目中，注意在添加一个设置的路径
  //目录设置
    sourceSets {
        main {
            java.srcDirs = ['src/main/java', 'src/main/greendao']
            jniLibs.srcDirs=['./libs']
        }
    }
然后自定义路径
greendao {
    schemaVersion 1
    daoPackage 'src/main/greendao'
    targetGenDir 'src/main/java'
}
4.创建一个实体类
@Entity
public class User {
    @Id 
    private Long id; 
    private String name; 
    @Transient 
    private int tempUsageCount; // not persisted  
}
5.编译即可，自动生成代码
6.此项目中的demo诠释一切
