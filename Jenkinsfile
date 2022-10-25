@Library('jenkins-libraries') _
import com.tomtom.DependencyUtil

def navKitArtifactVersion = DependencyUtil.getLatestNavKitVersion('main')
def michiArtifactVersion = DependencyUtil.getLatestMichiVersion('main')
def navClArtifactVersion = DependencyUtil.getLatestNavClVersion('main')

pipeline {
  agent any

    stages {
      stage('checkout-revision') {
        steps {
          checkout(
              [
                $class: 'GitSCM',
                branches: [[name: '*/test']],
                extensions: [[$class: 'CloneOption', depth: 1, noTags: true, reference: '', shallow: true], [$class: 'SparseCheckoutPaths', sparseCheckoutPaths: [[path: 'revision.txt']]]],
                userRemoteConfigs: [[credentialsId: 'ssh_svc_bitbucket_access', url: 'ssh://git@bitbucket.tomtomgroup.com:7999/nk1ptx/navkit-main-sdk.git']]
              ]
          )

          echo "- NavKit: ${navKitArtifactVersion}"
          echo "- NavCl: ${navClArtifactVersion}"
          echo "- Michi: ${michiArtifactVersion}"

          sh '''
          version=$(cat revision.txt | sed "s/revision=//" | sed "s/-SNAPSHOT//")
          major=`echo $version | cut -d. -f1`
          minor=`echo $version | cut -d. -f2`
          revision=`echo $version | cut -d. -f3`
          revision=`expr $revision - 1`
          echo "$major.$minor.$revision" > /tmp/revision
          '''

          script {
            def revision = readFile(file: '/tmp/revision')
            def needBuildNavkit = compareVersions v1: "$revision", v2: "$navKitArtifactVersion"

            println("Current navkit revision: $revision")
            println("Current artifactory revision: $navKitArtifactVersion")
            println("Should trigger build: $needBuildNavkit")
            writeFile(file: '/tmp/needBuildNavkit', text: "${needBuildNavkit}")

            println("Should trigger build: $needBuildNavkit")
            //buildNavkit = readFile('/tmp/needBuildNavkit').trim()
          }
        }
      }
      stage('test AAR') {
        when { expression { false } }
        steps {
          echo "Build Navkit"
        }
      }
      //stage('NavKit-AAR') {
      //  steps {
      //    build 'Navkit-AAR'
      //  }
      //}
      //stage('Android-Adaptations') {
      //  steps {
      //    build 'Android-Adaptations'
      //  }
      //}
      //stage('Android-RRC') {
      //  steps {
      //    build 'Android-RRC'
      //  }
      //}
      //stage('iOS-Cocoapods-NavKit') {
      //  steps {
      //    build 'iOS-Cocoapods-NavKit'
      //  }
      //}
    }
}

