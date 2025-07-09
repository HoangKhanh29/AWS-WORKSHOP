---
title : "Web Interface"
date: 2025-06-18
weight : 5
chapter : false
pre : " <b> 4.5. </b> "
---
1. Tạo S3 Bucket cho Website
- Bucket name: ``yourname-serverless-website-2025``
![Picture80](/images/4.5/image80.png)
- Region: ap-southeast-1
- Uncheck "Block all public access" ⚠️
- Acknowledge warning
![Picture81](/images/4.5/image81.png)
- Encryption type chọn Server-side encryption with Amazon S3 managed keys (SSE-S3)
- Bucket Key: Enable
- Create bucket
![Picture82](/images/4.5/image82.png)
![Picture83](/images/4.5/image83.png)
2. Enable Static Website Hosting:
- Vào bucket → Properties → Static website hosting
![Picture84](/images/4.5/image84.png)
- Enable → Index document: ``index.html``
![Picture85](/images/4.5/image85.png)
- Save changes
![Picture86](/images/4.5/image86.png)
- Copy Website endpoint URL
3. Tạo file HTML:
- Tạo file `index.html` với nội dung sau:

```html
<!DOCTYPE html>
<html>
<head>
    <title>🚀 Serverless File Upload Dashboard</title>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body { 
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            max-width: 1200px; margin: 0 auto; padding: 20px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh; color: #333;
        }
        .container {
            background: white; border-radius: 12px; padding: 30px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
        }
        .header { text-align: center; margin-bottom: 30px; }
        .header h1 { margin: 0; color: #667eea; font-size: 2.5em; }
        .upload-zone { 
            border: 3px dashed #ccc; padding: 50px; text-align: center; 
            margin: 20px 0; border-radius: 12px; cursor: pointer;
            transition: all 0.3s ease;
        }
        .upload-zone:hover { 
            border-color: #667eea; background: #f8f9ff;
            transform: translateY(-2px);
        }
        .upload-zone.dragover {
            border-color: #667eea; background: #f0f8ff;
            transform: scale(1.02);
        }
        .stats { 
            display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); 
            gap: 20px; margin: 30px 0; 
        }
        .stat-card { 
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); 
            color: white; padding: 25px; border-radius: 12px; text-align: center;
            box-shadow: 0 8px 16px rgba(102, 126, 234, 0.3);
        }
        .stat-card h3 { margin: 0 0 10px 0; font-size: 1.1em; }
        .stat-card .value { font-size: 2em; font-weight: bold; }
        .file-list { 
            background: #f8f9fa; border: 1px solid #e9ecef; 
            border-radius: 12px; padding: 25px; margin: 20px 0;
        }
        .file-item {
            display: flex; justify-content: space-between; align-items: center;
            padding: 15px; background: white; margin: 10px 0;
            border-radius: 8px; border-left: 4px solid #667eea;
        }
        .file-item .info { flex: 1; }
        .file-item .name { font-weight: bold; color: #333; }
        .file-item .details { color: #666; font-size: 0.9em; }
        .file-item .status { 
            padding: 5px 12px; border-radius: 20px; font-size: 0.8em;
            font-weight: bold; text-transform: uppercase;
        }
        .status.uploading { background: #fff3cd; color: #856404; }
        .status.success { background: #d4edda; color: #155724; }
        .status.error { background: #f8d7da; color: #721c24; }
        .upload-progress {
            width: 100%; height: 6px; background: #e9ecef;
            border-radius: 3px; overflow: hidden; margin: 5px 0;
        }
        .upload-progress-bar {
            height: 100%; background: #667eea; transition: width 0.3s;
        }
        .config-section {
            background: #f8f9fa; padding: 20px; border-radius: 8px;
            margin: 20px 0; border: 1px solid #e9ecef;
        }
        .config-input {
            width: 100%; padding: 10px; margin: 5px 0;
            border: 1px solid #ddd; border-radius: 4px;
        }
        .btn {
            padding: 10px 20px; border: none; border-radius: 6px;
            cursor: pointer; font-weight: bold; transition: all 0.3s;
        }
        .btn-primary { background: #667eea; color: white; }
        .btn-primary:hover { background: #5a67d8; transform: translateY(-1px); }
        .alert { padding: 15px; margin: 10px 0; border-radius: 6px; }
        .alert-success { background: #d4edda; color: #155724; border: 1px solid #c3e6cb; }
        .alert-error { background: #f8d7da; color: #721c24; border: 1px solid #f5c6cb; }
        .alert-warning { background: #fff3cd; color: #856404; border: 1px solid #ffeaa7; }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>📁 Serverless File Upload Dashboard</h1>
            <p>Upload files to AWS S3 with serverless processing</p>
        </div>

        <!-- Configuration Section -->
        <div class="config-section">
            <h3>⚙️ AWS Configuration</h3>
            <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                <div>
                    <label>S3 Bucket Name:</label>
                    <input type="text" id="bucketName" class="config-input" placeholder="yourname-serverless-demo-2025">
                </div>
                <div>
                    <label>AWS Region:</label>
                    <input type="text" id="awsRegion" class="config-input" value="ap-southeast-1">
                </div>
            </div>
            <button class="btn btn-primary" onclick="saveConfig()">💾 Save Configuration</button>
            <div id="configAlert"></div>
        </div>
        
        <!-- Stats Dashboard -->
        <div class="stats">
            <div class="stat-card">
                <h3>📤 Total Uploads</h3>
                <div class="value" id="totalUploads">0</div>
            </div>
            <div class="stat-card">
                <h3>📊 Storage Used</h3>
                <div class="value" id="storageUsed">0 MB</div>
            </div>
            <div class="stat-card">
                <h3>⚡ Processing Queue</h3>
                <div class="value" id="queueSize">0</div>
            </div>
            <div class="stat-card">
                <h3>✅ Success Rate</h3>
                <div class="value" id="successRate">100%</div>
            </div>
        </div>
        
        <!-- Upload Zone -->
        <div class="upload-zone" id="uploadZone" onclick="document.getElementById('fileInput').click()">
            <h3>🚀 Drop files here or click to upload</h3>
            <p>Supported formats: Images, Documents, Text files (Max 10MB each)</p>
            <input type="file" id="fileInput" multiple style="display: none;" onchange="handleFileUpload(event)">
        </div>
        
        <!-- File List -->
        <div class="file-list">
            <h3>📋 Recent Uploads</h3>
            <div id="fileList">
                <div style="text-align: center; color: #666; padding: 20px;">
                    No files uploaded yet. Try uploading some files! 📁
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global variables
        let uploadedFiles = [];
        let totalUploads = 0;
        let totalSize = 0;
        let bucketName = '';
        let awsRegion = 'ap-southeast-1';

        // Initialize on page load
        window.onload = function() {
            loadConfig();
            updateDashboard();
            setupDragAndDrop();
        };

        // Save configuration
        function saveConfig() {
            bucketName = document.getElementById('bucketName').value;
            awsRegion = document.getElementById('awsRegion').value;
            
            if (!bucketName) {
                showAlert('configAlert', 'Please enter S3 bucket name', 'error');
                return;
            }
            
            localStorage.setItem('serverless-config', JSON.stringify({
                bucketName: bucketName,
                awsRegion: awsRegion
            }));
            
            showAlert('configAlert', '✅ Configuration saved successfully!', 'success');
        }

        // Load configuration
        function loadConfig() {
            const saved = localStorage.getItem('serverless-config');
            if (saved) {
                const config = JSON.parse(saved);
                document.getElementById('bucketName').value = config.bucketName;
                document.getElementById('awsRegion').value = config.awsRegion;
                bucketName = config.bucketName;
                awsRegion = config.awsRegion;
            }
        }

        // Setup drag and drop
        function setupDragAndDrop() {
            const uploadZone = document.getElementById('uploadZone');
            
            uploadZone.addEventListener('dragover', (e) => {
                e.preventDefault();
                uploadZone.classList.add('dragover');
            });
            
            uploadZone.addEventListener('dragleave', () => {
                uploadZone.classList.remove('dragover');
            });
            
            uploadZone.addEventListener('drop', (e) => {
                e.preventDefault();
                uploadZone.classList.remove('dragover');
                const files = e.dataTransfer.files;
                handleFileUpload({target: {files: files}});
            });
        }

        // Handle file upload
        function handleFileUpload(event) {
            if (!bucketName) {
                showAlert('configAlert', 'Please configure S3 bucket name first!', 'warning');
                return;
            }

            const files = Array.from(event.target.files);
            
            files.forEach(file => {
                // Validate file size (10MB limit)
                if (file.size > 10 * 1024 * 1024) {
                    alert(`File ${file.name} is too large. Max size is 10MB.`);
                    return;
                }
                
                uploadFileToS3(file);
            });
        }

        // Upload file to S3 (Simulated)
        function uploadFileToS3(file) {
            const fileId = 'file_' + Date.now() + '_' + Math.random().toString(36).substr(2, 9);
            const fileInfo = {
                id: fileId,
                name: file.name,
                size: file.size,
                type: file.type,
                uploadTime: new Date().toISOString(),
                status: 'uploading',
                progress: 0
            };
            
            uploadedFiles.unshift(fileInfo);
            updateFileList();
            
            // Simulate upload progress
            simulateUpload(fileInfo);
        }

        // Simulate upload progress
        function simulateUpload(fileInfo) {
            const progressInterval = setInterval(() => {
                fileInfo.progress += Math.random() * 20;
                
                if (fileInfo.progress >= 100) {
                    fileInfo.progress = 100;
                    fileInfo.status = 'success';
                    totalUploads++;
                    totalSize += fileInfo.size;
                    clearInterval(progressInterval);
                    
                    // Simulate S3 trigger → Lambda → SNS
                    setTimeout(() => {
                        showNotification(`✅ File ${fileInfo.name} processed successfully!`);
                    }, 2000);
                }
                
                updateFileList();
                updateDashboard();
            }, 500);
        }

        // Update file list display
        function updateFileList() {
            const fileList = document.getElementById('fileList');
            
            if (uploadedFiles.length === 0) {
                fileList.innerHTML = '<div style="text-align: center; color: #666; padding: 20px;">No files uploaded yet. Try uploading some files! 📁</div>';
                return;
            }
            
            fileList.innerHTML = uploadedFiles.map(file => `
                <div class="file-item">
                    <div class="info">
                        <div class="name">${file.name}</div>
                        <div class="details">
                            ${formatFileSize(file.size)} • ${file.type || 'Unknown type'} • ${formatDate(file.uploadTime)}
                        </div>
                        ${file.status === 'uploading' ? `
                            <div class="upload-progress">
                                <div class="upload-progress-bar" style="width: ${file.progress}%"></div>
                            </div>
                        ` : ''}
                    </div>
                    <div class="status ${file.status}">
                        ${file.status === 'uploading' ? `${Math.round(file.progress)}%` : file.status}
                    </div>
                </div>
            `).join('');
        }

        // Update dashboard stats
        function updateDashboard() {
            document.getElementById('totalUploads').textContent = totalUploads;
            document.getElementById('storageUsed').textContent = formatFileSize(totalSize);
            document.getElementById('queueSize').textContent = uploadedFiles.filter(f => f.status === 'uploading').length;
            
            const successRate = totalUploads > 0 ? Math.round((uploadedFiles.filter(f => f.status === 'success').length / totalUploads) * 100) : 100;
            document.getElementById('successRate').textContent = successRate + '%';
        }

        // Utility functions
        function formatFileSize(bytes) {
            if (bytes === 0) return '0 B';
            const k = 1024;
            const sizes = ['B', 'KB', 'MB', 'GB'];
            const i = Math.floor(Math.log(bytes) / Math.log(k));
            return parseFloat((bytes / Math.pow(k, i)).toFixed(1)) + ' ' + sizes[i];
        }

        function formatDate(dateString) {
            return new Date(dateString).toLocaleString();
        }

        function showAlert(elementId, message, type) {
            const alertElement = document.getElementById(elementId);
            alertElement.innerHTML = `<div class="alert alert-${type}">${message}</div>`;
            setTimeout(() => {
                alertElement.innerHTML = '';
            }, 5000);
        }

        function showNotification(message) {
            if (Notification.permission === 'granted') {
                new Notification('Serverless Upload', {
                    body: message,
                    icon: 'data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24"><path fill="%23667eea" d="M14,2H6A2,2 0 0,0 4,4V20A2,2 0 0,0 6,22H18A2,2 0 0,0 20,20V8L14,2M18,20H6V4H13V9H18V20Z"/></svg>'
                });
            }
        }

        // Request notification permission
        if (Notification.permission !== 'granted' && Notification.permission !== 'denied') {
            Notification.requestPermission();
        }

        // Auto-refresh dashboard every 30 seconds
        setInterval(updateDashboard, 30000);
    </script>
</body>
</html>
```

