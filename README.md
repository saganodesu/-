<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>見積書・請求書システム | 株式会社メカワーク</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Hiragino Kaku Gothic Pro', 'Meiryo', sans-serif;
            background: #e8f0fe;
            padding: 20px;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
        }

        /* ヘッダー */
        .header {
            background: linear-gradient(135deg, #1a3a5c, #2c5a7a);
            color: white;
            padding: 20px 25px;
            border-radius: 12px;
            margin-bottom: 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .header h1 {
            font-size: 1.6rem;
            font-weight: 500;
        }

        .header h1 small {
            font-size: 0.8rem;
            opacity: 0.8;
        }

        .company-info {
            text-align: right;
            font-size: 0.8rem;
            line-height: 1.4;
        }

        /* タブ */
        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            flex-wrap: wrap;
        }

        .tab-btn {
            padding: 12px 28px;
            border: none;
            background: white;
            border-radius: 30px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            color: #1a3a5c;
        }

        .tab-btn.active {
            background: linear-gradient(135deg, #1a3a5c, #2c5a7a);
            color: white;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
        }

        .tab-btn:hover:not(.active) {
            background: #d4e4f5;
            transform: translateY(-2px);
        }

        /* パネル */
        .panel {
            display: none;
            background: white;
            border-radius: 16px;
            padding: 25px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.08);
        }

        .panel.active {
            display: block;
        }

        /* 表 */
        .data-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 0.85rem;
        }

        .data-table th {
            background: #1a3a5c;
            color: white;
            padding: 12px 8px;
            text-align: center;
            font-weight: 600;
            position: sticky;
            top: 0;
        }

        .data-table td {
            border-bottom: 1px solid #ddd;
            padding: 10px 8px;
            text-align: center;
        }

        .data-table tr:hover {
            background: #f0f6ff;
        }

        .action-btn {
            padding: 4px 10px;
            margin: 0 3px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 0.75rem;
        }

        .edit-btn {
            background: #ffc107;
            color: #333;
        }

        .delete-btn {
            background: #dc3545;
            color: white;
        }

        .print-btn {
            background: #28a745;
            color: white;
            padding: 8px 20px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 0.9rem;
        }

        /* フォーム */
        .form-group {
            margin-bottom: 20px;
        }

        .form-row {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-bottom: 20px;
        }

        label {
            display: block;
            font-weight: 600;
            margin-bottom: 6px;
            color: #333;
        }

        input, select {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #ccc;
            border-radius: 8px;
            font-size: 0.9rem;
        }

        .submit-btn {
            background: linear-gradient(135deg, #1a3a5c, #2c5a7a);
            color: white;
            padding: 12px 30px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            cursor: pointer;
            margin-top: 10px;
        }

        /* 書類表示エリア */
        .document-area {
            background: #f9f9f9;
            border-radius: 12px;
            padding: 20px;
            margin-top: 20px;
        }

        .document-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 2px solid #1a3a5c;
        }

        .document-title {
            font-size: 1.8rem;
            font-weight: bold;
            color: #1a3a5c;
        }

        .document-table {
            width: 100%;
            border-collapse: collapse;
            margin: 15px 0;
        }

        .document-table th, .document-table td {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: left;
        }

        .document-table th {
            background: #e8f0fe;
        }

        .total-area {
            text-align: right;
            margin-top: 20px;
            padding-top: 15px;
            border-top: 2px solid #ddd;
        }

        /* 統計カード */
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .stat-card {
            background: linear-gradient(135deg, #1a3a5c, #2c5a7a);
            color: white;
            padding: 18px;
            border-radius: 12px;
            text-align: center;
        }

        .stat-card h3 {
            font-size: 0.9rem;
            opacity: 0.9;
        }

        .stat-card .number {
            font-size: 2rem;
            font-weight: bold;
        }

        /* レスポンシブ */
        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                text-align: center;
            }
            .company-info {
                text-align: center;
                margin-top: 10px;
            }
            .data-table {
                font-size: 0.7rem;
            }
        }

        @media print {
            body {
                background: white;
                padding: 0;
            }
            .tabs, .header, .stats, .form-group, .submit-btn, .action-btn, .print-btn, #selectDocument, label {
                display: none;
            }
            .panel {
                display: block !important;
                padding: 0;
                box-shadow: none;
            }
            .document-area {
                background: white;
                padding: 0;
            }
        }
    </style>
