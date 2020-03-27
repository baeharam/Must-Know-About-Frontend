# CI와 CD

## CI (Continuous Integration, 지속적 통합)

CI는 빌드와 테스트를 자동화해서 공유 저장소에 병합시키는 프로세스를 뜻한다. git과 같은 버전관리 시스템을 사용할 때 여러명의 개발자가 하나의 공유 저장소를 사용하는 경우가 많다. 이렇게 되면 새로운 코드의 변경 사항이 저장소에 통합되지 않을 경우 서로 충돌할 수 있다. 따라서 빌드/테스트 자동화부터 코드의 일관성(Consistency)을 제공하기 때문에 지속적으로 통합한다는 용어를 사용하는 것이다.

<br>

## CD (Continuous Delivery/Deploy, 지속적 전달/배포)

CD는 CI의 빌드/테스트를 통해서 정상적으로 수행됨을 확인하면 이는 배포를 수동으로 하느냐 자동으로 하느냐에 따라 2가지로 나뉜다.

* **지속적 전달** : 프로덕션 배포를 위한 상태가 되고 배포 자체는 수동으로 실행한다.
  * 개발팀과 비즈니스팀간의 커뮤니케이션 부족 문제를 해결한다.
* **지속적 배포** : 프로덕션까지 자동으로 배포한다.
  * 어플리케이션의 제공 속도를 증가시킨다.

<br>

CI/CD의 대표적인 서비스로 Jenkins, Travis CI, Circle CI 등이 있으며 이를 다이어그램으로 보면 아래와 같다.

<img src="../../images/frontend/ci-cd.png">

[이미지 출처](https://aws.amazon.com/ko/devops/continuous-integration/)

<br>

## 참고

* [AWS, 지속적 통합이란 무엇입니까?](https://aws.amazon.com/ko/devops/continuous-integration/)
* [Red Hat, CI/CD(지속적 통합/지속적 제공): 개념, 방법, 장점, 구현 과정](https://www.redhat.com/ko/topics/devops/what-is-ci-cd)
* [개발자노트님, CI(Continuous Integration), CD(Continuous Delivery/Deployment)에 대해 알아보자.](https://jhleed.tistory.com/130)