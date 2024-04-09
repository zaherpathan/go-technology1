# terraform resources for ec2 instances 
resource "aws_instance" "web" {
  ami           = "ami-080e1f13689e07408"
  instance_type = "t3.micro"

  tags = {
    Name = "HelloWorld"
  }
}

# requirements.txt file 
vi requiretments.txt
import boto3
import pymysql

# pythonscript file
vi ./your_script.py
import boto3
import pymysql
from botocore.exceptions import ClientError

def read_data_from_s3(bucket_name, key):
    s3 = boto3.client('s3')
    response = s3.get_object(Bucket=go-digital, Key=MYsqlCodes.txt)
    data = response['Body'].read().decode('utf-8')
    return data

def push_to_rds(data, db_endpoint, db_username, db_password, db_name):
    conn = pymysql.connect(host=database-1.cdaiegiuuwl6.us-east-1.rds.amazonaws.com,
                           user=admin,
                           password=zaher123,
                           database=database-1,
                           connect_timeout=5)
    with conn.cursor() as cursor:
        # Assuming data is a string separated by newline characters
        for line in data.split('\n'):
            cursor.execute("INSERT INTO your_table_name (column_name) VALUES (%s)", (line,))
        conn.commit()
    conn.close()

def push_to_glue_database(data, database_name, table_name):
    # Code to push data to Glue Database
    pass

def main():
    bucket_name = 'go-digital'
    key = 'MYsqlCodes.txt'
    db_endpoint = 'database-1.cdaiegiuuwl6.us-east-1.rds.amazonaws.com'
    db_username = 'admin'
    db_password = 'zaher123'
    db_name = 'database-1'
    
    data = read_data_from_s3(bucket_name, key)
    
    try:
        push_to_rds(data, db_endpoint, db_username, db_password, db_name)
        print("Data pushed to RDS successfully.")
    except pymysql.MySQLError as e:
        print(f"Failed to push data to RDS: {e}")
        try:
            push_to_glue_database(data, 'your_glue_database_name', 'your_table_name')
            print("Data pushed to Glue Database successfully.")
        except Exception as e:
            print(f"Failed to push data to Glue Database: {e}")

if __name__ == "__main__":
    main()

# vi Dockerfile 
FROM python:3.9
WORKDIR /app
COPY your_script.py /app
RUN pip install --no-cache-dir -r requirements.txt
CMD ["python", "./your_script.py"]

# command to build the image 
 docker build -t imagename .

 