</head>
<body>
<div class="container">
    <div class="header">
        <h1>📄 見積書・請求書システム <small>株式会社メカワーク</small></h1>
        <div class="company-info">
            〒551-0003 大阪府大阪市大正区千島2-4UR 千島団地2-611<br>
            TEL：070-3537-4004 / Email：motoyuki5611@gmail.com<br>
            登録番号：T8120001266455
        </div>
    </div>

    <div class="tabs">
        <button class="tab-btn active" data-tab="list">📋 一覧表示</button>
        <button class="tab-btn" data-tab="add">➕ 新規登録</button>
        <button class="tab-btn" data-tab="print">🖨️ 書類印刷</button>
        <button class="tab-btn" data-tab="stats">📊 集計ダッシュボード</button>
    </div>

    <!-- 一覧表示パネル -->
    <div id="listPanel" class="panel active">
        <div style="overflow-x: auto;">
            <table class="data-table" id="dataTable">
                <thead>
                    <tr><th>ID</th><th>日付</th><th>書類</th><th>顧客名</th><th>車両</th><th>作業内容</th><th>数量</th><th>単価</th><th>金額</th><th>依頼主</th><th>操作</th></tr>
                </thead>
                <tbody id="tableBody"></tbody>
            </table>
        </div>
    </div>

    <!-- 新規登録パネル -->
    <div id="addPanel" class="panel">
        <h3 style="margin-bottom: 20px;">新規案件登録</h3>
        <div class="form-row">
            <div class="form-group"><label>日付</label><input type="date" id="newDate"></div>
            <div class="form-group"><label>書類種別</label><select id="newType"><option>見積書</option><option>請求書</option></select></div>
            <div class="form-group"><label>顧客名</label><input type="text" id="newCustomer" placeholder="例：いすゞ自動車近畿"></div>
        </div>
        <div class="form-row">
            <div class="form-group"><label>車両</label><input type="text" id="newVehicle" placeholder="例：大阪100か1234"></div>
            <div class="form-group"><label>作業内容</label><input type="text" id="newWork" placeholder="例：ラジエーター交換"></div>
            <div class="form-group"><label>依頼主</label><input type="text" id="newRequester" placeholder="例：河合様"></div>
        </div>
        <div class="form-row">
            <div class="form-group"><label>数量</label><input type="number" id="newQty" value="1" min="1"></div>
            <div class="form-group"><label>単価（円）</label><input type="number" id="newPrice" value="0" min="0"></div>
            <div class="form-group"><label>金額（円）</label><input type="text" id="newAmount" readonly style="background:#e9ecef;"></div>
        </div>
        <button class="submit-btn" onclick="addRecord()">✅ 登録する</button>
    </div>

    <!-- 書類印刷パネル -->
    <div id="printPanel" class="panel">
        <div class="form-group">
            <label>IDを選択してください</label>
            <select id="selectDocument" style="width: 200px; margin-bottom: 20px;"></select>
            <button class="print-btn" onclick="printDocument()">🖨️ 印刷 / PDF保存</button>
        </div>
        <div id="documentDisplay" class="document-area"></div>
    </div>

    <!-- 集計パネル -->
    <div id="statsPanel" class="panel">
        <div class="stats" id="statsCards"></div>
        <div style="overflow-x: auto;">
            <table class="data-table" id="statsTable">
                <thead><tr><th>顧客名</th><th>件数</th><th>合計金額（税抜）</th><th>消費税</th><th>税込合計</th></tr></thead>
                <tbody id="statsBody"></tbody>
            </table>
        </div>
    </div>
</div>

