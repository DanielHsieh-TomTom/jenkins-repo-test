import com.tomtom.DependencyUtil

timestamps {
        def navKitVersion = DependencyUtil.getLatestNavKitVersion('main')
        def michiVersion = DependencyUtil.getLatestMichiVersion('main')
        def navClVersion = DependencyUtil.getLatestNavClVersion('main')

        // Determine the versions in develop
        def developNavKitVersion = com.tomtom.Utils.getCurrentDependencyVersion("navkit", "develop")
        def developNavClVersion = com.tomtom.Utils.getCurrentDependencyVersion("navcl", "develop")
        def developMichiVersion = com.tomtom.Utils.getCurrentDependencyVersion("michi", "develop")

        println "Develop versions:"
        println "- NavKit: ${developNavKitVersion}"
        println "- NavCl: ${developNavClVersion}"
        println "- Michi: ${developMichiVersion}"

        println "Latest versions:"
        println "- NavKit: ${navKitVersion}"
        println "- NavCl: ${navClVersion}"
        println "- Michi: ${michiVersion}"

    }
