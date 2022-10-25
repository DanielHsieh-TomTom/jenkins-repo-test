@Library('jenkins-libraries') _
import com.tomtom.DependencyUtil

def navKitArtifactVersion = DependencyUtil.getLatestNavKitVersion('main')
def michiArtifactVersion = DependencyUtil.getLatestMichiVersion('main')
def navClArtifactVersion = DependencyUtil.getLatestNavClVersion('main')

pipeline {
  agent linux

    stages {
      stage('Check-version') {
        steps {

          echo "Latest artifact versions:"
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

