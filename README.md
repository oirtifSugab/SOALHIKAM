# <!DOCTYPE html>
<html lang="id" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SoAL-HIKAM</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            box-sizing: border-box;
        }
        .file-item {
            transition: all 0.3s ease;
        }
        .file-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }
        .upload-zone {
            border: 2px dashed #cbd5e1;
            transition: all 0.3s ease;
        }
        .upload-zone.dragover {
            border-color: #3b82f6;
            background-color: #eff6ff;
        }
    </style>
</head>
<body class="h-full bg-gradient-to-br from-blue-50 to-indigo-100">
    <!-- Login Screen -->
    <div id="loginScreen" class="min-h-full flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8 transition-all duration-500 ease-in-out opacity-100">
        <div class="max-w-md w-full space-y-8">
            <div class="text-center">
                <h2 class="mt-6 text-3xl font-extrabold text-gray-900">Sistem Pengumpulan Soal</h2>
                <p class="mt-2 text-sm text-gray-600">SMP & SMK AL-HIKAM</p>
            </div>
            <form id="loginForm" class="mt-8 space-y-6">
                <div class="rounded-md shadow-sm space-y-4">
                    <div>
                        <label for="teacherName" class="block text-sm font-medium text-gray-700 mb-2">Nama Guru</label>
                        <input id="teacherName" name="teacherName" type="text" required 
                               class="appearance-none rounded-lg relative block w-full px-3 py-3 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" 
                               placeholder="Masukkan nama lengkap Anda">
                    </div>
                </div>
                <div>
                    <button type="submit" 
                            class="group relative w-full flex justify-center py-3 px-4 border border-transparent text-sm font-medium rounded-lg text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500 transition-colors">
                        Masuk
                    </button>
                </div>
            </form>
        </div>
    </div>

    <!-- Subject Selection Screen -->
<div id="subjectScreen" class="hidden min-h-full flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-2xl w-full space-y-8">
        <div class="text-center">
            <h2 class="mt-6 text-3xl font-extrabold text-gray-900">Sistem Pengumpulan Soal</h2>
            <p id="welcomeText" class="mt-2 text-sm text-gray-600"></p>
        </div>
        
        <!-- School Level Selection -->
        <div class="bg-white rounded-lg shadow-lg p-6">
            <h3 class="text-lg font-semibold text-gray-900 mb-4">Pilih Jenjang</h3>
            <div class="grid grid-cols-2 gap-4">
                <button id="smpBtn" class="school-level-btn bg-blue-50 hover:bg-blue-100 border-2 border-blue-200 rounded-lg p-4 text-center transition-colors">
                    <div class="text-xl font-bold text-blue-700">SMP</div>
                </button>
                <button id="smkBtn" class="school-level-btn bg-yellow-50 hover:bg-yellow-100 border-2 border-yellow-200 rounded-lg p-4 text-center transition-colors">
                    <div class="text-xl font-bold text-yellow-700">SMK</div>
                </button>
            </div>
        </div>

        <!-- Subject and Class Selection -->
        <div id="selectionForm" class="hidden bg-white rounded-lg shadow-lg p-6">
            <form id="subjectForm" class="space-y-6">
                <div>
                    <label for="filterClass" class="block text-sm font-medium text-gray-700 mb-2">
                        <span class="inline-flex items-center">
                            <span class="bg-indigo-500 text-white rounded-full w-5 h-5 flex items-center justify-center text-xs mr-2">1</span>
                            Kelas
                        </span>
                    </label>
                    <select id="filterClass" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <option value="">Pilih Kelas</option>
                    </select>
                </div>
                <div>
                    <label for="filterSubject" class="block text-sm font-medium text-gray-700 mb-2">
                        <span class="inline-flex items-center">
                            <span class="bg-gray-300 text-white rounded-full w-5 h-5 flex items-center justify-center text-xs mr-2">2</span>
                            Mata Pelajaran
                        </span>
                    </label>
                    <select id="filterSubject" class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <option value="">Pilih Mata Pelajaran</option>
                    </select>
                </div>
                <div class="flex gap-4">
                    <button type="button" id="backBtn" class="flex-1 bg-gray-500 hover:bg-gray-600 text-white py-3 px-4 rounded-lg font-medium transition-colors">
                        Kembali
                    </button>
                    <button type="submit" class="flex-1 bg-indigo-600 hover:bg-indigo-700 text-white py-3 px-4 rounded-lg font-medium transition-colors">
                        Lanjutkan
                    </button>
                </div>
            </form>
        </div>
    </div>
