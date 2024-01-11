In this project I visualized data using Amazon Quicksight.

The main steps summarized are:
1. Downloading a dataset of Best-selling amazon products
2. Storing my dataset using S3 bucekts
3. Connecting my S3 bucket with quicksight and creating visualizations

The first thing that I did was find a dataset of 50,000 best selling products on amazon. I downloaded this as a CSV file. The dataset is a real-life dataset from brightdata, this way I did not have to manually scrape the dataset.

After I had the dataset downloaded I navigated to the S3 service in my AWS console. I created a new S3 bucket with the default settings, and uploaded my CSV file to the S3 bucket. I then navigated to quicksight where I was using my trial of the enterprise version of 
quicksight. I linked my s3 bucket to amazon quicksight. In the quicksight dashboard I uploaded my S3 url so quicksight would be able to visualize my data. Below I will provide some visualizations that I was able to make from my dataset.![aws 1](https://github.com/BillyBlakee/AWS-Projects/assets/151226564/53061974-8057-443d-876d-303eb098b3dc)
![aws 1](https://github.com/BillyBlakee/AWS-Projects/assets/151226564/4ad03c5b-6860-4722-8200-582837b7dbd9)
Shows amout of products by brands
![aws 2](https://github.com/BillyBlakee/AWS-Projects/assets/151226564/1d94e8bd-05c5-4c85-8962-d15a52a4cc25)
![aws 3](https://github.com/BillyBlakee/AWS-Projects/assets/151226564/8603ef22-0eaf-4a79-8d7f-6605aea10d2f)
Shows brands pricing strategy
