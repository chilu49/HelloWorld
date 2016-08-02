/*

Example workflow to demonstrate simple logic

 */

node() {
    stage name: 'Start Sample Stage'
    echo 'Hello World from pipeline!'

    stage name: 'Code Checkout'
    checkout scm

    def version = null
    if (binding.variables.get('RELEASE_TYPE') == 'release') {
        version = "${MAJOR}.${MINOR}.${PATCH}.${env.BUILD_NUMBER}"
    } else {
        branch = ("branch-${env.BUILD_NUMBER}-${env.BRANCH_NAME}" =~ /\\|\/|:|"|<|>|\||\?|\*|\-/).replaceAll("_")
        version = "0.0.0-${branch}.${env.BUILD_NUMBER}"
    }

    stage name: 'Version Handling'
    writeFile([file: 'version.txt', text: version])

    archive('version.txt')
}