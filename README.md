<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Manajemen Mahasiswa - UNIDA</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-gradient: linear-gradient(135deg, #0f172a 0%, #1e3a8a 100%);
            --card-bg: #ffffff;
            --text-main: #1e293b;
            --text-muted: #475569;
            --border-color: #cbd5e1;
            --input-bg: #f8fafc;
            --primary: #2563eb;
            --primary-hover: #1d4ed8;
            --table-header: #f8fafc;
            --shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
        }

        [data-theme="dark"] {
            --bg-gradient: linear-gradient(135deg, #020617 0%, #0f172a 100%);
            --card-bg: #1e293b;
            --text-main: #f8fafc;
            --text-muted: #94a3b8;
            --border-color: #334155;
            --input-bg: #0f172a;
            --primary: #3b82f6;
            --primary-hover: #2563eb;
            --table-header: #0f172a;
            --shadow: 0 15px 35px rgba(0, 0, 0, 0.5);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Inter', sans-serif;
            transition: background 0.3s, color 0.3s, border-color 0.3s;
        }

        body {
            background: var(--bg-gradient);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        
        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr;
            gap: 25px;
            width: 100%;
            max-width: 1100px;
        }

        @media (min-width: 900px) {
            .dashboard-grid {
                grid-template-columns: 400px 1fr;
                align-items: start;
            }
        }

        .card {
            background: var(--card-bg);
            padding: 30px;
            border-radius: 16px;
            box-shadow: var(--shadow);
            position: relative;
        }

        .header-section {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 25px;
            border-bottom: 2px solid var(--border-color);
            padding-bottom: 15px;
        }

        .logo-unida {
            height: 48px;
            width: auto;
            object-fit: contain;
        }

        .top-controls {
            display: flex;
            gap: 8px;
            align-items: center;
        }

        .icon-btn {
            background: var(--input-bg);
            border: 1px solid var(--border-color);
            color: var(--text-main);
            padding: 8px 12px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 12px;
            font-weight: 600;
        }

        .icon-btn:hover {
            border-color: var(--primary);
        }

        h3 {
            color: var(--text-main);
            font-size: 18px;
            font-weight: 700;
        }

        .form-group {
            margin-bottom: 18px;
        }

        label {
            display: block;
            margin-bottom: 6px;
            color: var(--text-muted);
            font-weight: 600;
            font-size: 13px;
        }

        input[type="text"],
        select {
            width: 100%;
            padding: 11px 14px;
            border: 1.5px solid var(--border-color);
            border-radius: 8px;
            font-size: 14px;
            color: var(--text-main);
            outline: none;
            background-color: var(--input-bg);
        }

        input[type="text"]:focus,
        select:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(37, 99, 235, 0.15);
        }

        input.error-border, select.error-border {
            border-color: #dc2626 !important;
        }

        small {
            display: block;
            margin-top: 5px;
            color: #dc2626;
            font-size: 11px;
            font-weight: 500;
            display: none;
        }

        .btn-group {
            display: flex;
            gap: 10px;
            margin-top: 15px;
        }

        button.primary-btn {
            flex: 1;
            padding: 11px;
            background: var(--primary);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 15px;
            font-weight: 600;
            cursor: pointer;
        }

        button.primary-btn:hover {
            background: var(--primary-hover);
        }

        button.reset-btn {
            background: var(--input-bg);
            color: var(--text-muted);
            border: 1px solid var(--border-color);
        }

        
        .table-header-flex {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
            gap: 10px;
        }

        .counter-badge {
            background: rgba(37, 99, 235, 0.1);
            color: var(--primary);
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }

        .search-input {
            width: 100%;
            padding: 10px 14px;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            font-size: 13px;
            outline: none;
            margin-bottom: 15px;
            background-color: var(--input-bg);
            color: var(--text-main);
        }

        .table-responsive {
            width: 100%;
            overflow-x: auto; 
        }

        table {
            width: 100%;
            border-collapse: collapse;
            white-space: nowrap;
        }

        th, td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid var(--border-color);
            font-size: 13px;
            color: var(--text-main);
        }

        th {
            background-color: var(--table-header);
            color: var(--text-muted);
            font-weight: 600;
        }

        .btn-delete {
            background: #dc2626;
            color: white;
            padding: 5px 10px;
            border-radius: 6px;
            font-size: 11px;
            cursor: pointer;
            border: none;
        }

        .btn-delete:hover {
            background: #b91c1c;
        }

        
        #toast {
            visibility: hidden;
            min-width: 250px;
            background-color: #10b981;
            color: white;
            text-align: center;
            border-radius: 8px;
            padding: 12px;
            position: fixed;
            z-index: 1000;
            right: 30px;
            bottom: 30px;
            font-size: 14px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        #toast.show {
            visibility: visible;
            animation: fadein 0.5s, fadeout 0.5s 2.5s;
        }

        @keyframes fadein {
            from {bottom: 0; opacity: 0;}
            to {bottom: 30px; opacity: 1;}
        }

        @keyframes fadeout {
            from {bottom: 30px; opacity: 1;}
            to {bottom: 0; opacity: 0;}
        }
    </style>
</head>
<body data-theme="dark">

