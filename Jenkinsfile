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

    stage 'Running Assignment'
    sh "npm start --production"

    stage 'Testing'
    sh "npm test"
  } finally {
    stage 'Creating Report Artifact'
    sh "mv htmlhint-output.html output/htmlhint-output.html"
    step([$class: 'ArtifactArchiver', artifacts: 'output/*.html', fingerprint: true])
  }
}
