# Repair Compressed Air Leaks

Compressed air leaks are a significant source of energy waste in industrial facilities. Leaks occur at connections, fittings, valves, and distribution system components, causing compressors to run more frequently or at higher loads to maintain system pressure. Repairing leaks reduces compressor energy consumption and demand.

**ARC Code(s):** 2.5121

## Leak Rate Determination from Runtime Data

Compressed air leak rates can be determined by analyzing compressor power consumption during non-production hours when production equipment is idle. During these periods, compressor load represents only system leaks and minimal continuous loads. This method requires electrical monitoring data collected over at least one week to capture representative operating patterns.

The methodology differs based on compressor control type:

- **VFD (Variable Frequency Drive) compressors** modulate output continuously, requiring interpolation from power-flow performance curves
- **Non-VFD compressors** operate in discrete states (loaded, unloaded, off), requiring state-based analysis

!!! note "Period Selection Criteria"

    The selected non-production period should be:

    - At least 2-4 hours in duration for stable averaging
    - Free of startup/shutdown transients or maintenance activities
    - Representative of typical non-production conditions
    - At stable system pressure (verify from pressure logs if available)

### VFD Compressor Analysis

VFD compressors vary motor speed to modulate output, creating a continuous relationship between electrical power and air flow. Leak rate is determined by interpolating CFM output from measured power during non-production hours.

Obtain the compressor's power-to-flow relationship from CAGI (Compressed Air and Gas Institute) datasheets or manufacturer performance curves as discrete (kW, CFM) pairs. CAGI datasheets provide standardized performance data at various load points. A minimum of 4-6 data points spanning the operating range is required, with particular attention to the low-power region where leak-only operation typically occurs.

For each power measurement during the non-production period, interpolate the corresponding CFM using linear interpolation between adjacent performance points. Average the interpolated CFM values across all timesteps to obtain the facility leak rate.

### Non-VFD Compressor Analysis

Non-VFD compressors operate in discrete states with fixed power consumption and output at each state. Define three operating states from nameplate data:

- **Loaded**: Motor running at full power producing rated CFM capacity
- **Unloaded**: Motor running at 15-30% of full power with intake closed (typically 0 CFM, but verify with manufacturer documentation)
- **Off**: Motor not running, <5% of full power (parasitic losses only), 0 CFM

Assign power thresholds for each state using hysteresis margins (5-10% of state power) to prevent erratic state switching from measurement noise. For each timestep during the non-production period, assign the measured power to the appropriate state. Calculate the time-weighted average CFM by summing the product of flow and time duration for each timestep, then dividing by total period duration.

!!! warning "Unloaded Flow Verification"

    Most rotary screw and reciprocating compressors produce zero CFM when unloaded (intake valve closed). However, some designs may produce minimal flow in the unloaded state. Consult manufacturer documentation to determine the correct unloaded CFM value. If unknown, assume 0 CFM as a conservative estimate.

## Savings Calculation

Energy savings from compressed air leak repair result from reduced compressor runtime and loading. The calculation uses the facility-specific leak rate determined from runtime analysis and the compressor system's specific power (kW per 100 CFM).

### Annual Energy Savings

Annual energy savings are calculated as:

$$
\Delta E = \frac{Q_{\text{repaired}} \times H \times P_{\text{specific}}}{100}
$$

Where:

- $Q_{\text{repaired}}$ = leak rate repaired (CFM), typically 50-80% of identified leak rate
- $H$ = annual compressor operating hours (hours/year)
- $P_{\text{specific}}$ = specific power of compressed air system (kW per 100 CFM)

Specific power depends on compressor type and operating efficiency. For VFD compressors, calculate from the CAGI datasheet power-flow curve in the operating region. For non-VFD compressors, calculate from loaded state values:

$$
P_{\text{specific}} = \frac{P_{\text{loaded}} \times 100}{Q_{\text{loaded}}}
$$

Important assumptions to state in the analysis:

- Leak repair percentage (50-80% of identified leaks is realistic; 100% repair is rarely achievable)
- Annual operating hours should match actual compressor power-on time (this is often 24/7)

