JAVA
-------

- - -
```Index```
* [ClassLoader](#ClassLoader)
  + Bootstrap ClassLoader
  + Extension ClassLoader
  + System/Application ClassLoader
  
- - - 

## ClassLoader
 Java class들을 jvm 메모리에 동적으로 로드하는 JRE에 포함되어 있는 일부.    
 클래스 로더가 있으므로 자바 런타임 시스템은 파일과 파일 시스템에 대해 알 필요가 없다. 라이브러리들을 위치시키고 내용물을 읽으며 jar 안에 포함된 클래스들을 읽는 역할. 로딩은 클래스가 프로그램에 의해 호출될 때까지 로드하지 않으며 호출된 클래스는 한번만 로드됨(런타임 라이브러리도) 클래스의 타입과 위치에 의해 특정 클래스를 로드할 클래스 로더가 정해짐. 특정 클래스를 로드한 클래스 로더는 getClassLoader() 메소드로 알수 있음. 이름을 기준으로 클래스를 로드하며 클래스 찾지 못할 시 NoClassDefFoundError/ClassNotFoundException 발생. 세가지 클래스 로더가 위임 원칙에 따라 클래스를 로딩한다.
 
### Bootstrap Loader
최상위 클래스 로더. 자바 클래스인 다른 클래스 로더와 달리 네이티브 C 코드로 작성되어 있으며(String.class.getClassLoader() == null).   
```<JAVA_HOME>/jre/lib``` 에 위치한 핵심 자바 라이브러리(rt.jar 등의 코어 API)등을 로드한다. 

