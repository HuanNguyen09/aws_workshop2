---
title: "Khởi tạo S3"
date: "`r Sys.Date()`"
weight: 1
chapter: false
pre: " <b> 5.2 </b> "
---
#### Trước tiên, ta tạo role trong **AIM**
1. Nhập **S3** ở thanh tìm kiếm service trên AWS Console sau đó chọn **S3**.
![0](/images/5-Databases/s3/img-38.png)

2. Chọn **Create bucket**.
![0](/images/5-Databases/s3/img-37.png)

3. **Bucket name** nhập `webanalytics-huannguyen`.
![0](/images/5-Databases/s3/img-36.png)

4. Bỏ chọn **"Block all public access"**. Sau đó tích chọn **"I acknowledge that the current settings might result in this bucket and the objects within becoming public."**.
![0](/images/5-Databases/s3/img-35.png)

5. Giữ nguyên các cấu hình mặc định khác. Chọn **Create bucket**.
![0](/images/5-Databases/s3/img-34.png)

6. Chọn tab **Properties** vào kéo xuống cuối trang.

![0](/images/5-Databases/s3/img-30.png)

7. Tại phần **Static website hosting**, chọn **Edit**.
![0](/images/5-Databases/s3/img-29.png)

8. Phần **Static website hosting**, chọn **Enable**. Sau đó lần lượt nhập `index.html` và `error.html` vào ô **Index document** và **Error document**. Cuối cùng chọn **Save changes**.
![0](/images/5-Databases/s3/img-28.png)

9. Chọn tab **Permissions**. Sau đó, tại **Bucket policy** chọn **Edit**.
![0](/images/5-Databases/s3/img-27.png)

10. Sao chép và dán đoạn mã sau. Tiếp theo, chọn **Save changes**
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "Statement1",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::webanalytics-huannguyen/*"
        }
    ]
}
```
{{% notice warning %}}
Lưu ý: phần **Resource** cần điền chính xác bucket chúng ta sử dụng.
{{% /notice %}}

![0](/images/5-Databases/s3/img-26.png)

11. Tiếp theo, chúng ta sử dụng Visual Studio Code để tạo file **index.html** với đoạn mã sau:

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Data Visualization with D3.js</title>
  <!-- Import D3.js -->
  <script src="https://d3js.org/d3.v6.min.js"></script>
</head>
<body>
  <div style="width: 80%; margin: auto;">
    <!-- SVG element for drawing the chart -->
    <svg id="dataChart"></svg>
  </div>
  
  <!-- Data table display -->
  <div>
    <h2>Data Table</h2>
    <table>
      <thead>
        <tr>
          <th>Timestamp</th>
          <th>Route</th>
          <th>Count</th>
        </tr>
      </thead>
      <tbody id="dataTableBody"></tbody>
    </table>
  </div>
  
  <script>
    // Function to fetch and process data from the data.json file
    async function fetchData() {
      const response = await fetch('data.json');
      const data = await response.json();
      
      // Sort data by timestamp before rendering
      data.sort((a, b) => new Date(a.timestamp) - new Date(b.timestamp));
      
      return data;
    }
    
    // Initialize the chart and table
    async function initChart() {
      const data = await fetchData();
      
      const width = 800;
      const height = 400;
      
      // Select the SVG element for the chart
      const svg = d3.select('#dataChart')
        .attr('width', width)
        .attr('height', height);
      
      // Create a list of timestamps from the data
      const timestamps = data.map(entry => new Date(entry.timestamp));
      
      // Create a list of route names from the data
      const routeNames = Array.from(new Set(data.map(entry => entry.route)));
      
      // Define scaling for the x and y axes
      const xScale = d3.scaleTime()
        .domain(d3.extent(timestamps))
        .range([60, width - 40]);
      
      const yScale = d3.scaleLinear()
        .domain([0, d3.max(data, d => d.count)])
        .range([height - 40, 20]);
      
      // Create data lines for each route
      for (let i = 0; i < routeNames.length; i++) {
        const routeData = data.filter(d => d.route === routeNames[i]);
        
        // Define the line generator function
        const line = d3.line()
          .x((d, i) => xScale(new Date(d.timestamp)))
          .y(d => yScale(d.count));
        
        // Draw the data line on the chart
        svg.append('path')
          .datum(routeData)
          .attr('fill', 'none')
          .attr('stroke', d3.schemeCategory10[i]) // Different color for each route
          .attr('stroke-width', 2)
          .attr('d', line);
        
        // Display data in the table
        const dataTableBody = d3.select('#dataTableBody');
        routeData.forEach(entry => {
          dataTableBody.append('tr')
            .html(`<td>${entry.timestamp}</td><td>${entry.route}</td><td>${entry.count}</td>`);
        });
        
        // Add legend for each route
        svg.append('circle')
          .attr('cx', width - 100)
          .attr('cy', 20 + i * 20)
          .attr('r', 6)
          .attr('fill', d3.schemeCategory10[i]);
        
        svg.append('text')
          .attr('x', width - 90)
          .attr('y', 25 + i * 20)
          .attr('font-size', '12px')
          .text(routeNames[i]);
      }
      
      // Add x and y axes
      const xAxis = d3.axisBottom(xScale)
        .ticks(5);
      
      const yAxis = d3.axisLeft(yScale)
        .ticks(5);
      
      svg.append('g')
        .attr('transform', `translate(40, ${height - 40})`)
        .call(xAxis);
      
      svg.append('g')
        .attr('transform', `translate(40, 0)`)
        .call(yAxis);
      
      // Add gridlines
      svg.append('g')
        .attr('class', 'grid')
        .attr('transform', `translate(40, 0)`)
        .call(d3.axisLeft(yScale).ticks(5).tickSize(-width + 60).tickFormat(''));
      
      svg.append('g')
        .attr('class', 'grid')
        .attr('transform', `translate(40, ${height - 40})`)
        .call(d3.axisBottom(xScale).ticks(5).tickSize(-height + 60).tickFormat(''));
    }
    
    // Call the initChart function to initialize the chart and table
    initChart();
    
    // Automatically refresh the page every 10 seconds
    setInterval(() => {
      location.reload();
    }, 10000);
  </script>
</body>
</html>

```

![0](/images/5-Databases/s3/img-33.png)

12. Upload file **index.html** vừa tạo lên S3:

![0](/images/5-Databases/s3/img-32.png)


![0](/images/5-Databases/s3/img-31.png)

13. Sau khi upload file thành công. Ta quay lại tab **Properties** và kéo xuống cuối trang. Tại đây chúng ta sẽ thấy đường link của website. Click vào đường link.
![0](/images/5-Databases/s3/img-25.png)

14. Website hiện thị như sau là thành công.
![0](/images/5-Databases/s3/img-24.png)

{{% notice note %}}
Ghi chú: Hiện tại trong S3 vẫn chưa có dữ liệu nên trang web vẫn trống, chưa chứa nhiều thông tin.
{{% /notice %}}