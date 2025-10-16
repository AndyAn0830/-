# -<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>花蓮慈濟醫院環境巡檢管理系統</title>
    
    <!-- PWA 設定 -->
    <meta name="theme-color" content="#2c5aa0">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="慈濟巡檢">
    <link rel="manifest" href="manifest.json">
    
    <!-- APP 圖示 -->
    <link rel="icon" type="image/png" sizes="192x192" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%232c5aa0' width='100' height='100'/><text y='70' font-size='60' fill='white' text-anchor='middle' x='50' font-family='Arial'>巡</text></svg>">
    <link rel="apple-touch-icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%232c5aa0' width='100' height='100'/><text y='70' font-size='60' fill='white' text-anchor='middle' x='50' font-family='Arial'>巡</text></svg>">
    
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Microsoft JhengHei', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        /* 登入畫面 */
        .login-screen {
            padding: 60px 40px;
            text-align: center;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .login-box {
            background: white;
            padding: 40px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            max-width: 400px;
            width: 100%;
        }

        .login-box h2 {
            color: #2c5aa0;
            margin-bottom: 30px;
            font-size: 24px;
        }

        .login-box input {
            width: 100%;
            padding: 15px;
            margin-bottom: 20px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 16px;
        }

        .login-box button {
            width: 100%;
            padding: 15px;
            background: #2c5aa0;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: background 0.3s ease;
        }

        .login-box button:hover {
            background: #1e3c72;
        }

        .header {
            background: linear-gradient(135deg, #2c5aa0, #1e3c72);
            color: white;
            padding: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .header-left h1 {
            font-size: 28px;
            margin-bottom: 5px;
        }

        .header-right {
            text-align: right;
        }

        .user-info {
            font-size: 14px;
            margin-bottom: 10px;
        }

        .logout-btn {
            padding: 8px 16px;
            background: rgba(255,255,255,0.2);
            border: 1px solid white;
            color: white;
            border-radius: 5px;
            cursor: pointer;
            font-size: 14px;
        }

        .logout-btn:hover {
            background: rgba(255,255,255,0.3);
        }

        .tabs {
            display: flex;
            background: #f8f9fa;
            border-bottom: 1px solid #dee2e6;
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            background: none;
            border: none;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.3s ease;
            border-bottom: 3px solid transparent;
        }

        .tab.active {
            background: white;
            border-bottom-color: #2c5aa0;
            color: #2c5aa0;
            font-weight: bold;
        }

        .tab-content {
            display: none;
            padding: 25px;
        }

        .tab-content.active {
            display: block;
        }

        .form-section {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }

        input, select, textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e9ecef;
            border-radius: 8px;
            font-size: 14px;
            transition: border-color 0.3s ease;
        }

        input:focus, select:focus, textarea:focus {
            outline: none;
            border-color: #2c5aa0;
            box-shadow: 0 0 0 3px rgba(44, 90, 160, 0.1);
        }

        /* 記錄卡片樣式 */
        .record-card {
            background: white;
            border: 2px solid #e9ecef;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .record-card:hover {
            border-color: #2c5aa0;
            box-shadow: 0 4px 12px rgba(44, 90, 160, 0.15);
            transform: translateY(-2px);
        }

        .record-card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }

        .record-card-title {
            font-size: 18px;
            font-weight: bold;
            color: #2c5aa0;
        }

        .record-status {
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: bold;
        }

        .status-pending {
            background: #fff3cd;
            color: #856404;
        }

        .status-completed {
            background: #d4edda;
            color: #155724;
        }

        .status-failed {
            background: #f8d7da;
            color: #721c24;
        }

        .record-card-body {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
        }

        .record-info {
            font-size: 14px;
            color: #666;
        }

        .record-info strong {
            color: #333;
        }

        /* 模態框 */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.5);
            overflow: auto;
        }

        .modal.show {
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .modal-content {
            background-color: white;
            margin: 20px;
            padding: 0;
            border-radius: 15px;
            width: 90%;
            max-width: 800px;
            max-height: 90vh;
            overflow: hidden;
            display: flex;
            flex-direction: column;
        }

        .modal-header {
            background: linear-gradient(135deg, #2c5aa0, #1e3c72);
            color: white;
            padding: 20px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .modal-header h3 {
            margin: 0;
            font-size: 20px;
        }

        .close {
            color: white;
            font-size: 32px;
            font-weight: bold;
            cursor: pointer;
            line-height: 1;
            transition: opacity 0.3s;
        }

        .close:hover {
            opacity: 0.7;
        }

        .modal-body {
            padding: 25px;
            overflow-y: auto;
        }

        .detail-section {
            margin-bottom: 25px;
            padding-bottom: 20px;
            border-bottom: 1px solid #e9ecef;
        }

        .detail-section:last-child {
            border-bottom: none;
        }

        .detail-section h4 {
            color: #2c5aa0;
            margin-bottom: 15px;
            font-size: 16px;
        }

        .detail-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
        }

        .detail-item {
            padding: 10px;
            background: #f8f9fa;
            border-radius: 8px;
        }

        .detail-item label {
            font-size: 12px;
            color: #666;
            margin-bottom: 5px;
        }

        .detail-item .value {
            font-size: 14px;
            color: #333;
            font-weight: 500;
        }

        .atp-results {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 10px;
        }

        .atp-result-item {
            padding: 10px;
            border-radius: 8px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .atp-result-item.pass {
            background: #d4edda;
            border: 1px solid #c3e6cb;
        }

        .atp-result-item.fail {
            background: #f8d7da;
            border: 1px solid #f5c6cb;
        }

        .atp-result-item.none {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
        }

        .inspection-records {
            background: white;
            border-radius: 10px;
            border: 2px solid #e9ecef;
            overflow: hidden;
            margin-bottom: 20px;
        }

        .record-header {
            background: #2c5aa0;
            color: white;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .record-item {
            border-bottom: 1px solid #e9ecef;
            padding: 20px;
            position: relative;
        }

        .record-item:last-child {
            border-bottom: none;
        }

        .record-fields {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 15px;
        }

        .atp-section {
            background: #e3f2fd;
            border-radius: 8px;
            padding: 15px;
            margin-top: 15px;
        }

        .atp-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            max-height: 500px;
            overflow-y: auto;
        }

        .atp-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px;
            background: white;
            border-radius: 8px;
            border: 2px solid #ddd;
            margin-bottom: 8px;
            transition: border-color 0.3s ease;
        }

        .atp-item:hover {
            border-color: #2c5aa0;
        }

        .atp-item-label {
            flex: 1;
            font-size: 14px;
            font-weight: 500;
            margin: 0;
            color: #333;
        }

        .atp-radio-group {
            display: flex;
            gap: 20px;
            align-items: center;
        }

        .radio-option {
            display: flex;
            align-items: center;
            gap: 8px;
            cursor: pointer;
            padding: 8px 12px;
            border-radius: 20px;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }

        .radio-option:hover {
            background-color: #f0f0f0;
        }

        .radio-option input[type="radio"]:checked ~ label {
            font-weight: bold;
        }

        .radio-option.pass {
            border-color: #28a745;
            background-color: #d4edda;
        }

        .radio-option.fail {
            border-color: #dc3545;
            background-color: #f8d7da;
        }

        .radio-option input[type="radio"] {
            width: 18px;
            height: 18px;
            margin: 0;
            cursor: pointer;
            accent-color: #2c5aa0;
        }

        .radio-option label {
            font-size: 14px;
            margin: 0;
            cursor: pointer;
            padding: 0;
            font-weight: 600;
            color: #333;
        }

        .radio-option.pass label {
            color: #155724;
        }

        .radio-option.fail label {
            color: #721c24;
        }

        .review-section {
            border: 2px solid #ffeaa7;
            border-radius: 10px;
            padding: 20px;
            margin-top: 15px;
            background: #fff8e1;
        }

        .photo-preview {
            display: flex;
            gap: 10px;
            margin-top: 10px;
            flex-wrap: wrap;
        }

        .photo-item {
            position: relative;
            width: 80px;
            height: 80px;
            border-radius: 8px;
            overflow: hidden;
            border: 2px solid #dee2e6;
        }

        .photo-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .remove-photo {
            position: absolute;
            top: -5px;
            right: -5px;
            background: #dc3545;
            color: white;
            border: none;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            cursor: pointer;
            font-size: 12px;
        }

        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
            font-weight: bold;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-block;
            text-align: center;
        }

        .btn-primary {
            background: #2c5aa0;
            color: white;
        }

        .btn-primary:hover {
            background: #1e3c72;
            transform: translateY(-1px);
        }

        .btn-success {
            background: #28a745;
            color: white;
        }

        .btn-danger {
            background: #dc3545;
            color: white;
        }

        .btn-secondary {
            background: #6c757d;
            color: white;
        }

        .btn-sm {
            padding: 6px 12px;
            font-size: 12px;
        }

        .delete-record {
            position: absolute;
            top: 10px;
            right: 10px;
            background: #dc3545;
            color: white;
            border: none;
            border-radius: 50%;
            width: 30px;
            height: 30px;
            cursor: pointer;
            font-size: 14px;
        }

        .info-box {
            background: #fff3cd;
            border: 1px solid #ffeaa7;
            border-radius: 5px;
            padding: 10px;
            margin: 10px 0;
            font-size: 13px;
            color: #856404;
        }

        .info-box.blue {
            background: #d1ecf1;
            border-color: #bee5eb;
            color: #0c5460;
        }

        .info-box.orange {
            background: #fff8e1;
            border-color: #ffc107;
            color: #856404;
        }

        .hidden {
            display: none;
        }

        @media (max-width: 768px) {
            .container {
                margin: 10px;
                border-radius: 10px;
            }
            
            .form-row {
                grid-template-columns: 1fr;
            }
            
            .record-fields {
                grid-template-columns: 1fr;
            }

            .atp-grid {
                grid-template-columns: 1fr;
            }

            .atp-radio-group {
                gap: 10px;
            }

            .modal-content {
                width: 95%;
                margin: 10px;
            }
        }
    </style>
</head>
<body>
    <!-- 登入畫面 -->
    <div id="loginScreen" class="login-screen">
        <div class="login-box">
            <h2>花蓮慈濟醫院環境巡檢管理系統</h2>
            <p style="color: #666; margin-bottom: 30px;">請輸入您的姓名登入</p>
            <input type="text" id="loginName" placeholder="請輸入您的姓名" onkeypress="if(event.key==='Enter') login()">
            <button onclick="login()">登入系統</button>
        </div>
    </div>

    <!-- 主系統畫面 -->
    <div id="mainSystem" class="hidden">
        <div class="container">
            <div class="header">
                <div class="header-left">
                    <h1>花蓮慈濟醫院環境巡檢管理系統</h1>
                    <p>Hospital Environmental Inspection Management System</p>
                </div>
                <div class="header-right">
                    <div class="user-info">使用者：<span id="currentUser"></span></div>
                    <button class="logout-btn" onclick="logout()">登出</button>
                </div>
            </div>

            <div class="tabs">
                <button class="tab active" data-tab="inspection">新增巡檢</button>
                <button class="tab" data-tab="myRecords">我的記錄</button>
                <button class="tab" data-tab="allRecords">所有記錄</button>
                <button class="tab" data-tab="export">資料匯出</button>
            </div>

            <!-- 新增巡檢頁面 -->
            <div id="inspection" class="tab-content active">
                <div class="form-section">
                    <h2>新增巡檢記錄</h2>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="inspectionDateTime">巡檢日期時間 *</label>
                            <input type="datetime-local" id="inspectionDateTime" required>
                        </div>
                        <div class="form-group">
                            <label for="buildingSelect">棟別 *</label>
                            <select id="buildingSelect" required>
                                <option value="">請選擇棟別</option>
                                <option value="大愛樓">大愛樓</option>
                                <option value="感恩樓">感恩樓</option>
                                <option value="合心樓">合心樓</option>
                                <option value="協力樓">協力樓</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="areaSelect">區域 *</label>
                            <select id="areaSelect" required>
                                <option value="">請選擇區域</option>
                                <option value="公共區域">公共區域</option>
                                <option value="病房">病房</option>
                            </select>
                        </div>
                    </div>
                </div>

                <div class="inspection-records">
                    <div class="record-header">
                        <h3>巡檢項目記錄</h3>
                        <button class="btn btn-success btn-sm" id="addRecordBtn" style="display: none;">+ 新增巡檢項目</button>
                    </div>
                    <div id="recordsList">
                        <!-- 巡檢項目會動態生成在這裡 -->
                    </div>
                    <div id="areaMessage" style="text-align: center; padding: 40px; color: #999;">
                        請先選擇棟別和區域
                    </div>
                </div>

                <div style="text-align: center;">
                    <button class="btn btn-primary" id="submitBtn">提交巡檢記錄</button>
                </div>
            </div>

            <!-- 我的記錄頁面 -->
            <div id="myRecords" class="tab-content">
                <div class="form-section">
                    <h2>我的巡檢記錄</h2>
                    <div id="myRecordsDisplay">
                        <p style="text-align: center; color: #999; padding: 40px;">載入記錄中...</p>
                    </div>
                </div>
            </div>

            <!-- 所有記錄頁面 -->
            <div id="allRecords" class="tab-content">
                <div class="form-section">
                    <h2>所有巡檢記錄</h2>
                    <div id="allRecordsDisplay">
                        <p style="text-align: center; color: #999; padding: 40px;">載入記錄中...</p>
                    </div>
                </div>
            </div>

            <!-- 資料匯出頁面 -->
            <div id="export" class="tab-content">
                <div class="form-section">
                    <h2>資料匯出</h2>
                    
                    <div class="info-box blue" style="margin-bottom: 20px;">
                        <strong>說明：</strong>您可以選擇匯出格式和日期範圍，系統會將巡檢記錄匯出為可下載的檔案。
                    </div>
                    
                    <div class="form-row">
                        <div class="form-group">
                            <label for="exportFormat">匯出格式 *</label>
                            <select id="exportFormat">
                                <option value="excel">Excel 格式 (.xlsx)</option>
                                <option value="csv">CSV 格式 (.csv)</option>
                                <option value="json">JSON 格式 (.json)</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="exportRange">匯出範圍 *</label>
                            <select id="exportRange">
                                <option value="all">所有記錄</option>
                                <option value="my">僅我的記錄</option>
                                <option value="dateRange">指定日期範圍</option>
                            </select>
                        </div>
                    </div>
                    
                    <div id="dateRangeSection" style="display: none;">
                        <div class="form-row">
                            <div class="form-group">
                                <label for="exportStartDate">開始日期</label>
                                <input type="date" id="exportStartDate">
                            </div>
                            <div class="form-group">
                                <label for="exportEndDate">結束日期</label>
                                <input type="date" id="exportEndDate">
                            </div>
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label for="exportContent">匯出內容</label>
                        <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 10px;">
                            <label style="display: flex; align-items: center; gap: 8px; font-weight: normal; cursor: pointer;">
                                <input type="checkbox" id="includeBasicInfo" checked style="width: auto;">
                                基本資訊
                            </label>
                            <label style="display: flex; align-items: center; gap: 8px; font-weight: normal; cursor: pointer;">
                                <input type="checkbox" id="includeItems" checked style="width: auto;">
                                巡檢項目
                            </label>
                            <label style="display: flex; align-items: center; gap: 8px; font-weight: normal; cursor: pointer;">
                                <input type="checkbox" id="includeATP" checked style="width: auto;">
                                ATP檢測結果
                            </label>
                            <label style="display: flex; align-items: center; gap: 8px; font-weight: normal; cursor: pointer;">
                                <input type="checkbox" id="includeReview" checked style="width: auto;">
                                複查資訊
                            </label>
                        </div>
                    </div>
                    
                    <div style="text-align: center; margin-top: 30px;">
                        <button class="btn btn-primary" onclick="exportData()" style="padding: 15px 40px; font-size: 16px;">
                            <span style="margin-right: 8px;">📥</span> 匯出資料
                        </button>
                    </div>
                    
                    <div id="exportResult" style="margin-top: 30px; display: none;">
                        <div class="info-box" style="background: #d4edda; border-color: #c3e6cb; color: #155724;">
                            <h4 style="margin-bottom: 10px;">✓ 匯出成功</h4>
                            <p id="exportMessage"></p>
                            <a id="downloadLink" class="btn btn-success" style="margin-top: 10px; display: inline-block;">下載檔案</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 記錄詳情模態框 -->
    <div id="recordModal" class="modal">
        <div class="modal-content">
            <div class="modal-header">
                <h3>巡檢記錄詳情</h3>
                <span class="close" onclick="closeModal()">&times;</span>
            </div>
            <div class="modal-body" id="modalBody">
                <!-- 內容會動態生成 -->
            </div>
        </div>
    </div>

    <script>
        // 版本控制
        var SYSTEM_VERSION = '2025.1.16.fixed';
        console.log('花蓮慈濟醫院環境巡檢管理系統 v' + SYSTEM_VERSION + ' 啟動');

        // 全域變數
        var currentUser = null;
        var recordCounter = 0;
        var inspectionRecords = [];
        var currentViewingRecord = null;

        // 自訂訊息顯示（取代 alert 和 confirm）
        function showMessage(message, type) {
            type = type || 'info';
            var messageDiv = document.createElement('div');
            messageDiv.style.cssText = 'position: fixed; top: 20px; left: 50%; transform: translateX(-50%); padding: 15px 30px; border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); z-index: 10000; font-size: 16px; font-weight: bold; animation: slideDown 0.3s ease;';
            
            if (type === 'error') {
                messageDiv.style.background = '#dc3545';
                messageDiv.style.color = 'white';
            } else if (type === 'success') {
                messageDiv.style.background = '#28a745';
                messageDiv.style.color = 'white';
            } else {
                messageDiv.style.background = '#2c5aa0';
                messageDiv.style.color = 'white';
            }
            
            messageDiv.textContent = message;
            document.body.appendChild(messageDiv);
            
            setTimeout(function() {
                messageDiv.style.animation = 'slideUp 0.3s ease';
                setTimeout(function() {
                    document.body.removeChild(messageDiv);
                }, 300);
            }, 3000);
        }
        
        // 新增動畫樣式
        var style = document.createElement('style');
        style.textContent = '@keyframes slideDown { from { top: -100px; opacity: 0; } to { top: 20px; opacity: 1; } } @keyframes slideUp { from { top: 20px; opacity: 1; } to { top: -100px; opacity: 0; } }';
        document.head.appendChild(style);

        // ATP檢測項目
        var atpItems = [
            '1. 叫人鈴', '9. 門把',
            '2. 床欄', '10. 床頭洗手台',
            '3. 床頭燈座', '11. 紅漏斗',
            '4. 床腳板', '12. 馬桶及扶手',
            '5. 床尾按鈕', '13. 浴室水槽',
            '6. 窗台', '14. PUMP',
            '7. 陪病床', '15. 床旁桌',
            '8. 電腦開關', '16. 垃圾桶'
        ];

        // 登入
        function login() {
            var name = document.getElementById('loginName').value.trim();
            if (!name) {
                showMessage('請輸入您的姓名', 'error');
                return;
            }
            
            currentUser = name;
            localStorage.setItem('currentUser', name);
            
            document.getElementById('loginScreen').classList.add('hidden');
            document.getElementById('mainSystem').classList.remove('hidden');
            document.getElementById('currentUser').textContent = name;
            
            init();
        }

        // 登出
        function logout() {
            // 直接登出，不使用 confirm（避免 sandbox 限制）
            // 清空使用者資訊
            currentUser = null;
            localStorage.removeItem('currentUser');
            
            // 重置表單
            try {
                resetForm();
            } catch (e) {
                console.log('重置表單時發生錯誤:', e);
            }
            
            // 切換到登入畫面
            document.getElementById('mainSystem').classList.add('hidden');
            document.getElementById('loginScreen').classList.remove('hidden');
            document.getElementById('loginName').value = '';
            document.getElementById('loginName').focus();
            
            // 重置為第一個頁籤
            try {
                switchTab('inspection');
            } catch (e) {
                console.log('切換頁籤時發生錯誤:', e);
            }
            
            console.log('已登出系統');
        }

        // 初始化
        function init() {
            console.log('系統初始化中...');
            
            // 載入歷史記錄
            try {
                var saved = localStorage.getItem('hospitalRecords_v2025');
                if (saved) {
                    inspectionRecords = JSON.parse(saved);
                    console.log('載入了', inspectionRecords.length, '筆歷史記錄');
                }
            } catch (e) {
                console.log('載入歷史記錄失敗:', e);
                inspectionRecords = [];
            }
            
            // 設定預設時間
            var now = new Date();
            document.getElementById('inspectionDateTime').value = now.toISOString().slice(0, 16);
            
            // 綁定事件
            document.getElementById('buildingSelect').addEventListener('change', handleAreaChange);
            document.getElementById('areaSelect').addEventListener('change', handleAreaChange);
            document.getElementById('addRecordBtn').addEventListener('click', addRecord);
            document.getElementById('submitBtn').addEventListener('click', submitInspection);
            
            // 匯出功能事件綁定
            document.getElementById('exportRange').addEventListener('change', function() {
                var dateSection = document.getElementById('dateRangeSection');
                if (this.value === 'dateRange') {
                    dateSection.style.display = 'block';
                } else {
                    dateSection.style.display = 'none';
                }
            });
            
            // 頁籤切換
            var tabs = document.querySelectorAll('.tab');
            for (var i = 0; i < tabs.length; i++) {
                tabs[i].addEventListener('click', function() {
                    var tabId = this.getAttribute('data-tab');
                    switchTab(tabId);
                });
            }
            
            console.log('系統初始化完成');
        }

        // 頁籤切換
        function switchTab(tabId) {
            // 隱藏所有頁籤內容
            var contents = document.querySelectorAll('.tab-content');
            for (var i = 0; i < contents.length; i++) {
                contents[i].classList.remove('active');
            }
            
            // 移除所有頁籤的active狀態
            var tabs = document.querySelectorAll('.tab');
            for (var i = 0; i < tabs.length; i++) {
                tabs[i].classList.remove('active');
            }
            
            // 顯示選中的頁籤內容
            document.getElementById(tabId).classList.add('active');
            
            // 設定選中頁籤的active狀態
            document.querySelector('[data-tab="' + tabId + '"]').classList.add('active');
            
            // 載入對應的記錄
            if (tabId === 'myRecords') {
                loadMyRecords();
            } else if (tabId === 'allRecords') {
                loadAllRecords();
            }
        }

        // 處理區域變更
        function handleAreaChange() {
            var building = document.getElementById('buildingSelect').value;
            var area = document.getElementById('areaSelect').value;
            var addButton = document.getElementById('addRecordBtn');
            var recordsList = document.getElementById('recordsList');
            var areaMessage = document.getElementById('areaMessage');
            
            // 清空現有記錄
            recordsList.innerHTML = '';
            recordCounter = 0;
            
            if (!building || !area) {
                addButton.style.display = 'none';
                areaMessage.style.display = 'block';
                areaMessage.textContent = '請先選擇棟別和區域';
                return;
            }
            
            areaMessage.style.display = 'none';
            
            if (area === '公共區域') {
                addButton.style.display = 'inline-block';
                addRecord();
            } else if (area === '病房') {
                addButton.style.display = 'none';
                addRecord();
            }
        }

        // 新增記錄
        function addRecord() {
            var building = document.getElementById('buildingSelect').value;
            var area = document.getElementById('areaSelect').value;
            
            if (!building || !area) {
                showMessage('請先選擇棟別和區域', 'error');
                return;
            }
            
            recordCounter++;
            var container = document.getElementById('recordsList');
            var isWard = area === '病房';
            
            var recordDiv = document.createElement('div');
            recordDiv.className = 'record-item';
            recordDiv.id = 'record-' + recordCounter;
            
            var html = '';
            
            // 刪除按鈕（只有公共區域可以刪除多筆記錄）
            if (!isWard) {
                html += '<button class="delete-record" onclick="deleteRecord(' + recordCounter + ')">×</button>';
            }
            
            // 基本欄位
            html += '<div class="record-fields">';
            html += '<div class="form-group">';
            html += '<label>棟別</label>';
            html += '<input type="text" value="' + building + '" readonly style="background-color: #f8f9fa;">';
            html += '</div>';
            html += '<div class="form-group">';
            html += '<label>區域</label>';
            html += '<input type="text" value="' + area + '" readonly style="background-color: #f8f9fa;">';
            html += '</div>';
            
            if (isWard) {
                html += '<div class="form-group">';
                html += '<label>病房名稱 *</label>';
                html += '<input type="text" name="wardName" placeholder="請輸入病房名稱 (例如：301病房)" required>';
                html += '</div>';
                html += '<div class="form-group">';
                html += '<label>巡檢項目 (可選填)</label>';
                html += '<input type="text" name="item" placeholder="病房區域可選填">';
                html += '</div>';
                html += '<div class="info-box blue">';
                html += '病房區域以ATP檢測為主，巡檢項目為可選填';
                html += '</div>';
            } else {
                html += '<div class="form-group">';
                html += '<label>巡檢項目 *</label>';
                html += '<input type="text" name="item" placeholder="請輸入巡檢項目" required>';
                html += '</div>';
            }
            html += '</div>';
            
            // ATP檢測 (僅病房)
            if (isWard) {
                html += '<div class="atp-section">';
                html += '<h4>ATP檢測項目 (16項)</h4>';
                html += '<div class="atp-grid">';
                
                for (var i = 0; i < atpItems.length; i++) {
                    var itemId = recordCounter + '_atp_' + (i + 1);
                    html += '<div class="atp-item">';
                    html += '<label class="atp-item-label">' + atpItems[i] + '</label>';
                    html += '<div class="atp-radio-group">';
                    html += '<div class="radio-option pass">';
                    html += '<input type="radio" id="' + itemId + '_pass" name="atp_' + recordCounter + '_' + (i + 1) + '" value="合格">';
                    html += '<label for="' + itemId + '_pass">✓ 合格</label>';
                    html += '</div>';
                    html += '<div class="radio-option fail">';
                    html += '<input type="radio" id="' + itemId + '_fail" name="atp_' + recordCounter + '_' + (i + 1) + '" value="不合格">';
                    html += '<label for="' + itemId + '_fail">✗ 不合格</label>';
                    html += '</div>';
                    html += '</div>';
                    html += '</div>';
                }
                
                html += '</div>';
                html += '</div>';
            }
            
            // 備註
            html += '<div class="form-group">';
            html += '<label>備註說明</label>';
            html += '<textarea name="notes" rows="3" placeholder="請輸入備註..."></textarea>';
            html += '</div>';
            
            // 照片
            html += '<div class="form-group">';
            html += '<label>巡檢照片</label>';
            html += '<input type="file" multiple accept="image/*" onchange="handlePhotoUpload(this, ' + recordCounter + ')">';
            html += '<div id="photos-preview-' + recordCounter + '" class="photo-preview"></div>';
            html += '</div>';
            
            recordDiv.innerHTML = html;
            container.appendChild(recordDiv);
        }

        // 刪除記錄
        // 刪除記錄
        function deleteRecord(id) {
            // 直接刪除，不使用 confirm（避免 sandbox 限制）
            var element = document.getElementById('record-' + id);
            if (element) {
                element.remove();
                showMessage('項目已刪除', 'info');
            }
        }

        // 處理照片上傳
        function handlePhotoUpload(input, recordId) {
            var files = input.files;
            var preview = document.getElementById('photos-preview-' + recordId);
            
            for (var i = 0; i < files.length; i++) {
                var file = files[i];
                if (!file.type.startsWith('image/')) continue;
                
                var reader = new FileReader();
                reader.onload = function(e) {
                    var div = document.createElement('div');
                    div.className = 'photo-item';
                    div.innerHTML = '<img src="' + e.target.result + '"><button class="remove-photo" onclick="this.parentElement.remove()">×</button>';
                    preview.appendChild(div);
                };
                reader.readAsDataURL(file);
            }
        }

        // 提交記錄
        function submitInspection() {
            var dateTime = document.getElementById('inspectionDateTime').value;
            var building = document.getElementById('buildingSelect').value;
            var area = document.getElementById('areaSelect').value;
            
            if (!dateTime || !building || !area) {
                showMessage('請填寫基本資訊!', 'error');
                return;
            }
            
            var records = document.querySelectorAll('.record-item');
            if (records.length === 0) {
                showMessage('請至少新增一個項目!', 'error');
                return;
            }
            
            var items = [];
            
            for (var i = 0; i < records.length; i++) {
                var record = records[i];
                var item = record.querySelector('[name="item"]');
                var wardName = record.querySelector('[name="wardName"]');
                
                if (area === '公共區域' && !item.value.trim()) {
                    showMessage('公共區域必須填寫巡檢項目!', 'error');
                    return;
                }
                
                if (area === '病房' && wardName && !wardName.value.trim()) {
                    showMessage('病房區域必須填寫病房名稱!', 'error');
                    return;
                }
                
                // 收集ATP結果
                var atpResults = {};
                if (area === '病房') {
                    var recordId = record.id.split('-')[1];
                    for (var j = 1; j <= 16; j++) {
                        var radio = record.querySelector('[name="atp_' + recordId + '_' + j + '"]:checked');
                        if (radio) {
                            atpResults[atpItems[j-1]] = radio.value;
                        }
                    }
                }
                
                // 收集照片
                var photos = [];
                var imgs = record.querySelectorAll('#photos-preview-' + record.id.split('-')[1] + ' img');
                for (var k = 0; k < imgs.length; k++) {
                    photos.push(imgs[k].src);
                }
                
                var itemData = {
                    wardName: wardName ? wardName.value : '',
                    item: item.value || 'ATP檢測為主',
                    notes: record.querySelector('[name="notes"]').value,
                    photos: photos,
                    atpResults: atpResults,
                    reviewStatus: 'pending',
                    reviewResult: '',
                    reviewer: '',
                    reviewNotes: '',
                    reviewPhotos: [],
                    reviewDateTime: ''
                };
                
                items.push(itemData);
            }
            
            // 建立記錄
            var inspectionRecord = {
                id: Date.now(),
                inspector: currentUser,
                dateTime: dateTime,
                submitTime: new Date().toISOString(),
                building: building,
                area: area,
                items: items
            };
            
            // 儲存
            inspectionRecords.unshift(inspectionRecord);
            try {
                localStorage.setItem('hospitalRecords_v2025', JSON.stringify(inspectionRecords));
            } catch (e) {
                console.error('儲存失敗:', e);
            }
            
            showMessage('巡檢記錄提交成功!', 'success');
            
            // 重置表單
            resetForm();
        }

        // 重置表單
        function resetForm() {
            var now = new Date();
            document.getElementById('inspectionDateTime').value = now.toISOString().slice(0, 16);
            document.getElementById('buildingSelect').value = '';
            document.getElementById('areaSelect').value = '';
            document.getElementById('recordsList').innerHTML = '';
            document.getElementById('areaMessage').style.display = 'block';
            document.getElementById('addRecordBtn').style.display = 'none';
            recordCounter = 0;
        }

        // 載入我的記錄
        function loadMyRecords() {
            var container = document.getElementById('myRecordsDisplay');
            var myRecords = inspectionRecords.filter(function(r) { return r.inspector === currentUser; });
            
            if (myRecords.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: #999; padding: 40px;">您還沒有巡檢記錄</p>';
                return;
            }
            
            var html = '';
            
            for (var i = 0; i < myRecords.length; i++) {
                var record = myRecords[i];
                html += renderRecordCard(record);
            }
            
            container.innerHTML = html;
        }

        // 載入所有記錄
        function loadAllRecords() {
            var container = document.getElementById('allRecordsDisplay');
            
            if (inspectionRecords.length === 0) {
                container.innerHTML = '<p style="text-align: center; color: #999; padding: 40px;">尚無巡檢記錄</p>';
                return;
            }
            
            var html = '';
            
            for (var i = 0; i < inspectionRecords.length; i++) {
                var record = inspectionRecords[i];
                html += renderRecordCard(record);
            }
            
            container.innerHTML = html;
        }

        // 渲染記錄卡片
        function renderRecordCard(record) {
            var date = new Date(record.dateTime);
            var status = getRecordStatus(record);
            var statusClass = status === '待複查' ? 'status-pending' : (status === '已完成' ? 'status-completed' : 'status-failed');
            
            var html = '';
            html += '<div class="record-card" onclick="viewRecord(' + record.id + ')">';
            html += '<div class="record-card-header">';
            var title = record.building + ' - ' + record.area;
            // 如果是病房且有病房名稱，顯示病房名稱
            if (record.area === '病房' && record.items.length > 0 && record.items[0].wardName) {
                title += ' - ' + record.items[0].wardName;
            }
            html += '<div class="record-card-title">' + title + '</div>';
            html += '<span class="record-status ' + statusClass + '">' + status + '</span>';
            html += '</div>';
            html += '<div class="record-card-body">';
            html += '<div class="record-info"><strong>巡檢人員：</strong>' + record.inspector + '</div>';
            html += '<div class="record-info"><strong>巡檢時間：</strong>' + date.toLocaleString() + '</div>';
            html += '<div class="record-info"><strong>項目數量：</strong>' + record.items.length + ' 項</div>';
            
            // ATP統計
            if (record.area === '病房') {
                var totalAtp = 0, passAtp = 0;
                record.items.forEach(function(item) {
                    for (var key in item.atpResults) {
                        totalAtp++;
                        if (item.atpResults[key] === '合格') passAtp++;
                    }
                });
                if (totalAtp > 0) {
                    html += '<div class="record-info"><strong>ATP檢測：</strong>' + passAtp + '/' + totalAtp + ' 合格</div>';
                }
            }
            
            html += '</div>';
            html += '</div>';
            
            return html;
        }

        // 獲取記錄狀態
        function getRecordStatus(record) {
            var hasReview = false;
            var allPass = true;
            
            for (var i = 0; i < record.items.length; i++) {
                if (record.items[i].reviewResult) {
                    hasReview = true;
                    if (record.items[i].reviewResult === '不合格') {
                        allPass = false;
                    }
                }
            }
            
            // 病房區域沒有複查也算正常，公共區域才需要複查
            if (!hasReview) {
                return record.area === '病房' ? '已完成' : '待複查';
            }
            return allPass ? '已完成' : '有問題';
        }

        // 查看記錄詳情
        function viewRecord(recordId) {
            var record = inspectionRecords.find(function(r) { return r.id === recordId; });
            if (!record) return;
            
            currentViewingRecord = record;
            
            var modal = document.getElementById('recordModal');
            var body = document.getElementById('modalBody');
            
            var date = new Date(record.dateTime);
            
            var html = '';
            
            // 基本資訊
            html += '<div class="detail-section">';
            html += '<h4>基本資訊</h4>';
            html += '<div class="detail-grid">';
            html += '<div class="detail-item"><label>巡檢人員</label><div class="value">' + record.inspector + '</div></div>';
            html += '<div class="detail-item"><label>巡檢時間</label><div class="value">' + date.toLocaleString() + '</div></div>';
            html += '<div class="detail-item"><label>棟別</label><div class="value">' + record.building + '</div></div>';
            html += '<div class="detail-item"><label>區域</label><div class="value">' + record.area + '</div></div>';
            html += '</div>';
            html += '</div>';
            
            // 巡檢項目
            for (var i = 0; i < record.items.length; i++) {
                var item = record.items[i];
                
                html += '<div class="detail-section">';
                if (item.wardName) {
                    html += '<h4>【' + item.wardName + '】 - ' + item.item + '</h4>';
                } else {
                    html += '<h4>巡檢項目 ' + (i + 1) + '：' + item.item + '</h4>';
                }
                
                // ATP檢測結果
                if (Object.keys(item.atpResults).length > 0) {
                    html += '<div style="margin-bottom: 15px;">';
                    html += '<label style="font-weight: bold; margin-bottom: 10px; display: block;">ATP檢測結果</label>';
                    html += '<div class="atp-results">';
                    
                    for (var key in item.atpResults) {
                        var resultClass = item.atpResults[key] === '合格' ? 'pass' : 'fail';
                        html += '<div class="atp-result-item ' + resultClass + '">';
                        html += '<span>' + key + '</span>';
                        html += '<span style="font-weight: bold;">' + item.atpResults[key] + '</span>';
                        html += '</div>';
                    }
                    
                    html += '</div>';
                    html += '</div>';
                }
                
                // 備註
                if (item.notes) {
                    html += '<div class="detail-item"><label>備註</label><div class="value">' + item.notes + '</div></div>';
                }
                
                // 照片
                if (item.photos.length > 0) {
                    html += '<div style="margin-top: 15px;">';
                    html += '<label style="font-weight: bold; margin-bottom: 10px; display: block;">巡檢照片</label>';
                    html += '<div class="photo-preview">';
                    for (var j = 0; j < item.photos.length; j++) {
                        html += '<div class="photo-item"><img src="' + item.photos[j] + '" onclick="window.open(this.src)"></div>';
                    }
                    html += '</div>';
                    html += '</div>';
                }
                
                html += '</div>';
                
                // 複查區域 (病房可選填)
                html += '<div class="detail-section">';
                html += '<h4>複查資訊 ' + (record.area === '病房' ? '(選填)' : '') + '</h4>';
                
                if (item.reviewResult) {
                    var resultColor = item.reviewResult === '合格' ? '#28a745' : '#dc3545';
                    html += '<div class="detail-grid">';
                    html += '<div class="detail-item"><label>複查結果</label><div class="value" style="color: ' + resultColor + '; font-weight: bold;">' + item.reviewResult + '</div></div>';
                    if (item.reviewer) {
                        html += '<div class="detail-item"><label>複查人員</label><div class="value">' + item.reviewer + '</div></div>';
                    }
                    if (item.reviewDateTime) {
                        var reviewDate = new Date(item.reviewDateTime);
                        html += '<div class="detail-item"><label>複查時間</label><div class="value">' + reviewDate.toLocaleString() + '</div></div>';
                    }
                    html += '</div>';
                    
                    if (item.reviewNotes) {
                        html += '<div class="detail-item" style="margin-top: 10px;"><label>複查備註</label><div class="value">' + item.reviewNotes + '</div></div>';
                    }
                    
                    if (item.reviewPhotos && item.reviewPhotos.length > 0) {
                        html += '<div style="margin-top: 15px;">';
                        html += '<label style="font-weight: bold; margin-bottom: 10px; display: block;">複查照片</label>';
                        html += '<div class="photo-preview">';
                        for (var k = 0; k < item.reviewPhotos.length; k++) {
                            html += '<div class="photo-item"><img src="' + item.reviewPhotos[k] + '" onclick="window.open(this.src)"></div>';
                        }
                        html += '</div>';
                        html += '</div>';
                    }
                } else {
                    html += '<div class="review-section">';
                    if (record.area === '病房') {
                        html += '<h4 style="color: #0c5460; margin-bottom: 15px;">選填：進行複查（病房區域可選擇是否複查）</h4>';
                        html += '<div class="info-box blue" style="margin-bottom: 15px;">病房區域的複查為選填項目，如有需要再進行複查即可</div>';
                    } else {
                        html += '<h4 style="color: #856404; margin-bottom: 15px;">進行複查</h4>';
                    }
                    html += '<div class="form-row">';
                    html += '<div class="form-group">';
                    html += '<label>複查結果 ' + (record.area === '公共區域' ? '*' : '(選填)') + '</label>';
                    html += '<select id="reviewResult_' + i + '" ' + (record.area === '公共區域' ? 'required' : '') + '>';
                    html += '<option value="">請選擇結果</option>';
                    html += '<option value="合格">合格</option>';
                    html += '<option value="不合格">不合格</option>';
                    html += '</select>';
                    html += '</div>';
                    html += '<div class="form-group">';
                    html += '<label>複查人員</label>';
                    html += '<input type="text" id="reviewer_' + i + '" value="' + currentUser + '">';
                    html += '</div>';
                    html += '</div>';
                    html += '<div class="form-group">';
                    html += '<label>複查備註</label>';
                    html += '<textarea id="reviewNotes_' + i + '" rows="3"></textarea>';
                    html += '</div>';
                    html += '<div class="form-group">';
                    html += '<label>複查照片</label>';
                    html += '<input type="file" multiple accept="image/*" id="reviewPhotos_' + i + '" onchange="handleReviewPhotoUpload(this, ' + i + ')">';
                    html += '<div id="review-photos-preview-' + i + '" class="photo-preview"></div>';
                    html += '</div>';
                    html += '<button class="btn btn-success" onclick="submitReview(' + i + ')">提交複查</button>';
                    if (record.area === '病房') {
                        html += ' <button class="btn btn-secondary" onclick="closeModal()" style="margin-left: 10px;">暫不複查</button>';
                    }
                    html += '</div>';
                }
                
                html += '</div>';
            }
            
            body.innerHTML = html;
            modal.classList.add('show');
        }

        // 關閉模態框
        function closeModal() {
            document.getElementById('recordModal').classList.remove('show');
            currentViewingRecord = null;
        }

        // 處理複查照片上傳
        function handleReviewPhotoUpload(input, itemIndex) {
            var files = input.files;
            var preview = document.getElementById('review-photos-preview-' + itemIndex);
            
            for (var i = 0; i < files.length; i++) {
                var file = files[i];
                if (!file.type.startsWith('image/')) continue;
                
                var reader = new FileReader();
                reader.onload = function(e) {
                    var div = document.createElement('div');
                    div.className = 'photo-item';
                    div.innerHTML = '<img src="' + e.target.result + '"><button class="remove-photo" onclick="this.parentElement.remove()">×</button>';
                    preview.appendChild(div);
                };
                reader.readAsDataURL(file);
            }
        }

        // 提交複查
        function submitReview(itemIndex) {
            var result = document.getElementById('reviewResult_' + itemIndex).value;
            var reviewer = document.getElementById('reviewer_' + itemIndex).value;
            var notes = document.getElementById('reviewNotes_' + itemIndex).value;
            
            // 病房區域允許不填結果，公共區域必填
            if (!result && currentViewingRecord.area === '公共區域') {
                showMessage('公共區域必須選擇複查結果!', 'error');
                return;
            }
            
            // 收集複查照片
            var reviewPhotos = [];
            var imgs = document.querySelectorAll('#review-photos-preview-' + itemIndex + ' img');
            for (var i = 0; i < imgs.length; i++) {
                reviewPhotos.push(imgs[i].src);
            }
            
            // 更新記錄 (只在有填寫內容時才更新)
            if (result || reviewer || notes || reviewPhotos.length > 0) {
                currentViewingRecord.items[itemIndex].reviewResult = result;
                currentViewingRecord.items[itemIndex].reviewer = reviewer;
                currentViewingRecord.items[itemIndex].reviewNotes = notes;
                currentViewingRecord.items[itemIndex].reviewPhotos = reviewPhotos;
                currentViewingRecord.items[itemIndex].reviewDateTime = new Date().toISOString();
                currentViewingRecord.items[itemIndex].reviewStatus = result ? 'completed' : 'partial';
                
                // 儲存
                try {
                    localStorage.setItem('hospitalRecords_v2025', JSON.stringify(inspectionRecords));
                    showMessage('複查已提交!', 'success');
                    closeModal();
                    
                    // 重新載入記錄
                    var activeTab = document.querySelector('.tab.active').getAttribute('data-tab');
                    if (activeTab === 'myRecords') {
                        loadMyRecords();
                    } else if (activeTab === 'allRecords') {
                        loadAllRecords();
                    }
                } catch (e) {
                    console.error('儲存失敗:', e);
                    showMessage('儲存失敗，請重試', 'error');
                }
            } else {
                closeModal();
            }
        }

        // 頁面載入完成後檢查登入狀態
        document.addEventListener('DOMContentLoaded', function() {
            var savedUser = localStorage.getItem('currentUser');
            if (savedUser) {
                currentUser = savedUser;
                document.getElementById('loginScreen').classList.add('hidden');
                document.getElementById('mainSystem').classList.remove('hidden');
                document.getElementById('currentUser').textContent = savedUser;
                init();
            }
        });

        // 點擊模態框外部關閉
        window.onclick = function(event) {
            var modal = document.getElementById('recordModal');
            if (event.target == modal) {
                closeModal();
            }
        }

        // ========== 資料匯出功能 ==========
        
        // 匯出資料主函數
        function exportData() {
            var format = document.getElementById('exportFormat').value;
            var range = document.getElementById('exportRange').value;
            var includeBasicInfo = document.getElementById('includeBasicInfo').checked;
            var includeItems = document.getElementById('includeItems').checked;
            var includeATP = document.getElementById('includeATP').checked;
            var includeReview = document.getElementById('includeReview').checked;
            
            // 過濾記錄
            var records = filterRecordsByRange(range);
            
            if (records.length === 0) {
                showMessage('沒有符合條件的記錄可以匯出', 'error');
                return;
            }
            
            // 根據格式匯出
            if (format === 'excel') {
                exportToExcel(records, includeBasicInfo, includeItems, includeATP, includeReview);
            } else if (format === 'csv') {
                exportToCSV(records, includeBasicInfo, includeItems, includeATP, includeReview);
            } else if (format === 'json') {
                exportToJSON(records);
            }
        }
        
        // 根據範圍過濾記錄
        function filterRecordsByRange(range) {
            var records = inspectionRecords;
            
            if (range === 'my') {
                records = records.filter(function(r) { return r.inspector === currentUser; });
            } else if (range === 'dateRange') {
                var startDate = document.getElementById('exportStartDate').value;
                var endDate = document.getElementById('exportEndDate').value;
                
                if (!startDate || !endDate) {
                    showMessage('請選擇日期範圍', 'error');
                    return [];
                }
                
                records = records.filter(function(r) {
                    var recordDate = r.dateTime.split('T')[0];
                    return recordDate >= startDate && recordDate <= endDate;
                });
            }
            
            return records;
        }
        
        // 匯出為 Excel
        function exportToExcel(records, includeBasicInfo, includeItems, includeATP, includeReview) {
            var csv = [];
            
            // 標題行
            var headers = [];
            if (includeBasicInfo) {
                headers.push('記錄ID', '巡檢人員', '巡檢日期', '巡檢時間', '提交時間', '棟別', '區域');
            }
            if (includeItems) {
                headers.push('項目編號', '病房名稱', '巡檢項目', '備註');
            }
            if (includeATP) {
                headers.push('ATP檢測統計');
            }
            if (includeReview) {
                headers.push('複查狀態', '複查結果', '複查人員', '複查時間', '複查備註');
            }
            csv.push(headers);
            
            // 數據行
            for (var i = 0; i < records.length; i++) {
                var record = records[i];
                var dateTime = new Date(record.dateTime);
                var submitTime = new Date(record.submitTime);
                
                for (var j = 0; j < record.items.length; j++) {
                    var item = record.items[j];
                    var row = [];
                    
                    if (includeBasicInfo) {
                        row.push(
                            record.id,
                            record.inspector,
                            dateTime.toLocaleDateString(),
                            dateTime.toLocaleTimeString(),
                            submitTime.toLocaleString(),
                            record.building,
                            record.area
                        );
                    }
                    
                    if (includeItems) {
                        row.push(
                            j + 1,
                            item.wardName || '',
                            item.item || '',
                            item.notes || ''
                        );
                    }
                    
                    if (includeATP) {
                        var atpCount = Object.keys(item.atpResults || {}).length;
                        var atpPass = 0;
                        for (var key in item.atpResults) {
                            if (item.atpResults[key] === '合格') atpPass++;
                        }
                        row.push(atpCount > 0 ? atpPass + '/' + atpCount + ' 合格' : '無ATP檢測');
                    }
                    
                    if (includeReview) {
                        var reviewStatus = item.reviewResult ? '已複查' : '未複查';
                        var reviewTime = item.reviewDateTime ? new Date(item.reviewDateTime).toLocaleString() : '';
                        row.push(
                            reviewStatus,
                            item.reviewResult || '',
                            item.reviewer || '',
                            reviewTime,
                            item.reviewNotes || ''
                        );
                    }
                    
                    csv.push(row);
                }
            }
            
            // 轉換為 CSV 格式
            var csvContent = csv.map(function(row) {
                return row.map(function(cell) {
                    var cellStr = String(cell);
                    // 處理包含逗號或換行的內容
                    if (cellStr.indexOf(',') !== -1 || cellStr.indexOf('\n') !== -1 || cellStr.indexOf('"') !== -1) {
                        return '"' + cellStr.replace(/"/g, '""') + '"';
                    }
                    return cellStr;
                }).join(',');
            }).join('\n');
            
            // 加入 BOM 以支援中文
            var BOM = '\uFEFF';
            var blob = new Blob([BOM + csvContent], { type: 'text/csv;charset=utf-8;' });
            downloadFile(blob, '巡檢記錄_' + getDateString() + '.csv', records.length);
        }
        
        // 匯出為 CSV
        function exportToCSV(records, includeBasicInfo, includeItems, includeATP, includeReview) {
            exportToExcel(records, includeBasicInfo, includeItems, includeATP, includeReview);
        }
        
        // 匯出為 JSON
        function exportToJSON(records) {
            var json = JSON.stringify(records, null, 2);
            var blob = new Blob([json], { type: 'application/json' });
            downloadFile(blob, '巡檢記錄_' + getDateString() + '.json', records.length);
        }
        
        // 下載檔案
        function downloadFile(blob, filename, recordCount) {
            var url = URL.createObjectURL(blob);
            var a = document.createElement('a');
            a.href = url;
            a.download = filename;
            
            // 顯示結果
            var resultDiv = document.getElementById('exportResult');
            var messageDiv = document.getElementById('exportMessage');
            var downloadLink = document.getElementById('downloadLink');
            
            messageDiv.textContent = '成功匯出 ' + recordCount + ' 筆記錄';
            downloadLink.href = url;
            downloadLink.download = filename;
            downloadLink.textContent = '下載 ' + filename;
            
            resultDiv.style.display = 'block';
            
            // 自動下載
            document.body.appendChild(a);
            a.click();
            document.body.removeChild(a);
            
            // 捲動到結果區域
            resultDiv.scrollIntoView({ behavior: 'smooth' });
        }
        
        // 獲取日期字串
        function getDateString() {
            var now = new Date();
            var year = now.getFullYear();
            var month = String(now.getMonth() + 1).padStart(2, '0');
            var day = String(now.getDate()).padStart(2, '0');
            var hour = String(now.getHours()).padStart(2, '0');
            var minute = String(now.getMinutes()).padStart(2, '0');
            return year + month + day + '_' + hour + minute;
        }
        
        // ========== PWA 功能 ==========
        
        // 註冊 Service Worker
        if ('serviceWorker' in navigator) {
            window.addEventListener('load', function() {
                navigator.serviceWorker.register('service-worker.js')
                    .then(function(registration) {
                        console.log('Service Worker 註冊成功:', registration.scope);
                    })
                    .catch(function(error) {
                        console.log('Service Worker 註冊失敗:', error);
                    });
            });
        }
        
        // PWA 安裝提示
        let deferredPrompt;
        
        window.addEventListener('beforeinstallprompt', function(e) {
            // 防止預設的安裝提示
            e.preventDefault();
            deferredPrompt = e;
            
            // 顯示自訂安裝提示（在使用者登入後）
            if (currentUser) {
                showInstallPrompt();
            }
        });
        
        function showInstallPrompt() {
            if (!deferredPrompt) return;
            
            // 檢查是否已經提示過
            if (localStorage.getItem('pwa-install-prompted')) return;
            
            // 建立安裝提示
            var promptDiv = document.createElement('div');
            promptDiv.style.cssText = 'position: fixed; bottom: 20px; left: 50%; transform: translateX(-50%); background: white; padding: 20px; border-radius: 10px; box-shadow: 0 4px 12px rgba(0,0,0,0.3); z-index: 10000; max-width: 90%; text-align: center;';
            promptDiv.innerHTML = '<div style="margin-bottom: 15px; font-weight: bold;">📱 安裝到手機</div>' +
                '<div style="margin-bottom: 15px; font-size: 14px; color: #666;">將系統加入主畫面，就像 APP 一樣使用</div>' +
                '<button id="installBtn" style="background: #2c5aa0; color: white; border: none; padding: 10px 20px; border-radius: 5px; margin-right: 10px; cursor: pointer;">立即安裝</button>' +
                '<button id="cancelBtn" style="background: #ccc; color: #333; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer;">稍後再說</button>';
            
            document.body.appendChild(promptDiv);
            
            document.getElementById('installBtn').addEventListener('click', function() {
                deferredPrompt.prompt();
                deferredPrompt.userChoice.then(function(choiceResult) {
                    if (choiceResult.outcome === 'accepted') {
                        console.log('使用者接受安裝');
                    }
                    deferredPrompt = null;
                    document.body.removeChild(promptDiv);
                    localStorage.setItem('pwa-install-prompted', 'true');
                });
            });
            
            document.getElementById('cancelBtn').addEventListener('click', function() {
                document.body.removeChild(promptDiv);
                localStorage.setItem('pwa-install-prompted', 'true');
            });
        }
        
        // 檢測 APP 是否已安裝
        window.addEventListener('appinstalled', function() {
            console.log('PWA 已安裝');
            showMessage('系統已安裝到主畫面！', 'success');
        });
    </script>
</body>
</html>


