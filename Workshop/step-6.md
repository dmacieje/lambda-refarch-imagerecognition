# Step 6: Build and Launch the web application

To see the processing workflow in action, we will use an AngularJS web application to create photo albums and upload pictures to them.

### Step 6A: Set up the Photo Processing Web Application

To complete the workshop tests, you will use an AngularJS web application to create photo albums and upload pictures to them.

In this section, you will use a cloudformation template to package and deploy the web application on an S3 bucket configured for website hosting.

> This cloudformation template leverages AWS CodeBuild and AWS CodePipeline to automate building, packaging and deploying the web application

Region| Code | Launch
------|------|-------
EU (Ireland) | <span style="font-family:'Courier';">eu-west-1</span> | [![Launch Step 0B in eu-west-1](images/cfn-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new?stackName=sfn-workshop-setup-webapp&templateURL=https://s3-eu-west-1.amazonaws.com/sfn-image-workshop-eu-west-1/cloudformation/step0-webapp.yaml)
US West (Oregon) | <span style="font-family:'Courier';">us-west-2</span> | [![Launch Step 0B in us-west-2](images/cfn-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new?stackName=sfn-workshop-setup-webapp&templateURL=https://s3-us-west-2.amazonaws.com/sfn-image-workshop-us-west-2/cloudformation/step0-webapp.yaml)

#### CloudFormation launch instructions

1. Click the **Launch Stack** link above for the region of your choice (make sure to pick the same region you have launched your other resources in)

1. Click **Next** on the Select Template page.

1. On the Specify Details page, leave all the defaults and click **Next**.

1. On the Options page, also leave all the defaults and click **Next**.

1. On the Review page, check the boxes to acknowledge that CloudFormation will create IAM resources and click **Create Change Set**.
	![Acknowledge IAM Screenshot](./images/0b-cfn-create-change-set.png)


1. Wait for the change set to finish computing changes and click **Execute**
	![Execute Change Set Screenshot](./images/0b-cfn-execute-change-set.png)

1. Wait for the `sfn-workshop-setup-webapp` stack to reach a status of `CREATE_COMPLETE`.

	The stack will take a minute of so to complete. As part ot that, it copies the web application sources over to the target bucket and that will trigger the delivery pipleline.

1. Go to the [AWS CodePipeline management console](http://console.aws.amazon.com/codepipeline/home). Click on the pipeline identified by `sfn-workshop-pipeline` and verify it finishes succesfully.  
	<img alt="Pipeline Screenshot" src="./images/0b-code-pipeline.png" width="50%">

1. Go to the [AWS CloudFormation management console](http://console.aws.amazon.com/cloudformation/home). With the stack `sfn-workshop-setup-webapp` selected click on the Outputs tab. The `WebsiteURL` key points at the link to access the **Media Sharing Web Application**

	![CloudFormation Outputs Screenshot](./images/0b-cfn-outputs.png)

1. Click on that link to navigate to the **Media Sharing Web Application**
**Note: Make sure to use Chrome browser to open the web application.**

	![Media Sharing Web Application Screenshot](./images/0b-webapp.png)

</p></details>



### Step 6B: Test the end-to-end workflow using the sample web app
##### Login
Pick any username to log in (This is a test app to showcase the backend so it's not using real user authentication. In an actual app, you can use Amazon Cognito to manage user sign-up and login.)

The username will be used in storing ownership metadata of the uploaded images.

##### Album list
Create new or select existing albums to upload images to.

##### Photo gallery
Upload images and see status updates when:

1. Upload to S3 bucket succeeds
2. The AWS Step Function execution is started. The execution ARN is provided in the UI so you can easily look up its details in the Step Functions [Console](https://console.aws.amazon.com/states/home)
3. The AWS Step Function execution completes

A sample set of extracted image metadata and recognized tags, along with the thumbnail generated in the Step Function execution is displayed for each uploaded image.

<img alt="Pipeline Screenshot" src="./images/web-app-screenshot.png" width="90%">


### Next step: extra credits 

Now you have built a end-to-end image processing workflow using Step Functions, ready for some fun challenges? 

See the [extra credits](./additional-steps.md) section

If you are ready to clean up resources created for this workshop, see the [cleanup](./clean-up.md) instructions

