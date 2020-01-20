[TOC]

## 基本概念

​	Maven 是一个项目管理工具，它包含了一个项目对象模 型 (POM：Project Object Model)，一组标准集合，一个项目生命周期(Project Lifecycle)，一个依赖管 理系统(Dependency Management System)，和用来运行定义在生命周期阶段(phase)中插件(plugin)目标 (goal)的逻辑。

### Maven的目录结构

bin: 存放了 maven 的命令

boot: 存放了一些 maven 本身的引导程序，如类加载器等 

conf: 存放了 maven 的一些配置文件，如 setting.xml 文件 

lib: 存放了 maven 本身运行所需的一些 jar 包 

### 仓库种类

- 本地仓库 ：用来存储从远程仓库或中央仓库下载的插件和 jar 包，项目使用一些插件或 jar 包， 优先从本地仓库查找  
- 远程仓库(私服)：如果本地需要插件或者 jar 包，本地仓库没有，默认去远程仓库下载。 远程仓库可以在互联网内也可以在局域网内。
-  中央仓库 ：在 maven 软件中内置一个远程仓库地址 http://repo1.maven.org/maven2 ，它是中央仓库，服务于整个互联网，它是由 Maven 团队自己维护，里面存储了非常全的 jar 包，它包含了世界上大部分流行的开源项目构件

## 依赖管理

​	maven 工程中不直接将 jar 包导入到工程中，而是通过在 pom.xml 文件中添加所需 jar 包的坐标，这样就很好的避免了 jar 直接引入进来，在需要用到 jar 包的时候，只要查找 pom.xml 文 件，再通过 pom.xml 文件中的坐标，到一个专门用于”存放 jar 包的仓库”(maven 仓库)中根据坐标从 而找到这些 jar 包，再把这些 jar 包拿去运行。 

### Maven 项目目录结构

- src/main/java: 存放项目的.java 文件 
- src/main/resource: 存放项目资源文件，如 spring配置文件 
- src/test/java: 存放所有单元测试.java 文件，如 JUnit 测试类
- src/test/resource: 测试资源文件
- target: 项目输出位置，编译后的class 文件会输出到此目录 
- pom.xml: maven 项目核心配置文件 

## Maven的常用命令

- **clean** : 清理命令, 执行 clean 会删除 target 目录及内容
- **validate** : 验证命令, 验证项目是正确的, 所有必要的信息可用
- **compile** : 编译命令，作用是将 src/main/java 下的文件编译为 class 文件输出到 target 目录下
- **test** : 测试命令, 会执行src/test/java下的单元测试类。 
- **package** : 打包命令, 根据pom.xml配置对于 java 工程执行 package 打成 jar 包，对于web 工程打成war 包
- **verify** : 校验命令, 运行任何检查以验证包是否有效并符合质量标准
- **install** : 安装命令, 执行 install 将 maven 打成 jar 包或 war 包发布到本地仓库
- **site** : 站点命令, 生成项目的站点文档
- **deploy** : 部署命令, 在集成或发布环境中完成, 将最终软件包复制到远程存储库中

## Maven的生命周期

- 清理生命周期(clean) : 
  - 预清洁(pre-clean): 执行实际项目清理之前所需流程
  - **清洁(clean)**  : 删除以前构建生成的所有文件
  - 后清洁(post-clean): 执行完成项目清理所需的流程
- 默认生命周期(default): 
  - **验证(validate)** : 验证项目是正确的, 所有必要的信息可用
  - 初始化(initialize): 初始化构建状态, 例如设置属性或创建目录
  - 产生来源(generate-sources): 生成包含在编译中的任何源代码
  - 流程源(process-sources): 处理源代码, 例如过滤任何值
  - 生成资源(generate-resources): 生成包含在包中的资源
  - 流程资源(process- resource): 将资源复制并处理到目标目录中, 准备打包
  - **编译(compile)** : 编译项目的源代码
  - 工艺类(process-classes): 从编译后处理生成的文件, 例如对Java类进行字节码增强
  - 生成测试来源(generate-test-sources): 生成包含在编译中的任何测试源代码
  - 流程测试来源(process-test-sources): 处理测试源代码, 例如过滤任何值
  - 生成测试资源(generate-test-resources): 创建测试资源
  - 流程测试资源(process-test-resources): 将资源复制并处理到测试目标目录中
  - 测试编译(test-compile): 将测试源代码编译到测试目标目录中
  - 流程检验类(process-test-classes): 从测试编译中处理生成的文件, 例如对Java类进行字节码增强
  - **测试(test)** : 使用合适的单元测试框架运行测试, 这些测试不应该要去代码被打败或者部署
  - 制备包(prepare-package): 在实际打包之前, 执行必要的准备包装的操作
  - **打包(package)** : 采取编译的代码, 打包成可分发的格式(jar, war)
  - 预集成测试(pre-integration-test): 在之前集成测试之前执行所需的操作, 涉及设置所需环境
  - 集成测试(integration-test): 如果需要, 可以将该包执行并部署到可以运行集成测试的环境中
  - 整合后的测试(post-integration-test): 执行集成测试后执行所需操作, 例如清理环境
  - **校验(verify)** : 运行任何检查以验证包是否有效并符合质量标准
  - **安装(install)** : 将软件包安装到本地存储库中，以作为本地其他项目的依赖关系
  - **部署(deploy)** : 在集成或发布环境中完成, 将最终软件包复制到远程存储库中, 方便与其他开发人员共享项目
