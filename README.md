# Sales Data Projection System

The **Sales Data Projection System** is a real-time data pipeline designed to process dynamic and high-volume sales data. It leverages AWS services and Python automation for seamless data generation, transformation, storage, and analysis. 

---

## **Key Features**

1. **Mock Data Generation**
   - Generates random sales data for testing and validation.
   - Inserts the generated data into an AWS DynamoDB table (`OrderTable`).

2. **Data Transformation Layer**
   - Cleanses, validates, and transforms raw data from DynamoDB Streams.
   - Converts DynamoDB records into a structured format suitable for analysis.

---

## **System Architecture**

### **1. Mock Data Generation**
- **File:** `mock_data_generator_for_dynamodb.py`
- **Description:**
  - Simulates sales orders with random `orderid`, `product_name`, `quantity`, and `price`.
  - Inserts the generated data into DynamoDB using the `put_item` API.
- **Key Details:**
  - Configured for AWS profile `default` and region `us-east-1`.
  - Runs continuously, generating a new record every 3 seconds.

### **2. Data Transformation Layer**
- **File:** `transformation_layer_with_lambda.py`
- **Description:**
  - Processes records from DynamoDB Streams.
  - Extracts, transforms, and encodes fields from the `NewImage` field of a stream record.
  - Handles both successful and failed processing cases.
- **Workflow:**
  - Decodes input data from base64.
  - Parses and validates fields (`orderid`, `product_name`, `quantity`, `price`).
  - Encodes transformed data back into base64 for downstream processing.

---
