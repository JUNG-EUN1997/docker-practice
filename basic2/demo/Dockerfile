# 멀티 스테이지 빌드 방법 사용

# 첫번째 스테이지 진행 시작
FROM openjdk:11 as stage1

WORKDIR /app

# .은 WORKDIR인 /app에 생성된다는 의미
# /app/gradlew 파일로 생성
COPY gradlew .
# /app/gradle 폴더로 생성
COPY gradle gradle
COPY src src
COPY build.gradle .
COPY settings.gradle .

RUN ./gradlew bootJar


# 두번째 스테이지 진행 시작
FROM openjdk:11 as stage2
WORKDIR /app
# stage1에 있는 jar를 stage2의 app.jar 라는 이름으로 copy
COPY --from=stage1 /app/build/libs/*.jar app.jar

#CMD 또는 ENTRYPOINT를 통해 컨테이너를 실행
ENTRYPOINT ["java", "-jar", "app.jar"]


# 실행하기
# 1. PS C:\study\devops\docker-practice\basic2\demo> 로 이동
# 2. docker run spring_test:latest
# 3. docker images 로 생성 잘 되었는지 검색
# 4. docker run -d  -p 8082:80 spring_test:latest

# 추가설명
# docker 컨테이너 내에서 밖의 전체 host를 지칭하는 도메인 : host.docker.internal
# docker run -d -p 8081:8080 -e SPRING_DATASOURCE_URL=jdbc:mariadb://host.docker.internal:3306/board spring_test:latest
