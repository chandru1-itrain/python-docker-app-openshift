node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'Github-ID', url: 'https://github.com/itrainspartans/python-docker-app-openshifts.git'
      }
   
   stage('Docker Build') {
     def app = docker.build "manee2k6/py-newrelic"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag manee2k6/py-newrelic manee2k6/py-newrelic:dev'
          sh 'docker push manee2k6/py-newrelic:dev'
          sh 'docker push manee2k6/py-newrelic:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=fwlXR0uVPx2BncCc4UQtb5plpO9eJyJ2ZA6Ubo0ETvc --server=https://api.us-west-1.starter.openshift-online.com:6443'
     sh 'oc project itrainspartans'
     //sh 'oc new-app --name py-mani manee2k6/py-spartans'
      sh 'oc rollout latest dc/py-mani -o json' 
      sh 'oc rollout latest manee2k6/py-newrelic --name python \
          --env NEWRELIC_LICENSE=xxxxxx \
                NEWRELIC_APPNAME=pyapp'
     //sh 'oc expose svc py-mani' 
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }

  }