### Peak Demand Savings

Demand savings occur when leak repair reduces compressor loading during facility peak demand periods. Calculate demand savings separately for summer (3 months) and winter (9 months) periods with appropriate coincidence factors:

$$
\Delta kW_{\text{summer}} = \frac{Q_{\text{repaired}} \times P_{\text{specific}}}{100} \times 0.947
$$

$$
\Delta kW_{\text{winter}} = \frac{Q_{\text{repaired}} \times P_{\text{specific}}}{100} \times 0.743
$$

Annual demand savings in kW-months:

$$
\Delta kW\text{-months} = (\Delta kW_{\text{summer}} \times 3) + (\Delta kW_{\text{winter}} \times 9)
$$

Where:

- $\Delta kW_{\text{summer}}$ = summer peak demand reduction with 94.7% coincidence factor
- $\Delta kW_{\text{winter}}$ = winter peak demand reduction with 74.3% coincidence factor
- 3 = number of summer months
- 9 = number of winter months

!!! note "Coincidence Factors"

    The coincidence factors (94.7% for summer, 74.3% for winter) account for the probability that leak-related compressor demand occurs during facility peak demand periods. These values are based on typical industrial compressed air system load profiles.

## Anticipated Costs

Implementation costs for leak repair include ultrasonic leak detection survey costs, repair labor, and replacement components (fittings, valves, hoses, flexible couplings). Survey costs depend on facility size and accessibility. Labor costs vary with leak location, accessibility, and whether repairs require system shutdown. Component costs depend on leak type and size.

Estimate the number of individual leaks from the total leak rate using typical leak sizes. Significant compressed air leaks range from 5-50 CFM each depending on orifice size and system pressure.

Many utilities offer incentives for compressed air leak surveys and leak repair programs. Check with the local utility energy efficiency program for current prescriptive rebates or custom incentive opportunities. Incentive structures typically cover a portion of survey costs and may provide per-CFM payments for verified leak repairs.

Simple payback periods for comprehensive leak repair programs typically range from 6 months to 2 years depending on leak severity, repair costs, and utility incentives.

---

## Interactive Leak Rate Calculator

Use this calculator to automatically determine leak rates from compressor power data. Upload a CSV file with power measurements and configure the analysis parameters. The DateTime should be in the second column and the current should be in the third column. 

<div id="leak-calculator" style="max-width: 1200px; margin: 20px auto; padding: 20px; border: 1px solid #ddd; border-radius: 8px; background: var(--md-code-bg-color);">

<h3>Step 1: Upload CSV File</h3>

<div style="margin: 15px 0;">
    <input type="file" id="csvFileInput" accept=".csv" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
    <button onclick="loadCSV()" style="margin-left: 10px; padding: 8px 16px; background: #4051b5; color: white; border: none; border-radius: 4px; cursor: pointer;">Load Data</button>
</div>

<div id="fileInfo" style="margin: 10px 0; font-size: 0.9em; color: var(--md-default-fg-color--light);"></div>

<h3>Step 2: Enter System Voltage</h3>

<div style="margin: 15px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px;">
    <p style="font-size: 0.9em; color: var(--md-default-fg-color--light); margin-bottom: 10px;">
        Enter the 3-phase system voltage. Power will be calculated as: P = √3 × V × I
    </p>
    <div style="max-width: 300px;">
        <label for="systemVoltage" style="display: block; margin-bottom: 5px; font-weight: 500;">System Voltage (V):</label>
        <input type="number" id="systemVoltage" placeholder="480" step="1" value="480" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Common values: 208V, 240V, 480V, 600V</p>
    </div>
</div>

<div id="powerHistogram" style="margin: 20px 0; height: 300px; display: none;"></div>

<h3>Step 3: Select Control Type and Configure</h3>

<div style="margin: 15px 0;">
    <label style="display: block; margin-bottom: 10px; font-weight: 500;">
        <input type="radio" name="controlType" value="vfd" checked onchange="updateControlTypeUI()"> VFD Compressor
        <input type="radio" name="controlType" value="nonvfd" style="margin-left: 20px;" onchange="updateControlTypeUI()"> Non-VFD Compressor
    </label>