</div>

<!-- Main Application -->
<div id="mainApp" class="hidden min-h-full">
    <!-- Header -->
    <header class="bg-white shadow-sm border-b border-gray-200">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between items-center py-4">
                <div class="flex items-center">
                    <button id="backToSelectionBtn" class="hidden mr-4 bg-gray-500 hover:bg-gray-600 text-white px-3 py-2 rounded-lg text-sm font-medium transition-colors">
                        ← Kembali
                    </button>
                    <h1 class="text-2xl font-bold text-gray-900">Sistem Pengumpulan Soal</h1>
                    <span id="userInfo" class="ml-4 px-3 py-1 bg-indigo-100 text-indigo-800 rounded-full text-sm font-medium"></span>
                </div>
                <button id="logoutBtn" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg text-sm font-medium transition-colors">
                    Keluar
                </button>
            </div>
        </div>
    </header>

    <!-- Main Content -->
    <main class="max-w-7xl mx-auto py-6 sm:px-6 lg:px-8">
        <!-- Teacher View -->
        <div id="teacherView" class="px-4 py-6 sm:px-0">
            <div class="bg-white rounded-lg shadow-lg p-6 mb-6">
                <div class="bg-red-50 border-l-4 border-red-500 text-red-700 p-4 mb-4" role="alert">
                    <p class="font-bold">📌 Informasi Penting</p>
                    <p class="text-sm">• Hanya file .docx yang diperbolehkan</p>
                    <p class="text-sm">• Ukuran maksimal: 10MB per file</p>
                    <p class="text-sm">• File disimpan di browser (localStorage)</p>
                    <p class="text-sm">• Untuk database permanen, hubungi Ketua saja!</p>
                </div>
                <h2 class="text-xl font-semibold text-gray-900 mb-4">Upload File Soal</h2>
                
                <!-- Upload Zone -->
                <div id="uploadZone" class="upload-zone rounded-lg p-8 text-center mb-4">
                    <svg class="mx-auto h-12 w-12 text-gray-400 mb-4" stroke="currentColor" fill="none" viewBox="0 0 48 48">
                        <path d="M28 8H12a4 4 0 00-4 4v20m32-12v8m0 0v8a4 4 0 01-4 4H12a4 4 0 01-4-4v-4m32-4l-3.172-3.172a4 4 0 00-5.656 0L28 28M8 32l9.172-9.172a4 4 0 015.656 0L28 28m0 0l4 4m4-24h8m-4-4v8m-12 4h.02" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
                    </svg>
                    <p class="text-lg text-gray-600 mb-2">Drag & drop file soal di sini</p>
                    <p class="text-sm text-gray-500 mb-4">atau</p>
                    <input type="file" id="fileInput" class="hidden" accept=".docx">
                    <button id="browseBtn" class="bg-indigo-600 hover:bg-indigo-700 text-white px-6 py-2 rounded-lg font-medium transition-colors">
                        Pilih File
                    </button>
                </div>

                <!-- File Info -->
                <div id="fileInfo" class="hidden bg-gray-50 rounded-lg p-4 mb-4">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center">
                            <svg class="h-8 w-8 text-indigo-600 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                            </svg>
                            <div>
                                <p id="fileName" class="font-medium text-gray-900"></p>
                                <p id="fileSize" class="text-sm text-gray-500"></p>
                            </div>
                        </div>
                        <button id="removeFile" class="text-red-500 hover:text-red-700">
                            <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                            </svg>
                        </button>
                    </div>
                </div>

                <button id="uploadBtn" class="w-full bg-yellow-600 hover:bg-yellow-700 text-white py-3 px-4 rounded-lg font-medium transition-colors disabled:bg-gray-400 disabled:cursor-not-allowed" disabled>
                    Upload File Soal
                </button>
            </div>

            <!-- My Files -->
            <div class="bg-white rounded-lg shadow-lg p-6">
                <h2 class="text-xl font-semibold text-gray-900 mb-4">File Soal Saya</h2>
                <div id="myFiles" class="space-y-3">
                    <p class="text-gray-500 text-center py-8">Belum ada file yang diupload</p>
                </div>
            </div>
        </div>

        <!-- Admin View -->
        <div id="adminView" class="hidden px-4 py-6 sm:px-0">
            <div class="bg-white rounded-lg shadow-lg p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-xl font-semibold text-gray-900">Dashboard Admin</h2>
                    <div class="text-sm text-gray-600">
                        Total: <span id="totalFiles" class="font-semibold">0</span> file
                    </div>
                </div>
                
                <!-- Filter -->
                <div class="mb-6 grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label for="adminFilterClass" class="block text-sm font-medium text-gray-700 mb-2">
                            <span class="inline-flex items-center">
                                <span class="bg-indigo-500 text-white rounded-full w-6 h-6 flex items-center justify-center text-xs mr-2">1</span>
                                Filter Kelas
                            </span>
                        </label>
                        <select id="adminFilterClass" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            <option value="">Pilih Kelas Terlebih Dahulu</option>
                        </select>
                    </div>
                    <div>
                        <label for="adminFilterSubject" class="block text-sm font-medium text-gray-700 mb-2">
                            <span class="inline-flex items-center">
                                <span class="bg-gray-300 text-white rounded-full w-6 h-6 flex items-center justify-center text-xs mr-2">2</span>
                                Filter Mata Pelajaran
                            </span>
                        </label>
                        <select id="adminFilterSubject" class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-indigo-500 bg-gray-50" disabled>
                            <option value="">-- Pilih Kelas Dahulu --</option>
                        </select>
                    </div>
                </div>

                <div id="allFiles" class="space-y-3">
                    <p class="text-gray-500 text-center py-8">Belum ada file yang diupload</p>
                </div>
            </div>
        </div>
    </main>
