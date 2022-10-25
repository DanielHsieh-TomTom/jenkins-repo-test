@Library('jenkins-libraries') _
import com.tomtom.DependencyUtil

def navKitArtifactVersion = DependencyUtil.getLatestNavKitVersion('main')
def michiArtifactVersion = DependencyUtil.getLatestMichiVersion('main')
def navClArtifactVersion = DependencyUtil.getLatestNavClVersion('main')

def artifactoryMajor = navKitArtifactVersion.substring(0,2)
def artifactoryMinor = navKitArtifactVersion.substring(3,5)
def artifactoryRevision = navKitArtifactVersion.substring(6)

def needUpdate = '/tmp/needBuildNavkit'

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

          echo "- Major: ${artifactoryMajor}"
          echo "- Minor: ${artifactoryMinor}"
          echo "- Revision: ${artifactoryRevision}"

          sh "export artifactoryMajor=$artifactoryMajor"
          sh "export artifactoryMinor=$artifactoryMinor"
          sh "export artifactoryRevision=$artifactoryMinor"

          sh '''
          [ -f /tmp/needBuildNavkit ] && rm -f /tmp/needBuildNavkit
          version=$(cat revision.txt | sed "s/revision=//" | sed "s/-SNAPSHOT//")
          major=`echo $version | cut -d. -f1`
          minor=`echo $version | cut -d. -f2`
          revision=`echo $version | cut -d. -f3`
          revision=`expr $revision - 1`

          export version=$version

          if [ $major -gt $artifactoryMajor ]
          then
            echo 1 > $needUpdate
          elif [ $major -lt $artifactoryMajor ]
          then
            echo 0 > $needUpdate
          else
            if [ $minor -gt $artifactoryMinor ]
            then
              echo 1 > $needUpdate
            elif [ $minor -lt $artifactoryMinor ]
          then
              echo 0 > $needUpdate
            else
              if [ $revision -gt $artifactoryRevision ]
              then
                echo 1 > $needUpdate
              else
                echo 0 > $needUpdate
              fi
            fi
          fi

          cat $needUpdate
          '''

          echo "version: \${version}"
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

