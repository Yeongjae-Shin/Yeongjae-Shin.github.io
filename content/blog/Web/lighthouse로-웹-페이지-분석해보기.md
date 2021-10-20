---
title: Lighthouse로 웹 페이지 분석해보기
date: 2021-10-20 23:10:34
category: Web
thumbnail: { thumbnailSrc }
draft: false
---

<img src="https://media.vlpt.us/images/wosk0106/post/ff1955a0-ba8f-4eb9-80fa-1bcc8de5c0a9/pwa-lighthouse.png" />

# Lighthouse란?
Lighthouse는 구글에서 개발한, 웹 페이지의 품질을 개선할 수 있는 오픈 소스 형태의 자동화 도구입니다. 어떤 웹 페이지든 사용할 수 있습니다.

# Lighthouse에서 확인할 수 있는 부분
가장 중요한 `Performace`부분만 자세하게 설명해보겠습니다.

## Performance
퍼포먼스는 말 그대로 웹 사이트의 성능을 보여주는 부분입니다. 간단하게 얘기하면 `얼마나 빠르게 화면에 그려지고 사용자는 얼마나 빠르게 해당 콘텐츠를 인식하는지`를 측정하는 것입니다.
Lighthouse에서 권고하는 대부분은 `리소스 절약`과 관련 있습니다. 자바스크립트 파일을 청크 단위로 쪼개고 크기를 줄이고 하면 점수가 올라가게 됩니다.
아래 사진은 현재 회사에서 서비스중인 웹 페이지의 퍼포먼스 점수 입니다.

<div style='text-align: center;'>
    <figure>
        <img src="https://user-images.githubusercontent.com/60685930/138118373-413f8c13-b789-4f4f-a253-c662963058d2.png" />
        <figcaption>퍼포먼스 100점의 위용</figcaption>
    </figure>
</div>

물론 배포가 된 후의 점수이고 `localhost`에서 Lighthouse를 실행해보면 점수가 처참합니다. 하지만 실제 유저가 보는 화면은 배포된 화면이기 때문에 로컬의 점수는 크게 신경쓰지 않아도 됩니다.

다음은 세부적인 항목에 대해서 살펴보겠습니다.

## Performance의 세부항목
Lighthouse는 성능을 측정하기 위해 다음의 메트릭을 사용합니다.

### Metrics
퍼포먼스의 측정 지표라고 생각하면 됩니다.

1. First Contentful Paint(FCP): 사용자가 특정 웹 페이지로 이동했을 때, 브라우저가 첫 번째 DOM의 콘텐츠를 렌더링하는 데 걸리는 시간
2. Time to Interactive(TTI): 웹 페이지가 완전히 상호작용을 할 수 있는 상태가 될 때까지 걸리는 시
3. Speed Index: 웹 페이지를 불러올 때, 콘텐츠가 시각적으로 표기되는 데까지 걸리는 시간
4. Total Blocking Time(TBT): 웹 페이지가 사용자 입력에 응답하지 못하도록 차단된 총 시간(로딩 중 메인 쓰레드가 긴 시간동안 중단되어 응답을 받을 수 없을 정도로 걸린 시간)
5. Largest Contentful Paint(LCP): 뷰포트에서 가장 큰 콘텐츠 요소가 화면에 렌더링 될 때까지 걸리는 시간
6. Cumulative Layout Shift(CLS): 이미지/광고의 느린 로딩, 비동기 동작, 동적 DOM 변경 등으로 웹 페이지의 레이아웃이 얼마나 변하는 지 측정한 값. 사용자가 잘못된 클릭을 하도록 유발하는 시각적 불안전성을 체크하는 지표

### Opportunities

<div style='text-align: center'><img src="https://user-images.githubusercontent.com/60685930/138121241-1515b72a-ecbc-4473-adbd-b07d10adaaee.png" /></div>

설명에 나오듯이 아래 제안을 따르면 페이지 로드를 빠르게 도와줄 수 있다고 합니다. 하지만 퍼포먼스 점수에는 영향을 미치지 않습니다.
저의 경우에는 사용하지 않는 자바스크립트 파일을 줄이고 용량을 조금 더 줄이라고 하네요.

### Diagnostic

<div style='text-align: center'><img src="https://user-images.githubusercontent.com/60685930/138121953-ed8fb2f2-e5b9-4ddb-a223-f81fe3eb237c.png" /></div>

웹 페이지의 퍼포먼스와 관련한 더 많은 정보를 보여줍니다. 위의 Opportunities와 마찬가지로 퍼포먼스 점수에 영향을 주지 않습니다.
토글 버튼을 클릭하면 어떤 부분을 개선해 볼 수 있는지 확인할 수 있습니다. 저의 경우에는 웹 폰트와 관련해서 조금 더 개선할 수 있지만 꼭 써야하는 폰트이기에 어쩔 수 없이 그대로 두고 있습니다.
경량화 폰트를 제공한다거나 폰트를 `preload`하는 방식으로 성능을 개선해볼 수 있을 것 같습니다.

## 그 밖의 항목
### Accessibility
이 항목은 웹 접근성을 체크하는 항목입니다. `img`태그에 `alt`속성이 있는지 `head`태그에 `title`태그 등이 있는지를 확인합니다.

### Best Practices
이 항목은 해당 웹 페이지가 웹 표준 모범 사례를 따르고 있는지를 확인하는 항목입니다. 콘솔에 에러가 출력되지는 않는지, HTTPS를 통해 해당 페이지에 접근할 수 있는지와 같은 부분을 확인합니다.

### SEO
이 항목은 웹 페이지가 검색 엔진에 대해 최적화된 순위 결과를 가지고 있는지 확인합니다. 각 사용자가 자신의 디바이스를 이용하여 웹 페이지에 접근하였을 때 콘텐츠를 읽는 데
무리가 없는 글꼴 크기를 사용하는지, 웹 페이지의 `robots.txt`파일이 유효한지 등을 확인합니다.

### PWA
Progressive Web App을 정의하는 일련의 기준에 따라 웹 페이지를 확인합니다. 이 항목은 해당 웹 페이지가 기준을 따르고 있는지 측정하여 점수를 부여하는 것이 아닙니다.
웹이 HTTP를 HTTPS로 리다이렉션 하는지, 응답 코드는 명확한지, 3G 네트워크 상태에서도 로딩이 빠르게 이루어지는지 같은 여부를 검사하여 합격 또는 실패를 부여합니다.

