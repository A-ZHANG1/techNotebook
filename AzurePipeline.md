- **Expression**: [Azure DevOps Expressions Documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops)
    
    1. **Static expression**: strings, job names
    2. **Compile-time expression**: `${{ <expression> }}`, parameters + statically defined variables
    3. **Runtime expression**: `$[ <expression> ]`, variables

- **variables**: string
- **parameter**: can be typed
- **Macro syntax variables** `$(isA11y)` evaluate before each task runs

- **condition**:
    - Conditions are evaluated at compile time, variables are passed at runtime, so only job names (static variables) can be used.
    1. `eq(variables.isA11y, 'true')`: [StackOverflow Reference](https://stackoverflow.com/questions/61079112/how-to-reference-an-azure-devops-matrix-variable-inside-an-expression)
    2. `condition: and(succeededOrFailed(), ${{ eq(variables.isA11y, 'true') }})`: [Azure DevOps Conditions Documentation](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/conditions?view=azure-devops#parameters-in-conditions)

- **Pitfalls**:
    <!-- Concluded from: https://msdata.visualstudio.com/A365/_git/trident-de-ds-app/pullrequest/1434744 -->
    1. Step names must be unique
    2. Matrix variables must be defined for each job (can be blank) [Matrix Variables](https://learn.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/jobs-job-strategy?view=azure-pipelines#strategy-matrix-maxparallel)
    3. Matrix variables can be referenced as `variables.VARNAME` (or `variables['VARNAME']`) in a job: [Developer Community Reference](https://developercommunity.visualstudio.com/t/matrix-variable-that-is-passed-to-a-template-as-a/1184356)
    4. Matrix variables are passed at runtime but evaluated at compile time.

```yaml
  - task: PublishPipelineArtifact@1
    displayName: Publish Sarif Results 1
    inputs:
      targetPath: ${{ parameters.testResultsDirectory }} # string. Alias: path. Required. File or directory path. Default: $(Pipeline.Workspace).
      artifact: CodeAnalysisLogs # string. Alias: artifactName. Artifact name.
      publishLocation: 'pipeline' # 'pipeline' | 'filepath'. Alias: artifactType. Required. Artifact publish location. Default: pipeline.
    # condition: and(succeededOrFailed(), eq(variables.isA11y, 'true')) # skipped
    # condition: and(succeededOrFailed(), ${{ eq(parameters.isA11y, true) }}) # skipped
    # condition: and(succeededOrFailed(), ${{ eq(parameters.isA11y, 'true') }}) # skipped
    condition: and(succeededOrFailed(), contains(variables['System.JobName'], 'A11y')) # get variable from job name
```
- To reduce build time: **Cache@2**
```yaml
  - task: Cache@2
    displayName: Cache Yarn Packages
    inputs:
      key: '"yarn" | "$(Agent.OS)" | yarn.lock'
      path: ${{ parameters.yarn_config_cache }}
      restoreKeys: |
        yarn | "$(Agent.OS)"
        yarn
```
- **oneBranch** (security for azure only) can use good pool. i.e. the `Build-Workspace.ps1` took 7m to run in onebranch
but 17m to run in traditional pipeline https://msdata.visualstudio.com/A365/_build/results?buildId=140709940&view=logs&j=129d6898-74a5-5955-ceda-edd03eb28dc9&t=ae60905a-f21c-5eda-df98-dd6412475798
