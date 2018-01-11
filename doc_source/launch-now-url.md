# Constructing a Launch Now URL<a name="launch-now-url"></a>

You can construct a custom uniform resource locator \(URL\) so that anyone can quickly deploy and run a predetermined web application in Elastic Beanstalk\. This URL is called a Launch Now URL\. You might need a Launch Now URL, for example, to demonstrate a web application that is built to run on Elastic Beanstalk\. With Launch Now URL, you can use parameters to add the required information to the Create Application wizard in advance\. When you do, anyone can use the URL link to launch an Elastic Beanstalk environment with your web application source in just a few clicks\. This means users don't need to manually upload or specify the location of the application source bundle or provide any additional input to the wizard\.

A Launch Now URL gives Elastic Beanstalk the minimum information required to create an application: the application name, solution stack, instance type, and environment type\. Elastic Beanstalk uses default values for other configuration details that are not explicitly specified in your custom Launch Now URL\.

A Launch Now URL uses standard URL syntax\. For more information, see [RFC 3986 \- Uniform Resource Identifier \(URI\): Generic Syntax](http://tools.ietf.org/html/rfc3986)\.

## URL Parameters<a name="using-features.deploy-existing-version.CON"></a>

The URL must contain the following parameters, which are case\-sensitive:

+ **region** – Specify an AWS region\. For a list of regions supported by Elastic Beanstalk, see [AWS Elastic Beanstalk](http://docs.aws.amazon.com/general/latest/gr/rande.html#elasticbeanstalk_region) in the *Amazon Web Services General Reference*\.

+ **applicationName** – Specify the name of your application\. Elastic Beanstalk displays the application name in the AWS Management Console to distinguish it from other applications\. By default, the application name also forms the basis of the environment name and environment URL\.

+ **solutionStackName** – Specify the platform and version that will be used for the environment\. For more information, see [Elastic Beanstalk Supported Platforms](concepts.platforms.md)\.

A Launch Now URL can optionally contain the following parameters\. If you do not include the optional parameters in your Launch Now URL, Elastic Beanstalk uses default values to create and run your application\. When you do not include the **sourceBundleUrl** parameter, Elastic Beanstalk uses the default sample application for the specified **solutionStackName**\.

+ **sourceBundleUrl** – Specify the location of your web application source bundle in URL format\. For example, if you uploaded your source bundle to an Amazon Simple Storage Service bucket, you might specify the value of the **sourceBundleUrl** parameter as `http://s3.amazonaws.com/mybucket/myobject`\.
**Note**  
You can specify the value of the **sourceBundleUrl** parameter as an HTTP URL, but the user's web browser will convert characters as needed by applying HTML URL encoding\.

+ **environmentType** – Specify whether the environment is load balancing and autoscaling or just a single instance\. For more information, see [Environment Types](using-features-managing-env-types.md)\. You can specify either `LoadBalancing` or `SingleInstance` as the parameter value\.

+ **tierName** – Specify whether the environment supports a web application that processes web requests or a web application that runs background jobs\. For more information, see [Worker Environments](using-features-managing-env-tiers.md)\. You can specify either `WebServer` or `Worker`,

+ **instanceType** – Specify a server with the characteristics \(including memory size and CPU power\) that are most appropriate to your application\. To see the instance types that are available in your Elastic Beanstalk region, see InstanceType in the topic [Configuration Options](command-options.md)\. To see the detailed specifications for each Amazon EC2 instance type, see [Instance Types](http://aws.amazon.com/ec2/instance-types/#instance-details)\.

+ **withVpc** – Specify whether to create the environment in an Amazon VPC\. You can specify either `true` or `false`\. For more information about using Elastic Beanstalk with Amazon VPC, see [Using Elastic Beanstalk with Amazon Virtual Private Cloud](vpc.md)\.

+ **withRds** – Specify whether to create an Amazon RDS database instance with this environment\. For more information, see [Using Elastic Beanstalk with Amazon Relational Database Service](AWSHowTo.RDS.md)\. You can specify either `true` or `false`\.

+ **rdsDBEngine** – Specify the database engine that you want to use for your Amazon EC2 instances in this environment\. You can specify `mysql`, `oracle-sel`, `sqlserver-ex`, `sqlserver-web`, or `sqlserver-se`\. The default value is `mysql`\.

+ **rdsDBAllocatedStorage** – Specify the allocated database storage size in gigabytes\. You can specify the following values:

  + **MySQL** – `5` to `1024`\. The default is `5`\.

  + **Oracle** – `10` to `1024`\. The default is `10`\.

  + **Microsoft SQL Server Express Edition** – `30`\.

  + **Microsoft SQL Server Web Edition** – `30`\.

  + **Microsoft SQL Server Standard Edition** – `200`\.

+ **rdsDBInstanceClass** – Specify the database instance type\. The default value is `db.t2.micro` \(`db.m1.large` for an environment not running in an Amazon VPC\)\. For a list of database instance classes supported by Amazon RDS, see [DB Instance Class](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.DBInstanceClass.html) in the * Amazon Relational Database Service User Guide*\.

+ **rdsMultiAZDatabase** – Specify whether Elastic Beanstalk needs to create the database instance across multiple Availability Zones\. You can specify either `true` or `false`\. For more information about multiple Availability Zone deployments with Amazon RDS, go to [Regions and Availability Zones](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html) in the * Amazon Relational Database Service User Guide*\.

+ **rdsDBDeletionPolicy** – Specify whether to delete or snapshot the database instance on environment termination\. You can specify either `Delete` or `Snapshot`\.

## Example<a name="w3ab1c19c35c30c11"></a>

The following is an example Launch Now URL\. After you construct your own, you can give it to your users\. For example, you might want to embed the URL on a web page or in training materials\. When users create an application using the Launch Now URL, the Elastic Beanstalk Create an Application wizard requires no additional input\.

 `https://console.aws.amazon.com/elasticbeanstalk/?region=us-west-2#/newApplication?applicationName=YourCompanySampleApp&solutionStackName=PHP&sourceBundleUrl=http://s3.amazonaws.com/mybucket/myobject&environmentType=SingleInstance&tierName=WebServer&instanceType=m1.small&withVpc=true&withRds=true&rdsDBEngine=postgres&rdsDBAllocatedStorage=6&rdsDBInstanceClass=db.m1.small&rdsMultiAZDatabase=true&rdsDBDeletionPolicy=Snapshot.`

When users click a Launch Now URL, Elastic Beanstalk displays a page similar to the following\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/images/aeb-launch-now-page.png)

**To use the Launch Now URL**

1. Click the Launch Now URL\.

1. When the Elastic Beanstalk console opens, on the **Application Info** page, click **Review and Launch** to view the settings Elastic Beanstalk will use to create the application and launch the environment in which the application runs\.

1. On the **Review** page, click **Launch** to create the application\.