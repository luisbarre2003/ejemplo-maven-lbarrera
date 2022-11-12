# Getting Started

## Windows

### Compile Code
* ./mvnw.cmd clean compile -e

### Test Code
* ./mvnw.cmd clean test -e

### Jar Code
* ./mvnw.cmd clean package -e

### Run Jar
* Local:      ./mvnw.cmd spring-boot:run 
* Background: nohup bash mvnw.cmd spring-boot:run &

### Testing Application
* Abrir navegador: http://localhost:8081/rest/mscovid/test?msg=testing

## Linux

### Compile Code
* ./mvnw clean compile -e

### Test Code
* ./mvnw clean test -e

### Jar Code
* ./mvnw clean package -e

### Run Jar
* Local:      ./mvnw spring-boot:run 
* Background: nohup bash mvnw spring-boot:run &

### Testing Application
* curl -X GET 'http://localhost:8081/rest/mscovid/test?msg=testing'

# Using Docker to test this app.
⚠️ **Is mandatory to use Powershell in Windows**
## Docker in Windows
```bash
### Compile Code
docker run -it --rm -v ${pwd}:/code --workdir /code maven mvn clean compile -e

### Test Code
docker run -it --rm -v ${pwd}:/code --workdir /code maven mvn clean test -e

### Jar Code
docker run -it --rm -v ${pwd}:/code --workdir /code maven mvn clean package -e

### Run Jar
docker run -it --rm -p 8081:8081  -v ${pwd}:/code --workdir /code maven mvn spring-boot:run
```
## Docker in Linux
```bash
### Compile Code
docker run -it --rm -v $(pwd):/code --workdir /code maven mvn clean compile -e

### Test Code
docker run -it --rm -v $(pwd):/code --workdir /code maven mvn clean test -e

### Jar Code
docker run -it --rm -v $(pwd):/code --workdir /code maven mvn clean package -e

### Run Jar
docker run -it --rm -p 8081:8081  -v $(pwd):/code --workdir /code maven mvn spring-boot:run
```


*****dentro de import

def COLOR_MAP = [
  'SUCCESS' : 'GOOD'
  'FAILURE' : 'DANGER'
]

def getBuildUser(){
  return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

*****dentro de pipeline

enviroment{
  BUILD_USER = ''
}

*****DENTRO DE POST always

script{
    BUILD_USER = getBuildUser()
}

slackSend channel: 'jen-example'
          color : COLOR_MAP[currentBuild.currentResult],
          message: "*{currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${BUILD_USER} \n Test executed ${SPEC} at ${BROWSER} \n more info at ${env.BUILD_URL}HTML_20Report/"
