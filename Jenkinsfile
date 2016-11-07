node {
  stage: 'Environment Variables'
  sh "env"

  stage 'Checkout Repository'
  git url: '<PROVIDE YOUR REPO NAME HERE>', branch: "${env.BRANCH_NAME}"

  stage 'Installing Dependencies'
  sh "npm prune"
  sh "npm install"

  try {
    stage 'Linting'
    sh "npm run lint"

    stage 'Linking Data Files'
    sh "ln -s /datafiles ."

    stage 'Running Assignment'
    sh "npm start --production"

    stage 'Testing'
    sh "npm test"
  } finally {
    stage 'Unlinking Data Files'
    sh "rm datafiles"

    stage 'Creating Report Artifact'
    sh "mv htmlhint-output.html output/htmlhint-output.html"
    step([$class: 'ArtifactArchiver', artifacts: 'output/*.html', fingerprint: true])
  }
}
