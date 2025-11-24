[index.html.html](https://github.com/user-attachments/files/23701276/index.html.html)
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Control de Asistencia BM</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      background: #f2f4f8;
      color: #222;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      padding: 16px;
    }

    .app {
      width: 100%;
      max-width: 1100px;
      background: #ffffff;
      border-radius: 16px;
      box-shadow: 0 10px 30px rgba(0, 0, 0, 0.06);
      overflow: hidden;
      display: flex;
      flex-direction: column;
    }

    header {
      background: linear-gradient(135deg, #1c6dd0, #4895ef);
      color: white;
      padding: 20px 24px;
    }

    header h1 {
      font-size: 1.6rem;
      margin-bottom: 4px;
    }

    header p {
      opacity: 0.9;
      font-size: 0.9rem;
    }

    main {
      padding: 20px 24px 24px;
      display: grid;
      grid-template-columns: minmax(0, 1.1fr) minmax(0, 1.1fr);
      gap: 16px;
    }

    @media (max-width: 900px) {
      main {
        grid-template-columns: 1fr;
      }
    }

    .panel {
      background: #f8fafc;
      border-radius: 12px;
      padding: 16px 16px 18px;
      border: 1px solid #e2e8f0;
    }

    .panel h2 {
      font-size: 1.05rem;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .panel h2 span.icon {
      font-size: 1.2rem;
    }

    label {
      font-size: 0.85rem;
      margin-bottom: 4px;
      display: block;
      color: #4a5568;
    }

    input[type="text"],
    input[type="number"],
    input[type="date"] {
      width: 100%;
      padding: 8px 10px;
      border-radius: 8px;
      border: 1px solid #cbd5e0;
      font-size: 0.9rem;
      outline: none;
      transition: border-color 0.15s, box-shadow 0.15s;
      background: #ffffff;
    }

    input:focus {
      border-color: #3182ce;
      box-shadow: 0 0 0 1px rgba(49, 130, 206, 0.4);
    }

    .row {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
    }

    .field {
      margin-bottom: 10px;
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 8px 14px;
      font-size: 0.9rem;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      transition: transform 0.08s, box-shadow 0.08s, background 0.15s;
      white-space: nowrap;
    }

    button:active {
      transform: translateY(1px);
      box-shadow: none;
    }

    .btn-primary {
      background: #2563eb;
      color: white;
      box-shadow: 0 4px 10px rgba(37, 99, 235, 0.3);
    }

    .btn-primary:hover {
      background: #1d4ed8;
    }

    .btn-secondary {
      background: #e2e8f0;
      color: #1a202c;
    }

    .btn-secondary:hover {
      background: #cbd5e0;
    }

    .btn-outline {
      background: transparent;
      border: 1px solid #cbd5e0;
      color: #2d3748;
      border-radius: 999px;
      padding: 7px 12px;
    }

    .btn-outline:hover {
      background: #edf2f7;
    }

    .btn-danger {
      background: #e53e3e;
      color: #fff;
      box-shadow: 0 4px 10px rgba(229, 62, 62, 0.3);
    }

    .btn-danger:hover {
      background: #c53030;
    }

    .btn-group {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      margin-top: 4px;
    }

    .summary {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
      margin-top: 4px;
    }

    @media (max-width: 600px) {
      .summary {
        grid-template-columns: 1fr;
      }
    }

    .summary-card {
      background: #ffffff;
      border-radius: 10px;
      padding: 10px 12px;
      border: 1px solid #e2e8f0;
    }

    .summary-card h3 {
      font-size: 0.75rem;
      color: #718096;
      margin-bottom: 3px;
    }

    .summary-card p {
      font-size: 0.98rem;
      font-weight: 600;
      color: #1a202c;
    }

    .summary-card small {
      font-size: 0.75rem;
      color: #a0aec0;
    }

    .table-panel {
      grid-column: 1 / -1;
      margin-top: -4px;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.8rem;
      margin-top: 8px;
    }

    thead {
      background: #e2e8f0;
    }

    th,
    td {
      padding: 6px 8px;
      text-align: left;
      border-bottom: 1px solid #edf2f7;
    }

    th {
      font-weight: 600;
      color: #4a5568;
      white-space: nowrap;
    }

    tbody tr:nth-child(even) {
      background: #fafbff;
    }

    .status-pill {
      font-size: 0.7rem;
      padding: 2px 8px;
      border-radius: 999px;
      display: inline-block;
    }

    .status-open {
      background: #fef3c7;
      color: #92400e;
    }

    .status-closed {
      background: #dcfce7;
      color: #166534;
    }

    .muted {
      color: #a0aec0;
      font-size: 0.8rem;
    }

    .divider {
      border-top: 1px dashed #e2e8f0;
      margin: 10px 0;
    }

    .pill {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: #ebf5ff;
      color: #1e40af;
      padding: 4px 10px;
      border-radius: 999px;
      font-size: 0.75rem;
    }
  </style>
</head>
<body>
  <div class="app">
    <header>
      <h1>Control de Asistencia BM</h1>
      <p>Marca entradas y salidas, calcula horas, salario (2.16 US$/h) e INSS, y genera reporte en PDF por fechas.</p>
    </header>

    <main>
      <!-- Panel de marcaje -->
      <section class="panel">
        <h2><span class="icon">🕒</span>Asistencia</h2>

        <div class="field">
          <label for="employeeName">Empleado (escribe el nombre)</label>
          <input
            type="text"
            id="employeeName"
            placeholder="Ej: Belky Mendez"
          />
        </div>

        <div class="divider"></div>

        <div class="field">
          <label>Marcaje rápido</label>
          <div class="btn-group">
            <button id="entradaBtn" class="btn-primary">
              ✅ Marcar entrada
            </button>
            <button id="salidaBtn" class="btn-secondary">
              🔚 Marcar salida
            </button>
          </div>
          <p class="muted" style="margin-top:6px;">
            Se usará la fecha y hora actual del dispositivo.
          </p>
        </div>

        <div class="divider"></div>

        <div class="row">
          <div class="field">
            <label for="wagePerHourInput">Pago por hora (US$)</label>
            <input
              type="number"
              id="wagePerHourInput"
              min="0"
              step="0.01"
              value="2.16"
            />
          </div>
          <div class="field">
            <label for="inssPercentInput">% INSS (deducción)</label>
            <input
              type="number"
              id="inssPercentInput"
              min="0"
              max="50"
              step="0.01"
              value="7"
            />
          </div>
        </div>

        <span class="pill">
          ⚙️ Datos guardados en este dispositivo (navegador)
        </span>
      </section>

      <!-- Panel de resumen y filtros -->
      <section class="panel">
        <h2><span class="icon">📊</span>Resumen y reportes</h2>

        <div class="row">
          <div class="field">
            <label for="startDateInput">Desde</label>
            <input type="date" id="startDateInput" />
          </div>
          <div class="field">
            <label for="endDateInput">Hasta</label>
            <input type="date" id="endDateInput" />
          </div>
        </div>

        <div class="btn-group">
          <button id="refreshBtn" class="btn-outline">🔄 Actualizar resumen</button>
          <button id="clearFiltersBtn" class="btn-secondary">🧹 Limpiar filtros</button>
        </div>

        <div class="summary">
          <div class="summary-card">
            <h3>Horas trabajadas</h3>
            <p id="totalHours">0.00 h</p>
            <small>Nombre escrito arriba + rango de fechas</small>
          </div>
          <div class="summary-card">
            <h3>Salario bruto</h3>
            <p id="grossPay">US$ 0.00</p>
            <small>Antes de INSS</small>
          </div>
          <div class="summary-card">
            <h3>INSS estimado</h3>
            <p id="inssAmount">US$ 0.00</p>
            <small>Deducción</small>
          </div>
          <div class="summary-card">
            <h3>Salario neto</h3>
            <p id="netPay">US$ 0.00</p>
            <small>Después de INSS</small>
          </div>
        </div>

        <div class="divider"></div>

        <div class="btn-group">
          <button id="pdfBtn" class="btn-primary">📄 Generar PDF</button>
          <button id="clearAllBtn" class="btn-danger">🗑️ Borrar TODOS los registros de este dispositivo</button>
        </div>
      </section>

      <!-- Tabla -->
      <section class="panel table-panel">
        <h2><span class="icon">📅</span>Registros</h2>
        <p class="muted" style="margin-bottom:4px;">
          Mostrando asistencias del nombre escrito arriba y rango de fechas seleccionadas (en este dispositivo).
        </p>
        <div style="overflow-x:auto;">
          <table>
            <thead>
              <tr>
                <th>Fecha</th>
                <th>Empleado</th>
                <th>Entrada</th>
                <th>Salida</th>
                <th>Estado</th>
                <th>Horas</th>
                <th>Bruto (US$)</th>
                <th>INSS (US$)</th>
                <th>Neto (US$)</th>
              </tr>
            </thead>
            <tbody id="recordsTbody">
            </tbody>
          </table>
        </div>
      </section>
    </main>
  </div>

  <!-- jsPDF para PDF -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <script>
    const STORAGE_KEYS = {
      RECORDS: "bm_attendance_records_mes_v1",
      SETTINGS: "bm_settings_mes_v1",
    };

    let records = [];
    let settings = {
      wagePerHour: 2.16,
      inssPercent: 7,
    };

    const employeeNameInput = document.getElementById("employeeName");
    const entradaBtn = document.getElementById("entradaBtn");
    const salidaBtn = document.getElementById("salidaBtn");
    const wagePerHourInput = document.getElementById("wagePerHourInput");
    const inssPercentInput = document.getElementById("inssPercentInput");

    const startDateInput = document.getElementById("startDateInput");
    const endDateInput = document.getElementById("endDateInput");
    const refreshBtn = document.getElementById("refreshBtn");
    const clearFiltersBtn = document.getElementById("clearFiltersBtn");

    const totalHoursEl = document.getElementById("totalHours");
    const grossPayEl = document.getElementById("grossPay");
    const inssAmountEl = document.getElementById("inssAmount");
    const netPayEl = document.getElementById("netPay");
    const pdfBtn = document.getElementById("pdfBtn");
    const clearAllBtn = document.getElementById("clearAllBtn");
    const recordsTbody = document.getElementById("recordsTbody");

    function saveToStorage() {
      try {
        localStorage.setItem(STORAGE_KEYS.RECORDS, JSON.stringify(records));
        localStorage.setItem(STORAGE_KEYS.SETTINGS, JSON.stringify(settings));
      } catch (e) {}
    }

    function loadFromStorage() {
      try {
        const storedRecords = localStorage.getItem(STORAGE_KEYS.RECORDS);
        const storedSettings = localStorage.getItem(STORAGE_KEYS.SETTINGS);

        records = storedRecords ? JSON.parse(storedRecords) : [];
        if (!Array.isArray(records)) records = [];

        const defaults = { wagePerHour: 2.16, inssPercent: 7 };
        settings = storedSettings ? JSON.parse(storedSettings) : defaults;

        if (typeof settings.wagePerHour !== "number") settings.wagePerHour = 2.16;
        if (typeof settings.inssPercent !== "number") settings.inssPercent = 7;
      } catch (e) {
        records = [];
        settings = { wagePerHour: 2.16, inssPercent: 7 };
      }
    }

    function formatDate(dateObj) {
      return dateObj.toISOString().slice(0, 10);
    }

    function formatTime(dateObj) {
      return dateObj.toTimeString().slice(0, 5);
    }

    function parseISO(iso) {
      return new Date(iso);
    }

    function hoursBetween(startIso, endIso) {
      if (!startIso || !endIso) return 0;
      const start = parseISO(startIso);
      const end = parseISO(endIso);
      const diffMs = end - start;
      if (diffMs <= 0) return 0;
      return diffMs / (1000 * 60 * 60);
    }

    function getMonthDefaultRange() {
      const now = new Date();
      const first = new Date(now.getFullYear(), now.getMonth(), 1);
      const last = new Date(now.getFullYear(), now.getMonth() + 1, 0);
      return {
        start: formatDate(first),
        end: formatDate(last),
      };
    }

    function setDefaultDatesIfEmpty() {
      const { start, end } = getMonthDefaultRange();
      if (!startDateInput.value) startDateInput.value = start;
      if (!endDateInput.value) endDateInput.value = end;
    }

    function getFilters() {
      const name = employeeNameInput.value.trim();
      const startDate = startDateInput.value || null;
      const endDate = endDateInput.value || null;
      return { name, startDate, endDate };
    }

    function recordMatchesFilters(record, filters) {
      if (filters.name && record.employee !== filters.name) {
        return false;
      }
      if (filters.startDate && record.date < filters.startDate) return false;
      if (filters.endDate && record.date > filters.endDate) return false;
      return true;
    }

    function getFilteredRecords() {
      const filters = getFilters();
      return records
        .filter((r) => recordMatchesFilters(r, filters))
        .sort((a, b) => {
          if (a.date === b.date) return a.entry.localeCompare(b.entry);
          return a.date.localeCompare(b.date);
        });
    }

    function renderTableAndSummary() {
      const wage = parseFloat(wagePerHourInput.value) || 0;
      const inssPercent = parseFloat(inssPercentInput.value) || 0;

      settings.wagePerHour = wage;
      settings.inssPercent = inssPercent;
      saveToStorage();

      const filtered = getFilteredRecords();
      recordsTbody.innerHTML = "";

      let totalHours = 0;
      let totalGross = 0;
      let totalInss = 0;
      let totalNet = 0;

      filtered.forEach((rec) => {
        const hours = hoursBetween(rec.entry, rec.exit);
        const gross = hours * wage;
        const inss = gross * (inssPercent / 100);
        const net = gross - inss;

        totalHours += hours;
        totalGross += gross;
        totalInss += inss;
        totalNet += net;

        const entryDate = parseISO(rec.entry);
        const exitDate = rec.exit ? parseISO(rec.exit) : null;

        const tr = document.createElement("tr");
        tr.innerHTML = `
          <td>${rec.date}</td>
          <td>${rec.employee}</td>
          <td>${formatTime(entryDate)}</td>
          <td>${exitDate ? formatTime(exitDate) : "<span class='muted'>—</span>"}</td>
          <td>
            <span class="status-pill ${rec.exit ? "status-closed" : "status-open"}">
              ${rec.exit ? "Cerrado" : "Abierto"}
            </span>
          </td>
          <td>${hours.toFixed(2)}</td>
          <td>${gross.toFixed(2)}</td>
          <td>${inss.toFixed(2)}</td>
          <td>${net.toFixed(2)}</td>
        `;
        recordsTbody.appendChild(tr);
      });

      totalHoursEl.textContent = totalHours.toFixed(2) + " h";
      grossPayEl.textContent = "US$ " + totalGross.toFixed(2);
      inssAmountEl.textContent = "US$ " + totalInss.toFixed(2);
      netPayEl.textContent = "US$ " + totalNet.toFixed(2);
    }

    entradaBtn.addEventListener("click", () => {
      const name = employeeNameInput.value.trim();
      if (!name) {
        alert("Escribe el nombre del empleado.");
        return;
      }
      const now = new Date();
      const rec = {
        id: Date.now().toString(),
        employee: name,
        date: formatDate(now),
        entry: now.toISOString(),
        exit: null,
      };
      records.push(rec);
      setDefaultDatesIfEmpty();
      renderTableAndSummary();
      alert("Entrada registrada para " + name + " a las " + formatTime(now));
    });

    salidaBtn.addEventListener("click", () => {
      const name = employeeNameInput.value.trim();
      if (!name) {
        alert("Escribe el nombre del empleado.");
        return;
      }

      const openRecords = records
        .filter((r) => r.employee === name && !r.exit)
        .sort((a, b) => b.entry.localeCompare(a.entry));

      if (openRecords.length === 0) {
        alert("No hay una entrada abierta para este empleado.");
        return;
      }

      const now = new Date();
      openRecords[0].exit = now.toISOString();
      setDefaultDatesIfEmpty();
      renderTableAndSummary();
      alert("Salida registrada para " + name + " a las " + formatTime(now));
    });

    refreshBtn.addEventListener("click", () => {
      renderTableAndSummary();
    });

    clearFiltersBtn.addEventListener("click", () => {
      startDateInput.value = "";
      endDateInput.value = "";
      renderTableAndSummary();
    });

    clearAllBtn.addEventListener("click", () => {
      if (confirm("¿Seguro que quieres borrar TODOS los registros de este dispositivo?")) {
        records = [];
        saveToStorage();
        renderTableAndSummary();
      }
    });

    // PDF con columnas bien alineadas + resumen
    pdfBtn.addEventListener("click", () => {
      const filtered = getFilteredRecords();
      if (filtered.length === 0) {
        alert("No hay registros en el rango seleccionado para generar el PDF.");
        return;
      }

      const wage = parseFloat(wagePerHourInput.value) || 0;
      const inssPercent = parseFloat(inssPercentInput.value) || 0;
      const { name, startDate, endDate } = getFilters();

      const jspdfLib = window.jspdf;
      if (!jspdfLib || !jspdfLib.jsPDF) {
        alert("No se pudo cargar jsPDF. Verifica tu conexión a internet.");
        return;
      }

      const doc = new jspdfLib.jsPDF();

      // Encabezado
      doc.setFontSize(16);
      doc.text("Control de Asistencia BM", 14, 20);
      doc.setFontSize(11);
      doc.text("Empleado: " + (name || "Todos"), 14, 28);
      doc.text(
        "Rango: " + (startDate || "Inicio") + " a " + (endDate || "Hoy"),
        14,
        34
      );
      doc.text(
        "Pago por hora: US$ " +
          wage.toFixed(2) +
          "   |   INSS: " +
          inssPercent.toFixed(2) +
          "%",
        14,
        40
      );

      // Columnas
      const colX = {
        fecha: 14,
        entrada: 40,
        salida: 58,
        horas: 78,
        bruto: 105,
        inss: 132,
        neto: 159,
      };

      let y = 50;
      doc.setFontSize(10);

      // Encabezados de tabla
      doc.text("Fecha", colX.fecha, y);
      doc.text("Ent.",   colX.entrada, y);
      doc.text("Sal.",   colX.salida,  y);
      doc.text("Horas",  colX.horas,   y);
      doc.text("Bruto",  colX.bruto,   y);
      doc.text("INSS",   colX.inss,    y);
      doc.text("Neto",   colX.neto,    y);

      y += 2;
      doc.line(14, y, 196, y);
      y += 6;

      let totalHours = 0;
      let totalGross = 0;
      let totalInss = 0;
      let totalNet = 0;

      // Filas
      filtered.forEach((rec) => {
        const hours = hoursBetween(rec.entry, rec.exit);
        const gross = hours * wage;
        const inss = gross * (inssPercent / 100);
        const net = gross - inss;

        totalHours += hours;
        totalGross += gross;
        totalInss += inss;
        totalNet += net;

        const entryDate = parseISO(rec.entry);
        const exitDate = rec.exit ? parseISO(rec.exit) : null;

        doc.text(rec.date, colX.fecha, y);
        doc.text(formatTime(entryDate), colX.entrada, y);
        doc.text(exitDate ? formatTime(exitDate) : "--:--", colX.salida, y);
        doc.text(hours.toFixed(2), colX.horas, y);
        doc.text(gross.toFixed(2), colX.bruto, y);
        doc.text(inss.toFixed(2), colX.inss, y);
        doc.text(net.toFixed(2), colX.neto, y);

        y += 6;

        if (y > 260) {
          doc.addPage();
          y = 20;
        }
      });

      // Resumen final
      if (y > 250) {
        doc.addPage();
        y = 20;
      } else {
        y += 4;
      }

      doc.setFontSize(11);
      doc.text("Resumen del periodo", 14, y);
      y += 6;
      doc.setFontSize(10);
      doc.text("Total de horas trabajadas: " + totalHours.toFixed(2) + " h", 14, y);
      y += 5;
      doc.text("Total salario bruto: US$ " + totalGross.toFixed(2), 14, y);
      y += 5;
      doc.text("Total INSS: US$ " + totalInss.toFixed(2), 14, y);
      y += 5;
      doc.text("Total salario neto: US$ " + totalNet.toFixed(2), 14, y);

      const fileName =
        "reporte_asistencia_" +
        (name || "todos") +
        "_" +
        (startDate || "") +
        "_" +
        (endDate || "") +
        ".pdf";

      doc.save(fileName);
    });

    // Inicializar
    loadFromStorage();
    wagePerHourInput.value = settings.wagePerHour;
    inssPercentInput.value = settings.inssPercent;
    setDefaultDatesIfEmpty();
    renderTableAndSummary();
  </script>
</body>
</html>
