# 🚀 **End-to-End AWS Data Visualization Project**

## **Build an End-to-End AWS Project with QuickSight, DynamoDB, Athena, S3 & IAM**

### **Overview**
This project demonstrates how to integrate multiple AWS services to visualize data effectively. We will store task-related data in **DynamoDB**, query it using **Athena**, and visualize insights in **QuickSight** while utilizing **S3** for storage and **IAM** for access control.

---

## **Project Architecture**
![Image](https://github.com/user-attachments/assets/8e484544-c770-4fc6-bf8d-26b32c84030d)
---

## **🔧 Tech Stack**
- **Amazon DynamoDB** – NoSQL Database to store task data.
- **Amazon Athena** – SQL-based query engine for analyzing DynamoDB data.
- **AWS Glue** – Schema and metadata cataloging.
- **AWS Lambda** – Data transformation via Athena-DynamoDB Connector.
- **Amazon S3** – Temporary spill location for Athena queries.
- **Amazon QuickSight** – Dashboard for visualizing task data.
- **AWS IAM** – Secure access and permissions.

---

## **🛠️ Setup Instructions**

### **Step 1: Create a DynamoDB Table**
1. Navigate to **AWS Console > DynamoDB**.
2. Create a new table called `TasksTable`.
3. Set **Partition Key** as `taskID (String)` and **Sort Key** as `category (String)`.
4. Add sample data:
```json
{
  "taskID": "1",
  "taskName": "Build UI",
  "category": "Development",
  "completionStatus": true,
  "createdDate": "2025-03-01"
}
add extra tasks with my json txt file
```
![Image](https://github.com/user-attachments/assets/97fb0397-b0e7-40ce-a9fa-2c513f28e972)
![Image](https://github.com/user-attachments/assets/173712e6-ef67-44af-9ddf-edb9e4eea52b)
Query
![Image](https://github.com/user-attachments/assets/3e08b364-9564-4015-8d39-544ea8433cf7)

---

### **Step 2: Set Up Athena & AWS Glue**
1. Navigate to **AWS Console > Athena**.
2. Create a new **Data Source** and select **DynamoDB**.
3. Name it `DynamoDBTasks` and choose **AWS Glue** as the catalog.
4. Set **S3 Bucket** for spillover location (`s3://your-spill-bucket/`).
5. Run an Athena query to verify data retrieval:
```sql
SELECT * FROM "default"."taskstable" LIMIT 10;
```
![Image](https://github.com/user-attachments/assets/d5105f0f-7a81-490f-b58d-a55ffb08f3d2)

---

### **Step 3: Configure IAM Permissions**
1. Navigate to **AWS Console > IAM**.
2. Search for the role **QuickSightServiceRole**.
3. Attach the following policy to allow QuickSight access:
```json
{
  "Effect": "Allow",
  "Action": [
    "lambda:InvokeFunction",
    "s3:GetObject",
    "s3:ListBucket"
  ],
  "Resource": ["arn:aws:lambda:your-region:your-account-id:function:*"]
}
```
use the correct arn to get connect properly
![Image](https://github.com/user-attachments/assets/f0cd3d87-b309-46f1-8cef-078b022a9a41)
![Image](https://github.com/user-attachments/assets/47e1a760-2467-484e-ac88-7baf7918aae6)
![Image](https://github.com/user-attachments/assets/78b8eec0-8801-4dd4-adb8-023384903991)
![Image](https://github.com/user-attachments/assets/b0924bd8-0a1d-46d8-9da4-5ecfee1fa303)

---

### **Step 4: Connect QuickSight to Athena**
1. Navigate to **AWS Console > QuickSight**.
2. Select **Data Sources > New Data Source > Athena**.
3. Choose `DynamoDBTasks` as the database and `taskstable` as the table.
4. Select **Direct Query** mode for real-time data.
5. Click **Visualize**.
![Image](https://github.com/user-attachments/assets/92d7491b-9af2-4f97-bfbf-2032fb338075)
![Image](https://github.com/user-attachments/assets/44afdcae-c29f-4093-a04f-f8b25e28d817)
![Image](https://github.com/user-attachments/assets/e1052208-189e-4498-8f56-dccf820258d0)
![Image](https://github.com/user-attachments/assets/6e5bb2cf-aca1-4cbe-9ca6-b4aff76119db)


---

### **Step 5: Create QuickSight Visualizations**
#### **📊 Task Completion Pie Chart**
- Select **Donut Chart**.
- Add **Completion Status** as the `Group` field.
- Add **Task ID** as the `Value` field.
- Customize colors: ✅ Green for complete, ❌ Red for incomplete.

#### **📈 Tasks by Category Bar Chart**
- Select **Horizontal Bar Chart**.
- Add **Category** as the `Y-axis`.
- Add **Task ID (Count)** as the `Value`.
- Adjust sorting and labels.

#### **📃 Task List Table**
- Select **Table** visualization.
- Add columns: `Task Name`, `Created Date`, `Category`, `Completion Status`.

- Play with your creativity

![Image](https://github.com/user-attachments/assets/32e2354b-0a97-4045-802e-6a5af857b53a)
![Image](https://github.com/user-attachments/assets/2a43e76d-445b-4e04-ad1e-0352fcaffd36)
![Image](https://github.com/user-attachments/assets/8b4b62b9-660e-44cb-9368-6a20460574ed)

---

## **🚀 Deployment & Cleanup**

### **🚨 Cleanup Resources**
- **Delete DynamoDB Table**: `TasksTable`.
- **Remove Athena Data Source**: `DynamoDBTasks`.
- **Delete S3 Spill Bucket**: `your-spill-bucket`.
- **Revoke IAM Permissions**: Remove QuickSight IAM role policies.
- **Terminate QuickSight Subscription**: Avoid monthly charges!

---

## **🎯 Key Learnings**
✅ Integrating AWS services for real-time analytics.
✅ Querying NoSQL (DynamoDB) with SQL (Athena).
✅ Creating interactive dashboards in QuickSight.
✅ Managing AWS costs and permissions.

📌 **Consider adding a short demo video or GIF showcasing dashboard interactivity** 📌

---

## **📢 Contributing**
Feel free to fork this repo, raise issues, and contribute enhancements!

🌟 If you found this useful, don’t forget to ⭐ star the repo!

---

## **🔗 References & Further Reading**
- [AWS QuickSight Documentation](https://docs.aws.amazon.com/quicksight/latest/user/welcome.html)
- [DynamoDB Best Practices](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/best-practices.html)
- [Athena Pricing](https://aws.amazon.com/athena/pricing/)

---

🚀 **Happy Building!** 💻⚡
