# AWS Note

## AWS Lambda
AWS Lambda는 이벤트에 응답하여 코드를 실행하고 자동으로 기본 컴퓨팅 리소스를 관리하는  서버없는 컴퓨팅 서비스이다.

- AWS 서비스와 관계가 적은 복잡한 기능을 수행해야 한다면 EC2 사용이 권장된다.
- AWS Lambda의 trigger로 AWS 서비스와 연계된 이벤트를 처리할 때 사용하거나,
    
    ![](https://blog.algopie.com/wp-content/uploads/2017/02/lambda_triger.png)

- API서버 기능을 서버 없이 구현할 때 유용하다.
    - API 서버로는 AWS Gateway와 연계하여 설계하는 것이 더 효율적

- ex. HTTP API 서버 기능 / S3를 활용한 이미지 자동 처리 / SNS로 notification에 대한 자동 처리 / CloudWatch 특정 이벤트 발생에 대한 처리

- 배포에 대해 간소시킬 수 있어 코드를 lambda 콘솔에서 인라인으로 작성하거나, 패키지로 업로드하면 자동 배포된다.
- CloudWatch를 통해 각종 지표를 확인할 수 있다.
- 스케일링도 가능하여 대규모 트래픽 발생 시 빠르게 확장할 수 있다.
- 요청 수와 요청을 처리하는 함수 시간에 따라 요금이 발생하여 비용효율적이다.

### 게임 개발 예시
lambda는 보통 stateless 방식으로 백엔드를 구성하는데 최적화되어 있으며 서버의 백엔드를 REST API로 정의할 수 있다.

![](https://d2908q01vomqb2.cloudfront.net/7b52009b64fd0a2a49e6d8a939753077792b0554/2020/06/23/image-2-1.png)

1. 서비리스 백엔드

- lambda가 main, gameStart, gameEnd 3가지 로직을 수행할 수 있도록 한다. API Gateway를 통해 API endpoint를 관리할 수 있다.
- lambda에서 VPC내의 RDS에 액세스할 수 있다. 
- 랭킹 대시보드를 만들거나 분산 환경에서 활용할 수 있는 비정형 데이터 워크로드를 처리하는데는 DynamoDB도 사용할 수 있다.

2. 처리 자동화
- 여러 서버의 로그를 Kinesis Data Firehose에 저장하고 해당 로그 포맷을 변환하는 함수를 호출할 수 있다.

3. 주기적인 작업

![](https://d2908q01vomqb2.cloudfront.net/7b52009b64fd0a2a49e6d8a939753077792b0554/2020/06/23/image-5-1.png)


*(출처)*
- https://blog.algopie.com/aws/aws-lambda%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-api-%EC%84%9C%EB%B9%84%EC%8A%A4-%EB%B0%B0%ED%8F%AC-12/
- https://aws.amazon.com/ko/blogs/korea/using-aws-lambda-within-your-game/*