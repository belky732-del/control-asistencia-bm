<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Control de Asistencia BM</title>
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />

  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      background: #f3f4f6;
      color: #1f2933;
    }

    .app {
      max-width: 1100px;
      margin: 0 auto;
      padding: 16px;
    }

    header {
      background: linear-gradient(135deg, #1e88ff, #0060df);
      color: #fff;
      padding: 18px 20px;
      border-radius: 16px 16px 0 0;
    }

    header h1 {
      margin: 0 0 6px;
      font-size: 1.4rem;
    }

    header p {
      margin: 0;
      font-size: 0.9rem;
      opacity: 0.9;
    }

    .content {
      background: #ffffff;
      border-radius: 0 0 16px 16px;
      box-shadow: 0 12px 25px rgba(15, 23, 42, 0.12);
      padding: 16px;
    }

    .grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 16px;
    }

    @media (min-width: 900px) {
      .grid {
        grid-template-columns: 1.1fr 0.9fr;
      }
    }

    .card {
      border-radius: 12px;
      border: 1px solid #e5e7eb;
      padding: 14px 16px 16px;
      background: #ffffff;
    }

    .card-title {
      font-weight: 600;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .card-title span.icon {
      width: 20px;
      height: 20px;
      border-radius: 999px;
      background: #e0efff;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.85rem;
      color: #1e88ff;
    }

    label {
      display: block;
      font-size: 0.82rem;
      margin-bottom: 4px;
      color: #4b5563;
    }

    input[type="text"],
    input[type="number"],
    input[type="date"],
    input[type="time"] {
      width: 100%;
      padding: 7px 9px;
      border-radius: 8px;
      border: 1px solid #d1d5db;
      font-size: 0.88rem;
      outline: none;
      transition: border-color 0.12s, box-shadow 0.12s;
    }

    input:focus {
      border-color: #1e88ff;
      box-shadow: 0 0 0 1px #1e88ff20;
    }

    .row {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
    }

    .row-3 {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 10px;
    }

    .row + .row,
    .row-3 + .row-3,
    .row + .row-3,
    .row-3 + .row {
      margin-top: 10px;
    }

    .badge-note {
      margin-top: 6px;
      font-size: 0.75rem;
      color: #6b7280;
    }

    .btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
      border-radius: 999px;
      border: none;
      padding: 7px 14px;
      font-size: 0.85rem;
      cursor: pointer;
      transition: background 0.15s, transform 0.05s, box-shadow 0.1s;
      white-space: nowrap;
    }

    .btn-primary {
      background: #1e88ff;
      color: #fff;
      box-shadow: 0 4px 10px rgba(37, 99, 235, 0.25);
    }

    .btn-primary:hover {
      background: #1b6fe0;
    }

    .btn-secondary {
      background: #e5f0ff;
      color: #1e40af;
    }

    .btn-secondary:hover {
      background: #d9e8ff;
    }

    .btn-danger {
      background: #ef4444;
      color: #fff;
    }

    .btn-danger:hover {
      background: #dc2626;
    }

    .btn:active {
      transform: scale(0.97);
      box-shadow: none;
    }

    .btn-group {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
      margin-top: 12px;
    }

    .small-text {
      font-size: 0.8rem;
      color: #6b7280;
      margin-top: 6px;
    }

    /* Resumen */
    .summary-grid {
      display: grid;
      grid-template-columns: 1fr;
      gap: 8px;
      margin-top: 10px;
    }

    @media (min-width: 600px) {
      .summary-grid {
        grid-template-columns: repeat(2, minmax(0, 1fr));
      }
    }

    .summary-box {
      border-radius: 10px;
      border: 1px solid #e5e7eb;
      padding: 10px 12px;
      background: #f9fafb;
      font-size: 0.83rem;
    }

    .summary-box strong {
      display: block;
      font-size: 0.89rem;
      margin-bottom: 4px;
    }

    .summary-value {
      font-weight: 700;
      font-size: 1.05rem;
      margin-top: 2px;
      color: #111827;
    }

    /* Registros / tabla */
    .table-wrapper {
      overflow-x: auto;
      margin-top: 10px;
      border-radius: 10px;
      border: 1px solid #e5e7eb;
    }

    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.78rem;
      min-width: 680px;
    }

    th,
    td {
      padding: 6px 8px;
      border-bottom: 1px solid #e5e7eb;
      text-align: left;
      white-space: nowrap;
    }

    th {
      background: #f3f4f6;
      font-weight: 600;
      font-size: 0.8rem;
    }

    tr:last-child td {
      border-bottom: none;
    }

    .tag {
      border-radius: 999px;
      padding: 2px 8px;
      font-size: 0.72rem;
      display: inline-block;
    }

    .tag-open {
      background: #fef3c7;
      color: #92400e;
    }

    .tag-closed {
      background: #dcfce7;
      color: #166534;
    }

    .footer-note {
      margin-top: 8px;
      font-size: 0.76rem;
      color: #6b7280;
    }

    /* Botón imprimir solo en pantalla */
    @media print {
      header,
      .btn-danger,
      .btn-secondary,
      .btn-primary.print-hide {
        display: none !important;
      }

      body {
        background: #ffffff;
      }

      .app {
        padding: 0;
        box-shadow: none;
      }

      .content {
        box-shadow: none;
      }
    }
  </style>