- 站点生命周期(site)
  - 预网站(pre-site): 在实际的项目现场生成之前执行所需的进程
  - **网站(site)** : 生成项目的站点文档
  - 后网站(post-site): 执行完成站点生成所需的进程, 并准备站点部署
  - 网站部署(site-deploy): 将生成的站点文档部署到指定的Web服务器

## Maven 概念模型

- 项目对象模型 POM (Project Object Mode)

  - 一个maven工程 就有一个pom.xml文件, 通过pom.xml文件定义项目的坐标, 项目依赖, 

- 项目生命周期(Project Lifecycle)

- 依赖管理系统(Dependency Management System)

  - 通过 maven 的依赖管理对项目所依赖的 jar 包进行统一管理。

- 一组标准集合

  - maven 将整个项目管理过程定义一组标准 , 比如: 通过maven 构建工程有标准的目录结构

    , 标准的生命周期阶段, 依赖管理有标准的坐标定义等

- 运行定义在生命周期阶段(phase)中插件目标(goal)的逻辑

## 坐标

```xml
<dependency>
  <!--项目名称，定义为组织名+项目名，类似包名-->
  <groupId>javax.servlet</groupId>
  <!-- 模块名称 -->
  <artifactId>javax.servlet-api</artifactId>
  <!-- 当前项目版本号，snapshot 为快照版本即非正式版本，release为正式发布版本 -->
  <version>3.1.0</version>
  <!-- 依赖范围 -->
  <scope>provided</scope>
</dependency>
```

- 依赖范围
  - **compile** : 编译范围, 指 A在编译时依赖 B，此范围为默认依赖范围。编译范围的依赖会用在 编译、测试、运行，由于运行时需要所以编译范围的依赖会被打包
  - **provided** : provided 依赖只有在当JDK 或者一个容器已经提供该依赖之后才使用,provided 依 赖在编译和测试时需要，在运行时不需要，比如：servlet api 被 tomcat 容器提供。 
  - **runtime**: runtime 依赖在运行和测试系统的时候需要, 在编译时候不需要, 例如JDBC的驱动包,由于运行时需要所以runtime范围的依赖会被打包
  - **test**: test 范围依赖 在编译和运行时都不需要, 它们只有再测试编译和测试运行阶段可用, 比如junit, 由于运行时不需要所以test范围依赖不会被打包
  - **system**: system范围依赖与 provided类似, 但是必须显示的提供一个对于本地系统中JAR文件的路径, 需要指定systemPath 磁盘路径, system依赖不推荐使用
- 依赖范围强->弱顺序: compile > provided > runtime > test
- 依赖建议
  - 默认引入的jar包 -- compile (默认范围, 可以不写) （编译、测试、运行 都有效 ） 
  - servlet-api, jsp-api -- provided (编译,测试有效 运行时无效以防和tomcat冲突)
  - jdbc驱动jar包 -- runtime(测试, 运行 有效)
  - junit -- test(测试有效)

## pom 基本配置

pom.xml 是 Maven 项目的核心配置文件，位于每个工程的根目录

- <project > ：文件的根节点 . 
- <modelversion > ： pom.xml 使用的对象模型版本 
- <groupId > ：项目名称，一般写项目的域名
- <artifactId > ：模块名称，子项目名或模块名称 
- <version > ：产品的版本号 .   
- <packaging > ：打包类型，一般有 jar、war、pom 等 
- <name > ：项目的显示名，常用于 Maven 生成的文档。
- <description > ：项目描述，常用于 Maven 生成的文档
- <dependencies> ：项目依赖构件配置，配置项目依赖构件的坐标
- <dependencyManagement> 锁定jar包版本不会引入jar包,  防止其他项目引用jar包直接依赖覆盖掉
- <build> ：项目构建配置，配置编译、运行插件等。 

## pom 解决jar冲突方式

### 基本概念

- 直接依赖: 项目中直接导入的jar包, 就是该项目的直接依赖包
- 传递依赖: 项目中没有直接导入的jar包, 可以通过项目直接依赖jar包传递到项目中

### 解决方式

- 第一声明优先原则: 先声明的jar包坐标依赖, 可以优先进入项目中

  ​	即<dependencies> 中靠上的坐标优先引入