<script>
    // ==================== データ（元のExcelから抽出） ====================
    let documents = [
        { id: 1, date: "2025-08-04", type: "見積書", customer: "脇田運輸株式会社", vehicle: "なにわ100き6451", work: "ウォーターポンプ交換・サーモスタッド交換・インナーシール交換", qty: 1, price: 30000, amount: 30000, requester: "河合様" },
        { id: 2, date: "2025-08-05", type: "見積書", customer: "クレベ運輸株式会社", vehicle: "なにわ100き4077", work: "オイルクーラーバイパスバルブ交換", qty: 1, price: 47300, amount: 47300, requester: "前田様" },
        { id: 3, date: "2025-08-08", type: "見積書", customer: "株式会社サンスターライン", vehicle: "なにわ200か2405", work: "DPD清掃・排気インジェクター交換", qty: 1, price: 40000, amount: 40000, requester: "久保田様" },
        { id: 4, date: "2025-08-28", type: "見積書", customer: "クレベ運送株式会社", vehicle: "なにわ100き6176", work: "オイルクーラー交換", qty: 1, price: 34100, amount: 34100, requester: "前田様" },
        { id: 5, date: "2025-09-03", type: "見積書", customer: "株式会社TBSワークス", vehicle: "大阪101い56", work: "ミッション脱着・トルコン脱着・オイルポンプ交換", qty: 1, price: 30000, amount: 30000, requester: "後藤様" },
        { id: 6, date: "2025-09-05", type: "見積書", customer: "株式会社日本トランスネット", vehicle: "大阪130あ1518", work: "DPD清掃", qty: 1, price: 41800, amount: 41800, requester: "山名様" },
        { id: 7, date: "2025-09-08", type: "見積書", customer: "株式会社大興運輸", vehicle: "堺130あ5767", work: "DPD清掃", qty: 1, price: 30000, amount: 30000, requester: "久保田様" },
        { id: 8, date: "2025-10-21", type: "見積書", customer: "株式会社三和", vehicle: "大阪800か4552", work: "エキゾーストパイプ交換・DPD清掃", qty: 1, price: 50000, amount: 50000, requester: "森野様" },
        { id: 9, date: "2025-10-23", type: "見積書", customer: "株式会社アクタス", vehicle: "大阪115か1111", work: "コンプレッサーヘッド交換", qty: 1, price: 28000, amount: 28000, requester: "船越様" },
        { id: 10, date: "2025-11-02", type: "見積書", customer: "株式会社中野商会", vehicle: "なにわ100き7289", work: "エンジンリターダー交換", qty: 2, price: 5500, amount: 11000, requester: "久保田様" },
        { id: 11, date: "2025-11-03", type: "見積書", customer: "一宮運輸株式会社", vehicle: "大阪101か2564", work: "ラジエーター交換", qty: 1, price: 20000, amount: 20000, requester: "久保田様" },
        { id: 12, date: "2025-11-10", type: "見積書", customer: "シナノライン株式会社", vehicle: "大阪101か3381", work: "ラジエーター・ホース交換", qty: 1, price: 19800, amount: 19800, requester: "山名様" },
        { id: 13, date: "2025-11-12", type: "見積書", customer: "LINK ONE株式会社", vehicle: "", work: "クラッチOH", qty: 1, price: 30000, amount: 30000, requester: "中井様" },
        { id: 14, date: "2025-11-26", type: "見積書", customer: "", vehicle: "大阪137け6666", work: "リアリール交換・リターダー・シフトフォーク交換", qty: 1, price: 94050, amount: 94050, requester: "森野様" },
        { id: 15, date: "2025-12-02", type: "見積書", customer: "神山運輸株式会社", vehicle: "愛媛830あ667", work: "コンプレッサーヘッド・ドライヤOH・サーモ交換", qty: 1, price: 36000, amount: 36000, requester: "久保田様" },
        { id: 16, date: "2025-12-16", type: "見積書", customer: "株式会社フジラインエキスプレス", vehicle: "堺100か1740", work: "ラジエーター交換", qty: 1, price: 27000, amount: 27000, requester: "河合様" },
        { id: 17, date: "2026-01-05", type: "見積書", customer: "株式会社トーヨーふれ愛バス", vehicle: "大阪200か5039", work: "ミッション脱着", qty: 1, price: 65000, amount: 65000, requester: "飯田様" },
        { id: 18, date: "2026-01-06", type: "見積書", customer: "アクアロジ株式会社", vehicle: "和泉800あ5239", work: "EGRクーラー交換・DPD・タービン・配管清掃", qty: 1, price: 55000, amount: 55000, requester: "飯田" },
        { id: 19, date: "2026-01-07", type: "見積書", customer: "ラボリス株式会社", vehicle: "神戸130こ7070", work: "クラッチOH・パワーアシスト・リアシール他", qty: 1, price: 100000, amount: 100000, requester: "小堀様" },
        { id: 20, date: "2026-01-10", type: "見積書", customer: "上武運送", vehicle: "大阪102あ6841", work: "ターボ・ダイナモ・セルモーター・EGRクーラー脱着", qty: 1, price: 60000, amount: 60000, requester: "森野様" },
        { id: 21, date: "2026-01-17", type: "見積書", customer: "大正貨物株式会社", vehicle: "大阪100き9093", work: "サーモスタッド・シール・ハウジング交換", qty: 1, price: 30000, amount: 30000, requester: "森野様" },
        { id: 22, date: "2026-01-19", type: "見積書", customer: "株式会社ジーウエスト", vehicle: "大阪101か6774", work: "エンジンassy交換・タイヤ空気圧調整", qty: 1, price: 139000, amount: 139000, requester: "河合様" },
        { id: 23, date: "2026-01-22", type: "請求書", customer: "北港運輸株式会社", vehicle: "なにわ100き1965", work: "サーモスタッド・シールリング交換", qty: 1, price: 27600, amount: 27600, requester: "福井様" },
        { id: 24, date: "2026-01-28", type: "請求書", customer: "株式会社豊中ヤード", vehicle: "大阪100は4964", work: "クラッチOH・ディスク・ベアリング・プレート交換", qty: 1, price: 55000, amount: 55000, requester: "小堀様" },
        { id: 25, date: "2026-01-30", type: "請求書", customer: "日本トランスネット", vehicle: "北九州130い3918", work: "ラジエーター交換", qty: 1, price: 27000, amount: 27000, requester: "久保田様" },
        { id: 26, date: "2026-02-02", type: "見積書", customer: "フジラインエキスプレス", vehicle: "滋賀100か9737", work: "サーモスタッド・インナーシール交換", qty: 1, price: 18000, amount: 18000, requester: "河合様" },
        { id: 27, date: "2026-07-31", type: "請求書", customer: "古川自動車販売株式会社", vehicle: "", work: "作業工賃", qty: 0, price: 0, amount: 0, requester: "" }
    ];

    // 日付フォーマット
    function formatDate(dateStr) {
        if (!dateStr) return "";
        let d = new Date(dateStr);
        return `${d.getFullYear()}/${d.getMonth()+1}/${d.getDate()}`;
    }

    // 金額フォーマット
    function formatMoney(amount) {
        return new Intl.NumberFormat('ja-JP').format(amount) + "円";
    }

    // 一覧表示更新
    function renderTable() {
        let html = "";
        documents.forEach(doc => {
            html += `<tr>
                <td>${doc.id}</td>
                <td>${formatDate(doc.date)}</td>
                <td>${doc.type}</td>
                <td>${doc.customer}</td>
                <td>${doc.vehicle}</td>
                <td style="text-align:left">${doc.work}</td>
                <td>${doc.qty}</td>
                <td>${formatMoney(doc.price)}</td>
                <td>${formatMoney(doc.amount)}</td>
                <td>${doc.requester}</td>
                <td>
                    <button class="action-btn edit-btn" onclick="editRecord(${doc.id})">編集</button>
                    <button class="action-btn delete-btn" onclick="deleteRecord(${doc.id})">削除</button>
                </td>
            </tr>`;
        });
        document.getElementById("tableBody").innerHTML = html;
        
        // 印刷用セレクトボックス更新
        let selectHtml = `<option value="">-- IDを選択 --</option>`;
        documents.forEach(doc => {
            selectHtml += `<option value="${doc.id}">${doc.id}: ${doc.customer} (${formatDate(doc.date)})</option>`;
        });
        document.getElementById("selectDocument").innerHTML = selectHtml;
        
        // 集計更新
        updateStats();
    }

    // 編集
    function editRecord(id) {
        let doc = documents.find(d => d.id === id);
        if (!doc) return;
        let newAmount = prompt("新しい金額（円）を入力してください", doc.amount);
        if (newAmount !== null && !isNaN(parseFloat(newAmount))) {
            doc.amount = parseInt(newAmount);
            renderTable();
        }
    }

    // 削除
    function deleteRecord(id) {
        if (confirm("この案件を削除しますか？")) {
            documents = documents.filter(d => d.id !== id);
            renderTable();
        }
    }

    // 新規登録
    function addRecord() {
        let newDate = document.getElementById("newDate").value;
        let newType = document.getElementById("newType").value;
        let newCustomer = document.getElementById("newCustomer").value;
        let newVehicle = document.getElementById("newVehicle").value;
        let newWork = document.getElementById("newWork").value;
        let newRequester = document.getElementById("newRequester").value;
        let newQty = parseInt(document.getElementById("newQty").value);
        let newPrice = parseInt(document.getElementById("newPrice").value);
        
        if (!newDate) {
            alert("日付を入力してください");
            return;
        }
        if (!newCustomer) {
            alert("顧客名を入力してください");
            return;
        }
        
        let newAmount = newQty * newPrice;
        let newId = documents.length > 0 ? Math.max(...documents.map(d => d.id)) + 1 : 1;
        
        documents.push({
            id: newId, date: newDate, type: newType, customer: newCustomer,
            vehicle: newVehicle, work: newWork, qty: newQty, price: newPrice,
            amount: newAmount, requester: newRequester
        });
        
        // フォームクリア
        document.getElementById("newDate").value = "";
        document.getElementById("newCustomer").value = "";
        document.getElementById("newVehicle").value = "";
        document.getElementById("newWork").value = "";
        document.getElementById("newRequester").value = "";
        document.getElementById("newQty").value = "1";
        document.getElementById("newPrice").value = "0";
        
        renderTable();
        alert(`ID ${newId} を登録しました`);
        
        // タブを一覧に移動
        switchTab("list");
    }

    // 金額自動計算
    document.getElementById("newQty")?.addEventListener("input", updateAmount);
    document.getElementById("newPrice")?.addEventListener("input", updateAmount);
    
    function updateAmount() {
        let qty = parseInt(document.getElementById("newQty").value) || 0;
        let price = parseInt(document.getElementById("newPrice").value) || 0;
        document.getElementById("newAmount").value = formatMoney(qty * price);
    }

    // 書類表示
    function printDocument() {
        let id = document.getElementById("selectDocument").value;
        if (!id) {
            alert("IDを選択してください");
            return;
        }
        let doc = documents.find(d => d.id == id);
        if (!doc) return;
        
        let tax = Math.floor(doc.amount * 0.1