</head>

<body>
  <div class="app">
    <header>
      <h1>Control de Asistencia BM</h1>
      <p>Marca entradas y salidas, calcula horas, salario, INSS, y genera reporte por fechas (datos guardados en este dispositivo).</p>
    </header>

    <div class="content">
      <div class="grid">
        <!-- ASISTENCIA -->
        <section class="card">
          <div class="card-title">
            <span class="icon">⏱</span>
            <span>Asistencia</span>
          </div>

          <div>
            <label for="employeeName">Empleado (escribe el nombre)</label>
            <input id="employeeName" type="text" placeholder="Ej: Belky Méndez" autocomplete="off" />
          </div>

          <div class="row" style="margin-top:10px;">
            <div>
              <label for="hourlyRate">Pago por hora (US$)</label>
              <input id="hourlyRate" type="number" step="0.01" min="0" value="2.16" />
            </div>
            <div>
              <label for="inssPercent">% INSS (deducción)</label>
              <input id="inssPercent" type="number" step="0.01" min="0" value="7" />
            </div>
          </div>

          <div style="margin-top:12px;">
            <strong style="font-size:0.86rem;">Fecha y hora del marcaje</strong>
            <p class="small-text">Puedes cambiarlas si estás registrando una asistencia pasada. Si las dejas tal cual, se usa la fecha y hora actuales.</p>
            <div class="row">
              <div>
                <label for="markDate">Fecha</label>
                <input id="markDate" type="date" />
              </div>
              <div>
                <label for="markTime">Hora</label>
                <input id="markTime" type="time" />
              </div>
            </div>
          </div>

          <div class="btn-group">
            <button id="btnEntrada" class="btn btn-primary">
              ✅ Marcar entrada
            </button>
            <button id="btnSalida" class="btn btn-secondary">
              ⏹ Marcar salida
            </button>
          </div>

          <p class="badge-note">Se usará la fecha y hora de los campos de arriba (o la actual si los dejas vacíos).</p>

          <p class="small-text">Datos guardados en este dispositivo (navegador).</p>
        </section>

        <!-- RESUMEN Y REPORTES -->
        <section class="card">
          <div class="card-title">
            <span class="icon">📊</span>
            <span>Resumen y reportes</span>
          </div>

          <div class="row">
            <div>
              <label for="filterFrom">Desde</label>
              <input id="filterFrom" type="date" />
            </div>
            <div>
              <label for="filterTo">Hasta</label>
              <input id="filterTo" type="date" />
            </div>
          </div>

          <div style="margin-top:10px;">
            <label for="filterEmployee">Empleado (opcional)</label>
            <input id="filterEmployee" type="text" placeholder="Dejar vacío para todos" />
          </div>

          <div class="btn-group">
            <button id="btnActualizarResumen" class="btn btn-primary">
              🔄 Actualizar resumen
            </button>
            <button id="btnLimpiarFiltros" class="btn btn-secondary">
              ✨ Limpiar filtros
            </button>
          </div>

          <div class="summary-grid">
            <div class="summary-box">
              <strong>Horas trabajadas</strong>
              <div class="summary-value" id="sumHoras">0.00 h</div>
              <span id="sumLabelHoras" class="small-text"></span>
            </div>
            <div class="summary-box">
              <strong>Salario bruto</strong>
              <div class="summary-value" id="sumBruto">US$ 0.00</div>
              <span class="small-text">Antes de INSS</span>
            </div>
            <div class="summary-box">
              <strong>INSS estimado</strong>
              <div class="summary-value" id="sumInss">US$ 0.00</div>
              <span class="small-text">Deducción total</span>
            </div>
            <div class="summary-box">
              <strong>Salario neto</strong>
              <div class="summary-value" id="sumNeto">US$ 0.00</div>
              <span class="small-text">Después de INSS</span>
            </div>
          </div>

          <div class="btn-group" style="margin-top:14px;">
            <button id="btnPDF" class="btn btn-primary print-hide">
              📄 Generar PDF / Imprimir
            </button>
            <button id="btnBorrarTodo" class="btn btn-danger">
              🗑 Borrar TODOS los registros de este dispositivo
            </button>
          </div>
        </section>
      </div>

      <!-- REGISTROS -->
      <section class="card" style="margin-top:16px;">
        <div class="card-title">
          <span class="icon">📋</span>
          <span>Registros</span>
        </div>

        <p class="small-text" id="labelRegistros">
          Mostrando todas las asistencias guardadas en este dispositivo.
        </p>

        <div class="table-wrapper">
          <table>
            <thead>
              <tr>
                <th>Fecha</th>
                <th>Empleado</th>
                <th>% INSS</th>
                <th>Entrada</th>
                <th>Salida</th>
                <th>Estado</th>
                <th>Horas</th>
                <th>Bruto (US$)</th>
                <th>INSS (US$)</th>
                <th>Neto (US$)</th>
              </tr>
            </thead>
            <tbody id="tbodyRegistros">
              <!-- filas dinámicas -->
            </tbody>
          </table>
        </div>

        <p class="footer-note">
          Nota: cada dispositivo (teléfono, computadora) tiene sus propios registros. No se comparten entre equipos.
        </p>
      </section>
    </div>
  </div>

  <script>
    const STORAGE_KEY = "control_asistencia_bm";

    let registros = [];

    const employeeNameInput = document.getElementById("employeeName");
    const hourlyRateInput = document.getElementById("hourlyRate");
    const inssPercentInput = document.getElementById("inssPercent");
    const markDateInput = document.getElementById("markDate");
    const markTimeInput = document.getElementById("markTime");

    const filterFromInput = document.getElementById("filterFrom");
    const filterToInput = document.getElementById("filterTo");
    const filterEmployeeInput = document.getElementById("filterEmployee");

    const sumHorasEl = document.getElementById("sumHoras");
    const sumBrutoEl = document.getElementById("sumBruto");
    const sumInssEl = document.getElementById("sumInss");
    const sumNetoEl = document.getElementById("sumNeto");
    const sumLabelHorasEl = document.getElementById("sumLabelHoras");

    const labelRegistros = document.getElementById("labelRegistros");
    const tbodyRegistros = document.getElementById("tbodyRegistros");

    function cargarRegistros() {
      try {
        const raw = localStorage.getItem(STORAGE_KEY);
        registros = raw ? JSON.parse(raw) : [];
      } catch (e) {
        registros = [];
      }
    }

    function guardarRegistros() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(registros));
    }

    function redondear(num, dec = 2) {
      return Number(num.toFixed(dec));
    }

    function formatearFecha(fechaISO) {
      if (!fechaISO) return "";
      const d = new Date(fechaISO);
      if (isNaN(d)) return "";
      return d.toLocaleDateString("es-ES");
    }

    function formatearHora(fechaISO) {
      if (!fechaISO) return "";
      const d = new Date(fechaISO);
      if (isNaN(d)) return "";
      return d.toLocaleTimeString("es-ES", { hour: "2-digit", minute: "2-digit" });
    }

    function formatearDinero(num) {
      return "US$ " + redondear(num).toFixed(2);
    }

    function establecerFechaHoraActual() {
      const ahora = new Date();
      const yyyy = ahora.getFullYear();
      const mm = String(ahora.getMonth() + 1).padStart(2, "0");
      const dd = String(ahora.getDate()).padStart(2, "0");
      const hh = String(ahora.getHours()).padStart(2, "0");
      const mi = String(ahora.getMinutes()).padStart(2, "0");

      markDateInput.value = ${yyyy}-${mm}-${dd};
      markTimeInput.value = ${hh}:${mi};
    }

    function obtenerFechaHoraMarcaje() {
      let fecha = markDateInput.value;
      let hora = markTimeInput.value;

      if (!fecha || !hora) {
        const ahora = new Date();
        fecha = ahora.toISOString().slice(0, 10);
        hora = ahora.toTimeString().slice(0, 5);
      }
      const iso = ${fecha}T${hora}:00;
      return new Date(iso);
    }

    function marcarEntrada() {
      const empleado = employeeNameInput.value.trim();
      if (!empleado) {
        alert("Escribe el nombre del empleado para marcar la entrada.");
        return;
      }

      const pagoHora = parseFloat(hourlyRateInput.value) || 0;
      const inssPercent = parseFloat(inssPercentInput.value) || 0;
      const fechaHora = obtenerFechaHoraMarcaje();

      const registro = {
        id: Date.now(),
        empleado,
        pagoHora,
        inssPercent,
        entrada: fechaHora.toISOString(),
        salida: null,
        estado: "Abierto",
        horas: 0,
        bruto: 0,
        inss: 0,
        neto: 0,
      };

      registros.push(registro);
      guardarRegistros();
      renderizarTabla();
      actualizarResumen();
      establecerFechaHoraActual();
    }

    function marcarSalida() {
      const empleado = employeeNameInput.value.trim();
      if (!empleado) {
        alert("Escribe el nombre del empleado para marcar la salida.");
        return;
      }

      const abiertos = registros.filter(
        (r) => r.empleado.toLowerCase() === empleado.toLowerCase() && r.estado === "Abierto"
      );

      if (abiertos.length === 0) {
        alert("No hay un registro de entrada abierto para este empleado.");
        return;
      }

      const registro = abiertos.sort((a, b) => a.entrada.localeCompare(b.entrada))[abiertos.length - 1];

      const fechaHora = obtenerFechaHoraMarcaje();
      const entrada = new Date(registro.entrada);
      const salida = fechaHora;

      if (salida < entrada) {
        if (!confirm("La hora de salida es anterior a la de entrada. ¿Quieres guardarla de todas formas?")) {
          return;
        }
      }

      const diffMs = salida - entrada;
      const horas = diffMs > 0 ? diffMs / (1000 * 60 * 60) : 0;

      const bruto = horas * registro.pagoHora;
      const inss = bruto * (registro.inssPercent / 100);
      const neto = bruto - inss;

      registro.salida = salida.toISOString();
      registro.estado = "Cerrado";
      registro.horas = redondear(horas);
      registro.bruto = redondear(bruto);
      registro.inss = redondear(inss);
      registro.neto = redondear(neto);

      guardarRegistros();
      renderizarTabla();
      actualizarResumen();
      establecerFechaHoraActual();
    }

    function obtenerRegistrosFiltrados() {
      let filtrados = [...registros];

      const fDesde = filterFromInput.value ? new Date(filterFromInput.value + "T00:00:00") : null;
      const fHasta = filterToInput.value ? new Date(filterToInput.value + "T23:59:59") : null;
      const fEmpleado = filterEmployeeInput.value.trim().toLowerCase();

      filtrados = filtrados.filter((r) => {
        const fecha = new Date(r.entrada);
        if (fDesde && fecha < fDesde) return false;
        if (fHasta && fecha > fHasta) return false;
        if (fEmpleado && !r.empleado.toLowerCase().includes(fEmpleado)) return false;
        return true;
      });

      return filtrados;
    }

    function actualizarResumen() {
      const filtrados = obtenerRegistrosFiltrados().filter((r) => r.estado === "Cerrado");

      const totalHoras = filtrados.reduce((acc, r) => acc + (r.horas || 0), 0);
      const totalBruto = filtrados.reduce((acc, r) => acc + (r.bruto || 0), 0);
      const totalInss = filtrados.reduce((acc, r) => acc + (r.inss || 0), 0);
      const totalNeto = filtrados.reduce((acc, r) => acc + (r.neto || 0), 0);

      sumHorasEl.textContent = redondear(totalHoras).toFixed(2) + " h";
      sumBrutoEl.textContent = formatearDinero(totalBruto);
      sumInssEl.textContent = formatearDinero(totalInss);
      sumNetoEl.textContent = formatearDinero(totalNeto);

      if (filterEmployeeInput.value.trim()) {
        sumLabelHorasEl.textContent = "Para: " + filterEmployeeInput.value.trim();
      } else {
        sumLabelHorasEl.textContent = "Para todos los empleados.";
      }

      const hayFiltros = filterFromInput.value || filterToInput.value || filterEmployeeInput.value.trim();
      if (hayFiltros) {
        labelRegistros.textContent =
          "Mostrando asistencias según los filtros de fechas y empleado de arriba.";
      } else {
        labelRegistros.textContent = "Mostrando todas las asistencias guardadas en este dispositivo.";
      }
    }

    function renderizarTabla() {
      const filtrados = obtenerRegistrosFiltrados().sort((a, b) => a.entrada.localeCompare(b.entrada));
      tbodyRegistros.innerHTML = "";

      if (filtrados.length === 0) {
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.colSpan = 10;
        td.textContent = "No hay registros para mostrar.";
        td.style.textAlign = "center";
        td.style.padding = "10px";
        tr.appendChild(td);
        tbodyRegistros.appendChild(tr);
        return;
      }

      filtrados.forEach((r) => {
        const tr = document.createElement("tr");

        const tdFecha = document.createElement("td");
        tdFecha.textContent = formatearFecha(r.entrada);

        const tdEmp = document.createElement("td");
        tdEmp.textContent = r.empleado;

        const tdInss = document.createElement("td");
        tdInss.textContent = (r.inssPercent || 0).toFixed(2) + " %";

        const tdEntrada = document.createElement("td");
        tdEntrada.textContent = formatearHora(r.entrada);

        const tdSalida = document.createElement("td");
        tdSalida.textContent = r.salida ? formatearHora(r.salida) : "-";

        const tdEstado = document.createElement("td");
        const span = document.createElement("span");
        span.classList.add("tag");
        if (r.estado === "Abierto") {
          span.classList.add("tag-open");
          span.textContent = "Abierto";
        } else {
          span.classList.add("tag-closed");
          span.textContent = "Cerrado";
        }
        tdEstado.appendChild(span);

        const tdHoras = document.createElement("td");
        tdHoras.textContent = (r.horas || 0).toFixed(2);

        const tdBruto = document.createElement("td");
        tdBruto.textContent = (r.bruto || 0).toFixed(2);

        const tdInssMonto = document.createElement("td");
        tdInssMonto.textContent = (r.inss || 0).toFixed(2);

        const tdNeto = document.createElement("td");
        tdNeto.textContent = (r.neto || 0).toFixed(2);

        tr.append(tdFecha, tdEmp, tdInss, tdEntrada, tdSalida, tdEstado, tdHoras, tdBruto, tdInssMonto, tdNeto);
        tbodyRegistros.appendChild(tr);
      });
    }

    function limpiarFiltros() {
      filterFromInput.value = "";
      filterToInput.value = "";
      filterEmployeeInput.value = "";
      actualizarResumen();
      renderizarTabla();
    }

    function borrarTodos() {
      if (!confirm("¿Seguro que deseas borrar TODOS los registros de este dispositivo?")) return;
      registros = [];
      guardarRegistros();
      renderizarTabla();
      actualizarResumen();
    }

    function generarPDF() {
      window.print();
    }

    document.getElementById("btnEntrada").addEventListener("click", marcarEntrada);
    document.getElementById("btnSalida").addEventListener("click", marcarSalida);
    document.getElementById("btnActualizarResumen").addEventListener("click", () => {
      actualizarResumen();
      renderizarTabla();
    });
    document.getElementById("btnLimpiarFiltros").addEventListener("click", limpiarFiltros);
    document.getElementById("btnBorrarTodo").addEventListener("click", borrarTodos);
    document.getElementById("btnPDF").addEventListener("click", generarPDF);

    cargarRegistros();
    establecerFechaHoraActual();
    renderizarTabla();
    actualizarResumen();
  </script>
</body>
</html>
