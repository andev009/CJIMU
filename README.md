# CJIMU
Android组件化方案(copy from JIMU)

从https://github.com/mqzhangw/JIMU
项目中来，删除了原项目自带的Router，直接使用Arouter,方便直接在项目中使用。
使用时，参考readcomponent即可。

一、Module直接的依赖关系如下：

componentservice-->basicres-->basiclib

app-->componentservice

readcomponent-->componentservice

sharecomponent-->componentservice

二、app如何引用到readcomponent,sharecomponent?

app的build.gradle文件里没有compile project引用readcomponent和sharecomponent，其中的秘密在app的gradle.properties文件。
gradle.properties文件里有debugComponent=onecomponent,com.example.oneonecomponent:oneonecomponent这样的类似字段。
查看build-gradle这个Module里的ComBuild.groovy的compileComponents方法可以知道，如果是使用Module名称的方式，app将使用
project.dependencies.add("compile", project.project(':' + str))，就是类似compile project(':readcomponent')这样。如果
使用带":"的完整路径，将使用project.dependencies.add("compile", str + "-release@aar")，即引用arr文件的方式引入。这样的好处在原作者的文章里
有说明。

三、build-gradle打包发布在本地

具体查看build-gradle的build-gradle最后的代码，当然还得在Project的build-gradle里加上本地maven地址。

 maven {
    url uri('./repo')
}



