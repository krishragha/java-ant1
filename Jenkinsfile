pipeline {

agent none

stages {

stage('Unit Tests') {
agent {
label 'apache'
}
steps {
sh 'ant -f test.xml -v'
junit 'reports/result.xml'
}
}

stage('build') {
agent {
label 'apache'
}

steps {

sh 'ant -f build.xml -v'
}
post {

success {

archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
}
}
}


stage('deploy') {
agent {
label 'apache'
}

steps {
sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
}
}
stage("Running on CentOS") {
agent   {
label 'CentOS'


}

steps {

sh "wget http://krishragha1.mylabserver.com/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"

sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 5"
}
}


stage("Test on debian"){

agent  {

label "CentOS"

docker 'openjdk:8u141-jre'

}

steps {

sh "wget http://krishragha1.mylabserver.com/rectangles/all/rectangle_${env.BUID_NUMBER}.jar"

sh "java -jar rectangle_${env.BUILD_NUMBER}.JAR 3 10"
}
}


}
}
