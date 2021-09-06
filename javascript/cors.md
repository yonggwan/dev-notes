### CORS 오류가 아닌데도, CORS 오류처럼 보이는 case를 겪으면서 정

프론트엔드 서버와 백엔드 서버가 Cross-site에 해당되는 환경에서,
AJAX 통신시 백엔드 서버에서 500오류가 발생했을경우에
프론트엔드에서는 CORS오류가 발생된것처럼 보이게 된다.

이 문제는 `Access-Control-Allow-Origin` Header를 적절히 설정해두었음에도 불구하고 기대처럼 동작하지않는다.

그 이유는 Preflight 요청에서는 백엔드에서 실제 작업을 거치지 않기 때문에 OPTION Method 로써는 cors설정이 기대처럼 동작하지만
실제 요청한 Method(POST, PUT..)에서는 백엔드 어플리케이션의 로직을 거치게 된다. 이 과정에서 서버에 오류가발생할경우
적절한 Response Header `Access-Control-Allow-Origin`를 응답하지 못하게 되어 cors 오류가 발생하게 된다.

이는 웹서버(Nginx, ..) cors 설정을 통해 해결 가능할것이다.
