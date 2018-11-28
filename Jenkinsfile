#!/usr/bin/groovy
@Library('github.com/pradeepitm12/osio-pipeline@staging')_

osio {
    
    config runtime: 'node'

    ci {
        def app = processTemplate()
        build app: app
    }

    cd {
     
      def resources = processTemplate(params: [
        release_version: "1.0.${env.BUILD_NUMBER}"
      ])

      def cm = loadResources(file: ".openshiftio/resource.configmap.yaml")
      echo "$cm"

      echo "$resources"
 
      echo "-------------- build default ----------------------------"
      build resources: resources
      
      echo "-------------- Pradeep test msg 2 --------------"
      echo "-------------- deploy stage-----------------------------------"
      deploy resources: [resources,  cm], env: 'stage'
    }
}
