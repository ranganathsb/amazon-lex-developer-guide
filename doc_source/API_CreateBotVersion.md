# CreateBotVersion<a name="API_CreateBotVersion"></a>

Creates a new version of the bot based on the `$LATEST` version\. If the `$LATEST` version of this resource hasn't changed since you created the last version, Amazon Lex doesn't create a new version\. It returns the last created version\.

**Note**  
You can update only the `$LATEST` version of the bot\. You can't update the numbered versions that you create with the `CreateBotVersion` operation\.

 When you create the first version of a bot, Amazon Lex sets the version to 1\. Subsequent versions increment by 1\. For more information, see [Versioning](versioning-aliases.md#versioning-intro)\. 

 This operation requires permission for the `lex:CreateBotVersion` action\. 

## Request Syntax<a name="API_CreateBotVersion_RequestSyntax"></a>

```
POST /bots/name/versions HTTP/1.1
Content-type: application/json

{
   "checksum": "string"
}
```

## URI Request Parameters<a name="API_CreateBotVersion_RequestParameters"></a>

The request requires the following URI parameters\.

 ** name **   
The name of the bot that you want to create a new version of\. The name is case sensitive\.   
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

## Request Body<a name="API_CreateBotVersion_RequestBody"></a>

The request accepts the following data in JSON format\.

 ** checksum **   
Identifies a specific revision of the `$LATEST` version of the bot\. If you specify a checksum and the `$LATEST` version of the bot has a different checksum, a `PreconditionFailedException` exception is returned and Amazon Lex doesn't publish a new version\. If you don't specify a checksum, Amazon Lex publishes the `$LATEST` version\.  
Type: String  
Required: No

## Response Syntax<a name="API_CreateBotVersion_ResponseSyntax"></a>

```
HTTP/1.1 201
Content-type: application/json

{
   "abortStatement": { 
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "checksum": "string",
   "childDirected": boolean,
   "clarificationPrompt": { 
      "maxAttempts": number,
      "messages": [ 
         { 
            "content": "string",
            "contentType": "string",
            "groupNumber": number
         }
      ],
      "responseCard": "string"
   },
   "createdDate": number,
   "description": "string",
   "failureReason": "string",
   "idleSessionTTLInSeconds": number,
   "intents": [ 
      { 
         "intentName": "string",
         "intentVersion": "string"
      }
   ],
   "lastUpdatedDate": number,
   "locale": "string",
   "name": "string",
   "status": "string",
   "version": "string",
   "voiceId": "string"
}
```

## Response Elements<a name="API_CreateBotVersion_ResponseElements"></a>

If the action is successful, the service sends back an HTTP 201 response\.

The following data is returned in JSON format by the service\.

 ** abortStatement **   
The message that Amazon Lex uses to abort a conversation\. For more information, see [PutBot](API_PutBot.md)\.  
Type: [Statement](API_Statement.md) object

 ** checksum **   
Checksum identifying the version of the bot that was created\.  
Type: String

 ** childDirected **   
For each Amazon Lex bot created with the Amazon Lex Model Building Service, you must specify whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to the Children's Online Privacy Protection Act \(COPPA\) by specifying `true` or `false` in the `childDirected` field\. By specifying `true` in the `childDirected` field, you confirm that your use of Amazon Lex **is** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. By specifying `false` in the `childDirected` field, you confirm that your use of Amazon Lex **is not** related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\. You may not specify a default value for the `childDirected` field that does not accurately reflect whether your use of Amazon Lex is related to a website, program, or other application that is directed or targeted, in whole or in part, to children under age 13 and subject to COPPA\.  
If your use of Amazon Lex relates to a website, program, or other application that is directed in whole or in part, to children under age 13, you must obtain any required verifiable parental consent under COPPA\. For information regarding the use of Amazon Lex in connection with websites, programs, or other applications that are directed or targeted, in whole or in part, to children under age 13, see the [Amazon Lex FAQ\.](https://aws.amazon.com/lex/faqs#data-security)   
Type: Boolean

 ** clarificationPrompt **   
The message that Amazon Lex uses when it doesn't understand the user's request\. For more information, see [PutBot](API_PutBot.md)\.   
Type: [Prompt](API_Prompt.md) object

 ** createdDate **   
The date when the bot version was created\.  
Type: Timestamp

 ** description **   
A description of the bot\.  
Type: String  
Length Constraints: Minimum length of 0\. Maximum length of 200\.

 ** failureReason **   
If `status` is `FAILED`, Amazon Lex provides the reason that it failed to build the bot\.  
Type: String

 ** idleSessionTTLInSeconds **   
The maximum time in seconds that Amazon Lex retains the data gathered in a conversation\. For more information, see [PutBot](API_PutBot.md)\.  
Type: Integer  
Valid Range: Minimum value of 60\. Maximum value of 86400\.

 ** intents **   
An array of `Intent` objects\. For more information, see [PutBot](API_PutBot.md)\.  
Type: Array of [Intent](API_Intent.md) objects

 ** lastUpdatedDate **   
The date when the `$LATEST` version of this bot was updated\.   
Type: Timestamp

 ** locale **   
 Specifies the target locale for the bot\.   
Type: String  
Valid Values:` en-US` 

 ** name **   
The name of the bot\.  
Type: String  
Length Constraints: Minimum length of 2\. Maximum length of 50\.  
Pattern: `^([A-Za-z]_?)+$` 

 ** status **   
 When you send a request to create or update a bot, Amazon Lex sets the `status` response element to `BUILDING`\. After Amazon Lex builds the bot, it sets `status` to `READY`\. If Amazon Lex can't build the bot, it sets `status` to `FAILED`\. Amazon Lex returns the reason for the failure in the `failureReason` response element\.   
Type: String  
Valid Values:` BUILDING | READY | FAILED | NOT_BUILT` 

 ** version **   
The version of the bot\.   
Type: String  
Length Constraints: Minimum length of 1\. Maximum length of 64\.  
Pattern: `\$LATEST|[0-9]+` 

 ** voiceId **   
The Amazon Polly voice ID that Amazon Lex uses for voice interactions with the user\.  
Type: String

## Errors<a name="API_CreateBotVersion_Errors"></a>

 **BadRequestException**   
The request is not well formed\. For example, a value is invalid or a required field is missing\. Check the field values, and try again\.  
HTTP Status Code: 400

 **ConflictException**   
 There was a conflict processing the request\. Try your request again\.   
HTTP Status Code: 409

 **InternalFailureException**   
An internal Amazon Lex error occurred\. Try your request again\.  
HTTP Status Code: 500

 **LimitExceededException**   
The request exceeded a limit\. Try your request again\.  
HTTP Status Code: 429

 **NotFoundException**   
The resource specified in the request was not found\. Check the resource and try again\.  
HTTP Status Code: 404

 **PreconditionFailedException**   
 The checksum of the resource that you are trying to change does not match the checksum in the request\. Check the resource's checksum and try again\.  
HTTP Status Code: 412

## See Also<a name="API_CreateBotVersion_SeeAlso"></a>

For more information about using this API in one of the language\-specific AWS SDKs, see the following:

+  [AWS Command Line Interface](http://docs.aws.amazon.com/goto/aws-cli/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for \.NET](http://docs.aws.amazon.com/goto/DotNetSDKV3/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for C\+\+](http://docs.aws.amazon.com/goto/SdkForCpp/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for Go](http://docs.aws.amazon.com/goto/SdkForGoV1/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for Java](http://docs.aws.amazon.com/goto/SdkForJava/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for JavaScript](http://docs.aws.amazon.com/goto/AWSJavaScriptSDK/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for PHP V3](http://docs.aws.amazon.com/goto/SdkForPHPV3/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for Python](http://docs.aws.amazon.com/goto/boto3/lex-models-2017-04-19/CreateBotVersion) 

+  [AWS SDK for Ruby V2](http://docs.aws.amazon.com/goto/SdkForRubyV2/lex-models-2017-04-19/CreateBotVersion) 