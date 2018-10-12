node {
    def server = Artifactory.server 'ART'
    def rtMaven = Artifactory.newMavenBuild()
    def buildInfo

    stage ('Clone') {
        git url: 'https://github.com/NinhHuong/maven-app.git'
    }

    stage ('Artifactory configuration') {
        rtMaven.tool = 'M3'
        rtMaven.deployer releaseRepo: 'maven-repo', snapshotRepo: 'maven-repo', server: server
        buildInfo = Artifactory.newBuildInfo()
        buildInfo.env.capture = true
    }

    stage ('Exec Maven') {
        rtMaven.run pom: 'pom.xml', goals: 'clean install', buildInfo: buildInfo
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
}
