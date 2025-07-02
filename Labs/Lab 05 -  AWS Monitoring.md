## 🧪 Task 1: Launch a test EC2 instance

We will launch a simple EC2 instance to monitor later.

1. Go to the AWS Console.
2. In the top search bar, type `EC2` and select the **EC2** service.
3. On the left menu, click **Instances**, then click **Launch instances**.
4. Name your instance `Monitoring-Test-Instance`.
5. For AMI, choose **Amazon Linux 2023** (or latest).
6. Choose `t2.micro` instance type (Free Tier eligible).
7. Under **Key pair (login)**, select an existing key pair or create a new one.
8. Click **Launch instance** at the bottom, then click **View all instances** to confirm it's running.

---

## 🧪 Task 2: Enable basic monitoring in CloudWatch

1. From the AWS Console, search for `CloudWatch` and click on it.
2. In the left menu, click **EC2** under **Metrics**.
3. Click **Per-Instance Metrics** and select your instance name.
4. View metrics like **CPUUtilization**, **NetworkIn**, **NetworkOut**.
5. Click on any metric (e.g., `CPUUtilization`) to open a detailed graph.
6. Click **Actions** > **Add to dashboard** to save this chart.
7. Create a new dashboard called `EC2-Monitoring`.
8. Save and explore your new dashboard.

---

## 🧪 Task 3: Create a CloudWatch Alarm

1. In CloudWatch, go to **Alarms** > **All alarms** on the left menu.
2. Click **Create alarm**.
3. Click **Select metric** > **EC2** > **Per-Instance Metrics**.
4. Choose `CPUUtilization` for your instance and click **Select metric**.
5. Set the threshold:
   - Whenever CPU is **Greater than 50%** for **5 minutes**.
6. Click **Next**.
7. For notification, choose **"Create new SNS topic"** and give it a name (e.g., `MyAlarmTopic`).
8. Enter your email to receive alarm notifications and confirm your email subscription afterward.

---

## 🧪 Task 4: Enable and explore CloudTrail

1. In the AWS Console, search for `CloudTrail` and click on it.
2. If prompted, click **Create trail**.
3. Name your trail `MonitorTrail`.
4. Apply trail to **All Regions**.
5. Choose `Create new S3 bucket` to store logs (e.g., `cloudtrail-monitoring-logs-<yourname>`).
6. Click **Create trail** and wait for confirmation.
7. Now simulate activity: go to EC2 and **stop your instance**.
8. Go back to CloudTrail > **Event history**, and look for the `StopInstances` event.

---

## 🧪 Task 5: Create a custom CloudWatch Dashboard

1. In CloudWatch, go to **Dashboards** > **Create dashboard**.
2. Name it `Full-Monitoring-Dashboard`.
3. Choose **Line** widget and click **Next**.
4. Under **Browse**, go to **EC2** > **Per-Instance Metrics** and select:
   - `CPUUtilization`
   - `DiskReadBytes`
   - `NetworkOut`
5. Click **Create widget** and repeat for other metrics you want.
6. Use **Text widget** to label sections of your dashboard.
7. Save the dashboard and try resizing/moving widgets.
8. Bookmark the dashboard for quick access.

---

## 🧪 Task 6: Simulate and respond to a CloudWatch Alarm

1. Start your EC2 instance again if it's stopped.
2. Connect to your EC2 instance (via EC2 Connect or SSH).
3. Run a CPU stress test to trigger the alarm:
   ```bash
   sudo yum install -y stress
   stress --cpu 2 --timeout 300
