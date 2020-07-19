# CH1. 인텔리제이로 스프링 부트 시작하기

## 1.1 인텔리제이 소개

### 인텔리제이의 강점?

- 강력한 추천 기능
- 훨씬 더 다양한 리팩토링 기능과 디버깅 기능
- 이클립스의 깃에 비해 훨씬 높은 자유도
- 프로젝트 시작할 때 인덱싱을 하여 파일을 비롯한 자원들에 대한 빠른 검색 속도
- HTML, CSS, JS, XML에 대한 강력한 기능 지원
- 자바, 스프링 부트 버전업에 맞춘 빠른 업데이트



 실제로 많은 IT 서비스 회사에서는 __인텔리제이 얼티메이트(유료)__를 공식 IDE로 사용하고 있습니다.

인텔리제이는 유료 버전인 얼티메이트와 무료버전인 커뮤니티 버전 두 가지가 있습니다.

커뮤니티 버전도 스프링 부트를 개발하는 데는 크게 어려움이 없습니다. 다만 HTML, CSS, JS에 대한 지원이 없으므로 이들에 대한 개발은 VS Code를 비롯한 다른 무료 개발 도구를 사용할 것을 추천합니다.



## 1.3 인텔리제이 설치 후 프로젝트 생성

1. Create Project
2. 프로젝트의 유형을 그레이들(Gradle), Java을 선택해 생성
3. GroupId와 ArtifactId를 등록, 특히 ArtifactId는 프로젝트의 이름이 되기 때문에 원하는 이름으로 작성



## 1. 4 그레이들 프로젝트를 스프링 부트 프로젝트로 변경하기

__스프링 부트와 그레이들을 충분히 이해하고 있는 사람이라면 스프링 이니셜라이저를 사용하자.__



아직 미숙한 사용자라면 하나씩 코드를 작성하면서 어떤 역할을 하는 지 이해하자.

```
// build.gradle

buildscript {
	// ext는 build.gradle에서 사용하는 전역변수를 설정
    ext {
    // springBootVersion 전역변수를 '2.2.0.RELEASE로 생성
        springBootVersion = '2.2.0.RELEASE'
    }
    /* 
    repositories는 각종 의존성(라이브러리)들을 어떤 원격 저장소     에서 받을지를 결정합니다. 
    기본적으로 mavenCentral을 많이 사용하지만,
    최근 추세는 전부 jcenter를 사용한다. 
    */
    repositories {
        mavenCentral()
        jcenter()
    }
    /*
    dependencies는 프로젝트 개발에 필요한 의존성들을 선언하는 곳
    커뮤니티 버전을 써도 의존성 자동완성이 가능하다.
    compile 메소드 안에 라이브러리의 이름의 앞부분만 추가한 뒤
    자동완성(Ctrl + Space)을 사용하면 해당 라이브러리 목록을 
    볼 수 있습니다.
    */
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
    }
}
// 여기까지는 플러그인 의존성 관리를 위한 설정입니다.

/* 다음은 앞서 선언한 플러그인 의존성들을 적용할 것인지 결정
이 4개의 플러그인은 자바와 스프링 부트를 사용하기 위해서는
필수플러그인이니 항상 추가하면 된다. */

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'org.springframework.boot'
// 이 플러그인은 스프링 부트의 의존성들을 관리해 주는 플러그인이라 꼭 추가해야만 합니다.
apply plugin: 'io.spring.dependency-management'


group 'org.example'
version '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    compile('org.springframework.boot:spring-boot-starter-web')
    compile('org.projectlombok:lombok')
    compile('org.springframework.boot:spring-boot-starter-data-jpa')
    compile('com.h2database:h2')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```



코드 작성이 다 되었다면 build.gradle에 변경이 있으니 반영하라는 알람이 오른쪽 아래에 나옵니다. 알람의 `Enable Auto-import`를 클릭하면 변경마다 자동반영이 되며, `Import Changes` 버튼을 클릭하면 1번만 반영됩니다.

모두 받게 되면 화면 오른쪽 위의 `Gradle` 탭을 클릭해서 의존성들이 잘 받아졌는지 확인해 봅니다. main에서는 spring-boot-start-web이, test에서는 spring-boot-start-web, spring-boot-start-test 의존성이 잘 받아졌던 것을 확인할 수 있습니다.

__여기까지 인텔리제이에 기본적인 스프링 부트 개발환경을 구축했습니다!__

여기서 한 가지 환경을 더 구성해봅시다. 깃허브와 연동하는 것입니다.

## 1.5 인텔리제이에서 깃과 깃허브 사용하기

Github 아이디가 있다면 바로 단축키 

윈도우: `Ctrl + Shift + A`

맥: `Command + Shift + A` 

1. Action 검색창을 열어 share project on github을 검색

2. 로그인 후 깃허브에 생성할 저장소 정보 입력

`Repository name` 필드에 등록한 이름으로 __깃허브에 저장소가 생성__ 됩니다. 대부분은 프로젝트 이름을 깃허브 저장소와 같은 이름을 사용하니, 같은 이름을 등록합니다.

3. `Share` 버튼을 클릭하면 깃허브 저장소와 동기화 진행

   동기화 과정에서 커밋 항목으로 추가할 것인지 묻는 안내문이 나오는데

   처음에는 `No`를 선택합니다.

4. 첫 번째 커밋을 위한 팝업창이 등장하는데 여기서 __.idea 디렉토리는 커밋하지 않습니다__ 이는 인텔리제이에서 프로젝트 __실행시 자동으로 생성되는 파일들__이기 때문에 깃허브에 불필요합니다. 나머지 파일들을 체크하고 커밋 메시지를 작성해서 `OK`버튼을 누르면 깃 커밋과 깃허브 푸시가 진행됩니다.

5. 플러그인에서 지원하는 .igonore 플러그인을 설치하자. 

   1. `Ctrl + Shitf + A`에 Plugins 를 검색 후 `Marketplace` 탭 선택
   2. .ignore를 검색하여 Install
   3. 인텔리제이를 재시작(그래야 적용됨)

6. 이그노어 파일 생성 방법

   1. `Alt + Insert` 입력 후 생성 목록 아래에 .ignore file -> gitignore file[Git]을 선택하여 Generate로 파일 생성

   2. __인텔리제이에서 자동으로 생성되는 파일__들을 모두 이그노어 처리

      > .gradle
      >
      > .idea

7. 깃 커밋을 하자 `Ctrl + K` (맥은 `Command + K`)

8. 깃 푸쉬를 하자 `Ctrl + Shift + K`