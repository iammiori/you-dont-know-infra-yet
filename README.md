# Frontend 성능최적화 ; Infra level 에서의 성능 최적화
> 서버 구성, 네트워크 최적화, 캐싱 전략 등등 Infra 레벨에서의 Frontend 성능을 최적화 해보자.

> version 1.0.0  CSR 기준

## Deployment pipeline
![image](https://images.weserv.nl/?url=github.com/user-attachments/assets/9eeb27f0-46a0-444a-924e-ab59650dd125)

## Link
- [Bucket Web Site Endpoint](http://personal-dev-study-ap-northeast-2.s3-website-ap-southeast-2.amazonaws.com/)
- [CloudFront Deployment Domain](https://d2kz50r1rufk4p.cloudfront.net)

## Details
| 카테고리 | 역할 | 필요성 | 특징 |
|---------|------|--------|----------------|
| GitHub Actions & CI/CD | • main 브랜치 Push시 자동 빌드/배포<br>• npm ci로 정확한 의존성 설치<br>• out 디렉토리 S3 동기화 | • CSR 배포 자동화<br>• 빌드 프로세스 일관성<br>• 수동 배포 에러 방지 | • workflow_dispatch 수동 실행<br>• S3 sync 명령어<br>• AWS 인증 자동화 |
| S3 스토리지 | • index.html 진입점 제공<br>• 정적 에셋 호스팅<br>• CloudFront 원본 역할 | • CSR 번들 파일 저장<br>• 정적 리소스 제공<br>• 웹사이트 호스팅 | • 웹사이트 엔드포인트<br>• 정적 파일 전송<br>• 버킷 정책 |
| CloudFront | • S3 컨텐츠 전역 배포<br>• HTTPS 연결<br>• 정적 파일 압축 | • 글로벌 접근성<br>• SSL 보안<br>• 사용자 경험 향상 | • 엣지 캐싱<br>• Gzip 압축<br>• 커스텀 도메인 |
| 캐시 무효화 | • 배포 후 전체 캐시 삭제<br>• /* 경로 무효화<br>• CDN 캐시 관리 | • CSR 앱 최신화<br>• 즉각적인 업데이트<br>• 캐시 정합성 | • 배포 시 자동화<br>• 경로 기반 무효화<br> |
| Repository Secrets | • AWS 키 저장<br>• 리전 설정<br>• 버킷/배포 ID 관리 | • 보안 자격증명 보호<br>• 설정값 중앙화<br>• 민감정보 격리 | • GitHub 환경변수<br>• AWS 인증정보<br>• 프로젝트별 관리 |