- 路径近者优先原则: 直接依赖路径比传递依赖路径近,

  ​	 最终项目依赖jar包是路径近的依赖

- 直接排除法: 使用<exclusions> 排除jar包下面的依赖包

## Maven 私服(nexus)

### nexus.properties

- application-port: nexus 的访问端口配置 
- application-host: nexus主机监听配置
- nexus-webapp: nexus工程目录
- nexus-webapp-context-path: nexus的web访问路径
- nexus-work: nexus仓库目录
- runtime: nexus运行程序目录

### nexus 仓库类型

- **hosted** : 宿主仓库, 部署自己的jar 到这个类型的仓库, 包括releases 和 snapshot两部分

  , Releases 公司内部发布版本仓库, Snapshots 公司内部测试版本仓库

- **proxy** : 代理仓库, 用于代理远程的公共仓库, 如maven 中央仓库, 用户连接私服, 私服自动去

  中央仓库下载 jar 或插件

- **group** : 仓库组, 用来合并多个hosted/proxy 仓库, 通常配置自己的maven连接仓库组

- **virtual** : 虚拟, 兼容Maven1版本的jar或插件

### nexus 初始仓库

- **central** : 代理仓库, 代理中央仓库

- **apache-snapshots**: 代理仓库

  存储snapshots 构件, 代理地址 https://repository.apache.org/snapshots/

- **central-m1**: virtual类型仓库, 兼容Maven1版本的jar或者插件

- **releases**: 本地仓库, 存储 releases 构件

- **snapshots**: 本地仓库, 存储 snapshots 构件

- **thirdparty**: 第三方仓库

### maven 配置 nexus

- 修改maven中setting的<server>

  ```xml
  <server>
    <id>releases</id>
    <username>admin</username>
    <password>admin123</password>
  </server>

  <server>
    <id>snapshots</id>
    <username>admin</username>
    <password>admin123</password>
  </server>
  ```

- 私服上传

  ```xml
     <distributionManagement>
          <repository>
              <id>releases</id>
              <url>http://localhost:8081/nexus/content/repositories/releases/</url>
          </repository>
          <snapshotRepository>
              <id>snapshots</id>
              <url>http://localhost:8081/nexus/content/repositories/snapshots/</url>
          </snapshotRepository>
      </distributionManagement>
  ```

- setting.xml中配置仓库

  ```xml
  <profile>
    <!--profile 的 id-->
    <id>dev</id>
    <repositories>
      <repository>
        <!--仓库 id，repositories 可以配置多个仓库，保证 id 不重复-->
        <id>nexus</id>
        <!--仓库地址，即 nexus 仓库组的地址-->
        <url>http://localhost:8081/nexus/content/groups/public/</url>
        <!--是否下载 releases 构件-->
        <releases>
          <enabled>true</enabled>
        </releases>
        <!--是否下载 snapshots 构件-->
        <snapshots>
          <enabled>true</enabled>
        </snapshots>
      </repository>
    </repositories>
    <pluginRepositories>
      <!--  插件仓库，maven 的运行依赖插件，也需要从私服下载插件 -->
      <pluginRepository>
        <!--  插件仓库的 id 不允许重复，如果重复后边配置会覆盖前边 -->
        <id>public</id>
        <name>Public Repositories</name>
        <url>http://localhost:8081/nexus/content/groups/public/</url>
      </pluginRepository>
    </pluginRepositories>
  </profile>
  ```

  激活

  ```xml
    <activeProfiles>
      <!-- 激活dev -->
      <activeProfile>dev</activeProfile>
    </activeProfiles>
  ```

- 安装第三方jar包到本地仓库

  - 打开cmd直接运行

  ```bash
  mvn install:install-file -DgroupId=com.alibaba -DartifactId=fastjson -Dversion=1.1.37 -Dpackaging=jar -Dfile=D:\jar\fastjson-1.1.37.jar
  ```

- 安装第三方jar包到私服

  -  在setting中配置登录私服第三方登录信息

    ```xml
    <server>
    <id>thirdparty</id>
    <username>admin</username>
    <password>admin123</password>
    </server>
    ```

  - 打开cmd直接运行

    ```bash
    mvn deploy:deploy-file -DgroupId=com.alibaba -DartifactId=fastjson -Dversion=1.1.37 -Dpackaging=jar -Dfile=D:\jar\fastjson-1.1.37.jar -Durl=http://localhost:8081/nexus/content/repositories/thirdparty/ -DrepositoryId=thirdparty
    ```

  - 参数说明

    - DgroupId 和 DartifactId 构成该jar包在pom.xml的坐标
    - Dfile 表示需要上传jar包的绝对路径
    - Durl 私服上仓库的位置, 打开 nexus ->repositories 菜单可以看到该路径
    - DrepositoryId 服务器的表示id, 在 nexus的configuration中可以看到
    - Dversion 表示版本信息