</div>

<div id="vfdConfig" style="margin: 20px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px;">
    <h4 style="margin-top: 0;">VFD Configuration: Power-Flow Data Points</h4>
    <p style="font-size: 0.9em; color: var(--md-default-fg-color--light); margin-bottom: 10px;">
        Enter at least 4 power-flow data points. Click "Add Point" for more rows.
    </p>
    <div id="vfdPointsContainer" style="margin: 10px 0;">
        <div style="display: grid; grid-template-columns: 1fr 1fr 50px; gap: 10px; margin-bottom: 8px; font-weight: 500;">
            <div>Power (kW)</div>
            <div>Flow (CFM)</div>
            <div></div>
        </div>
        <div class="vfd-point" style="display: grid; grid-template-columns: 1fr 1fr 50px; gap: 10px; margin-bottom: 8px;">
            <input type="number" class="vfd-power" placeholder="10" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <input type="number" class="vfd-flow" placeholder="50" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <div></div>
        </div>
        <div class="vfd-point" style="display: grid; grid-template-columns: 1fr 1fr 50px; gap: 10px; margin-bottom: 8px;">
            <input type="number" class="vfd-power" placeholder="40" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <input type="number" class="vfd-flow" placeholder="250" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <div></div>
        </div>
        <div class="vfd-point" style="display: grid; grid-template-columns: 1fr 1fr 50px; gap: 10px; margin-bottom: 8px;">
            <input type="number" class="vfd-power" placeholder="75" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <input type="number" class="vfd-flow" placeholder="475" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <div></div>
        </div>
        <div class="vfd-point" style="display: grid; grid-template-columns: 1fr 1fr 50px; gap: 10px; margin-bottom: 8px;">
            <input type="number" class="vfd-power" placeholder="95" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <input type="number" class="vfd-flow" placeholder="600" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <button onclick="removeVFDPoint(this)" style="padding: 6px; background: #d32f2f; color: white; border: none; border-radius: 4px; cursor: pointer;">✕</button>
        </div>
    </div>
    <button onclick="addVFDPoint()" style="padding: 8px 16px; background: #4caf50; color: white; border: none; border-radius: 4px; cursor: pointer;">+ Add Point</button>
</div>

<div id="nonvfdConfig" style="margin: 20px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px; display: none;">
    <h4 style="margin-top: 0;">Non-VFD Configuration: Operating States</h4>
    <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; margin: 15px 0;">
        <div>
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Loaded Power (kW):</label>
            <input type="number" id="loadedPower" placeholder="100" step="0.1" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
        <div>
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Loaded Flow (CFM):</label>
            <input type="number" id="loadedFlow" placeholder="500" step="0.1" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
        <div>
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Margin (% of loaded):</label>
            <input type="number" id="loadedMargin" placeholder="10" step="1" min="0" max="20" value="10" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
    </div>
    <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; margin: 15px 0;">
        <div>
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Unloaded Power (kW):</label>
            <input type="number" id="unloadedPower" placeholder="25" step="0.1" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
        <div>
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Unloaded Flow (CFM):</label>
            <input type="number" id="unloadedFlow" placeholder="0" step="0.1" value="0" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
        <div>
            <label style="display: block; margin-bottom: 5px; font-weight: 500;">Margin (% of unloaded):</label>
            <input type="number" id="unloadedMargin" placeholder="10" step="1" min="0" max="20" value="10" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
    </div>
</div>

<h3>Step 4: Select Non-Production Period</h3>

<div style="margin: 15px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px;">
    <p style="font-size: 0.9em; color: var(--md-default-fg-color--light); margin-bottom: 10px;">
        Select the start and end of the non-production period to analyze:
    </p>
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
        <div>
            <label for="startTime" style="display: block; margin-bottom: 5px; font-weight: 500;">Start DateTime:</label>
            <input type="datetime-local" id="startTime" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
        <div>
            <label for="endTime" style="display: block; margin-bottom: 5px; font-weight: 500;">End DateTime:</label>
            <input type="datetime-local" id="endTime" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        </div>
    </div>
    <div id="periodInfo" style="margin-top: 10px; font-size: 0.9em; color: var(--md-default-fg-color--light);"></div>
