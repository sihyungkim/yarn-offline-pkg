# Offline 작업환경을 위한 node package 배포

[yarn offline mirror](https://classic.yarnpkg.com/blog/2016/11/24/offline-mirror/)

## 1. 패키지 레지스트리 서버에 있는 .tgz 파일을 로컬에 저장
`온라인상태`

- **`.yarnrc` 파일 생성**

  ```
  yarn-offline-mirror "./yarn-offline-mirror"
  yarn-offline-mirror-pruning true
  ```
- **`./yarn-offline-mirror` 폴더 생성**
- **`node_modules`, `yarn.lock` 제거**

- **yarn 캐시삭제 및 패키지 인스톨**
  ```
  yarn cache clean
  yarn install
  ```

- yarn-offline-mirror에 tgz파일이 생성되고, 프로젝트 루트에 yarn.lock파일이 생성됨
- 해당 파일들을 가져가야 함 

## 2. ./yarn-offline-mirror에 있는  .tgz로 패키지 설치
`오프라인상태`
- 인터넷연결을 끊고 아래 명령어로 패키지 인스톨
```
yarn install --offline
```


## 3. 패키지업데이트 할 때 
- 패키지 추가 혹은 버전 업하기 전에 yarn 캐시부터 지운다.



## 정리
npmjs 패키지 레지스트리서버에서 .tgz 파일을 로컬에 다운받는 과정이 필요하고, 해당 과정에서 yarn-offline-mirror 기능을 사용 한다. 

node_modules와 yarn.lock 파일을 삭제하고 
yarn cache cleand으로 캐시도 말끔하게 지운 후, yarn install로 .tgz파일을 yarn-offline-mirror에 저장시키고, 
node_modules 폴더만 지운후, 나머지 생성된 파일을 업로드 한다.





## [추가] yarn 단독실행js파일을 받을 수 있음   
[Yarn Github Release Page](https://github.com/yarnpkg/yarn/releases)

아래 두 코드는 같음
```
yarn install 
node ./yarn-1.22.4.js install
```
