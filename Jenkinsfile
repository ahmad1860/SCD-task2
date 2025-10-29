pipeline {
agent any

tools {
nodejs &#39;NodeJS&#39;
}

parameters {
string(name: &#39;BRANCH_NAME&#39;, defaultValue: &#39;main&#39;, description: &#39;Branch to build from&#39;)

string(name: &amp;#39;STUDENT_NAME&amp;#39;, defaultValue: &amp;#39;your name&amp;#39;) //provide
your name here, no name, no marks
choice(name: &#39;ENVIRONMENT&#39;, choices: [&#39;dev&#39;, &#39;qa&#39;, &#39;prod&#39;], description: &#39;Select
environment&#39;)
booleanParam(name: &#39;RUN_TESTS&#39;, defaultValue: true, description: &#39;Run Jest tests after
build&#39;)
}

environment {
APP_VERSION = &quot;1.0.${BUILD_NUMBER}&quot;
MAINTAINER = &quot;Student&quot;
}

stages {
stage(&#39;Checkout&#39;) {
steps {
echo &quot;Checking out branch: ${params.BRANCH_NAME}&quot;
checkout scm
}
}

stage(&#39;Install Dependencies&#39;) {
steps {
echo &quot;Installing required packages...&quot;
bat &#39;npm install&#39;
}
}

stage(&#39;Build&#39;) {
steps {
echo &quot; Building version ${APP_VERSION} for ${params.ENVIRONMENT} environment&quot;
bat &#39;&#39;&#39;
echo Simulating build process...
if not exist build mkdir build
copy *.js build
echo Build completed successfully!
echo App version: %APP_VERSION% &gt; build\\version.txt
&#39;&#39;&#39;
}
}

stage(&#39;Test&#39;) {
when {
expression { return params.RUN_TESTS }
}
steps {
echo &quot;Running Jest tests...&quot;
bat &#39;npm test&#39;
}
}

stage(&#39;Package&#39;) {
steps {

echo &quot;Creating zip archive for version ${APP_VERSION}&quot;
bat &#39;powershell Compress-Archive -Path build\\* -DestinationPath
build_%APP_VERSION%.zip&#39;
}
}

stage(&#39;Deploy (Simulation)&#39;) {
steps {
echo &quot;Simulating deployment of version ${APP_VERSION} to
${params.ENVIRONMENT}&quot;
}
}
}

post {
always {
echo &quot;Cleaning up workspace...&quot;
deleteDir()
}
success {
echo &quot; Pipeline succeeded! Version ${APP_VERSION} built and tested.&quot;
}
failure {
echo &quot; Pipeline failed! Check console output for details.&quot;
}
}
}