4. Upload file HTML lên S3:
- Vào bucket website → Upload → Chọn index.html
- Permissions → Grant public-read access
- Upload
![Picture87](/images/4.5/image87.png)
5. Tạo Bucket Policy
- Vào bucket → Permissions → Bucket policy
![Picture88](/images/4.5/image88.png)
- Add policy:
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::yourname-serverless-website-2025/*"
        }
    ]
}
```
![Picture89](/images/4.5/image89.png)
- Save changes
![Picture91](/images/4.5/image91.png)
6. Truy cập Website
- Copy Website endpoint URL từ Properties
![Picture92](/images/4.5/image92.png)
- Mở trong browser: ``http://yourname-serverless-website-2025.s3-website-ap-southeast-1.amazonaws.com``
![Picture93](/images/4.5/image93.png)
- Tính năng Web UI:
    - Drag & Drop upload files
    - Progress tracking (simulated)
    - Real-time dashboard với stats
    - File management với status
    - Responsive design mobile-friendly
    - Browser notifications khi upload xong
    - Configuration management save bucket name
- Lưu ý:
    - Web UI này chỉ simulate upload - không thực sự upload lên S3
    - Để thực upload: Cần implement S3 Presigned URLs hoặc API Gateway
    - Test thực: Vẫn upload trực tiếp vào S3 bucket qua AWS Console