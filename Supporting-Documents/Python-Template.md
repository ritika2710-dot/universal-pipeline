To Use a End to End Python Pipeline:



trigger:   
  branches:
    include:
      - develop  # To run and deploy post merge to develop branch

pr:
  branches:
    include:
      - develop  # To run only for PRs targeting 'develop' branch

pool:
  name: 'Azure Pipelines'


variables:
  - template: variables.yml

resources:
  repositories:
    - repository: Automation-Hub
      type: git
      name: Automation-Hub/Automation-Hub
      ref: refs/heads/main


extends:
  template: .azure-pipelines/templates/full-pipelines/python-azure-functions-end-to-end.yml@Automation-Hub
  parameters: 
    pythonVersion: $(pythonVersion)
    sonarQubeServiceConnection: '$(sonarQubeServiceConnection)'
    sonarQubeProjectKey: '$(sonarQubeProjectKey)'
    sonarQubeUrl: $(sonarQubeUrl)
    sonarQubeToken: $(sonarQubeToken)  
    wizClientId: $(wizClientId)
    wizClientSecret: $(wizClientSecret)
    wizServiceConnection: $(wizServiceConnection)
    runValidate: 'true'
    runBuild: 'true'
    runScan: 'true'
    runReleaseTag: 'true'
    runDeployment: 'true'
    runLogCollection: 'true'
 