</div>

<h3>Step 5: Calculate Leak Rate</h3>

<div style="margin: 20px 0;">
    <button onclick="calculateLeakRate()" style="padding: 12px 24px; background: #4051b5; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 1.1em; font-weight: 500;">Calculate Leak Rate</button>
</div>

<div id="results" style="margin: 20px 0; padding: 20px; background: var(--md-default-bg-color); border-radius: 6px; display: none;">
    <h3 style="margin-top: 0; color: #4caf50;">Results</h3>
    <div id="resultsContent"></div>
</div>

<div id="powerChart" style="margin: 20px 0; height: 400px; display: none;"></div>

</div>

<script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>

<script>
let csvData = [];
let headers = [];

function updateControlTypeUI() {
    const controlType = document.querySelector('input[name="controlType"]:checked').value;
    document.getElementById('vfdConfig').style.display = controlType === 'vfd' ? 'block' : 'none';
    document.getElementById('nonvfdConfig').style.display = controlType === 'nonvfd' ? 'block' : 'none';
}

function addVFDPoint() {
    const container = document.getElementById('vfdPointsContainer');
    const newPoint = document.createElement('div');
    newPoint.className = 'vfd-point';
    newPoint.style.cssText = 'display: grid; grid-template-columns: 1fr 1fr 50px; gap: 10px; margin-bottom: 8px;';
    newPoint.innerHTML = `
        <input type="number" class="vfd-power" placeholder="kW" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        <input type="number" class="vfd-flow" placeholder="CFM" step="0.1" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
        <button onclick="removeVFDPoint(this)" style="padding: 6px; background: #d32f2f; color: white; border: none; border-radius: 4px; cursor: pointer;">✕</button>
    `;
    container.appendChild(newPoint);
}

function removeVFDPoint(button) {
    const points = document.querySelectorAll('.vfd-point');
    if (points.length > 4) {
        button.parentElement.remove();
    } else {
        alert('Minimum 4 data points required for VFD interpolation');
    }
}

function loadCSV() {
    const fileInput = document.getElementById('csvFileInput');
    const file = fileInput.files[0];

    if (!file) {
        alert('Please select a CSV file');
        return;
    }

    const reader = new FileReader();
    reader.onload = function(e) {
        const text = e.target.result;
        parseCSV(text);
    };
    reader.readAsText(file);
}

function parseCSV(text) {
    const lines = text.split('\n').filter(line => line.trim());
    headers = lines[0].split(',').map(h => h.trim());

    csvData = [];
    for (let i = 1; i < lines.length; i++) {
        const values = lines[i].split(',');
        const row = {};
        headers.forEach((header, index) => {
            row[header] = values[index] ? values[index].trim() : '';
        });
        csvData.push(row);
    }

    // Columns are fixed: column 0 = ID, column 1 = DateTime, column 2 = Current
    const dateTimeCol = headers[1];
    const currentCol = headers[2];

    document.getElementById('fileInfo').innerHTML = `
        <strong>✓ File loaded:</strong> ${csvData.length} data points |
        Timestep: ${calculateTimestep()} minutes<br>
        <strong>DateTime Column:</strong> ${dateTimeCol} | <strong>Current Column:</strong> ${currentCol}
    `;

    // Set default period to full range
    const firstDate = parseDateString(csvData[0][dateTimeCol]);
    const lastDate = parseDateString(csvData[csvData.length - 1][dateTimeCol]);

    document.getElementById('startTime').value = formatDateTimeLocal(firstDate);
    document.getElementById('endTime').value = formatDateTimeLocal(lastDate);

    updatePeriodInfo();

    // Update histogram if voltage is entered
    updatePowerHistogram();
}

