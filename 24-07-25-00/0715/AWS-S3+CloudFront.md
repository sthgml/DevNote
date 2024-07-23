# AWS S3 와 CloudFront로 정적 페이지 배포하기

## 1. 정적 사이트 <-> 동적 사이트

### 1-1. 정적 사이트

![정적사이트](/99_images/정적사이트.png)

1. 특징
    1. 웹 서버 컴퓨터에 이미 저장된 파일을 클라이언트에게 **변경없이** 전송
    1. 서버 내 데이터가 변경되지 않는 한 **같은 사이트 화면**을 보게 됨
    1. 모든 사용자가 **같은 화면**을 응답 받음
1. 장점
    1. 다른 process 없이 요청에 대한 파일만 전송하므로 **속도가 빠르다.**
    1. 단순한 문서로 웹서버를 구축해 호스팅 **서버 연결 비용이 작다.**

### 1-2. 동적 사이트

![동적사이트](/99_images/동적사이트.png)

1. 특징
    1. 서버에 저장된 HTML이 그대로 보여지지 않음
    1. 동적으로 **만들어지는** 웹페이지
    1. 사용자는 상황, 시간, 요청 등 **다양한 조건에 따라 다른 웹페이지**를 보게 된다.
1. 종류
    1. CSR (Client Side Rendering)
    1. SSR (Server Side Rendering)
    1. MPA (Multi Page Application)
    1. SPA (Single Page Application)

## 2. AWS S3

### 2-1. AWS S3의 정의

1. Simple Storage Service
1. 객체 기반
1. 스토리지 서비스

### 2-2. AWS S3의 특징

1. 확장성
    1. 추가 스토리지가 필요할 때, 알아서 스토리지 용량 추가됨
1. 가용성
    1. 서비스가 **항상** 사용 가능한지를 나타내는 지표
    1. 퍼센티지(%)로 표기할 수 있음
    1. AWS S3에서 보장하는 가용성: 99.999999999%
    1. 즉, 1000억개 데이터 중 1 개 데이터가 손실될 수 있다.
1. 내구성
    1. S3에 저장된 데이터는 대부분의 상황에서 **보존**됨
    1. AWS S3에서 보장하는 내구성: 99.99%
    1. 즉, 하루에 8.6초 미만으로 다운타임이 발생할 가능성이 있다.
1. 객체 및 성능
    1. 일반적인 SSD/HDD 방식이 아니며 I/O (input/output) 병목지점이 거의 발생하지 않음
    1. 단, 객체의 키 설계의 **분포가 낮을 경우** I/O 병목이 발생할 수 있음

## 3. CDN (Contents Delivery Network) 서비스

### 3-1. 개념

1. 지리적으로 분산된 여러 개의 서버
1. 전 세계 데이터 센터에 파일 사본을 임시로 저장
1. 웹 콘텐츠를 사용자와 가까운 곳에서 전송함으로써 전송 속도 향상

### 3-2. 작동원리

1. 캐싱 & 엣지
  ![캐싱 & 엣지](/99_images/캐싱-엣지.png)
    1. 캐싱
        1. 정적 콘텐츠는 서버에서 데이터를 변경하지 않는 한 항상 같은 정보를 보여주기 때문에
        1. 매번 서버에 요청하고 resource를 받아올 필요 없이
        1. client와 가까운 edge에 최근 response 내용을 저장해 놨다가 특정 시간 내에 같은 요청이 들어오면
        1. 저장된 복사본을 반환하는 것
    1. 엣지
        1. 캐싱이 이루어지는 저장소
1. PoP (Points of Presence) 지역 접속 지점
1. REC (Regional Edge Cache) 지역 엣지 캐시

### 3-3. 작동 방식

1. 세 가지 서버에 의존
    1. 오리진 서버: S3, Google Cloud Storage, 혹은 자체 서버 등
    1. 엣지 서버:
        1. 전세계 여러 **지리적** 위치에 존재
        1. PoP(Point of Presence) 라고도 함
        1. 오리진 서버의 콘텐츠를 복사하여 캐싱
    1. DNS 서버:
        1. 오리진 및 엣지 서버의 IP 주소를 추적하고 제공
        1. 오리진으로 요청이 오면 컨텐츠를 **더 빠르게 제공할 수 있는 페어링 된 엣지 서버의 이름**으로 응답
1. 수행하는 기능
    1. 지연 시간 단축
        1. 데이터가 이동해야 하는 **물리적** 거리를 줄임
        1. CDN이 보다 넓고 광범위하게 분산되어 있을수록 유리
    1. 부하 분산
        1. 하나의 웹소스에 도달할 수 있는 경로를 여러개로 만들어 전체 트래픽의 균형을 맞춤

### 3-4. 장점

1. 성능 향상 (물리적 거리 및 트래픽 감소)
1. 가용성 보장
    1. 고도로 분산된 아키텍쳐와 대규모 서버 플랫폼을 갖춘 고급 CDN
    1. 100Tbps를 흡수할 수 있어 더 많은 사용자를 기반을 갖출 수 있음
1. 보안 강화 (DDos 차단)
1. 인텔리전스 수집 (Analytics)
1. 고객 경험 개선
1. 트래픽 부하 분산
1. 대역폭 비용 절감

