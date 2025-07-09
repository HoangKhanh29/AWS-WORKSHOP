---
title : "Web Interface"
date: 2025-06-18
weight : 5
chapter : false
pre : " <b> 4.5. </b> "
---

1. **Create S3 Bucket for Website**
- Bucket name: `yourname-serverless-website-2025`
![Picture80](/images/4.5/image80.png)
- Region: ap-southeast-1
- Uncheck "Block all public access" ⚠️
- Acknowledge warning
![Picture81](/images/4.5/image81.png)
- Encryption type: Select **Server-side encryption with Amazon S3 managed keys (SSE-S3)**
- Bucket Key: **Enable**
- **Create bucket**
![Picture82](/images/4.5/image82.png)
![Picture83](/images/4.5/image83.png)

2. **Enable Static Website Hosting:**
- Go to bucket → **Properties** → **Static website hosting**
![Picture84](/images/4.5/image84.png)
- **Enable** → Index document: `index.html`
![Picture85](/images/4.5/image85.png)
- **Save changes**
![Picture86](/images/4.5/image86.png)
- **Copy Website endpoint URL**

3. **Create HTML file:**
- Create `index.html` file with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Serverless File Upload System</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            color: white;
            margin-bottom: 30px;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .main-content {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
            margin-bottom: 30px;
        }

        .card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .upload-section {
            text-align: center;
        }

        .upload-zone {
            border: 3px dashed #ddd;
            border-radius: 10px;
            padding: 40px 20px;
            margin: 20px 0;
            transition: all 0.3s ease;
            cursor: pointer;
        }

        .upload-zone:hover, .upload-zone.dragover {
            border-color: #667eea;
            background-color: #f8f9ff;
        }

        .upload-icon {
            font-size: 3rem;
            color: #667eea;
            margin-bottom: 15px;
        }

        .file-input {
            display: none;
        }

        .upload-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 16px;
            font-weight: 600;
            transition: transform 0.2s ease;
        }

        .upload-btn:hover {
            transform: translateY(-2px);
        }

        .config-section h3 {
            color: #333;
            margin-bottom: 20px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 5px;
            color: #555;
            font-weight: 500;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 14px;
        }

        .form-group input:focus, .form-group select:focus {
            outline: none;
            border-color: #667eea;
        }

        .dashboard {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            color: #667eea;
        }

        .stat-label {
            color: #666;
            margin-top: 5px;
        }

        .file-list {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .file-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            border-bottom: 1px solid #eee;
        }

        .file-item:last-child {
            border-bottom: none;
        }

        .file-info .name {
            font-weight: 600;
            color: #333;
        }

        .file-info .details {
            font-size: 0.9rem;
            color: #666;
            margin-top: 5px;
        }

        .upload-progress {
            width: 100%;
            height: 4px;
            background: #eee;
            border-radius: 2px;
            margin-top: 8px;
            overflow: hidden;
        }

        .upload-progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            transition: width 0.3s ease;
        }

        .status {
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        .status.success {
            background: #d4edda;
            color: #155724;
        }

        .status.uploading {
            background: #fff3cd;
            color: #856404;
        }

        .alert {
            padding: 12px;
            border-radius: 8px;
            margin: 10px 0;
        }

        .alert-success {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .alert-error {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .alert-warning {
            background: #fff3cd;
            color: #856404;
            border: 1px solid #ffeaa7;
        }

        @media (max-width: 768px) {
            .main-content {
                grid-template-columns: 1fr;
            }
            
            .header h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🚀 Serverless File Upload System</h1>
            <p>Upload files and receive instant email notifications via AWS serverless architecture</p>
        </div>

        <div class="dashboard">
            <div class="stat-card">
                <div class="stat-number" id="totalUploads">0</div>
                <div class="stat-label">Total Uploads</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="storageUsed">0 B</div>
                <div class="stat-label">Storage Used</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="queueSize">0</div>
                <div class="stat-label">Queue Size</div>
            </div>
            <div class="stat-card">
                <div class="stat-number" id="successRate">100%</div>
                <div class="stat-label">Success Rate</div>
            </div>
        </div>

        <div class="main-content">
            <div class="card upload-section">
                <h3>📁 Upload Files</h3>
                <div class="upload-zone" id="uploadZone" onclick="document.getElementById('fileInput').click()">
                    <div class="upload-icon">☁️</div>
                    <p><strong>Click to upload</strong> or drag and drop files here</p>
                    <p style="color: #666; font-size: 0.9rem; margin-top: 10px;">Maximum file size: 10MB</p>
                </div>
                <input type="file" id="fileInput" class="file-input" multiple onchange="handleFileUpload(event)">
                <button class="upload-btn" onclick="document.getElementById('fileInput').click()">
                    Choose Files
                </button>
            </div>

            <div class="card config-section">
                <h3>⚙️ Configuration</h3>
                <div id="configAlert"></div>
                <div class="form-group">
                    <label for="bucketName">S3 Bucket Name:</label>
                    <input type="text" id="bucketName" placeholder="yourname-serverless-files-2025">
                </div>
                <div class="form-group">
                    <label for="awsRegion">AWS Region:</label>
                    <select id="awsRegion">
                        <option value="ap-southeast-1">ap-southeast-1 (Singapore)</option>
                        <option value="us-east-1">us-east-1 (N. Virginia)</option>
                        <option value="us-west-2">us-west-2 (Oregon)</option>
                        <option value="eu-west-1">eu-west-1 (Ireland)</option>
                    </select>
                </div>
                <button class="upload-btn" onclick="saveConfig()">Save Configuration</button>
            </div>
        </div>

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
        let uploadedFiles = [];
        let totalUploads = 0;
        let totalSize = 0;
        let bucketName = '';
        let awsRegion = 'ap-southeast-1';

        // Initialize
        window.onload = function() {
            loadConfig();
            setupDragAndDrop();
            updateDashboard();
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
                    <div class="file-info">
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

4. **Upload HTML file to S3:**
- Go to website bucket → **Upload** → Choose index.html
- Permissions → **Grant public-read access**
- **Upload**
![Picture87](/images/4.5/image87.png)

5. **Create Bucket Policy**
- Go to bucket → **Permissions** → **Bucket policy**
![Picture88](/images/4.5/image88.png)
- **Add policy:**

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
- **Save changes**
![Picture91](/images/4.5/image91.png)

6. **Access Website**
- Copy Website endpoint URL from Properties
![Picture92](/images/4.5/image92.png)
- Open in browser: `http://yourname-serverless-website-2025.s3-website-ap-southeast-1.amazonaws.com`
![Picture93](/images/4.5/image93.png)

**Web UI Features:**
- **Drag & Drop** upload files
- **Progress tracking** (simulated)
- **Real-time dashboard** with stats
- **File management** with status
- **Responsive design** mobile-friendly
- **Browser notifications** when upload completes
- **Configuration management** to save bucket name

**Important Notes:**
- This Web UI only **simulates upload** - doesn't actually upload to S3
- For real upload: Need to implement S3 Presigned URLs or API Gateway
- For testing: Still upload directly to S3 bucket via AWS Console