function updatePowerHistogram() {
    const voltage = parseFloat(document.getElementById('systemVoltage').value);

    if (csvData.length === 0 || isNaN(voltage) || voltage <= 0) {
        document.getElementById('powerHistogram').style.display = 'none';
        return;
    }

    const currentCol = headers[2];

    // Calculate power for all data points
    const powers = csvData.map(row => {
        const current = parseFloat(row[currentCol]);
        return Math.sqrt(3) * voltage * current / 1000; // kW
    }).filter(p => !isNaN(p));

    if (powers.length === 0) return;

    // Create histogram
    const trace = {
        x: powers,
        type: 'histogram',
        nbinsx: 50,
        marker: {
            color: '#4051b5',
            line: {
                color: '#ffffff',
                width: 1
            }
        },
        name: 'Power Distribution'
    };

    const layout = {
        title: 'Power Distribution (All Data)',
        xaxis: {
            title: 'Power (kW)',
            zeroline: false
        },
        yaxis: {
            title: 'Frequency (count)',
            zeroline: false
        },
        paper_bgcolor: 'rgba(0,0,0,0)',
        plot_bgcolor: 'rgba(0,0,0,0)',
        font: {color: getComputedStyle(document.body).getPropertyValue('--md-default-fg-color')},
        margin: {t: 40, b: 50, l: 60, r: 20},
        showlegend: false
    };

    const config = {responsive: true, displayModeBar: true};

    document.getElementById('powerHistogram').style.display = 'block';
    Plotly.newPlot('powerHistogram', [trace], layout, config);
}

function calculateTimestep() {
    if (csvData.length < 2) return 'unknown';

    const dateTimeCol = headers[1]; // DateTime is always column 1

    const date1 = parseDateString(csvData[0][dateTimeCol]);
    const date2 = parseDateString(csvData[1][dateTimeCol]);

    const diffMinutes = (date2 - date1) / (1000 * 60);
    return Math.round(diffMinutes);
}

function parseDateString(dateStr) {
    // Format: MM/DD/YYYY HH:MM:SS
    const parts = dateStr.split(' ');
    const dateParts = parts[0].split('/');
    const timeParts = parts[1].split(':');

    return new Date(
        parseInt(dateParts[2]),           // year
        parseInt(dateParts[0]) - 1,       // month (0-indexed)
        parseInt(dateParts[1]),           // day
        parseInt(timeParts[0]),           // hours
        parseInt(timeParts[1]),           // minutes
        parseInt(timeParts[2])            // seconds
    );
}

function formatDateTimeLocal(date) {
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, '0');
    const day = String(date.getDate()).padStart(2, '0');
    const hours = String(date.getHours()).padStart(2, '0');
    const minutes = String(date.getMinutes()).padStart(2, '0');

    return `${year}-${month}-${day}T${hours}:${minutes}`;
}

function updatePeriodInfo() {
    const startTime = document.getElementById('startTime').value;
    const endTime = document.getElementById('endTime').value;

    if (startTime && endTime) {
        const start = new Date(startTime);
        const end = new Date(endTime);
        const durationHours = (end - start) / (1000 * 60 * 60);

        document.getElementById('periodInfo').innerHTML = `
            Period duration: ${durationHours.toFixed(1)} hours
        `;
    }
}

// Update period info when times change
document.getElementById('startTime').addEventListener('change', updatePeriodInfo);
document.getElementById('endTime').addEventListener('change', updatePeriodInfo);

// Update histogram when voltage changes
document.getElementById('systemVoltage').addEventListener('input', function() {
    if (csvData.length > 0) {
        updatePowerHistogram();
    }
});

function linearInterpolate(x, xArray, yArray) {
    // Find bracketing points
    let lowerIdx = 0;
    let upperIdx = xArray.length - 1;

    // If x is outside range, use boundary values
    if (x <= xArray[0]) return yArray[0];
    if (x >= xArray[xArray.length - 1]) return yArray[yArray.length - 1];

    // Find bracketing indices
    for (let i = 0; i < xArray.length - 1; i++) {
        if (x >= xArray[i] && x <= xArray[i + 1]) {
            lowerIdx = i;
            upperIdx = i + 1;
            break;
        }
    }

    const x0 = xArray[lowerIdx];
    const x1 = xArray[upperIdx];
    const y0 = yArray[lowerIdx];
    const y1 = yArray[upperIdx];

    return y0 + (x - x0) * (y1 - y0) / (x1 - x0);
}

