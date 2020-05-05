# cloud-computing
Deeplens Face Detection &amp; Facial Recognition


AWS Deeplens Project documentation
By: Malik Warren


Security is a top priority in any project.

Create an IAM Role that will be used by a Lambda Function
Select: S3FullAccess, AmazonRekognitionReadOnlyAccess, CloudWatchFullAccess, CloudWatchLogsFullAccess, AWSIoTDataAccess
Create an additional role with the following Policies: AmazonS3FullAccess, AWSLambdaFullAccess

2. Create S3 Bucket, it will be used to store dataset images
	# All of this can be done via terminal (cloud9)
	Upload image of the first employee/family member
	Create Rekognition collection
		aws rekognition create-collection —collection-id <name_collection>
	After receiving confirmation message, you can add a face to the Rekogntion collection

aws rekognition index-faces \
       --image ‘{“S3Object”:{“Bucket”:"<name_of_your_database","Name":"malik-selfie.jpg"}}' \
       --collection-id “<cosc491-proj>“ \
       --detection-attributes "ALL" \
       --external-image-id “<myphoto.jpg>" 

Parse through the results and locate: Faceid: “xxxxxxxxxxxxxxxxxxx”

3. Create an employee/family profile using AWS 	DynamoDB
	1. Create a table using DynamoDB
		define attributes of table as: FaceId, AttributeType= <Additional information you may want>, key, and specify: region as us-east1
	2. Add record in the DynamoDB Table

aws dynamodb put-item --table-name <“table name”> --item '{ "FaceId": {"S": “<Faceid_from_previous_step>"}, “<Family/Employee>": {"<AttributeType>": “Hey! It’s Malik"}}'
4. Activate Deeplens
	1. Register device
	2. Deploy a Face detection example model
		(additional resources can be found under documentation below
	
3. Create a new lambda function by going to lambda services in AWS.
	select runtime as Python 2.7
	Set execution role permissions to the role created in (IAM Role 1.1) 
	Then create environment variable with key: “iot_topic” and value “worker-demo”
	change the timeout under basic settings to 10 secs 
	
4. Listed above are some screenshots of what these difference services after configuration.


5. After successfully setting up device and the necessary tools go to AWS IoT.
	1. Click on test
	2. Then go to a subscription and add the topic “rekognition”


Please Open PDF file to view screenshots
https://github.com/Mawar2/cloud-computing/blob/master/greengrass-deeplens/AWS%20-%20Project.pdf

Documentation:
https://www.aws.training/Details/Video?id=27179
https://docs.aws.amazon.com/deeplens/latest/dg/deeplens-inference-lambda-create.html
https://www.aws.training/Details/eLearning?id=32077
https://github.com/mahendrabairagi/DeeplensWorkshop/blob/master/FaceRekognition.md