## 4. CloudFront

### 4-1. 정의

1. 캐싱과 엣지를 이용한 CDN(콘텐츠 배포 네트워크) 서비스

### 4-2. CloudFront의 Edge

![viewr->cloudFront](/99_images/cloudfront전달.png)

1. 전달 순서
    1. Viewer
    1. POP (캐싱 기능 포함)
    1. REC (캐싱 기능 포함)
    1. Origin (eg. S3)

![실제 분포](/99_images/cloudfront분포.png)

1. 실제 cloudfront의 엣지 서버 분포

### 4-3. CloudFront의 장점

1. 물리적 거리가 감소되어 지연 시간이 줄어듦
1. 콘텐츠 보안 유지
    1. 지리적 제한, 서명된 URL, 서명된 쿠키 등을 기준으로 액세스 제한을 추가로 설정하여 기준이 다른 컨텐츠에 접근을 제한할 수 있다.
    1. OAI (Origin Access Identity)
        1. S3 버킷 및 컨텐츠에 대한 액세스를 Cloudfront로 제한
    1. 악성 공격 차단 가능
        1. AWS WAF
        1. AWS Shield

<!-- ## 5. Route53에서 도메인 연결하기

### 5-1. record?

1. DNS 서버에 어떤 URL이 어떤 IP 또는 서비스 등으로 매핑 되는지 알려주는 설정을 말함

```json
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "PublicRead",
			"Effect": "Allow",
			"Principal": "*",
			"Action": [
				"s3:GetObject",
				"s3:GetObjectVersion"
			],
			"Resource": "arn:aws:s3:::keyduck-keydueck-2/*"
		}
	]
}
```

**제어 설정 생성의 이름은 원본 도메인과 일치해야 합니다!!! 다르면 AccessDenied 뜹니다~!~!**

https://rainbound.tistory.com/entry/AWS-cloudfront-S3%EC%97%B0%EB%8F%99-OAI%EB%A5%BC-%EC%9D%B4%EC%9A%A9-access-denied-%EB%AC%B8%EC%A0%9C-%EA%B4%80%EB%A0%A8-%ED%95%B4%EA%B2%B0 -->

## 6. 배포해보기

### 6-1. 사전 준비

1. 정적 파일 준비하기 build

### 6-2. S3 bucket

1. s3 bucket 생성하기
    ![alt text](/99_images/240723_aws_s3+cloudfront/image.png)
1. 파일을 bucket에 업로드 하기
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-1.png)
1. bucket 정책 수정하기
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-2.png)
1. s3 정적 호스팅하기
    1. 속성 탭의 가장 아래
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-3.png)
    1. 정적 웹사이트 호스팅 활성화
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-4.png)
    1. 확인해보기
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-5.png)

### 6-3. Cloudfront

![alt text](/99_images/240723_aws_s3+cloudfront/image-7.png)

1. cloudfront 배포 생성하기
    1. 원본으로 s3 bucket 연결하기
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-8.png)
    1. 원본 액세스 제한하기
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-9.png)
    1. 기본 캐시 동작
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-10.png)
    1. 도메인 연결은 나중에 여기서
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-11.png)
    1. 하고 나면 버킷 권한을 수정하라고 알림이 뜬다. 일단 냅두고 도메인을 구매하러 갑니다.
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-12.png)

### 6-4. route 53

1. 도메인 구매하기
1. ACM AWS certificate manager에서 퍼블릭 인증서 요청하기
    1. 리전이 버지니아 북부인지 확인하기!
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-13.png)
    1. 인증서 요청
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-14.png)
    1. 구매한 도메인 이름으로 퍼블릭 인증서 요청
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-15.png)
    1. 검증을 위해 route 53에서 record 생성하기
    ![alt text](/99_images/240723_aws_s3+cloudfront/image-16.png)
1. 도메인에 레코드 추가하기
1. 도메인 cloudfront 배포 도메인 연결하기
        1. cloudfront > 일반 > 설정 > 편집
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-17.png)
        1. alternative domain name에 설정하기
        1. 발급 완료된 SSL을 custom ssl certificate 에 추가하기
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-18.png)
1. 퍼블릭 액세스를 차단하고 cloudfront로만 접근 가능하게 하기위해 s3 bucket 권한 수정하기
    1. cloudfront 원본 > 편집
    1. 정책 복사하기
    1. s3 권한 수정하러 가기
    1. 버킷 정책 편집
    1. 붙여넣기
    1. s3 퍼블릭 액세스 차단 항목 편집
        1. 다시 모든 퍼블릭 액세스 차단 선택
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-19.png)
    1. 확인해보면 이제 public도메인은 접근이 불가능하고, cloudfront는 접근 가능함
        ![alt text](/99_images/240723_aws_s3+cloudfront/image-20.png)

### 6-5. SPA 새로고침시 404 에러 해결

1. cloudfront의 오류 페이지 응답 생성 * 2
    1. HTTP 에러 코드: 404, 403
    1. Customize error response: Yesy
        1. Response page path: /index.html
        1. http response code: 200
1. cloudfront의 무효화
    1. 무효화 생성
    1. 객체 경로 추가: /*