function calculateLeakRate() {
    // Validate inputs
    if (csvData.length === 0) {
        alert('Please load a CSV file first');
        return;
    }

    const voltage = parseFloat(document.getElementById('systemVoltage').value);
    if (isNaN(voltage) || voltage <= 0) {
        alert('Please enter a valid system voltage');
        return;
    }

    const startTime = new Date(document.getElementById('startTime').value);
    const endTime = new Date(document.getElementById('endTime').value);

    const dateTimeCol = headers[1]; // DateTime is always column 1
    const currentCol = headers[2];  // Current is always column 2

    // Filter data for non-production period and calculate power
    const periodData = csvData.filter(row => {
        const rowDate = parseDateString(row[dateTimeCol]);
        return rowDate >= startTime && rowDate <= endTime;
    }).map(row => {
        const current = parseFloat(row[currentCol]);
        const power = Math.sqrt(3) * voltage * current / 1000; // Convert to kW
        return {
            ...row,
            calculatedPower: power
        };
    });

    if (periodData.length === 0) {
        alert('No data points found in selected period');
        return;
    }

    const controlType = document.querySelector('input[name="controlType"]:checked').value;

    let results;
    if (controlType === 'vfd') {
        results = calculateVFDLeakRate(periodData, voltage);
    } else {
        results = calculateNonVFDLeakRate(periodData, voltage);
    }

    displayResults(results, periodData, dateTimeCol, voltage);
}

function calculateVFDLeakRate(periodData, voltage) {
    // Get VFD performance points
    const vfdPoints = document.querySelectorAll('.vfd-point');
    const powerArray = [];
    const flowArray = [];

    vfdPoints.forEach(point => {
        const power = parseFloat(point.querySelector('.vfd-power').value);
        const flow = parseFloat(point.querySelector('.vfd-flow').value);
        if (!isNaN(power) && !isNaN(flow)) {
            powerArray.push(power);
            flowArray.push(flow);
        }
    });

    if (powerArray.length < 4) {
        alert('Please enter at least 4 VFD performance points');
        return null;
    }

    // Sort arrays by power
    const combined = powerArray.map((p, i) => ({power: p, flow: flowArray[i]}));
    combined.sort((a, b) => a.power - b.power);
    const sortedPower = combined.map(c => c.power);
    const sortedFlow = combined.map(c => c.flow);

    // Interpolate flow for each timestep (using calculated 3-phase power)
    const flows = [];
    const powers = [];

    periodData.forEach(row => {
        const power = row.calculatedPower;
        if (!isNaN(power)) {
            const flow = linearInterpolate(power, sortedPower, sortedFlow);
            flows.push(flow);
            powers.push(power);
        }
    });

    const avgLeakRate = flows.reduce((a, b) => a + b, 0) / flows.length;
    const avgPower = powers.reduce((a, b) => a + b, 0) / powers.length;

    return {
        type: 'VFD',
        leakRate: avgLeakRate,
        avgPower: avgPower,
        dataPoints: periodData.length,
        performancePoints: combined,
        voltage: voltage,
        detailedData: periodData.map((row, i) => ({
            power: powers[i],
            flow: flows[i]
        }))
    };
}