<div class="dashboard-grid">
    
    <div class="card">
        <div class="header-section">
            <img src="https://unida.ac.id/img/logo-unida.png" alt="Logo UNIDA" class="logo-unida">
            <div class="top-controls">
                <button class="icon-btn" onclick="toggleTheme()" id="themeBtn">☀️ light</button>
            </div>
        </div>

        <h3 style="margin-bottom: 20px;">Tambah Data Mahasiswa</h3>

        <form id="formMahasiswa">
            <div class="form-group">
                <label for="nim">NIM:</label>
                <input type="text" id="nim" placeholder="Masukkan NIM">
                <small id="errorNim">NIM harus diisi!</small>
            </div>

            <div class="form-group">
                <label for="nama">Nama Lengkap:</label>
                <input type="text" id="nama" placeholder="Masukkan Nama">
                <small id="errorNama">Nama harus diisi!</small>
            </div>

            <div class="form-group">
                <label for="matkul">Mata Kuliah:</label>
                <select id="matkul">
                    <option value="">-- Pilih Mata Kuliah --</option>
                    <option>Pemrograman Web</option>
                    <option>Basis Data</option>
                    <option>Desain UI/UX</option>
                </select>
                <small id="errorMatkul">Pilih mata kuliah!</small>
            </div>

            <div class="btn-group">
                <button type="submit" class="primary-btn">Simpan</button>
                <button type="reset" class="primary-btn reset-btn">Reset</button>
            </div>
        </form>
    </div>

    
    <div class="card" id="tableCard" style="display: none;">
        <div class="table-header-flex">
            <h3>Daftar Mahasiswa</h3>
            <span class="counter-badge" id="studentCount">Total: 0</span>
        </div>
        
        <input type="text" id="searchBox" class="search-input" placeholder="Cari NIM atau Nama...">

        <div class="table-responsive">
            <table>
                <thead>
                    <tr>
                        <th>NIM</th>
                        <th>Nama</th>
                        <th>Mata Kuliah</th>
                        <th>Aksi</th>
                    </tr>
                </thead>
                <tbody id="dataTable">
                </tbody>
            </table>
        </div>
    </div>
</div>


<div id="toast">Data berhasil disimpan!</div>

<script>
    let students = JSON.parse(localStorage.getItem('unida_students')) || [];

    function showToast(message, isError = false) {
        let toast = document.getElementById("toast");
        toast.innerText = message;
        toast.style.backgroundColor = isError ? "#dc2626" : "#10b981";
        toast.className = "show";
        setTimeout(() => { toast.className = toast.className.replace("show", ""); }, 3000);
    }

    function toggleTheme() {
        let body = document.body;
        let btn = document.getElementById("themeBtn");
        if (body.getAttribute("data-theme") === "dark") {
            body.setAttribute("data-theme", "light");
            btn.innerText = "🌙 Dark";
        } else {
            body.setAttribute("data-theme", "dark");
            btn.innerText = "☀️ light";
        }
    }

    function renderTable() {
        let dataTable = document.getElementById('dataTable');
        let tableCard = document.getElementById('tableCard');
        let studentCount = document.getElementById('studentCount');
        let searchTerm = document.getElementById('searchBox').value.toLowerCase();

        dataTable.innerHTML = '';

        if (students.length > 0) {
            tableCard.style.display = 'block';
        } else {
            tableCard.style.display = 'none';
        }

        let filtered = students.filter(s => 
            s.nim.toLowerCase().includes(searchTerm) || 
            s.nama.toLowerCase().includes(searchTerm)
        );

        studentCount.innerText = `Total: ${students.length}`;

        filtered.forEach((student, index) => {
            let row = document.createElement('tr');
            row.innerHTML = `
                <td>${student.nim}</td>
                <td>${student.nama}</td>
                <td>${student.matkul}</td>
                <td><button class="btn-delete" onclick="deleteStudent(${index})">Hapus</button></td>
            `;
            dataTable.appendChild(row);
        });
    }

    function deleteStudent(index) {
        students.splice(index, 1);
        localStorage.setItem('unida_students', JSON.stringify(students));
        renderTable();
        showToast("Data berhasil dihapus!", true);
    }

    document.getElementById('searchBox').addEventListener('input', renderTable);

    document.getElementById('formMahasiswa').addEventListener('submit', function(e) {
        e.preventDefault();
        
        let nimInput = document.getElementById('nim');
        let namaInput = document.getElementById('nama');
        let matkulInput = document.getElementById('matkul');
        
        let nim = nimInput.value.trim();
        let nama = namaInput.value.trim();
        let matkul = matkulInput.value;

        let isValid = true;

        if (nim === '') {
            document.getElementById('errorNim').style.display = 'block';
            nimInput.classList.add('error-border');
            isValid = false;
        } else {
            document.getElementById('errorNim').style.display = 'none';
            nimInput.classList.remove('error-border');
        }

        if (nama === '') {
            document.getElementById('errorNama').style.display = 'block';
            namaInput.classList.add('error-border');
            isValid = false;
        } else {
            document.getElementById('errorNama').style.display = 'none';
            namaInput.classList.remove('error-border');
        }

        if (matkul === '') {
            document.getElementById('errorMatkul').style.display = 'block';
            matkulInput.classList.add('error-border');
            isValid = false;
        } else {
            document.getElementById('errorMatkul').style.display = 'none';
            matkulInput.classList.remove('error-border');
        }

        if (isValid) {
            students.push({ nim, nama, matkul });
            localStorage.setItem('unida_students', JSON.stringify(students));
            renderTable();
            document.getElementById('formMahasiswa').reset();
            showToast("Data berhasil disimpan!");
        }
    });

    window.onload = renderTable;
</script>

</body>
</html>
