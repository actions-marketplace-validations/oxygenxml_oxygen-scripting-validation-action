# Oxygen Validation Script

This action triggers Oxygen Scripting to perform a validation on your repository files. All you have to do is to include this action in your workflow and choose the directory to be validated. Find more info about workflows on https://docs.github.com/en/actions/using-workflows.

# Requirements

In order to use this action, you need to obtain an <i>Oxygen Scripting</i> license key from https://www.oxygenxml.com/xml_scripting/pricing.html (you can also request a [trial](https://www.oxygenxml.com/xml_scripting/register.html)). Add it as a secret to your repository (Settings &rarr; Secrets &rarr; Actions &rarr; New repository secret), and name it "SCRIPTING_LICENSE_KEY".
Then use it as an environment variable:
```yaml
env:
  SCRIPTING_LICENSE_KEY: ${{secrets.SCRIPTING_LICENSE_KEY}}
```

# Sample usage

If you don't already have a workflow defined in your repository, you can use the sample below.

```yaml
name: Run Validation
on:
  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:
    inputs:
      validationDir:
        description: 'The directory to be validated.'
        required: true
jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - name: Oxygen Validation Script
        uses: oxygenxml/oxygen-scripting-validation-action@v1.0.0
        env:
          SCRIPTING_LICENSE_KEY: ${{secrets.SCRIPTING_LICENSE_KEY}}
        with:
          validationDir: ${{ github.event.inputs.validationDir }}
```
You can also check [Oxygen Scripting - Validation template](https://github.com/oxygenxml/oxygen-script-validation-template) for sample validation files.

# Deployment to GitHub Pages

After a successful run of the Validation Script, a "validationReport.html" file is created on the <i>gh-pages</i> branch. If you want this report to be published to GitHub Pages, all you have to do is go to Settings &rarr; Pages, and under <i>Build and deployment</i> section select the <i>gh-pages</i> branch instead of the <i>main</i> branch. 
The deployment workflow should automatically start and the report should be available shortly at: https://{userid}.github.io/{reponame}/validationReport.html.