function calculateNonVFDLeakRate(periodData, voltage) {
    // Get non-VFD configuration
    const loadedPower = parseFloat(document.getElementById('loadedPower').value);
    const loadedFlow = parseFloat(document.getElementById('loadedFlow').value);
    const loadedMargin = parseFloat(document.getElementById('loadedMargin').value) / 100;

    const unloadedPower = parseFloat(document.getElementById('unloadedPower').value);
    const unloadedFlow = parseFloat(document.getElementById('unloadedFlow').value);
    const unloadedMargin = parseFloat(document.getElementById('unloadedMargin').value) / 100;

    if (isNaN(loadedPower) || isNaN(loadedFlow) || isNaN(unloadedPower)) {
        alert('Please enter all non-VFD configuration values');
        return null;
    }

    // Calculate thresholds
    const loadedThreshold = loadedPower * (1 - loadedMargin);
    const unloadedThreshold = unloadedPower * (1 - unloadedMargin);

    // Assign states (using calculated 3-phase power)
    let loadedCount = 0, unloadedCount = 0, offCount = 0;
    let totalCFMMinutes = 0;
    const stateData = [];

    periodData.forEach(row => {
        const power = row.calculatedPower;
        if (isNaN(power)) return;

        let state, flow;
        if (power > loadedThreshold) {
            state = 'Loaded';
            flow = loadedFlow;
            loadedCount++;
        } else if (power >= unloadedThreshold) {
            state = 'Unloaded';
            flow = unloadedFlow;
            unloadedCount++;
        } else {
            state = 'Off';
            flow = 0;
            offCount++;
        }

        totalCFMMinutes += flow;
        stateData.push({power, state, flow});
    });

    const totalCount = loadedCount + unloadedCount + offCount;
    const avgLeakRate = totalCFMMinutes / totalCount;

    return {
        type: 'Non-VFD',
        leakRate: avgLeakRate,
        dataPoints: totalCount,
        voltage: voltage,
        states: {
            loaded: {
                count: loadedCount,
                percent: (loadedCount / totalCount * 100).toFixed(1),
                power: loadedPower,
                flow: loadedFlow,
                threshold: loadedThreshold
            },
            unloaded: {
                count: unloadedCount,
                percent: (unloadedCount / totalCount * 100).toFixed(1),
                power: unloadedPower,
                flow: unloadedFlow,
                threshold: unloadedThreshold
            },
            off: {
                count: offCount,
                percent: (offCount / totalCount * 100).toFixed(1)
            }
        },
        detailedData: stateData
    };
}

