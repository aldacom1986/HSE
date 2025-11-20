<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Cotización | Home Support Electric</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
  <style>
    /* ===== VARIABLES DE DISEÑO ===== */
    :root {
      /* Colores corporativos */
      --primary: #1e40af;       /* Azul eléctrico (oscuro) */
      --primary-light: #3b82f6; /* Azul brillante */
      --primary-dark: #1d4ed8;
      --secondary: #0d9488;     /* Verde técnico (opcional para éxitos) */
      --gray-50: #f8fafc;
      --gray-100: #f1f5f9;
      --gray-200: #e2e8f0;
      --gray-300: #cbd5e1;
      --gray-400: #94a3b8;
      --gray-600: #475569;
      --gray-700: #334155;
      --gray-800: #1e293b;
      --gray-900: #0f172a;
      --danger: #ef4444;
      --success: #10b981;

      /* Espaciado modular */
      --space-xs: 0.25rem;
      --space-sm: 0.5rem;
      --space-md: 1rem;
      --space-lg: 1.5rem;
      --space-xl: 2rem;

      /* Tipografía */
      --font-sans: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      --text-base: 0.875rem;
      --text-sm: 0.75rem;
      --text-lg: 1rem;

      /* Sombras */
      --shadow-sm: 0 1px 2px 0 rgba(0, 0, 0, 0.05);
      --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
      --shadow-md: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);

      /* Transiciones */
      --transition: all 0.2s ease-in-out;
    }

    /* ===== RESET Y BASE ===== */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: var(--font-sans);
      background-color: #f9fafb;
      color: var(--gray-800);
      line-height: 1.5;
      padding: var(--space-lg);
    }

    .container {
      max-width: 1100px;
      margin: 0 auto;
      background: white;
      border-radius: 12px;
      box-shadow: var(--shadow-md);
      overflow: hidden;
    }

    /* ===== ENCABEZADO ===== */
    .header {
      display: flex;
      align-items: center;
      gap: var(--space-lg);
      padding: var(--space-lg);
      background: linear-gradient(135deg, var(--primary), var(--primary-dark));
      color: white;
    }

    .logo {
      width: 100px;
      height: 100px;
      border: 2px solid rgba(255, 255, 255, 0.2);
      border-radius: 50%;
      background: white;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .logo img {
      width: 70px;
      height: 70px;
      object-fit: contain;
    }

    .header-content h1 {
      font-weight: 700;
      font-size: 1.75rem;
      margin-bottom: var(--space-xs);
    }

    .header-content p {
      font-weight: 400;
      opacity: 0.9;
      font-size: var(--text-lg);
    }

    /* ===== SECCIONES DE INFO ===== */
    .info-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: var(--space-lg);
      padding: var(--space-lg);
      background-color: var(--gray-50);
      border-bottom: 1px solid var(--gray-200);
    }

    .info-card {
      background: white;
      border-radius: 10px;
      padding: var(--space-md);
      box-shadow: var(--shadow-sm);
      border: 1px solid var(--gray-200);
    }

    .info-card h2 {
      font-size: var(--text-lg);
      font-weight: 600;
      color: var(--primary);
      margin-bottom: var(--space-sm);
      display: flex;
      align-items: center;
      gap: var(--space-xs);
    }

    .info-card h2::before {
      content: "";
      display: inline-block;
      width: 4px;
      height: 16px;
      background: var(--primary);
      border-radius: 2px;
    }

    .info-row {
      display: flex;
      margin-bottom: var(--space-xs);
      font-size: var(--text-sm);
    }

    .info-label {
      font-weight: 600;
      color: var(--gray-700);
      min-width: 90px;
    }

    .info-value {
      flex: 1;
      color: var(--gray-800);
    }

    .info-value input,
    .info-value textarea {
      width: 100%;
      border: none;
      background: transparent;
      font: inherit;
      padding: 2px 0;
      outline: none;
      border-bottom: 1px dashed var(--gray-300);
    }

    .info-value input:focus,
    .info-value textarea:focus {
      border-bottom: 1px solid var(--primary);
      background: rgba(59, 130, 246, 0.05);
    }

    /* ===== TABLA DE PRODUCTOS ===== */
    .section-title {
      padding: var(--space-md) var(--space-lg);
      font-weight: 700;
      color: var(--gray-800);
      font-size: 1.125rem;
      background: white;
      border-bottom: 2px solid var(--primary-light);
    }

    .table-container {
      overflow-x: auto;
      padding: 0 var(--space-lg) var(--space-lg);
    }

    table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0;
      font-size: var(--text-sm);
    }

    thead th {
      background: var(--primary);
      color: white;
      font-weight: 600;
      text-align: left;
      padding: var(--space-sm) var(--space-md);
      position: sticky;
      top: 0;
    }

    tbody tr {
      border-bottom: 1px solid var(--gray-200);
      transition: var(--transition);
    }

    tbody tr:hover {
      background-color: rgba(59, 130, 246, 0.03);
    }

    tbody td {
      padding: var(--space-sm) var(--space-md);
      vertical-align: top;
    }

    /* Inputs en tabla */
    .input-cell {
      width: 100%;
      border: none;
      background: transparent;
      font: inherit;
      padding: 4px 6px;
      border-radius: 4px;
      outline: 2px solid transparent;
      transition: var(--transition);
    }

    .input-cell:focus {
      outline-color: var(--primary-light);
      background: white;
      box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.2);
    }

    /* Textarea autoajustable */
    .desc-cell textarea {
      width: 100%;
      min-height: 50px;
      resize: vertical;
      border: 1px solid var(--gray-200);
      border-radius: 6px;
      padding: 6px 10px;
      font-size: var(--text-sm);
      line-height: 1.4;
    }

    .desc-cell textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 2px rgba(59, 130, 246, 0.2);
    }

    /* Botones en tabla */
    .action-cell {
      text-align: center;
      padding: 8px !important;
    }

    .btn-icon {
      width: 32px;
      height: 32px;
      border-radius: 6px;
      border: none;
      background: var(--gray-100);
      color: var(--gray-600);
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      transition: var(--transition);
    }

    .btn-icon:hover {
      background: var(--danger);
      color: white;
    }

    /* ===== TOTALES ===== */
    .totals-card {
      max-width: 320px;
      margin-left: auto;
      margin-right: var(--space-lg);
      background: white;
      border-radius: 10px;
      box-shadow: var(--shadow);
      border: 1px solid var(--gray-200);
      overflow: hidden;
    }

    .totals-header {
      background: var(--primary-light);
      color: white;
      padding: var(--space-sm) var(--space-md);
      font-weight: 600;
      text-align: center;
    }

    .totals-body {
      padding: var(--space-md);
    }

    .total-row {
      display: flex;
      justify-content: space-between;
      padding: var(--space-xs) 0;
      font-size: var(--text-sm);
    }

    .total-row.total {
      font-weight: 700;
      font-size: 1.125rem;
      color: var(--primary-dark);
      margin-top: var(--space-sm);
      padding-top: var(--space-sm);
      border-top: 2px solid var(--gray-200);
    }

    /* ===== NOTAS ===== */
    .notes-section {
      padding: 0 var(--space-lg) var(--space-lg);
    }

    .notes-section label {
      display: block;
      font-weight: 600;
      margin-bottom: var(--space-xs);
      color: var(--gray-700);
    }

    .notes-section textarea {
      width: 100%;
      min-height: 100px;
      padding: var(--space-md);
      border: 1px solid var(--gray-300);
      border-radius: 8px;
      font: inherit;
      resize: vertical;
      transition: var(--transition);
    }

    .notes-section textarea:focus {
      border-color: var(--primary);
      box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.2);
    }

    /* ===== BOTONES DE ACCIÓN ===== */
    .action-bar {
      display: flex;
      justify-content: center;
      gap: var(--space-md);
      padding: var(--space-lg);
      background: var(--gray-50);
      border-top: 1px solid var(--gray-200);
    }

    .btn {
      display: inline-flex;
      align-items: center;
      gap: var(--space-xs);
      padding: 0.75rem 1.25rem;
      font-weight: 600;
      font-size: var(--text-sm);
      border-radius: 8px;
      border: none;
      cursor: pointer;
      transition: var(--transition);
      box-shadow: var(--shadow-sm);
    }

    .btn-primary {
      background: var(--primary);
      color: white;
    }

    .btn-primary:hover {
      background: var(--primary-dark);
      transform: translateY(-2px);
      box-shadow: var(--shadow);
    }

    .btn-success {
      background: var(--secondary);
      color: white;
    }

    .btn-success:hover {
      background: #0f766e;
      transform: translateY(-2px);
      box-shadow: var(--shadow);
    }

    .btn-outline {
      background: transparent;
      border: 2px solid var(--primary);
      color: var(--primary);
    }

    .btn-outline:hover {
      background: rgba(30, 64, 175, 0.05);
    }

    /* ===== FOOTER ===== */
    .footer-section {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      flex-wrap: wrap;
      gap: var(--space-md);
      padding: var(--space-md) var(--space-lg);
      background: white;
      border-top: 1px solid var(--gray-200);
    }

    .dates-group {
      display: flex;
      gap: var(--space-lg);
    }

    .date-field {
      display: flex;
      flex-direction: column;
    }

    .date-field label {
      font-size: var(--text-sm);
      font-weight: 600;
      color: var(--gray-600);
      margin-bottom: 4px;
    }

    .date-field input {
      width: 160px;
      padding: 8px 12px;
      border: 1px solid var(--gray-300);
      border-radius: 6px;
      font: inherit;
    }

    .signature {
      text-align: right;
    }

    .signature p {
      margin: 4px 0;
      font-size: var(--text-sm);
    }

    .signature p:last-child {
      font-weight: 700;
      color: var(--primary);
    }

    /* ===== BOTÓN AGREGAR ===== */
    .add-row-btn {
      display: flex;
      align-items: center;
      gap: var(--space-xs);
      margin: 0 var(--space-lg) var(--space-lg);
      padding: 0.6rem 1.25rem;
      background: var(--gray-100);
      color: var(--gray-700);
      border: none;
      border-radius: 8px;
      font-weight: 600;
      cursor: pointer;
      transition: var(--transition);
      width: fit-content;
    }

    .add-row-btn:hover {
      background: var(--primary-light);
      color: white;
      transform: scale(1.03);
    }

    /* ===== RESPONSIVE ===== */
    @media (max-width: 768px) {
      .info-grid {
        grid-template-columns: 1fr;
      }

      .header {
        flex-direction: column;
        text-align: center;
      }

      .logo { margin-bottom: var(--space-md); }

      .dates-group {
        flex-direction: column;
        gap: var(--space-sm);
      }

      .date-field input { width: 100%; }

      .totals-card { margin: 0 var(--space-lg) var(--space-lg); }
    }

    /* ===== IMPRESIÓN ===== */
    @media print {
      body { padding: 0; background: white; }
      .container { box-shadow: none; border-radius: 0; }
      .action-bar, .add-row-btn { display: none !important; }

      table {
        font-size: 10pt;
      }

      .desc-cell textarea {
        border: none;
        background: none;
        box-shadow: none;
      }

      .input-cell:focus,
      .desc-cell textarea:focus {
        outline: none;
        box-shadow: none;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Encabezado -->
    <header class="header">
      <div class="logo">
        <img src="https://github.com/aldacom1986/HSE/blob/main/hselogoredondo.png?raw=true" alt="Home Support Electric">
      </div>
      <div class="header-content">
        <h1>Home Support Electric</h1>
        <p>Materiales Eléctricos Residenciales y Comerciales</p>
      </div>
    </header>

    <!-- Información -->
    <section class="info-grid">
      <div class="info-card">
        <h2>INFORMACIÓN DE LA EMPRESA</h2>
        <div class="info-row">
          <span class="info-label">RFC:</span>
          <span class="info-value">RUCJ810917N71</span>
        </div>
        <div class="info-row">
          <span class="info-label">Dirección:</span>
          <span class="info-value">Vista a la Catedral 3001, Cal. Míndico, CP. 45608</span>
        </div>
        <div class="info-row">
          <span class="info-label">Teléfono:</span>
          <span class="info-value">33 1295 8108</span>
        </div>
        <div class="info-row">
          <span class="info-label">WhatsApp:</span>
          <span class="info-value">33 1295 8108</span>
        </div>
        <div class="info-row">
          <span class="info-label">Sitio web:</span>
          <span class="info-value">
            <a href="http://www.homesupportelectric.com" target="_blank" style="color:var(--primary-light); text-decoration:underline;">www.homesupportelectric.com</a>
          </span>
        </div>
      </div>

      <div class="info-card">
        <h2>INFORMACIÓN DEL CLIENTE</h2>
        <div class="info-row">
          <span class="info-label">CLIENTE:</span>
          <span class="info-value"><input type="text" id="cliente" placeholder="[Nombre del Cliente]"></span>
        </div>
        <div class="info-row">
          <span class="info-label">CONTACTO:</span>
          <span class="info-value"><input type="text" id="contacto" placeholder="[Persona de Contacto]"></span>
        </div>
        <div class="info-row">
          <span class="info-label">TELÉFONO:</span>
          <span class="info-value"><input type="text" id="telefono" placeholder="[Número de Teléfono]"></span>
        </div>
        <div class="info-row">
          <span class="info-label">CORREO:</span>
          <span class="info-value"><input type="email" id="correo" placeholder="[Email del Cliente]"></span>
        </div>
      </div>
    </section>

    <!-- Tabla de productos -->
    <h2 class="section-title">DETALLE DE PRODUCTOS/SERVICIOS</h2>

    <div class="table-container">
      <table id="productos">
        <thead>
          <tr>
            <th style="width: 6%">ÍTEM</th>
            <th style="width: 10%">CANTIDAD</th>
            <th style="width: 10%">UNIDAD</th>
            <th style="width: 40%">DESCRIPCIÓN</th>
            <th style="width: 12%">P. UNITARIO</th>
            <th style="width: 12%">IMPORTE</th>
            <th style="width: 10%">ACCIONES</th>
          </tr>
        </thead>
        <tbody id="productos-body">
          <!-- Filas dinámicas -->
        </tbody>
      </table>

      <button class="add-row-btn" onclick="agregarFila()">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <line x1="12" y1="5" x2="12" y2="19"></line>
          <line x1="5" y1="12" x2="19" y2="12"></line>
        </svg>
        Agregar Producto/Servicio
      </button>
    </div>

    <!-- Totales -->
    <div class="totals-card">
      <div class="totals-header">TOTALES</div>
      <div class="totals-body">
        <div class="total-row">
          <span>SUBTOTAL:</span>
          <span id="subtotal">$0.00</span>
        </div>
        <div class="total-row">
          <span><strong>IVA (16%):</strong></span>
          <span id="iva">$0.00</span>
        </div>
        <div class="total-row total">
          <span>TOTAL:</span>
          <span id="total">$0.00</span>
        </div>
      </div>
    </div>

    <!-- Notas -->
    <section class="notes-section">
      <label for="notas">NOTAS, TÉRMINOS Y CONDICIONES:</label>
      <textarea id="notas" placeholder="[Condiciones de pago, entrega, garantía, etc.]"></textarea>
    </section>

    <!-- Botones de exportación -->
    <div class="action-bar">
      <button class="btn btn-success" onclick="exportarPDF()">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
          <polyline points="14 2 14 8 20 8"></polyline>
          <line x1="16" y1="13" x2="8" y2="13"></line>
          <line x1="16" y1="17" x2="8" y2="17"></line>
          <polyline points="10 9 9 9 8 9"></polyline>
        </svg>
        Exportar a PDF
      </button>
      <button class="btn btn-primary" onclick="exportarExcel()">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <path d="M12 2v20M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"></path>
        </svg>
        Exportar a Excel
      </button>
      <button class="btn btn-outline" onclick="guardarCache(); alert('✅ Cotización guardada localmente.')">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor">
          <path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"></path>
          <polyline points="17 21 17 13 7 13 7 21"></polyline>
          <polyline points="7 3 7 8 15 8"></polyline>
        </svg>
        Guardar Borrador
      </button>
    </div>

    <!-- Footer -->
    <footer class="footer-section">
      <div class="dates-group">
        <div class="date-field">
          <label for="fecha-emision">Fecha de Emisión</label>
          <input type="date" id="fecha-emision">
        </div>
        <div class="date-field">
          <label for="fecha-vencimiento">Válido hasta</label>
          <input type="date" id="fecha-vencimiento">
        </div>
      </div>

      <div class="signature">
        <p>Gerente de Ventas</p>
        <p>Home Support Electric</p>
      </div>
    </footer>
  </div>

  <script>
    const { jsPDF } = window.jspdf;

    // Fechas predeterminadas
    const hoy = new Date();
    const hoyStr = hoy.toISOString().split('T')[0];
    const vto = new Date();
    vto.setDate(hoy.getDate() + 30);
    const vtoStr = vto.toISOString().split('T')[0];

    document.getElementById('fecha-emision').value = hoyStr;
    document.getElementById('fecha-vencimiento').value = vtoStr;

    let contador = 1;

    function agregarFila() {
      const tbody = document.getElementById('productos-body');
      const tr = document.createElement('tr');

      tr.innerHTML = `
        <td style="font-weight:600; color:var(--gray-700)">${contador}</td>
        <td><input type="number" min="0" value="1" class="input-cell" oninput="calcularFila(this)"></td>
        <td><input type="text" placeholder="pza, m, kg..." class="input-cell" oninput="guardarCache()"></td>
        <td class="desc-cell"><textarea placeholder="Descripción detallada del producto o servicio..." oninput="guardarCache()"></textarea></td>
        <td><input type="number" min="0" step="0.01" value="0.00" class="input-cell" oninput="calcularFila(this)"></td>
        <td style="font-weight:600; color:var(--primary-dark)">$0.00</td>
        <td class="action-cell">
          <button class="btn-icon" title="Eliminar" onclick="eliminarFila(this)">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor">
              <line x1="18" y1="6" x2="6" y2="18"></line>
              <line x1="6" y1="6" x2="18" y2="18"></line>
            </svg>
          </button>
        </td>
      `;
      tbody.appendChild(tr);
      contador++;
      guardarCache();
    }

    function eliminarFila(btn) {
      const tr = btn.closest('tr');
      tr.remove();
      renumerar();
      calcularTotales();
      guardarCache();
    }

    function renumerar() {
      const filas = document.querySelectorAll('#productos-body tr');
      filas.forEach((tr, i) => {
        tr.cells[0].textContent = i + 1;
      });
      contador = filas.length + 1;
    }

    function calcularFila(input) {
      const tr = input.closest('tr');
      const cant = parseFloat(tr.cells[1].querySelector('input').value) || 0;
      const precio = parseFloat(tr.cells[4].querySelector('input').value) || 0;
      const importe = cant * precio;
      tr.cells[5].textContent = '$' + importe.toFixed(2);
      calcularTotales();
      guardarCache();
    }

    function calcularTotales() {
      let subtotal = 0;
      document.querySelectorAll('#productos-body tr').forEach(tr => {
        const txt = tr.cells[5].textContent.replace('$', '');
        subtotal += parseFloat(txt) || 0;
      });

      const iva = subtotal * 0.16;
      const total = subtotal + iva;

      document.getElementById('subtotal').textContent = '$' + subtotal.toFixed(2);
      document.getElementById('iva').textContent = '$' + iva.toFixed(2);
      document.getElementById('total').textContent = '$' + total.toFixed(2);
    }

    // ✅ Guardado en localStorage
    function guardarCache() {
      const data = {
        cliente: document.getElementById('cliente').value,
        contacto: document.getElementById('contacto').value,
        telefono: document.getElementById('telefono').value,
        correo: document.getElementById('correo').value,
        notas: document.getElementById('notas').value,
        fechaEmision: document.getElementById('fecha-emision').value,
        fechaVencimiento: document.getElementById('fecha-vencimiento').value,
        filas: []
      };

      document.querySelectorAll('#productos-body tr').forEach(tr => {
        const inputs = tr.querySelectorAll('input, textarea');
        data.filas.push({
          cantidad: inputs[0].value,
          unidad: inputs[1].value,
          descripcion: inputs[2].value,
          precio: inputs[3].value
        });
      });

      localStorage.setItem('hse_cotizacion', JSON.stringify(data));
    }

    // Cargar al iniciar
    document.addEventListener('DOMContentLoaded', () => {
      const saved = localStorage.getItem('hse_cotizacion');
      if (saved) {
        const d = JSON.parse(saved);
        document.getElementById('cliente').value = d.cliente || '';
        document.getElementById('contacto').value = d.contacto || '';
        document.getElementById('telefono').value = d.telefono || '';
        document.getElementById('correo').value = d.correo || '';
        document.getElementById('notas').value = d.notas || '';
        document.getElementById('fecha-emision').value = d.fechaEmision || hoyStr;
        document.getElementById('fecha-vencimiento').value = d.fechaVencimiento || vtoStr;

        // Cargar filas
        d.filas.forEach(f => {
          agregarFila();
          const rows = document.querySelectorAll('#productos-body tr');
          const last = rows[rows.length - 1];
          const inps = last.querySelectorAll('input, textarea');
          inps[0].value = f.cantidad;
          inps[1].value = f.unidad;
          inps[2].value = f.descripcion;
          inps[3].value = f.precio;
          calcularFila(inps[3]);
        });
      } else {
        agregarFila(); // iniciar vacío
      }
    });

    // ✅ Exportar a PDF (mejorado con diseño corporativo)
    function exportarPDF() {
      const doc = new jsPDF('p', 'mm', 'a4');
      const pageWidth = doc.internal.pageSize.width;
      const margin = 15;

      // Logo y encabezado
      const logoUrl = "https://github.com/aldacom1986/HSE/blob/main/hselogoredondo.png?raw=true";
      const img = new Image();
      img.crossOrigin = "anonymous";
      img.src = logoUrl;

      img.onload = () => {
        doc.addImage(img, 'PNG', margin, 15, 30, 30, undefined, 'FAST');

        doc.setFont('Inter', 'bold');
        doc.setFontSize(18);
        doc.setTextColor(30, 64, 175);
        doc.text("Home Support Electric", pageWidth / 2, 25, { align: 'center' });

        doc.setFont('Inter', 'normal');
        doc.setFontSize(11);
        doc.setTextColor(80, 80, 80);
        doc.text("Materiales Eléctricos Residenciales y Comerciales", pageWidth / 2, 32, { align: 'center' });

        // Línea divisoria
        doc.setDrawColor(226, 232, 240);
        doc.line(margin, 45, pageWidth - margin, 45);

        // Empresa y Cliente (2 columnas)
        doc.setFontSize(10);
        doc.setTextColor(0, 0, 0);
        doc.setFont('Inter', 'bold');
        doc.text("INFORMACIÓN DE LA EMPRESA", margin, 55);
        doc.setFont('Inter', 'normal');
        doc.text("RFC:", margin, 62); doc.text("RUCJ810917N71", margin + 20, 62);
        doc.text("Dirección:", margin, 67); doc.text("Vista a la Catedral 3001, Cal. Míndico, CP. 45608", margin + 20, 67, { maxWidth: 80 });
        doc.text("Tel/WhatsApp:", margin, 72); doc.text("33 1295 8108", margin + 20, 72);
        doc.text("Web:", margin, 77); doc.text("www.homesupportelectric.com", margin + 20, 77);

        doc.setFont('Inter', 'bold');
        doc.text("INFORMACIÓN DEL CLIENTE", pageWidth / 2 + 5, 55);
        doc.setFont('Inter', 'normal');
        const cliente = document.getElementById('cliente').value || "[Nombre]";
        const contacto = document.getElementById('contacto').value || "[Contacto]";
        const tel = document.getElementById('telefono').value || "[Teléfono]";
        const email = document.getElementById('correo').value || "[Email]";
        doc.text("CLIENTE:", pageWidth / 2 + 5, 62); doc.text(cliente, pageWidth / 2 + 25, 62, { maxWidth: 70 });
        doc.text("CONTACTO:", pageWidth / 2 + 5, 67); doc.text(contacto, pageWidth / 2 + 25, 67, { maxWidth: 70 });
        doc.text("TELÉFONO:", pageWidth / 2 + 5, 72); doc.text(tel, pageWidth / 2 + 25, 72);
        doc.text("CORREO:", pageWidth / 2 + 5, 77); doc.text(email, pageWidth / 2 + 25, 77, { maxWidth: 70 });

        // Tabla
        let y = 90;
        doc.setFont('Inter', 'bold');
        doc.setFontSize(12);
        doc.setTextColor(30, 64, 175);
        doc.text("DETALLE DE PRODUCTOS/SERVICIOS", margin, y);
        y += 10;

        // Cabeceras
        const headers = ["ÍTEM", "CANT", "UNIDAD", "DESCRIPCIÓN", "P. UNIT", "IMPORTE"];
        const colW = [12, 15, 20, 80, 25, 25];
        doc.setFont('Inter', 'bold');
        doc.setFontSize(9);
        doc.setTextColor(255);
        doc.setFillColor(30, 64, 175);
        let x = margin;
        headers.forEach((h, i) => {
          doc.rect(x, y, colW[i], 7, 'F');
          doc.text(h, x + 2, y + 4.5);
          x += colW[i];
        });
        y += 7;

        // Filas
        doc.setFont('Inter', 'normal');
        doc.setFontSize(8);
        doc.setTextColor(0);
        const filas = document.querySelectorAll('#productos-body tr');
        filas.forEach(tr => {
          const celdas = tr.cells;
          const item = celdas[0].textContent;
          const cant = celdas[1].querySelector('input').value;
          const uni = celdas[2].querySelector('input').value;
          const desc = celdas[3].querySelector('textarea').value || "";
          const precio = celdas[4].querySelector('input').value;
          const imp = celdas[5].textContent;

          const descLines = doc.splitTextToSize(desc, 78);
          const h = Math.max(10, descLines.length * 4 + 4);

          doc.setDrawColor(226, 232, 240);
          doc.rect(margin, y, 177, h);
          doc.text(item, margin + 2, y + 6);
          doc.text(cant, margin + 14, y + 6);
          doc.text(uni, margin + 29, y + 6);
          doc.text(descLines, margin + 50, y + 6);
          doc.text(`$${parseFloat(precio).toFixed(2)}`, margin + 132, y + 6);
          doc.text(imp, margin + 158, y + 6);

          y += h;
          if (y > 260) {
            doc.addPage();
            y = 20;
          }
        });

        // Totales
        if (y > 240) { doc.addPage(); y = 20; }
        y += 5;
        doc.setFont('Inter', 'bold');
        doc.setFontSize(10);
        doc.setTextColor(30, 64, 175);

        const subtotal = document.getElementById('subtotal').textContent;
        const iva = document.getElementById('iva').textContent;
        const total = document.getElementById('total').textContent;

        doc.text("SUBTOTAL:", pageWidth - 55, y);
        doc.text(subtotal, pageWidth - 15, y, { align: 'right' });
        y += 6;
        doc.text("IVA (16%):", pageWidth - 55, y);
        doc.text(iva, pageWidth - 15, y, { align: 'right' });
        y += 6;
        doc.setFontSize(12);
        doc.text("TOTAL:", pageWidth - 55, y);
        doc.text(total, pageWidth - 15, y, { align: 'right' });

        // Notas
        y += 10;
        doc.setFont('Inter', 'bold');
        doc.setFontSize(10);
        doc.setTextColor(0);
        doc.text("NOTAS, TÉRMINOS Y CONDICIONES:", margin, y);
        y += 5;
        const notas = document.getElementById('notas').value || "";
        const notasLines = doc.splitTextToSize(notas, 177);
        doc.setFont('Inter', 'normal');
        doc.setFontSize(9);
        doc.text(notasLines, margin, y);

        // Firma
        const fechaEmi = document.getElementById('fecha-emision').value || hoyStr;
        const fechaVto = document.getElementById('fecha-vencimiento').value || vtoStr;
        y = 275;
        doc.setFontSize(9);
        doc.setFont('Inter', 'normal');
        doc.text(`Fecha de Emisión: ${fechaEmi}`, margin, y);
        doc.text(`Válido hasta: ${fechaVto}`, pageWidth / 2, y);
        doc.setFont('Inter', 'bold');
        doc.text("Gerente de Ventas", pageWidth - 60, y - 12);
        doc.setTextColor(30, 64, 175);
        doc.text("Home Support Electric", pageWidth - 60, y);

        doc.save(`Cotizacion_HSE_${new Date().toISOString().slice(0,10)}.pdf`);
      };
    }

    // ✅ Exportar Excel
    function exportarExcel() {
      const data = [
        ["COTIZACIÓN / ORDEN DE COMPRA"],
        ["Home Support Electric — Materiales Eléctricos"],
        [],
        ["INFORMACIÓN DE LA EMPRESA", "", "", "INFORMACIÓN DEL CLIENTE"],
        ["RFC:", "RUCJ810917N71", "", "CLIENTE:", document.getElementById('cliente').value || '[Nombre]'],
        ["Dirección:", "Vista a la Catedral 3001, Cal. Míndico, CP. 45608", "", "CONTACTO:", document.getElementById('contacto').value || '[Persona]'],
        ["Teléfono:", "33 1295 8108", "", "TELÉFONO:", document.getElementById('telefono').value || '[Teléfono]'],
        ["Web:", "www.homesupportelectric.com", "", "CORREO:", document.getElementById('correo').value || '[Email]'],
        [],
        ["ÍTEM", "CANTIDAD", "UNIDAD", "DESCRIPCIÓN", "PRECIO UNITARIO", "IMPORTE"]
      ];

      document.querySelectorAll('#productos-body tr').forEach((tr, i) => {
        const inps = tr.querySelectorAll('input, textarea');
        data.push([
          i + 1,
          inps[0].value,
          inps[1].value,
          inps[2].value,
          parseFloat(inps[3].value) || 0,
          tr.cells[5].textContent.replace('$', '')
        ]);
      });

      data.push([]);
      data.push(["SUBTOTAL", "", "", "", "", document.getElementById('subtotal').textContent.replace('$', '')]);
      data.push(["IVA (16%)", "", "", "", "", document.getElementById('iva').textContent.replace('$', '')]);
      data.push(["TOTAL", "", "", "", "", document.getElementById('total').textContent.replace('$', '')]);
      data.push([]);
      data.push(["NOTAS"]);
      data.push([document.getElementById('notas').value || ""]);

      data.push([]);
      data.push([
        "Fecha Emisión:",
        document.getElementById('fecha-emision').value || hoyStr,
        "",
        "Válido hasta:",
        document.getElementById('fecha-vencimiento').value || vtoStr
      ]);
      data.push(["", "", "", "Gerente de Ventas"]);
      data.push(["", "", "", "Home Support Electric"]);

      const ws = XLSX.utils.aoa_to_sheet(data);
      ws['!cols'] = [{wch:6}, {wch:10}, {wch:12}, {wch:40}, {wch:15}, {wch:15}];
      const wb = XLSX.utils.book_new();
      XLSX.utils.book_append_sheet(wb, ws, "Cotización HSE");
      XLSX.writeFile(wb, `Cotizacion_HSE_${new Date().toISOString().slice(0,10)}.xlsx`);
    }

    // Guardar al escribir
    document.querySelectorAll('input, textarea').forEach(el => {
      el.addEventListener('input', guardarCache);
    });
  </script>
</body>
</html>
