Preparation
============

To deploy this framework you will need the following established:


    1. **AWS Account:**

      An AWS Account with the ability to use all of the AWS services previously mentioned.


    2. **SSM/KMS:**

      You'll need to design your parameter store pathing, and add your tokens or other data to be used with the framework. We used the following structure::

        /<Project_name>/<event_source_name>/<environment>/<authorizer_token_var>/

      **Note:** This allows us to keep track of the various event sources, what environment they are used in, and keep the same variables across all event sources that will contain different values.


    3. **A CodeCommit or Github repository:**

      This is where your configuration files will be stored in addition to the buildspec and deploy scripts.
      If you parameterize all your sensitive data, there shouldn't be any risk of sensitive data disclosure.

      **Note:** The env: variables that must be filled out, these can essentially be whatever you want them to be.


    4. **GitHub Framework Repo:**

      This repo contains all the templates you'll need to build out the pipeline. 
      The cloudformation template will automatically build your CI/CD pipeline which will deploy the serverless application. 
      You should not need to make any changes to it unless you plan to modify it for your own purposes, which is entirely OK with us!


    5. **Pick a Cloudformation template:**
    
      If you choose to use the multiple source cloudformation template, you'll need:

      * A private S3 bucket to hold the merge lambda code (merge.zip)
      * Add an archive of your zipped configuration files (templates are in the framework Github repo you clone) to the bucket you use for the merge lambda.

      **Note:** The CF template will create a CodeCommit Repo with your configuration structure.
      This will only need to be done once per event source, once the repo is created, you may commit to it via git or directly through aws-cli or the console.