function displayResults(results, periodData, dateTimeCol, voltage) {
    if (!results) return;

    let html = `
        <div style="margin-bottom: 20px;">
            <h4 style="color: #4caf50; margin-bottom: 10px;">Leak Rate: ${results.leakRate.toFixed(1)} CFM</h4>
            <p style="margin: 5px 0;"><strong>Control Type:</strong> ${results.type}</p>
            <p style="margin: 5px 0;"><strong>System Voltage:</strong> ${voltage} V (3-phase)</p>
            <p style="margin: 5px 0;"><strong>Data Points Analyzed:</strong> ${results.dataPoints}</p>
            <p style="margin: 5px 0;"><strong>Timestep:</strong> ${calculateTimestep()} minutes</p>
        </div>
    `;

    if (results.type === 'VFD') {
        html += `
            <div style="margin: 20px 0;">
                <h4>VFD Performance Points Used:</h4>
                <table style="width: 100%; border-collapse: collapse; margin: 10px 0;">
                    <tr style="background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">
                        <th style="padding: 8px; text-align: left;">Power (kW)</th>
                        <th style="padding: 8px; text-align: left;">Flow (CFM)</th>
                    </tr>
                    ${results.performancePoints.map(p => `
                        <tr style="border-bottom: 1px solid var(--md-default-fg-color--lightest);">
                            <td style="padding: 8px;">${p.power.toFixed(1)}</td>
                            <td style="padding: 8px;">${p.flow.toFixed(1)}</td>
                        </tr>
                    `).join('')}
                </table>
                <p style="margin: 10px 0;"><strong>Average Power During Period:</strong> ${results.avgPower.toFixed(2)} kW</p>
            </div>
        `;
    } else {
        html += `
            <div style="margin: 20px 0;">
                <h4>State Distribution:</h4>
                <table style="width: 100%; border-collapse: collapse; margin: 10px 0;">
                    <tr style="background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">
                        <th style="padding: 8px; text-align: left;">State</th>
                        <th style="padding: 8px; text-align: right;">Count</th>
                        <th style="padding: 8px; text-align: right;">% of Period</th>
                        <th style="padding: 8px; text-align: right;">Power (kW)</th>
                        <th style="padding: 8px; text-align: right;">Flow (CFM)</th>
                    </tr>
                    <tr style="border-bottom: 1px solid var(--md-default-fg-color--lightest);">
                        <td style="padding: 8px;">Loaded</td>
                        <td style="padding: 8px; text-align: right;">${results.states.loaded.count}</td>
                        <td style="padding: 8px; text-align: right;">${results.states.loaded.percent}%</td>
                        <td style="padding: 8px; text-align: right;">${results.states.loaded.power.toFixed(1)}</td>
                        <td style="padding: 8px; text-align: right;">${results.states.loaded.flow.toFixed(1)}</td>
                    </tr>
                    <tr style="border-bottom: 1px solid var(--md-default-fg-color--lightest);">
                        <td style="padding: 8px;">Unloaded</td>
                        <td style="padding: 8px; text-align: right;">${results.states.unloaded.count}</td>
                        <td style="padding: 8px; text-align: right;">${results.states.unloaded.percent}%</td>
                        <td style="padding: 8px; text-align: right;">${results.states.unloaded.power.toFixed(1)}</td>
                        <td style="padding: 8px; text-align: right;">${results.states.unloaded.flow.toFixed(1)}</td>
                    </tr>
                    <tr style="border-bottom: 1px solid var(--md-default-fg-color--lightest);">
                        <td style="padding: 8px;">Off</td>
                        <td style="padding: 8px; text-align: right;">${results.states.off.count}</td>
                        <td style="padding: 8px; text-align: right;">${results.states.off.percent}%</td>
                        <td style="padding: 8px; text-align: right;">~0</td>
                        <td style="padding: 8px; text-align: right;">0</td>
                    </tr>
                </table>
                <p style="margin: 10px 0; font-size: 0.9em; color: var(--md-default-fg-color--light);">
                    <strong>Thresholds:</strong> Loaded >${results.states.loaded.threshold.toFixed(1)} kW |
                    Unloaded ≥${results.states.unloaded.threshold.toFixed(1)} kW
                </p>
            </div>
        `;
    }

    document.getElementById('resultsContent').innerHTML = html;
    document.getElementById('results').style.display = 'block';

    // Create power vs time chart
    plotPowerChart(periodData, dateTimeCol, results);
}

function plotPowerChart(periodData, dateTimeCol, results) {
    const timestamps = periodData.map(row => parseDateString(row[dateTimeCol]));
    const powers = periodData.map(row => row.calculatedPower);

    let traces = [{
        x: timestamps,
        y: powers,
        type: 'scatter',
        mode: 'lines',
        name: 'Compressor Power',
        line: {color: '#4051b5', width: 2}
    }];

    if (results.type === 'VFD') {
        const flows = results.detailedData.map(d => d.flow);
        traces.push({
            x: timestamps,
            y: flows,
            type: 'scatter',
            mode: 'lines',
            name: 'Interpolated Flow',
            line: {color: '#4caf50', width: 2},
            yaxis: 'y2'
        });
    }

    const layout = {
        title: 'Compressor Power During Non-Production Period',
        xaxis: {title: 'Time'},
        yaxis: {title: 'Power (kW)'},
        yaxis2: results.type === 'VFD' ? {
            title: 'Flow (CFM)',
            overlaying: 'y',
            side: 'right'
        } : undefined,
        hovermode: 'x unified',
        paper_bgcolor: 'rgba(0,0,0,0)',
        plot_bgcolor: 'rgba(0,0,0,0)',
        font: {color: getComputedStyle(document.body).getPropertyValue('--md-default-fg-color')},
        margin: {t: 50, b: 50, l: 60, r: results.type === 'VFD' ? 60 : 10}
    };

    const config = {responsive: true, displayModeBar: true};

    document.getElementById('powerChart').style.display = 'block';
    Plotly.newPlot('powerChart', traces, layout, config);
}

// Initialize UI
updateControlTypeUI();
</script>
