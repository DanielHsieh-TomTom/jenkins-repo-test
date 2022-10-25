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
          sh '''
          version=$(cat revision.txt | sed "s/revision=//" | sed "s/-SNAPSHOT//")
          major=`echo $version | cut -d. -f1`
          minor=`echo $version | cut -d. -f2`
          revision=`echo $version | cut -d. -f3`
          revision=`expr $revision - 1`
          export version=$version
          '''

          echo "version: \${version}"
          echo "- NavKit: ${navKitArtifactVersion}"
          echo "- NavCl: ${navClArtifactVersion}"
          echo "- Michi: ${michiArtifactVersion}"
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