</div>

<script>
    // Data storage
    let currentUser = null;
    let files = JSON.parse(localStorage.getItem('examFiles') || '[]');
    let selectedFile = null;
    let selectedSchoolLevel = null;

    // Subject and class data
    const schoolData = {
        smp: {
            subjects: [
                'Pendidikan Agama Islam', 'PJOK', 'Anti Korupsi', 'IPS', 'Seni & Prakarya',
                'Bahasa Inggris', 'IPA', 'Matematika', 'Informatika', 'PKn',
                'Bahasa Lampung', 'Pendidikan Pancasila', 'Bahasa Indonesia'
            ],
            classes: ['VII-A', 'VII-B', 'VII-C', 'VIII-A', 'VIII-B', 'VIII-C', 'IX-A', 'IX-B', 'IX-C']
        },
        smk: {
            subjects: [
                'Kewirausahaan', 'PJOK', 'Pendidikan Anti Korupsi', 'Sejarah', 'Pendidikan Agama Islam',
                'Komputer Grafis', 'Desain Grafis Percetakan', 'Fundamental Desain', 'Desain Publikasi',
                'Projek IPAS', 'Matematika', 'Fotografi', 'Bahasa Indonesia', 'Pendidikan Pancasila',
                'Bahasa Inggris', 'Bahasa Lampung', 'Informatika', 'Peminatan TKJ', 'Seni Rupa', 'Bahasa Jepang'
            ],
            classes: ['X-DKV', 'X-APHP', 'XI-DKV', 'XI-APHP', 'XII-DKV', 'XII-APHP']
        }
    };

    // DOM elements
    const loginScreen = document.getElementById('loginScreen');
    const subjectScreen = document.getElementById('subjectScreen');
    const mainApp = document.getElementById('mainApp');
    const loginForm = document.getElementById('loginForm');
    const subjectForm = document.getElementById('subjectForm');
    const userInfo = document.getElementById('userInfo');
    const teacherView = document.getElementById('teacherView');
    const adminView = document.getElementById('adminView');
    const uploadZone = document.getElementById('uploadZone');
    const fileInput = document.getElementById('fileInput');
    const browseBtn = document.getElementById('browseBtn');
    const fileInfo = document.getElementById('fileInfo');
    const uploadBtn = document.getElementById('uploadBtn');
    const logoutBtn = document.getElementById('logoutBtn');
    const backToSelectionBtn = document.getElementById('backToSelectionBtn');

    // Login functionality
    loginForm.addEventListener('submit', function(e) {
        e.preventDefault();
        const teacherName = document.getElementById('teacherName').value.trim();

        if (teacherName) {
            if (teacherName.toUpperCase() === 'FANITAI') {
                // Admin login
                currentUser = {
                    name: teacherName,
                    isAdmin: true
                };
                
                loginScreen.classList.add('hidden');
                mainApp.classList.remove('hidden');
                userInfo.textContent = 'Admin';
                teacherView.classList.add('hidden');
                adminView.classList.remove('hidden');
                loadAdminView();
            } else {
                // Regular teacher login
                currentUser = {
                    name: teacherName,
                    isAdmin: false
                };
                
                document.getElementById('welcomeText').textContent = `Welcome, ${teacherName}`;
                loginScreen.classList.add('hidden');
                subjectScreen.classList.remove('hidden');
            }
        }
    });

    // School level selection
    document.getElementById('smpBtn').addEventListener('click', function() {
        selectedSchoolLevel = 'smp';
        showSubjectSelection();
    });

    document.getElementById('smkBtn').addEventListener('click', function() {
        selectedSchoolLevel = 'smk';
        showSubjectSelection();
    });

    function showSubjectSelection() {
        const selectionForm = document.getElementById('selectionForm');
        const subjectSelect = document.getElementById('filterSubject');
        const classSelect = document.getElementById('filterClass');
        
        // Clear previous options
        subjectSelect.innerHTML = '<option value="">Pilih Mata Pelajaran</option>';
        classSelect.innerHTML = '<option value="">Pilih Kelas</option>';
        
        // Populate subjects
        schoolData[selectedSchoolLevel].subjects.forEach(subject => {
            const option = document.createElement('option');
            option.value = subject;
            option.textContent = subject;
            subjectSelect.appendChild(option);
        });
        
        // Populate classes
        schoolData[selectedSchoolLevel].classes.forEach(className => {
            const option = document.createElement('option');
            option.value = className;
            option.textContent = className;
            classSelect.appendChild(option);
        });
        
        // Enable both selects
        subjectSelect.disabled = false;
        classSelect.disabled = false;
        
        selectionForm.classList.remove('hidden');
        
        // Update button styles
        document.querySelectorAll('.school-level-btn').forEach(btn => {
            btn.classList.remove('ring-2', 'ring-indigo-500');
        });
        
        if (selectedSchoolLevel === 'smp') {
            document.getElementById('smpBtn').classList.add('ring-2', 'ring-blue-500');
        } else {
            document.getElementById('smkBtn').classList.add('ring-2', 'ring-yellow-500');
        }
    }

    // Back button
    document.getElementById('backBtn').addEventListener('click', function() {
        document.getElementById('selectionForm').classList.add('hidden');
        selectedSchoolLevel = null;
        document.querySelectorAll('.school-level-btn').forEach(btn => {
            btn.classList.remove('ring-2', 'ring-indigo-500', 'ring-blue-500', 'ring-yellow-500');
        });
    });

    // Subject form submission
    subjectForm.addEventListener('submit', function(e) {
        e.preventDefault();
        const subject = document.getElementById('filterSubject').value;
        const className = document.getElementById('filterClass').value;

        if (subject && className) {
            currentUser.subject = subject;
            currentUser.class = className;
            currentUser.schoolLevel = selectedSchoolLevel.toUpperCase();

            subjectScreen.classList.add('hidden');
            mainApp.classList.remove('hidden');
            
            userInfo.textContent = `${currentUser.name} - ${subject} (${className})`;
            adminView.classList.add('hidden');
            teacherView.classList.remove('hidden');
            backToSelectionBtn.classList.remove('hidden');
            loadTeacherFiles();
        }
    });

    // Back to selection functionality
    backToSelectionBtn.addEventListener('click', function() {
        // Reset selection data but keep user name
        const userName = currentUser.name;
        currentUser = {
            name: userName,
            isAdmin: false
        };
        selectedFile = null;
        selectedSchoolLevel = null;
        
        mainApp.classList.add('hidden');
        subjectScreen.classList.remove('hidden');
        document.getElementById('subjectForm').reset();
        document.getElementById('selectionForm').classList.add('hidden');
        backToSelectionBtn.classList.add('hidden');
        
        // Reset school level button styles
        document.querySelectorAll('.school-level-btn').forEach(btn => {
            btn.classList.remove('ring-2', 'ring-indigo-500', 'ring-blue-500', 'ring-yellow-500');
        });
    });

    // Logout functionality
    logoutBtn.addEventListener('click', function() {
        currentUser = null;
        selectedFile = null;
        selectedSchoolLevel = null;
        mainApp.classList.add('hidden');
        subjectScreen.classList.add('hidden');
        loginScreen.classList.remove('hidden');
        document.getElementById('loginForm').reset();
        document.getElementById('subjectForm').reset();
        document.getElementById('selectionForm').classList.add('hidden');
        backToSelectionBtn.classList.add('hidden');
    });

    // File upload functionality
    browseBtn.addEventListener('click', () => fileInput.click());

    fileInput.addEventListener('change', function(e) {
        if (e.target.files.length > 0) {
            handleFileSelect(e.target.files[0]);
        }
    });

    // Drag and drop
    uploadZone.addEventListener('dragover', function(e) {
        e.preventDefault();
        uploadZone.classList.add('dragover');
    });

    uploadZone.addEventListener('dragleave', function(e) {
        e.preventDefault();
        uploadZone.classList.remove('dragover');
    });

    uploadZone.addEventListener('drop', function(e) {
        e.preventDefault();
        uploadZone.classList.remove('dragover');
        if (e.dataTransfer.files.length > 0) {
            handleFileSelect(e.dataTransfer.files[0]);
        }
    });

    function handleFileSelect(file) {
        // Validasi ekstensi file
        if (!file.name.toLowerCase().endsWith('.docx')) {
            showMessage('Hanya file .docx yang diperbolehkan!', 'error');
            return;
        }
        
        // Validasi ukuran file (max 10MB)
        if (file.size > 10 * 1024 * 1024) {
            showMessage('Ukuran file maksimal 10MB!', 'error');
            return;
        }
        
        selectedFile = file;
        document.getElementById('fileName').textContent = file.name;
        document.getElementById('fileSize').textContent = formatFileSize(file.size);
        fileInfo.classList.remove('hidden');
        uploadBtn.disabled = false;
    }

    document.getElementById('removeFile').addEventListener('click', function() {
        selectedFile = null;
        fileInfo.classList.add('hidden');
        uploadBtn.disabled = true;
        fileInput.value = '';
    });

    uploadBtn.addEventListener('click', function() {
        if (selectedFile && currentUser) {
            // Convert file to base64
            const reader = new FileReader();
            reader.onload = function(e) {
                const fileData = {
                    id: Date.now(),
                    name: selectedFile.name,
                    size: selectedFile.size,
                    subject: currentUser.subject,
                    class: currentUser.class,
                    schoolLevel: currentUser.schoolLevel,
                    teacherName: currentUser.name,
                    uploadDate: new Date().toISOString(),
                    teacher: `${currentUser.name} - ${currentUser.subject} (${currentUser.class})`,
                    data: e.target.result // Base64 data
                };

                // Check localStorage size
                const currentSize = JSON.stringify(files).length;
                const newSize = JSON.stringify(fileData).length;
                
                if (currentSize + newSize > 4.5 * 1024 * 1024) { // 4.5MB limit
                    showMessage('Peringatan: Kapasitas penyimpanan hampir penuh! Hapus file lama atau hubungi admin.', 'error');
                    return;
                }

                files.push(fileData);
                localStorage.setItem('examFiles', JSON.stringify(files));

                // Reset form
                selectedFile = null;
                fileInfo.classList.add('hidden');
                uploadBtn.disabled = true;
                fileInput.value = '';

                // Reload files
                loadTeacherFiles();

                // Show success message
                showMessage('File berhasil diupload!', 'success');
            };
            
            reader.onerror = function() {
                showMessage('Gagal membaca file!', 'error');
            };
            
            reader.readAsDataURL(selectedFile);
        }
    });

    function loadTeacherFiles() {
        const myFiles = files.filter(file => 
            file.subject === currentUser.subject && 
            file.class === currentUser.class && 
            file.teacherName === currentUser.name
        );

        const container = document.getElementById('myFiles');
        
        if (myFiles.length === 0) {
            container.innerHTML = '<p class="text-gray-500 text-center py-8">Belum ada file yang diupload</p>';
            return;
        }

        container.innerHTML = myFiles.map(file => `
            <div class="file-item bg-gray-50 rounded-lg p-4 flex items-center justify-between">
                <div class="flex items-center">
                    <svg class="h-8 w-8 text-indigo-600 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                    </svg>
                    <div>
                        <p class="font-medium text-gray-900">${file.name}</p>
                        <p class="text-sm text-gray-500">${formatFileSize(file.size)} • ${formatDate(file.uploadDate)}</p>
                        <p class="text-xs text-indigo-600 mt-1">Format: .docx</p>
                    </div>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="downloadFile(${file.id})" class="bg-green-500 hover:bg-green-600 text-white p-2 rounded-lg transition-colors" title="Unduh File">
                        <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                        </svg>
                    </button>
                    <button onclick="deleteFile(${file.id})" class="bg-red-500 hover:bg-red-600 text-white p-2 rounded-lg transition-colors" title="Hapus File">
                        <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                        </svg>
                    </button>
                </div>
            </div>
        `).join('');
    }

    function loadAdminView() {
        const container = document.getElementById('allFiles');
        const totalFilesSpan = document.getElementById('totalFiles');
        
        
        // Update total files count
        totalFilesSpan.textContent = files.length;

        // Populate filter options
        const classes = [...new Set(files.map(f => f.class))].filter(c => c).sort((a, b) => {
            // Custom sort untuk kelas (VII-A, VIII-B, X-DKV, etc)
            const getClassOrder = (className) => {
                if (className.startsWith('VII')) return 1;
                if (className.startsWith('VIII')) return 2;
                if (className.startsWith('IX')) return 3;
                if (className.startsWith('X-')) return 4;
                if (className.startsWith('XI')) return 5;
                if (className.startsWith('XII')) return 6;
                return 7;
            };
            return getClassOrder(a) - getClassOrder(b) || a.localeCompare(b);
            
        });
        const schoolLevels = [...new Set(files.map(f => f.schoolLevel))].filter(s => s);

        const subjectFilter = document.getElementById('adminFilterSubject');
        const classFilter = document.getElementById('adminFilterClass');

        // Populate class filter
        classFilter.innerHTML = '<option value="">Semua Kelas</option>' +
            classes.map(c => `<option value="${c}">${c}</option>`).join('');

        // Initially disable subject filter
        subjectFilter.innerHTML = '<option value="">-- Pilih Kelas Terlebih Dahulu --</option>';
        subjectFilter.disabled = true;

        // Remove old event listeners if any
        const newSubjectFilter = subjectFilter.cloneNode(true);
        const newClassFilter = classFilter.cloneNode(true);
        subjectFilter.parentNode.replaceChild(newSubjectFilter, subjectFilter);
        classFilter.parentNode.replaceChild(newClassFilter, classFilter);
        
        // Add event listener to class filter to update subject filter
        document.getElementById('adminFilterClass').addEventListener('change', function() {
            const selectedClass = this.value;
            const subjectFilterElement = document.getElementById('adminFilterSubject');
            
            if (selectedClass) {
                // Get subjects that have files in selected class
                const subjectsInClass = [...new Set(
                    files
                        .filter(f => f.class === selectedClass)
                        .map(f => f.subject)
                )].filter(s => s).sort();
                
                subjectFilterElement.innerHTML = '<option value="">Semua Mata Pelajaran</option>' +
                    subjectsInClass.map(s => `<option value="${s}">${s}</option>`).join('');
                
                subjectFilterElement.disabled = false;
            } else {
                // Reset if no class selected
                subjectFilterElement.innerHTML = '<option value="">-- Pilih Kelas Terlebih Dahulu --</option>';
                subjectFilterElement.disabled = true;
            }
            
            // Trigger filter update
            filterFiles();
        });

        // Add filter event listener for subject
        document.getElementById('filterSubject').addEventListener('change', filterFiles);

        displayFiles(files);
    }

    function filterFiles() {
        const subjectFilterElement = document.getElementById('adminFilterSubject');
        const classFilterElement = document.getElementById('adminFilterClass');
        
        const subjectFilter = subjectFilterElement.disabled ? '' : subjectFilterElement.value;
        const classFilter = classFilterElement.value;

        let filteredFiles = files;

        // Apply class filter first
        if (classFilter) {
            filteredFiles = filteredFiles.filter(f => f.class === classFilter);
        }

        // Then apply subject filter
        if (subjectFilter) {
            filteredFiles = filteredFiles.filter(f => f.subject === subjectFilter);
        }

        displayFiles(filteredFiles);
    }

    function displayFiles(filesToShow) {
        const container = document.getElementById('allFiles');
        
        if (filesToShow.length === 0) {
            container.innerHTML = '<p class="text-gray-500 text-center py-8">Tidak ada file yang sesuai filter</p>';
            return;
        }

        container.innerHTML = filesToShow.map(file => `
            <div class="file-item bg-gray-50 rounded-lg p-4 flex items-center justify-between">
                <div class="flex items-center">
                    <svg class="h-8 w-8 text-indigo-600 mr-3" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                    </svg>
                    <div>
                        <p class="font-medium text-gray-900">${file.name}</p>
                        <p class="text-sm text-gray-500">${formatFileSize(file.size)} • ${formatDate(file.uploadDate)}</p>
                        <p class="text-sm text-indigo-600 font-medium">${file.teacher}</p>
                        ${file.schoolLevel ? `<p class="text-xs text-gray-400">${file.schoolLevel}</p>` : ''}
                        <p class="text-xs text-green-600 mt-1">Format: .docx</p>
                    </div>
                </div>
                <div class="flex items-center gap-2">
                    <button onclick="downloadFile(${file.id})" class="bg-green-500 hover:bg-green-600 text-white p-2 rounded-lg transition-colors" title="Unduh File">
                        <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                        </svg>
                    </button>
                    <button onclick="deleteFile(${file.id})" class="bg-red-500 hover:bg-red-600 text-white p-2 rounded-lg transition-colors" title="Hapus File">
                        <svg class="h-5 w-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                        </svg>
                    </button>
                </div>
            </div>
        `).join('');
    }

    function downloadFile(fileId) {
        const file = files.find(f => f.id === fileId);
        
        if (!file) {
            showMessage('File tidak ditemukan!', 'error');
            return;
        }
        
        if (!file.data) {
            showMessage('Data file tidak tersedia untuk diunduh!', 'error');
            return;
        }
        
        try {
            // Convert base64 to blob
            const byteString = atob(file.data.split(',')[1]);
            const mimeString = file.data.split(',')[0].split(':')[1].split(';')[0];
            
            const ab = new ArrayBuffer(byteString.length);
            const ia = new Uint8Array(ab);
            
            for (let i = 0; i < byteString.length; i++) {
                ia[i] = byteString.charCodeAt(i);
            }
            
            const blob = new Blob([ab], { type: mimeString });
            
            // Create download link
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = file.name;
            document.body.appendChild(a);
            a.click();
            
            // Cleanup
            window.URL.revokeObjectURL(url);
            document.body.removeChild(a);
            
            showMessage('File berhasil diunduh!', 'success');
        } catch (error) {
            showMessage('Gagal mengunduh file!', 'error');
            console.error('Download error:', error);
        }
    }

    function deleteFile(fileId) {
        const fileToDelete = files.find(f => f.id === fileId);
        
        if (!fileToDelete) {
            showMessage('File tidak ditemukan!', 'error');
            return;
        }
        
        // Konfirmasi sebelum hapus
        if (!confirm(`Apakah Anda yakin ingin menghapus file "${fileToDelete.name}"?\n\nTindakan ini tidak dapat dibatalkan!`)) {
            return;
        }
        
        files = files.filter(f => f.id !== fileId);
        localStorage.setItem('examFiles', JSON.stringify(files));

        if (currentUser.isAdmin) {
            loadAdminView();
        } else {
            loadTeacherFiles();
        }

        showMessage('File berhasil dihapus!', 'success');
    }

    function formatFileSize(bytes) {
        if (bytes === 0) return '0 Bytes';
        const k = 1024;
        const sizes = ['Bytes', 'KB', 'MB', 'GB'];
        const i = Math.floor(Math.log(bytes) / Math.log(k));
        return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i];
    }

    function formatDate(dateString) {
        const date = new Date(dateString);
        return date.toLocaleDateString('id-ID', {
            year: 'numeric',
            month: 'short',
            day: 'numeric',
            hour: '2-digit',
            minute: '2-digit'
        });
    }

    function showMessage(message, type) {
        const messageDiv = document.createElement('div');
        messageDiv.className = `fixed top-4 right-4 px-6 py-3 rounded-lg text-white font-medium z-50 ${
            type === 'success' ? 'bg-green-500' : 'bg-red-500'
        }`;
        messageDiv.textContent = message;
        
        document.body.appendChild(messageDiv);
        
        setTimeout(() => {
            messageDiv.remove();
        }, 3000);
    }
</script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'994ba86aa2f16d16',t:'MTc2MTQ5OTU3OC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
