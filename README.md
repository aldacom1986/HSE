# HSE
cotizador
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>
  <title>Orden de Compra - Materiales Eléctricos</title>
  <script src="https://cdn.jsdelivr.net/npm/xlsx@0.18.5/dist/xlsx.full.min.js"></script>
  <style>
    :root {
      --primary: #1a3a6c;
      --secondary: #2c5282;
      --accent: #e63946;
      --light: #f8f9fa;
      --dark: #212529;
      --gray: #6c757d;
      --border: #dee2e6;
      --success: #28a745;
      --info: #17a2b8;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', system-ui, sans-serif;
    }

    body {
      background: #f0f4f8;
      padding: 12px;
      color: var(--dark);
      line-height: 1.5;
    }

    .document {
      max-width: 950px;
      margin: 0 auto;
      background: white;
      border-radius: 14px;
      overflow: hidden;
      box-shadow: 0 8px 25px rgba(0,0,0,0.1);
      border: 1px solid #eaeef5;
    }

    .header {
      background: linear-gradient(135deg, var(--primary), var(--secondary));
      color: white;
      padding: 20px;
      text-align: center;
    }

    .header img {
      max-height: 70px;
      margin-bottom: 10px;
      object-fit: contain;
    }

    .header h1 {
      font-size: 20px;
      font-weight: 600;
      letter-spacing: 0.5px;
    }

    .dual-section {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 20px;
      padding: 20px;
      border-bottom: 1px solid #f1f3f5;
    }

    .section-block h3 {
      font-size: 15px;
      font-weight: 700;
      color: var(--secondary);
      margin-bottom: 12px;
      padding-bottom: 5px;
      border-bottom: 2px solid var(--primary);
    }

    .field-group {
      display: flex;
      flex-direction: column;
      margin-bottom: 12px;
    }

    .field-group label {
      font-size: 13px;
      font-weight: 600;
      color: var(--gray);
      margin-bottom: 4px;
    }

    .field-group input, .field-group textarea {
      padding: 9px 12px;
      border: 1px solid var(--border);
      border-radius: 6px;
      font-size: 14px;
      background: #fdfdfd;
    }

    textarea.auto-resize {
      min-height: 44px;
      resize: none;
      overflow: hidden;
      padding: 10px 12px;
      font-family: inherit;
      font-size: 14px;
      width: 100%;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      margin: 20px;
      font-size: 14px;
    }

    th {
      background-color: #f1f5f9;
      color: var(--primary);
      padding: 10px;
      text-align: center;
      font-weight: 600;
      border: 1px solid #e2e8f0;
    }

    td {
      padding: 12px 8px;
      text-align: center;
      border: 1px solid #e2e8f0;
      vertical-align: top;
    }

    td input {
      width: 100%;
      padding: 6px 8px;
      border: 1px solid #cbd5e1;
      border-radius: 4px;
      font-size: 14px;
      text-align: center;
    }

    .descripcion-cell {
      text-align: left;
      padding: 8px;
    }

    .btn-group {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      padding: 0 20px 20px;
    }

    .btn {
      padding: 10px 16px;
      border: none;
      border-radius: 6px;
      font-weight: 600;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      font-size: 14px;
      transition: all 0.2s;
      justify-content: center;
    }

    .btn-add { background: var(--primary); color: white; }
    .btn-remove { background: var(--accent); color: white; padding: 6px 10px; font-size: 12px; }
    .btn-print { background: var(--success); color: white; }
    .btn-excel { background: #ffc107; color: var(--dark); }
    .btn-email { background: var(--info); color: white; }

    .totals-section {
      padding: 0 20px 20px;
    }

    .totals-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 12px;
      margin-top: 10px;
      font-size: 16px;
    }

    .total-row {
      display: flex;
      justify-content: space-between;
      padding: 8px 0;
      font-weight: 600;
    }

    .total-row.total {
      color: var(--success);
      font-size: 18px;
    }

    .notes-section, .signature-section, .dates-section {
      padding: 0 20px 20px;
    }

    .signature {
      text-align: center;
      font-weight: 600;
      color: var(--primary);
      margin-top: 10px;
    }

    .dates-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 15px;
      margin-top: 10px;
    }

    @media (max-width: 768px) {
      .dual-section { grid-template-columns: 1fr; }
      .btn-group { flex-direction: column; }
      .dates-grid { grid-template-columns: 1fr; }
      input, textarea { font-size: 16px; }
    }

    @media print {
      .btn-group { display: none !important; }
      body { background: white; padding: 0; }
      .document { box-shadow: none; border: none; }
    }
  </style>
