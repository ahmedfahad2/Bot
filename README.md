<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>صيدلي برو بلس - نظام إدارة المستوصفات</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
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
            color: #333;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        .header {
            background: white;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .logo-icon {
            width: 60px;
            height: 60px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 30px;
            color: white;
        }

        .main-layout {
            display: grid;
            grid-template-columns: 250px 1fr 350px;
            gap: 20px;
            height: calc(100vh - 140px);
        }

        .sidebar {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            overflow-y: auto;
        }

        .menu-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 15px;
            margin: 5px 0;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s;
        }

        .menu-item:hover, .menu-item.active {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            transform: translateX(-5px);
        }

        .main-content {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
            overflow-y: auto;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }

        .stat-card {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 25px;
            border-radius: 15px;
            text-align: center;
        }

        .stat-number {
            font-size: 36px;
            font-weight: bold;
            margin: 10px 0;
        }

        .section {
            display: none;
        }

        .section.active {
            display: block;
        }

        .medicine-card {
            background: white;
            border: 1px solid #e0e0e0;
            border-radius: 15px;
            padding: 20px;
            margin: 15px 0;
            transition: all 0.3s;
        }

        .medicine-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }

        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 16px;
        }

        .btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.3s;
            display: inline-flex;
            align-items: center;
            gap: 8px;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
        }

        .right-panel {
            display: flex;
            flex-direction: column;
            gap: 20px;
        }

        .panel-section {
            background: white;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.1);
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            background: white;
            border-radius: 10px;
            padding: 15px 20px;
            margin: 10px 0;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            display: flex;
            align-items: center;
            gap: 15px;
            animation: slideIn 0.3s ease-out;
            z-index: 1000;
        }

        @keyframes slideIn {
            from {
                transform: translateX(100%);
                opacity: 0;
            }
            to {
                transform: translateX(0);
                opacity: 1;
            }
        }

        @media (max-width: 1200px) {
            .main-layout {
                grid-template-columns: 1fr;
                grid-template-rows: auto auto auto;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Header -->
        <div class="header">
            <div class="logo">
                <div class="logo-icon">💊</div>
                <div>
                    <h2>صيدلي برو - نظام المستوصفات</h2>
                    <p>نظام إدارة الأدوية والمخزون</p>
                </div>
            </div>
            <div>
                <div><strong>صيدلية المستقبل</strong></div>
                <div style="font-size: 12px; color: #666;">رخصة: 123456</div>
            </div>
        </div>

        <!-- Main Layout -->
        <div class="main-layout">
            <!-- Sidebar -->
            <div class="sidebar">
                <h3 style="margin-bottom: 20px;">القائمة الرئيسية</h3>
                
                <div class="menu-item active" onclick="showSection('dashboard')">
                    <i class="fas fa-chart-line"></i>
                    <span>لوحة التحكم</span>
                </div>
                
                <div class="menu-item" onclick="showSection('medicines')">
                    <i class="fas fa-pills"></i>
                    <span>إدارة الأدوية</span>
                </div>
                
                <div class="menu-item" onclick="showSection('prescriptions')">
                    <i class="fas fa-prescription"></i>
                    <span>الوصفات الطبية</span>
                </div>
                
                <div class="menu-item" onclick="showSection('inventory')">
                    <i class="fas fa-boxes"></i>
                    <span>المخزون والجرد</span>
                </div>
                
                <div class="menu-item" onclick="showSection('reports')">
                    <i class="fas fa-chart-bar"></i>
                    <span>التقارير</span>
                </div>
            </div>

            <!-- Main Content -->
            <div class="main-content">
                <!-- Dashboard Section -->
                <div id="dashboard" class="section active">
                    <h2 style="margin-bottom: 20px;">📊 لوحة التحكم</h2>
                    
                    <div class="stats-grid">
                        <div class="stat-card">
                            <i class="fas fa-pills" style="font-size: 40px;"></i>
                            <div class="stat-number">847</div>
                            <div>إجمالي الأدوية</div>
                        </div>
                        
                        <div class="stat-card" style="background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);">
                            <i class="fas fa-exclamation-triangle" style="font-size: 40px;"></i>
                            <div class="stat-number">23</div>
                            <div>أدوية منتهية الصلاحية</div>
                        </div>
                        
                        <div class="stat-card" style="background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);">
                            <i class="fas fa-arrow-down" style="font-size: 40px;"></i>
                            <div class="stat-number">67</div>
                            <div>أدوية منخفضة المخزون</div>
                        </div>
                        
                        <div class="stat-card" style="background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%);">
                            <i class="fas fa-dollar-sign" style="font-size: 40px;"></i>
                            <div class="stat-number">45,320</div>
                            <div>إجمالي المبيعات (ريال)</div>
                        </div>
                    </div>

                    <div style="background: #f8f9fa; border-radius: 15px; padding: 20px; margin-top: 20px;">
                        <h3 style="margin-bottom: 15px;">⚡ إجراءات سريعة</h3>
                        <div style="display: flex; gap: 10px; flex-wrap: wrap;">
                            <button class="btn" onclick="addNewMedicine()">
                                <i class="fas fa-plus"></i> إضافة دواء جديد
                            </button>
                            <button class="btn" onclick="newPrescription()">
                                <i class="fas fa-prescription"></i> وصفة جديدة
                            </button>
                            <button class="btn" onclick="checkExpiry()">
                                <i class="fas fa-search"></i> فحص الصلاحية
                            </button>
                            <button class="btn" onclick="generateReport()">
                                <i class="fas fa-file-alt"></i> تقرير سريع
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Medicines Section -->
                <div id="medicines" class="section">
                    <h2 style="margin-bottom: 20px;">💊 إدارة الأدوية</h2>
                    
                    <div class="form-group">
                        <label>الاسم التجاري</label>
                        <input type="text" id="medicineName" placeholder="أدخل اسم الدواء">
                    </div>
                    
                    <div class="form-group">
                        <label>النوع</label>
                        <select id="medicineType">
                            <option value="">اختر النوع</option>
                            <option value="مسكن">مسكن</option>
                            <option value="مضاد حيوي">مضاد حيوي</option>
                            <option value="فيتامين">فيتامين</option>
                            <option value="مضاد الهيستامين">مضاد الهيستامين</option>
                        </select>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
                        <div class="form-group">
                            <label>الجرعة</label>
                            <input type="text" id="dosage" placeholder="مثال: 500 ملغ">
                        </div>
                        <div class="form-group">
                            <label>الكمية</label>
                            <input type="number" id="quantity" placeholder="العدد">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>سعر البيع</label>
                        <input type="number" id="price" placeholder="السعر بالريال">
                    </div>
                    
                    <button class="btn" onclick="saveMedicine()">
                        <i class="fas fa-save"></i> حفظ الدواء
                    </button>
                    
                    <div id="medicineList" style="margin-top: 30px;">
                        <!-- سيتم ملؤها بالأدوية -->
                    </div>
                </div>

                <!-- Prescriptions Section -->
                <div id="prescriptions" class="section">
                    <h2 style="margin-bottom: 20px;">📝 الوصفات الطبية</h2>
                    
                    <div class="form-group">
                        <label>اسم المريض</label>
                        <input type="text" id="patientName" placeholder="أدخل اسم المريض الكامل">
                    </div>
                    
                    <div class="form-group">
                        <label>الدواء</label>
                        <input type="text" id="prescriptionMedicine" placeholder="اسم الدواء">
                    </div>
                    
                    <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px;">
                        <div class="form-group">
                            <label>الجرعة</label>
                            <input type="text" id="prescriptionDosage" placeholder="مثال: 500 ملغ">
                        </div>
                        <div class="form-group">
                            <label>عدد المرات</label>
                            <input type="text" id="frequency" placeholder="مثال: 3 مرات يومياً">
                        </div>
                        <div class="form-group">
                            <label>المدة</label>
                            <input type="text" id="duration" placeholder="مثال: 7 أيام">
                        </div>
                    </div>
                    
                    <div class="form-group">
                        <label>ملاحظات</label>
                        <textarea id="notes" rows="3" placeholder="أي ملاحظات إضافية..."></textarea>
                    </div>
                    
                    <button class="btn" onclick="savePrescription()">
                        <i class="fas fa-save"></i> حفظ الوصفة
                    </button>
                    
                    <div id="prescriptionList" style="margin-top: 30px;">
                        <!-- سيتم ملؤها بالوصفات -->
                    </div>
                </div>

                <!-- Inventory Section -->
                <div id="inventory" class="section">
                    <h2 style="margin-bottom: 20px;">📦 المخزون والجرد</h2>
                    
                    <div style="background: #f8f9fa; padding: 20px; border-radius: 15px; margin-bottom: 20px;">
                        <h3>حالة المخزون الحالية</h3>
                        <div id="inventoryStatus">
                            <!-- سيتم ملؤها بالبيانات -->
                        </div>
                    </div>
                    
                    <button class="btn" onclick="generateInventoryReport()">
                        <i class="fas fa-file-alt"></i> إنشاء تقرير جرد
                    </button>
                    
                    <button class="btn" onclick="exportInventory()" style="margin-right: 10px;">
                        <i class="fas fa-download"></i> تصدير البيانات
                    </button>
                </div>

                <!-- Reports Section -->
                <div id="reports" class="section">
                    <h2 style="margin-bottom: 20px;">📊 التقارير</h2>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;">
                        <div style="background: #f8f9fa; padding: 20px; border-radius: 15px;">
                            <h4>تقرير المبيعات</h4>
                            <button class="btn" onclick="generateSalesReport()" style="width: 100%; margin-top: 10px;">
                                إنشاء تقرير المبيعات
                            </button>
                        </div>
                        
                        <div style="background: #f8f9fa; padding: 20px; border-radius: 15px;">
                            <h4>تقرير الأدوية المنتهية</h4>
                            <button class="btn" onclick="generateExpiryReport()" style="width: 100%; margin-top: 10px;">
                                إنشاء تقرير الصلاحية
                            </button>
                        </div>
                        
                        <div style="background: #f8f9fa; padding: 20px; border-radius: 15px;">
                            <h4>تقرير المخزون</h4>
                            <button class="btn" onclick="generateStockReport()" style="width: 100%; margin-top: 10px;">
                                إنشاء تقرير المخزون
                            </button>
                        </div>
                        
                        <div style="background: #f8f9fa; padding: 20px; border-radius: 15px;">
                            <h4>تقرير شامل</h4>
                            <button class="btn" onclick="generateComprehensiveReport()" style="width: 100%; margin-top: 10px;">
                                إنشاء تقرير شامل
                            </button>
                        </div>
                    </div>
                    
                    <div id="reportResults" style="margin-top: 30px;">
                        <!-- سيتم عرض النتائج هنا -->
                    </div>
                </div>
            </div>

            <!-- Right Panel -->
            <div class="right-panel">
                <!-- Alerts -->
                <div class="panel-section">
                    <h3 style="margin-bottom: 15px;">
                        <i class="fas fa-bell"></i> التنبيهات
                    </h3>
                    <div id="alertsContainer">
                        <div style="background: rgba(255, 193, 7, 0.1); padding: 10px; border-radius: 8px; margin: 10px 0; border-right: 4px solid #ffc107;">
                            <strong>تنبيه:</strong> ارتفاع في مبيعات أدوية الحساسية
                        </div>
                        <div style="background: rgba(220, 53, 69, 0.1); padding: 10px; border-radius: 8px; margin: 10px 0; border-right: 4px solid #dc3545;">
                            <strong>عاجل:</strong> انتهاء صلاحية 15 دواء خلال الأسبوع القادم
                        </div>
                        <div style="background: rgba(40, 167, 69, 0.1); padding: 10px; border-radius: 8px; margin: 10px 0; border-right: 4px solid #28a745;">
                            <strong>فرصة:</strong> خصم 20% على طلبيات الأدوية الموسمية
                        </div>
                    </div>
                </div>

                <!-- Quick Stats -->
                <div class="panel-section">
                    <h3 style="margin-bottom: 15px;">
                        <i class="fas fa-chart-pie"></i> إحصائيات سريعة
                    </h3>
                    <div style="font-size: 14px;">
                        <div style="display: flex; justify-content: space-between; margin: 10px 0;">
                            <span>الأدوية المباعة اليوم:</span>
                            <strong>156 دواء</strong>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin: 10px 0;">
                            <span>الوصفات الصادرة:</span>
                            <strong>42 وصفة</strong>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin: 10px 0;">
                            <span>المراجعين:</span>
                            <strong>67 مريض</strong>
                        </div>
                        <div style="display: flex; justify-content: space-between; margin: 10px 0;">
                            <span>المخزون الكلي:</span>
                            <strong>847 عنصر</strong>
                        </div>
                    </div>
                </div>

                <!-- Expiry Tracker -->
                <div class="panel-section">
                    <h3 style="margin-bottom: 15px;">
                        <i class="fas fa-calendar-times"></i> تتبع انتهاء الصلاحية
                    </h3>
                    <div id="expiryTracker">
                        <div style="background: rgba(255, 71, 87, 0.1); padding: 10px; border-radius: 8px; margin: 10px 0;">
                            <div style="font-weight: bold; color: #ff4757;">ينتهي خلال 3 أيام</div>
                            <div style="font-size: 14px;">أسبرين 100 ملغ - 25 علبة</div>
                        </div>
                        <div style="background: rgba(255, 165, 2, 0.1); padding: 10px; border-radius: 8px; margin: 10px 0;">
                            <div style="font-weight: bold; color: #ffa502;">ينتهي خلال أسبوع</div>
                            <div style="font-size: 14px;">فيتامين C - 40 علبة</div>
                        </div>
                        <div style="background: rgba(46, 213, 115, 0.1); padding: 10px; border-radius: 8px; margin: 10px 0;">
                            <div style="font-weight: bold; color: #2ed573;">ينتهي خلال شهر</div>
                            <div style="font-size: 14px;">مضاد حيوي - 120 علبة</div>
                        </div>
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="panel-section">
                    <button class="btn" style="width: 100%; margin-bottom: 10px;">
                        <i class="fas fa-print"></i> طباعة تقرير اليومية
                    </button>
                    <button class="btn" style="width: 100%; margin-bottom: 10px;">
                        <i class="fas fa-download"></i> تصدير البيانات
                    </button>
                    <button class="btn" style="width: 100%; background: #dc3545;">
                        <i class="fas fa-phone"></i> استدعاء الدعم الفني
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // قاعدة البيانات المحلية
        let medicines = [
            {
                id: 1,
                name: "باراسيتامول",
                type: "مسكن",
                dosage: "500 ملغ",
                quantity: 150,
                expiryDate: "2024-12-15",
                price: 15.50
            },
            {
                id: 2,
                name: "أموكسيسيلين",
                type: "مضاد حيوي",
                dosage: "500 ملغ",
                quantity: 45,
                expiryDate: "2024-10-30",
                price: 25.00
            },
            {
                id: 3,
                name: "أسبرين",
                type: "مميع دم",
                dosage: "100 ملغ",
                quantity: 25,
                expiryDate: "2024-09-10",
                price: 12.00
            }
        ];

        let prescriptions = [];

        // عرض الأقسام
        function showSection(sectionName) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            
            document.getElementById(sectionName).classList.add('active');
            
            document.querySelectorAll('.menu-item').forEach(item => {
                item.classList.remove('active');
            });
            event.target.closest('.menu-item').classList.add('active');
            
            if (sectionName === 'medicines') {
                displayMedicines();
            } else if (sectionName === 'prescriptions') {
                displayPrescriptions();
            } else if (sectionName === 'inventory') {
                displayInventory();
            }
        }

        // عرض الأدوية
        function displayMedicines() {
            const list = document.getElementById('medicineList');
            list.innerHTML = '<h3>قائمة الأدوية</h3>';
            
            medicines.forEach(medicine => {
                const daysToExpiry = Math.ceil((new Date(medicine.expiryDate) - new Date()) / (1000 * 60 * 60 * 24));
                const stockLevel = medicine.quantity > 50 ? 'كافي' : medicine.quantity > 20 ? 'متوسط' : 'منخفض';
                
                const card = document.createElement('div');
                card.className = 'medicine-card';
                card.innerHTML = `
                    <h4>${medicine.name}</h4>
                    <p><strong>النوع:</strong> ${medicine.type}</p>
                    <p><strong>الجرعة:</strong> ${medicine.dosage}</p>
                    <p><strong>الكمية:</strong> ${medicine.quantity} علبة</p>
                    <p><strong>السعر:</strong> ${medicine.price} ريال</p>
                    <p><strong>ينتهي خلال:</strong> ${daysToExpiry} يوم</p>
                    <p><strong>حالة المخزون:</strong> ${stockLevel}</p>
                    <div style="margin-top: 10px;">
                        <button class="btn" onclick="editMedicine(${medicine.id})">
                            <i class="fas fa-edit"></i> تعديل
                        </button>
                        <button class="btn" onclick="sellMedicine(${medicine.id})">
                            <i class="fas fa-shopping-cart"></i> بيع
                        </button>
                    </div>
                `;
                list.appendChild(card);
            });
        }

        // حفظ دواء جديد
        function saveMedicine() {
            const name = document.getElementById('medicineName').value;
            const type = document.getElementById('medicineType').value;
            const dosage = document.getElementById('dosage').value;
            const quantity = parseInt(document.getElementById('quantity').value);
            const price = parseFloat(document.getElementById('price').value);
            
            if (!name || !type || !dosage || !quantity || !price) {
                showNotification('يرجى ملء جميع الحقول', 'error');
                return;
            }
            
            const newMedicine = {
                id: medicines.length + 1,
                name,
                type,
                dosage,
                quantity,
                expiryDate: new Date(Date.now() + 365 * 24 * 60 * 60 * 1000).toISOString().split('T')[0],
                price
            };
            
            medicines.push(newMedicine);
            displayMedicines();
            
            // مسح الحقول
            document.getElementById('medicineName').value = '';
            document.getElementById('medicineType').value = '';
            document.getElementById('dosage').value = '';
            document.getElementById('quantity').value = '';
            document.getElementById('price').value = '';
            
            showNotification('تم حفظ الدواء بنجاح', 'success');
        }

        // بيع دواء
        function sellMedicine(id) {
            const medicine = medicines.find(m => m.id === id);
            if (medicine.quantity > 0) {
                medicine.quantity--;
                displayMedicines();
                showNotification(`تم بيع ${medicine.name} بنجاح`, 'success');
            } else {
                showNotification('الدواء غير متوفر في المخزون', 'error');
            }
        }

        // عرض الوصفات
        function displayPrescriptions() {
            const list = document.getElementById('prescriptionList');
            list.innerHTML = '<h3>الوصفات الطبية</h3>';
            
            prescriptions.forEach(prescription => {
                const card = document.createElement('div');
                card.className = 'medicine-card';
                card.innerHTML = `
                    <h4>مريض: ${prescription.patientName}</h4>
                    <p><strong>الدواء:</strong> ${prescription.medicine}</p>
                    <p><strong>الجرعة:</strong> ${prescription.dosage}</p>
                    <p><strong>عدد المرات:</strong> ${prescription.frequency}</p>
                    <p><strong>المدة:</strong> ${prescription.duration}</p>
                    <p><strong>التاريخ:</strong> ${prescription.date}</p>
                    ${prescription.notes ? `<p><strong>ملاحظات:</strong> ${prescription.notes}</p>` : ''}
                    <div style="margin-top: 10px;">
                        <button class="btn" onclick="printPrescription(${prescription.id})">
                            <i class="fas fa-print"></i> طباعة
                        </button>
                    </div>
                `;
                list.appendChild(card);
            });
        }

        // حفظ وصفة
        function savePrescription() {
            const patientName = document.getElementById('patientName').value;
            const medicine = document.getElementById('prescriptionMedicine').value;
            const dosage = document.getElementById('prescriptionDosage').value;
            const frequency = document.getElementById('frequency').value;
            const duration = document.getElementById('duration').value;
            const notes = document.getElementById('notes').value;
            
            if (!patientName || !medicine) {
                showNotification('يرجى إدخال اسم المريض واسم الدواء', 'error');
                return;
            }
            
            const newPrescription = {
                id: prescriptions.length + 1,
                patientName,
                medicine,
                dosage,
                frequency,
                duration,
                notes,
                date: new Date().toLocaleDateString('ar-EG')
            };
            
            prescriptions.push(newPrescription);
            displayPrescriptions();
            
            // مسح الحقول
            document.getElementById('patientName').value = '';
            document.getElementById('prescriptionMedicine').value = '';
            document.getElementById('prescriptionDosage').value = '';
            document.getElementById('frequency').value = '';
            document.getElementById('duration').value = '';
            document.getElementById('notes').value = '';
            
            showNotification('تم حفظ الوصفة بنجاح', 'success');
        }

        // عرض المخزون
        function displayInventory() {
            const status = document.getElementById('inventoryStatus');
            status.innerHTML = '';
            
            let totalValue = 0;
            let lowStockCount = 0;
            let expiredCount = 0;
            const today = new Date();
            
            medicines.forEach(medicine => {
                const value = medicine.quantity * medicine.price;
                totalValue += value;
                
                if (medicine.quantity < 20) lowStockCount++;
                
                const expiryDate = new Date(medicine.expiryDate);
                if (expiryDate < today) expiredCount++;
                
                const stockLevel = medicine.quantity > 50 ? 'كافي' : medicine.quantity > 20 ? 'متوسط' : 'منخفض';
                const expiryDays = Math.ceil((expiryDate - today) / (1000 * 60 * 60 * 24));
                
                status.innerHTML += `
                    <div style="background: white; padding: 15px; border-radius: 8px; margin: 10px 0; border-left: 4px solid ${medicine.quantity < 20 ? '#dc3545' : '#28a745'};">
                        <h4>${medicine.name}</h4>
                        <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 10px;">
                            <div>الكمية: ${medicine.quantity} علبة</div>
                            <div>القيمة: ${value.toFixed(2)} ريال</div>
                            <div>حالة المخزون: ${stockLevel}</div>
                            <div>الصلاحية: ${expiryDays} يوم</div>
                        </div>
                    </div>
                `;
            });
            
            status.innerHTML += `
                <div style="background: #f8f9fa; padding: 15px; border-radius: 8px; margin-top: 20px;">
                    <h4>ملخص المخزون</h4>
                    <p>القيمة الإجمالية: ${totalValue.toFixed(2)} ريال</p>
                    <p>الأدوية منخفضة المخزون: ${lowStockCount}</p>
                    <p>الأدوية المنتهية: ${expiredCount}</p>
                </div>
            `;
        }

        // إنشاء تقارير
        function generateSalesReport() {
            const reportResults = document.getElementById('reportResults');
            reportResults.innerHTML = `
                <div style="background: white; padding: 20px; border-radius: 15px; margin-top: 20px;">
                    <h3>تقرير المبيعات</h3>
                    <p><strong>الفترة:</strong> آخر 30 يوم</p>
                    <p><strong>إجمالي المبيعات:</strong> 45,320 ريال</p>
                    <p><strong>عدد المعاملات:</strong> 234 معاملة</p>
                    <p><strong>أكثر الأدوية مبيعاً:</strong> باراسيتامول</p>
                    <button class="btn" onclick="printReport('sales')">
                        <i class="fas fa-print"></i> طباعة التقرير
                    </button>
                </div>
            `;
            showNotification('تم إنشاء تقرير المبيعات', 'success');
        }

        function generateExpiryReport() {
            const reportResults = document.getElementById('reportResults');
            reportResults.innerHTML = `
                <div style="background: white; padding: 20px; border-radius: 15px; margin-top: 20px;">
                    <h3>تقرير انتهاء الصلاحية</h3>
                    <p><strong>الأدوية المنتهية خلال 30 يوم:</strong> 23 دواء</p>
                    <p><strong>القيمة التقديرية:</strong> 2,340 ريال</p>
                    <p><strong>أولوية التصرف:</strong> عالية</p>
                    <button class="btn" onclick="printReport('expiry')">
                        <i class="fas fa-print"></i> طباعة التقرير
                    </button>
                </div>
            `;
            showNotification('تم إنشاء تقرير الصلاحية', 'success');
        }

        function generateStockReport() {
            const reportResults = document.getElementById('reportResults');
            reportResults.innerHTML = `
                <div style="background: white; padding: 20px; border-radius: 15px; margin-top: 20px;">
                    <h3>تقرير المخزون</h3>
                    <p><strong>إجمالي الأصناف:</strong> ${medicines.length} دواء</p>
                    <p><strong>الأدوية منخفضة المخزون:</strong> 67 دواء</p>
                    <p><strong>القيمة التقديرية:</strong> 89,432 ريال</p>
                    <button class="btn" onclick="printReport('stock')">
                        <i class="fas fa-print"></i> طباعة التقرير
                    </button>
                </div>
            `;
            showNotification('تم إنشاء تقرير المخزون', 'success');
        }

        function generateComprehensiveReport() {
            const reportResults = document.getElementById('reportResults');
            reportResults.innerHTML = `
                <div style="background: white; padding: 20px; border-radius: 15px; margin-top: 20px;">
                    <h3>التقرير الشامل</h3>
                    <p><strong>الفترة:</strong> الربع الأول 2024</p>
                    <p><strong>إجمالي المبيعات:</strong> 135,960 ريال</p>
                    <p><strong>عدد الوصفات:</strong> 1,248 وصفة</p>
                    <p><strong>نسبة النمو:</strong> +12.5%</p>
                    <button class="btn" onclick="printReport('comprehensive')">
                        <i class="fas fa-print"></i> طباعة التقرير
                    </button>
                </div>
            `;
            showNotification('تم إنشاء التقرير الشامل', 'success');
        }

        // دوال مساعدة
        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = 'notification';
            notification.style.background = type === 'success' ? '#d4edda' : type === 'error' ? '#f8d7da' : '#d1ecf1';
            notification.style.borderLeft = `4px solid ${type === 'success' ? '#28a745' : type === 'error' ? '#dc3545' : '#17a2b8'}`;
            
            notification.innerHTML = `
                <i class="fas fa-${type === 'success' ? 'check-circle' : type === 'error' ? 'exclamation-circle' : 'info-circle'}"></i>
                <div>
                    <strong>${type === 'success' ? 'نجاح' : type === 'error' ? 'خطأ' : 'معلومات'}</strong>
                    <div style="font-size: 12px;">${message}</div>
                </div>
            `;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.remove();
            }, 3000);
        }

        function printReport(type) {
            showNotification(`جاري طباعة تقرير ${type}...`, 'info');
            setTimeout(() => {
                showNotification('تم إرسال التقرير للطباعة', 'success');
            }, 1000);
        }

        function exportInventory() {
            showNotification('جاري تصدير بيانات المخزون...', 'info');
            
            // إنشاء ملف CSV
            let csv = 'اسم الدواء,النوع,الجرعة,الكمية,سعر البيع,تاريخ الانتهاء\n';
            medicines.forEach(medicine => {
                csv += `${medicine.name},${medicine.type},${medicine.dosage},${medicine.quantity},${medicine.price},${medicine.expiryDate}\n`;
            });
            
            // إنشاء رابط تحميل
            const blob = new Blob([csv], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', 'inventory_report.csv');
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            showNotification('تم تصدير البيانات بنجاح', 'success');
        }

        function checkExpiry() {
            showNotification('جاري فحص تواريخ الصلاحية...', 'info');
            
            const today = new Date();
            const expiredMedicines = medicines.filter(medicine => {
                const expiryDate = new Date(medicine.expiryDate);
                return expiryDate < today;
            });
            
            if (expiredMedicines.length > 0) {
                showNotification(`تم العثور على ${expiredMedicines.length} أدوية منتهية الصلاحية`, 'error');
            } else {
                showNotification('لا توجد أدوية منتهية الصلاحية', 'success');
            }
        }

        function addNewMedicine() {
            showSection('medicines');
            showNotification('يمكنك الآن إضافة دواء جديد', 'info');
        }

        function newPrescription() {
            showSection('prescriptions');
            showNotification('يمكنك الآن إنشاء وصفة جديدة', 'info');
        }

        function generateInventoryReport() {
            displayInventory();
            showNotification('تم إنشاء تقرير الجرد', 'success');
        }

        // التهيئة الأولية
        document.addEventListener('DOMContentLoaded', function() {
            // عرض لوحة التحكم افتراضياً
            showSection('dashboard');
            
            // إشعار ترحيبي
            setTimeout(() => {
                showNotification('مرحباً بك في نظام صيدلي برو', 'success');
            }, 1000);
            
            // تحديث تلقائي للإحصائيات
            setInterval(() => {
                // محاكاة تحديث الأرقام
                const stats = document.querySelectorAll('.stat-number');
                stats.forEach(stat => {
                    const current = parseInt(stat.textContent.replace(/,/g, ''));
                    const change = Math.floor(Math.random() * 10) - 5;
                    const newValue = Math.max(0, current + change);
                    stat.textContent = newValue.toLocaleString('ar-EG');
                });
            }, 5000);
        });
    </script>
</body>
</html>
