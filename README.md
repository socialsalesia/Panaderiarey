<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Control de Ruta - Panadería</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>

    <header>
        <h1>Control de Ruta - Panadería</h1>
    </header>

    <main>
        <section id="cargaInicialSection">
            <h2>Registro de Carga Inicial</h2>

            <form id="cargaInicialForm">
                <label for="fechaCarga">Fecha de Carga:</label>
                <input type="date" id="fechaCarga" required>

                <label for="ruta">Ruta:</label>
                <select id="ruta" required>
                    <option value="">Selecciona una ruta</option>
                    <option value="macuspana">Macuspana (Lunes)</option>
                    <option value="villahermosa">Villahermosa (Martes)</option>
                    <option value="jalapa_tacotalpa">Jalapa/Tacotalpa (Miércoles)</option>
                    <option value="teapa">Teapa (Jueves)</option>
                    <option value="toda_frontera">Toda la Ruta/Frontera (Viernes)</option>
                </select>

                <label for="cargaPan">Bolsas de Pan Cargadas:</label>
                <input type="number" id="cargaPan" value="0" min="0" required oninput="calcularVentaAproximada()">

                <label for="cargaGalletasLeche">Paquetes de Galletas de Leche Cargados:</label>
                <input type="number" id="cargaGalletasLeche" value="0" min="0" required oninput="calcularVentaAproximada()">

                <label for="cargaKekis">Paquetes de Kekis Cargados:</label>
                <input type="number" id="cargaKekis" value="0" min="0" required oninput="calcularVentaAproximada()">

                <label for="cargaBolillo">Bolillos Cargados:</label>
                <input type="number" id="cargaBolillo" value="0" min="0" required oninput="calcularVentaAproximada()">

                <button type="button" onclick="guardarCargaInicial()">Guardar Carga Inicial</button>
            </form>

            <div id="cargaInicialMensajes"></div>
            <div id="ventaAproximada">Venta Aproximada: $0.00</div>
        </section>

        <section id="visualizacionCargaInicial" style="display: none;">
            <h2>Información de Carga Inicial Guardada</h2>
            <p><strong>Fecha de Carga:</strong> <span id="verFechaCarga"></span></p>
            <p><strong>Ruta:</strong> <span id="verRuta"></span></p>
            <p><strong>Carga Pan:</strong> <span id="verCargaPan"></span></p>
            <p><strong>Carga Galletas de Leche:</strong> <span id="verCargaGalletasLeche"></span></p>
            <p><strong>Carga Kekis:</strong> <span id="verCargaKekis"></span></p>
            <p><strong>Carga Bolillo:</strong> <span id="verCargaBolillo"></span></p>
            <p><strong>Venta Aproximada:</strong> <span id="verVentaAproximada"></span></p>
        </section>

        <section id="corteCajaSection">
            <h2>Corte de Caja al Regreso</h2>

            <form id="corteCajaForm">
                <label for="fechaCorte">Fecha del Corte:</label>
                <input type="date" id="fechaCorte" required>

                <label for="efectivoEntregado">Efectivo Entregado:</label>
                <input type="number" id="efectivoEntregado" value="0" min="0" required>

                <label for="sobroPan">Bolsas de Pan Sobrantes:</label>
                <input type="number" id="sobroPan" value="0" min="0" required>
                 <label for="mermaPan">Merma Pan:</label>
                <input type="number" id="mermaPan" value="0" min="0">

                <label for="sobroGalletasLeche">Paquetes de Galletas de Leche Sobrantes:</label>
                <input type="number" id="sobroGalletasLeche" value="0" min="0" required>
                 <label for="mermaGalletasLeche">Merma Galletas Leche:</label>
                <input type="number" id="mermaGalletasLeche" value="0" min="0">

                <label for="sobroKekis">Paquetes de Kekis Sobrantes:</label>
                <input type="number" id="sobroKekis" value="0" min="0" required>
                 <label for="mermaKekis">Merma Kekis:</label>
                <input type="number" id="mermaKekis" value="0" min="0">

                <label for="sobroBolillo">Bolillos Sobrantes:</label>
                <input type="number" id="sobroBolillo" value="0" min="0" required>
                 <label for="mermaBolillo">Merma Bolillo:</label>
                <input type="number" id="mermaBolillo" value="0" min="0">

                <label for="merma">Merma/Cambio (Descripción):</label>
                <textarea id="merma" rows="3" cols="30"></textarea>

                <label for="gastosRuta">Gastos en Ruta:</label>
                <input type="number" id="gastosRuta" value="0" min="0">

                <label for="descripcionGastos">Descripción de Gastos:</label>
                <textarea id="descripcionGastos" rows="3" cols="30"></textarea>

                <button type="button" onclick="realizarCorte()">Realizar Corte</button>
                <button type="button" onclick="imprimirCorte()">Imprimir Corte (PDF)</button>
            </form>

            <div id="resultadosCorte">
                <p id="totalVentas">Total de Ventas: $0.00</p>
                <p id="comisionPan">Comisión Pan: $0.00</p>
                <p id="comisionGalletasLeche">Comisión Galletas de Leche: $0.00</p>
                <p id="comisionKekis">Comisión Kekis: $0.00</p>
                 <p id="comisionBolillo">Comisión Bolillo: $0.00</p>
                <p id="comisionTotal">Comisión Total: $0.00</p>
                <p id="dineroEntregar">Dinero a Entregar: $0.00</p>
            </div>
            <div id="faltanteDinero" style="color: red; font-weight: bold;"></div>
            <div id="corteCajaMensajes"></div>
        </section>

        <section id="historialSection">
            <h2>Historial de Rutas</h2>

            <table id="tablaHistorial">
                <thead>
                    <tr>
                        <th>Fecha Carga</th>
                        <th>Ruta</th>
                        <th>Carga Pan</th>
                        <th>Carga Galletas Leche</th>
                        <th>Carga Kekis</th>
                         <th>Carga Bolillo</th>
                        <th>Ventas Proyectadas</th>
                        <th>Fecha Corte</th>
                        <th>Ventas Pan</th>
                        <th>Ventas Galletas Leche</th>
                        <th>Ventas Kekis</th>
                         <th>Ventas Bolillo</th>
                        <th>Efectivo</th>
                        <th>Sobro Pan</th>
                         <th>Merma Pan</th>
                        <th>Sobro Galletas Leche</th>
                         <th>Merma Galletas Leche</th>
                        <th>Sobro Kekis</th>
                         <th>Merma Kekis</th>
                          <th>Sobro Bolillo</th>
                         <th>Merma Bolillo</th>
                        <th>Merma</th>
                        <th>Gastos Ruta</th>
                        <th>Descripción Gastos</th>
                        <th>Comisión Pan</th>
                        <th>Comisión Galletas Leche</th>
                        <th>Comisión Kekis</th>
                         <th>Comisión Bolillo</th>
                        <th>Comisión Total</th>
                        <th>Dinero a Entregar</th>
                        <th>Faltante</th>
                        <th>Descargar PDF</th>
                    </tr>
                </thead>
                <tbody></tbody>
            </table>
        </section>
    </main>

    <footer>
        <p>© 2024 Control de Ruta - Panadería</p>
    </footer>

    <script src="script.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
</body>
</html>