</head>
<body>

<div class="document" id="orden-compra">
  <div class="header">
    <!-- ✅ Logo oficial del Colegio Cervantes (público y funcional) -->
    <img src="https://ccpgdl.edu.mx/wp-content/uploads/2022/09/colegio-cervantes-primaria-logo-2.png" alt="Colegio Cervantes">
    <h1>Materiales Eléctricos Residenciales y Comerciales</h1>
  </div>

  <div class="dual-section">
    <div class="section-block">
      <h3>INFORMACIÓN DE LA EMPRESA</h3>
      <div class="field-group"><label>RFC</label> <input type="text" value="RUCJ810917N71" readonly></div>
      <div class="field-group"><label>Dirección</label> <input type="text" value="Vista a la Catedral 3001, Col. Mirador del tesoro, CP. 45608" readonly></div>
      <div class="field-group"><label>Teléfono y WhatsApp</label> <input type="text" value="3312958108" readonly></div>
      <div class="field-group"><label>Sitio web</label> <input type="text" value="www.homesupportelectric.com" readonly></div>
    </div>

    <div class="section-block">
      <h3>INFORMACIÓN DEL CLIENTE</h3>
      <div class="field-group"><label>CLIENTE</label> <input type="text" id="cliente" placeholder="Nombre del Cliente" oninput="guardarEnCache()"></div>
      <div class="field-group"><label>CONTACTO</label> <input type="text" id="contacto" placeholder="Persona de Contacto" oninput="guardarEnCache()"></div>
      <div class="field-group"><label>TELÉFONO</label> <input type="text" id="telefono" placeholder="Número de Teléfono" oninput="guardarEnCache()"></div>
      <div class="field-group"><label>CORREO</label> <input type="email" id="correo" placeholder="Email del Cliente" oninput="guardarEnCache()"></div>
    </div>
  </div>

  <table id="tabla-productos">
    <thead>
      <tr>
        <th>Ítem</th>
        <th>Cant.</th>
        <th>Unidad</th>
        <th>Descripción del Producto/Servicio</th>
        <th>P. Unitario</th>
        <th>Importe</th>
        <th>Acción</th>
      </tr>
    </thead>
    <tbody id="cuerpo-productos"></tbody>
  </table>

  <div class="btn-group">
    <button class="btn btn-add" onclick="agregarFila()">➕ Agregar Ítem</button>
    <button class="btn btn-print" onclick="imprimirPDF()">🖨️ Guardar PDF</button>
    <button class="btn btn-excel" onclick="exportarExcel()">📊 Exportar Excel</button>
    <button class="btn btn-email" onclick="enviarCorreo()">✉️ Enviar por Correo</button>
  </div>

  <div class="totals-section">
    <div class="totals-grid">
      <div class="total-row"><span>SUBTOTAL:</span> <span id="subtotal">$0.00</span></div>
      <div class="total-row"><span>IVA (16%):</span> <span id="iva">$0.00</span></div>
      <div class="total-row total"><span>TOTAL:</span> <span id="total">$0.00</span></div>
    </div>
  </div>

  <div class="notes-section">
    <div class="field-group">
      <label>NOTAS, TÉRMINOS Y CONDICIONES</label>
      <textarea id="notas" placeholder="Ej. Validez: 15 días. Forma de pago: Transferencia..." oninput="guardarEnCache()"></textarea>
    </div>
  </div>

  <div class="signature-section">
    <div class="signature">Gerente de Ventas<br><strong>Materiales Eléctricos</strong></div>
  </div>

  <div class="dates-section">
    <div class="dates-grid">
      <div class="field-group"><label>Fecha de Emisión</label> <input type="date" id="fecha-emision" oninput="guardarEnCache()"></div>
      <div class="field-group"><label>Válido hasta</label> <input type="date" id="fecha-vencimiento" oninput="guardarEnCache()"></div>
    </div>
  </div>
