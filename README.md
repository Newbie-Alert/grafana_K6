# 터벅터벅 grafana_K6 부하테스트 학습기 ⚙️
### 내 가볍고, 통신도 적고, 유저도 없는 간단한 웹 사이트에 부하테스트를 해보았다.

[K6 릴리즈 페이지]: https://github.com/grafana/k6/releases
[K6 문서]: https://k6.io/docs/

<br/>


# grafana_k6 설치
- 나는 릴리즈 된 버전을 직접 받아서 사용했다.
  별 다른 이유는 없고 가장 간단했기 때문 [K6 릴리즈 페이지]
- 릴리즈 페이지의 하단에 운영체제에 따른 파일을 받으면 끝이다.

# grafana_k6 실행
- 우선 다운 받은 k6.exe는 window 기준 `CMD`를 통해 열어서 작동했다.
- k6와 자바스크립트로 짜여진 테스트 코드를 같은 폴더에 두고
  CMD에서 해당 파일들이 있는 곳으로 이동한다

``` cmd
< CMD >
cd k6.exe와 테스트코드.js 파일이 있는 경로
```
- 경로 이동 후 cmd에서 `k6` 라고 입력하면
<img src="https://github.com/Newbie-Alert/grafana_K6/blob/main/version,command.png?raw=true" width="70%">
k6의 버전과 사용 가능한 명령어들이 나오며 실행이 됐음을 확인할 수 있다.

# 테스트 코드
k6의 실행을 확인했다면 내 웹사이트가 마주했으면 할 시나리오를 만들어주는 코드를 작성해야 한다.  

- 테스트 코드는 javascript로 작성하는데
  시나리오 설정을 option에서 추가 하면 된다.
  나는  VUS(가상유저들)를 5명, 시간(duration)을 10초로 설정했다.
- `options` 안에는 `stage`를 통해 시나리오 조건을 중간중간에 바꿔 진행하도록 설정 할 수 있다.

``` Javascript

< test.js >

import http from "k6/http";
import { sleep } from "k6";

export const options = {
 // stages: [
 //   { duration: '30s', target: 20 },
 //   { duration: '1m30s', target: 10 },
 //  { duration: '20s', target: 0 },
 // ],

  duration: '10s', // 시나리오 진행시간
  vus: 5, // 가상 유저들(Virtual User s)
}

export default function () {
  http.get('https://imitation-project.du.r.appspot.com')
  sleep(1); // 가상 유저들의 get요청을 쉬는 것 sleep(초 단위)
}

export default function () {
  http.get('https://imitation-project.du.r.appspot.com')
  sleep(1);
}

```

# 결과

<img src="https://github.com/Newbie-Alert/grafana_K6/blob/main/result.png?raw=true">

# 마치며

- 공식문서를 읽어가며 따라가 보는 것은 이번이 2번째였던 거 같은데 어려웠다.
  공식문서 읽는 것도 많이 보고 익혀야 할 거 같다.

### 슬프게도 결과지를 보고 해석을 못 한다.
- data를 주고 받은 거, http 요청 막힌거, 연결, 실패, 대기 이런 항목들이 쭉 있는데
  공식 문서에는 모든 요청의 동단 간 시간, 중앙값 및 평균값, 최소값과 최대값, p90/p95/p99 값에 대해 나온다고 하는데
  아직 모르는 용어들이 많아서 학습이 필요하다.


### [k6 기본설명] 이 영상을 보고 학습 중
  
  [k6 기본설명]: https://youtu.be/gvounvDSDGg
  
