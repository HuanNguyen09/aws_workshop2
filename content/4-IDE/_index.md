---
title: "Creating Simulated Data"
date: "`r Sys.Date()`"
weight: 4
chapter: false
pre: " <b> 4. </b> "
---

In this workshop, since we do not have direct data from sensors, we will use Visual Studio Code to generate simulated data regarding the number of vehicles traveling on four different routes: "Route A," "Route B," "Route C," and "Route D." We will then send this data to the Kinesis data stream to continue the processing and analysis.

{{% notice note %}}
Note: The data is sent in JSON format as follows: **{
  "timestamp": "2023-08-15 19:22:02",
  "route": "Route B",
  "count": 75
}**
{{% /notice %}}

### Implementation Steps:

#### Part 1 - Sending Data
1. Open **Visual Studio Code** and create a new file named **createData.py**. Then open the **Terminal** to establish a connection with AWS using the previously created **Access Key**.
   - Use the command: 
   ``` 
   aws configure
   ```
   - Fill in the **Access Key - Secret access key - region name - output format** one by one.
     - **Access Key - Secret access key**: Get this information from Part 2.
     - **region name**: The region you are working in, such as `ap-southeast-1`.
     - **output format**: `json`

   ![0](/images/4-IDE/img-78.png)

2. Copy and paste the following code into the newly created file.

```python
import random
import json
import boto3
import time
from datetime import datetime

# Create a connection to Kinesis Data Streams
client = boto3.client('kinesis', region_name='ap-southeast-1')
stream_name = 'demo'

# List of routes
routes = ["Route A", "Route B", "Route C", "Route D"]

# Function to generate simulated traffic events for all routes
def generate_traffic_event(route):
    count = random.randint(30, 100)  # Number of vehicles on the route, 30-100
    timestamp = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    event_data = {
        'timestamp': timestamp,
        'route': route,
        'count': count
    }
    return json.dumps(event_data)

# Send simulated data to the data stream for all routes
while True:
    for route in routes:
        event_data = generate_traffic_event(route)
        response = client.put_record(
            StreamName=stream_name,
            Data=bytes(event_data, 'utf-8'),
            PartitionKey='123'
        )
        print(f"Sent: {event_data}")
        time.sleep(1)
    time.sleep(30)
```

![0](/images/4-IDE/img-73.png)

3. Click the triangle icon in the upper-right corner (Run code) to execute it. You will see notifications of the sent data in the terminal window.
   ![0](/images/4-IDE/img-71.png)

#### Part 2 - Checking Data Sent to Kinesis:

1. Open the Kinesis service. Choose the **Data Streams** that we created earlier.
   ![0](/images/4-IDE/img-70.png)

2. Go to the **Data viewer** tab. Select **Shard** as **ShardId-00000000000**, choose **Trim horizon** for **Starting position**, and then click **Get records**.
   ![0](/images/4-IDE/img-69.png)

Here, you will see the 4 lines of data that were sent earlier. This indicates that Kinesis has received the data.