</div>

<script>
  function autoResize(textarea) {
    textarea.style.height = 'auto';
    textarea.style.height = (textarea.scrollHeight) + 'px';
  }

  let contador = 1;
  const CLAVE_CACHE = 'cotizacion_electrica_v1';

  window.onload = function() {
    const cache = localStorage.getItem(CLAVE_CACHE);
    if (cache) {
      const data = JSON.parse(cache);
      document.getElementById('cliente').value = data.cliente || '';
      document.getElementById('contacto').value = data.contacto || '';
      document.getElementById('telefono').value = data.telefono || '';
      document.getElementById('correo').value = data.correo || '';
      document.getElementById('notas').value = data.notas || '';
      document.getElementById('fecha-emision').value = data.fechaEmision || new Date().toISOString().split('T')[0];
      document.getElementById('fecha-vencimiento').value = data.fechaVencimiento || '';

      const tbody = document.getElementById('cuerpo-productos');
      tbody.innerHTML = '';
      contador = 1;
      if (data.productos && data.productos.length > 0) {
        data.productos.forEach(p => {
          agregarFila(p.cantidad, p.unidad, p.descripcion, p.precio);
        });
      } else {
        agregarFila();
      }
    } else {
      const hoy = new Date();
      const emision = hoy.toISOString().split('T')[0];
      const vencimiento = new Date(hoy);
      vencimiento.setDate(vencimiento.getDate() + 15);
      document.getElementById('fecha-emision').value = emision;
      document.getElementById('fecha-vencimiento').value = vencimiento.toISOString().split('T')[0];
      agregarFila();
    }
    calcularTotales();
  };

  function formatear(valor) {
    return '$' + valor.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,');
  }

  function calcularTotales() {
    let subtotal = 0;
    document.querySelectorAll('#cuerpo-productos tr').forEach(fila => {
      const cant = parseFloat(fila.cells[1].querySelector('input').value) || 0;
      const precio = parseFloat(fila.cells[4].querySelector('input').value) || 0;
      const importe = cant * precio;
      fila.cells[5].textContent = formatear(importe);
      subtotal += importe;
    });

    const iva = subtotal * 0.16;
    const total = subtotal + iva;

    document.getElementById('subtotal').textContent = formatear(subtotal);
    document.getElementById('iva').textContent = formatear(iva);
    document.getElementById('total').textContent = formatear(total);
    guardarEnCache();
  }

  function eliminarFila(boton) {
    if (document.querySelectorAll('#cuerpo-productos tr').length <= 1) {
      alert('Debe haber al menos un ítem.');
      return;
    }
    boton.closest('tr').remove();
    recalcularIndices();
    calcularTotales();
  }

  function recalcularIndices() {
    const filas = document.querySelectorAll('#cuerpo-productos tr');
    filas.forEach((fila, index) => {
      fila.cells[0].textContent = index + 1;
    });
    contador = filas.length + 1;
  }

  function agregarFila(cant = 1, unidad = 'pz', desc = '', precio = 0) {
    const tbody = document.getElementById('cuerpo-productos');
    const fila = document.createElement('tr');

    const textareaId = 'desc-' + Date.now();
    fila.innerHTML = `
      <td>${contador}</td>
      <td><input type="number" min="0" step="1" value="${cant}" oninput="calcularTotales()"></td>
      <td><input type="text" value="${unidad}" style="width:60px;text-align:center;" oninput="guardarEnCache()"></td>
      <td class="descripcion-cell">
        <textarea class="auto-resize" id="${textareaId}" placeholder="Descripción del producto o servicio" oninput="autoResize(this); guardarEnCache();">${desc}</textarea>
      </td>
      <td><input type="number" min="0" step="0.01" value="${precio}" oninput="calcularTotales()"></td>
      <td>$0.00</td>
      <td><button class="btn btn-remove" onclick="eliminarFila(this)">🗑️ Quitar</button></td>
    `;
    tbody.appendChild(fila);
    setTimeout(() => autoResize(document.getElementById(textareaId)), 0);
    contador++;
  }

  function guardarEnCache() {
    const data = {
      cliente: document.getElementById('cliente').value,
      contacto: document.getElementById('contacto').value,
      telefono: document.getElementById('telefono').value,
      correo: document.getElementById('correo').value,
      notas: document.getElementById('notas').value,
      fechaEmision: document.getElementById('fecha-emision').value,
      fechaVencimiento: document.getElementById('fecha-vencimiento').value,
      productos: Array.from(document.querySelectorAll('#cuerpo-productos tr')).map(fila => ({
        cantidad: fila.cells[1].querySelector('input').value,
        unidad: fila.cells[2].querySelector('input').value,
        descripcion: fila.cells[3].querySelector('textarea').value,
        precio: fila.cells[4].querySelector('input').value
      }))
    };
    localStorage.setItem(CLAVE_CACHE, JSON.stringify(data));
  }

  function imprimirPDF() {
    window.print();
  }

  function exportarExcel() {
    const wb = XLSX.utils.book_new();
    const ws_data = [];
    ws_data.push(["COTIZACIÓN - MATERIALES ELÉCTRICOS"]);
    ws_data.push([""]);
    ws_data.push(["CLIENTE:", document.getElementById('cliente').value || ""]);
    ws_data.push(["CONTACTO:", document.getElementById('contacto').value || ""]);
    ws_data.push(["TELÉFONO:", document.getElementById('telefono').value || ""]);
    ws_data.push([""]);
    ws_data.push(["DETALLE DE PRODUCTOS/SERVICIOS"]);
    ws_data.push(["Ítem", "Cant.", "Unidad", "Descripción", "P. Unitario", "Importe"]);

    document.querySelectorAll('#cuerpo-productos tr').forEach(fila => {
      const c1 = fila.cells[1].querySelector('input').value || "";
      const c2 = fila.cells[2].querySelector('input').value || "";
      const c3 = fila.cells[3].querySelector('textarea').value || "";
      const c4 = fila.cells[4].querySelector('input').value || "";
      const imp = fila.cells[5].textContent.replace('$', '').replace(/,/g, '') || "0";
      ws_data.push([fila.cells[0].textContent, c1, c2, c3, parseFloat(c4) || "", parseFloat(imp) || ""]);
    });

    ws_data.push([""]);
    ws_data.push(["SUBTOTAL", "", "", "", "", document.getElementById('subtotal').textContent.replace('$', '').replace(/,/g, '')]);
    ws_data.push(["IVA (16%)", "", "", "", "", document.getElementById('iva').textContent.replace('$', '').replace(/,/g, '')]);
    ws_data.push(["TOTAL", "", "", "", "", document.getElementById('total').textContent.replace('$', '').replace(/,/g, '')]);
    ws_data.push([""]);
    ws_data.push(["NOTAS:", document.getElementById('notas').value || ""]);

    const ws = XLSX.utils.aoa_to_sheet(ws_data);
    XLSX.utils.book_append_sheet(wb, ws, "Cotización");
    XLSX.writeFile(wb, `Cotizacion_Electrica_${new Date().toISOString().slice(0,10)}.xlsx`);
  }

  function enviarCorreo() {
    const cliente = document.getElementById('cliente').value || "Cliente";
    const total = document.getElementById('total').textContent;
    const correo = document.getElementById('correo').value || "";
    const notas = document.getElementById('notas').value || "Sin notas.";
    const emision = document.getElementById('fecha-emision').value || "Sin fecha";
    const vence = document.getElementById('fecha-vencimiento').value || "Sin fecha";

    const cuerpo = `Hola ${cliente},

Adjunto cotización de Materiales Eléctricos.

• Fecha de emisión: ${emision}
• Válida hasta: ${vence}
• Total: ${total}

Notas:
${notas}

Gracias por su preferencia.
Gerente de Ventas
Tel: 3312958108
www.homesupportelectric.com`;

    const asunto = `Cotización - Materiales Eléctricos - ${cliente}`;
    window.location.href = `mailto:${correo}?subject=${encodeURIComponent(asunto)}&body=${encodeURIComponent(cuerpo)}`;
  }
</script>

</body>
</html>
