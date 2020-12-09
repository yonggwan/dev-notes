# S3 + Cloudfront + Route53에 연결하기 (with custom domain)

## aws certificate manager (HTTPS를 위한 SSL 인증서 생성)
- 리전선택 (!!!버지니아 북부로 설정해야 cloudfront 배포에 연결이 가능!!!)
- 인증서 프로비저닝 시작하여 인증서생성
- 아래 Route53, 도메인구입 의 절차를 마치면 aws가 주기적으로 도메인을 체크하여 인증상태를 발급완료 로 업데이트 함. (대략 30분 소요됨)

## aws cloudfront 배포생성
- Origin Domain Name을 생성한 AWS S3버킷으로 설정
- Price Class는 저렴한거로 설정
- Alternate Domain Names를 설정
- SSL 인증서를 ACM에서 생성한 Custom인증서로 설정
- Default Root Object를 S3의 index 파일로 설정 (ex: index.html)
- Redirect HTTP to HTTPS 설정

## aws route53
- 호스팅영역 생성
- 호스팅영역의 A유형 레코드 생성
- 라우팅 대상을 클라우드프론트 alias로 설정(ACM이 발급완료로 되있어야 선택이가능)
가비아 도메인 구입
- 가비아, 후이즈 등 호스팅업체에서 도메인을 구입
- 구입한 도메인 네임서버 설정에, route53에서 생성한 호스팅영역의 NS유형 레코드 값들을 모두 추가

## s3 버킷 생성
- 리전선택(seoul)
- 퍼블릭액세스 모두 차단
- 버킷에 view html소스를 업로드
