import com.tomtom.DependencyUtil

stages {
  stage('check') {
    def navKitVersion = DependencyUtil.getLatestNavKitVersion('main')
    def michiVersion = DependencyUtil.getLatestMichiVersion('main')
    def navClVersion = DependencyUtil.getLatestNavClVersion('main')

    println "Latest versions:"
    println "- NavKit: ${navKitVersion}"
    println "- NavCl: ${navClVersion}"
    println "- Michi: ${michiVersion}"
  }
}
