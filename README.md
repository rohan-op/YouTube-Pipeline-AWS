# YouTube Pipeline using AWS

This project involves setting up an AWS-based data pipeline to store YouTube trending videos data and process it using AWS services. The pipeline fetches, cleans, and transforms raw data received from the YouTube API. For testing purposes, the project utilizes the YouTube dataset available on Kaggle: [YouTube New](https://www.kaggle.com/datasets/datasnaek/youtube-new).

![Architecture](architecture.jpeg)

## Prerequisites

Before starting this project, you need an AWS account. If you don't have one, you can create a free AWS account [here](https://aws.amazon.com/free/?trk=78b916d7-7c94-4cab-98d9-0ce5e648dd5f&sc_channel=ps&ef_id=Cj0KCQiA5-uuBhDzARIsAAa21T_IFpDtNHGF5_WERClO9FMRGx_EYED-GB9JZtDqFOAZI0K1doK7a70aAhKBEALw_wcB:G:s&s_kwcid=AL!4422!3!432339156165!e!!g!!aws%20account!9572385111!102212379047&gclid=Cj0KCQiA5-uuBhDzARIsAAa21T_IFpDtNHGF5_WERClO9FMRGx_EYED-GB9JZtDqFOAZI0K1doK7a70aAhKBEALw_wcB&all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all).

## Steps

1. **Create an IAM User**: Avoid using the root account to create resources. Instead, create an IAM user with the following access:
    - S3
    - Lambda
    - Glue
    - Athena
    - IAM full access

2. **Set up S3 Bucket**: Create a new bucket on S3. This bucket will serve as your data lake.

3. **Push Data to S3**: Utilize the commands mentioned in `s3_cli_commands` to push the data to S3. Ensure that you replace placeholders with your bucket name and the local data location.

4. **Handle Reference Data with Lambda**: The reference data is in JSON format. Due to its complex nature and deviation from Serde guidelines, Glue crawler cannot accurately crawl through it. For this, create a Lambda function with the following steps:
    - Attach a role created using IAM, providing Lambda access to S3 and Glue.
    - Attach a Lambda layer containing the AWS Wrangler library.
    - Use the provided code in `lambda_function.py`.
    - Set environment variables and ensure all paths are correct.

5. **Test the Lambda Function**: Create a test that mimics the S3 Put function. Check if the cleaned data populates in your S3 bucket.

## Additional Notes

- Ensure proper configuration and permissions are set for all AWS resources involved.
- Monitor AWS services for any incurred costs, especially if your usage exceeds the free tier limits.
- Document your steps and configurations for future reference and troubleshooting.

This README provides a basic overview of setting up a YouTube data pipeline using AWS services. Adjustments may be required based on specific project requirements and AWS environment configurations.
