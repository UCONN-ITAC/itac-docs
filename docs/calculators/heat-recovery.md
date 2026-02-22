---
hide:
  - toc
---

# Compressor Heat Recovery Calculator

Use this calculator to estimate energy and cost savings from implementing compressor heat recovery. Enter your compressor and heating system parameters to see the annual fuel savings analysis.

<div id="heat-recovery-calculator" style="max-width: 1200px; margin: 20px auto; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">

<h3>Compressor Parameters</h3>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="motorPower" style="display: block; margin-bottom: 5px; font-weight: 500;">Compressor Motor Power:</label>
        <div style="display: flex; gap: 10px;">
            <input type="number" id="motorPower" value="100" step="1" style="flex: 1; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
            <select id="powerUnit" onchange="hrCalculate()" style="padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
                <option value="hp">HP</option>
                <option value="kw">kW</option>
            </select>
        </div>
    </div>
    <div>
        <label for="compressorType" style="display: block; margin-bottom: 5px; font-weight: 500;">Compressor Type:</label>
        <select id="compressorType" onchange="hrUpdateRejectionFactor()" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
            <option value="rotary-screw">Lubricant-Injected Rotary Screw (Air-Cooled)</option>
            <option value="oil-free">Oil-Free Rotary Screw</option>
            <option value="reciprocating">Reciprocating (Air-Cooled)</option>
            <option value="centrifugal">Centrifugal</option>
        </select>
    </div>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="rejectionFactor" style="display: block; margin-bottom: 5px; font-weight: 500;">Heat Rejection Factor:</label>
        <input type="number" id="rejectionFactor" value="0.85" step="0.01" min="0" max="1" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Fraction of input energy rejected as recoverable heat (auto-filled from compressor type)</p>
    </div>
    <div>
        <label for="annualCompressorHours" style="display: block; margin-bottom: 5px; font-weight: 500;">Annual Compressor Operating Hours:</label>
        <input type="number" id="annualCompressorHours" value="8760" step="1" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Total loaded hours compressor runs per year </p>
    </div>
</div>

<h3 style="margin-top: 30px;">Heating System Parameters</h3>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="fuelType" style="display: block; margin-bottom: 5px; font-weight: 500;">Heating Fuel Type:</label>
        <select id="fuelType" onchange="hrUpdateFuelDefaults()" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
            <option value="natural-gas">Natural Gas (MMBtu)</option>
            <option value="propane">Propane (MMBtu)</option>
            <option value="fuel-oil">No. 2 Fuel Oil (MMBtu)</option>
            <option value="electric">Electric Resistance (kWh)</option>
        </select>
    </div>
    <div>
        <label for="heatingEfficiency" style="display: block; margin-bottom: 5px; font-weight: 500;">Heating System Efficiency (%):</label>
        <input type="number" id="heatingEfficiency" value="85" step="1" min="1" max="100" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="fuelCost" style="display: block; margin-bottom: 5px; font-weight: 500;">Fuel Cost ($ per unit):</label>
        <input type="number" id="fuelCost" value="15.00" step="0.01" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;" id="fuelCostLabel">$/MMBtu for natural gas</p>
    </div>
    <div>
        <label for="fuelHoC" style="display: block; margin-bottom: 5px; font-weight: 500;">Heat of Combustion (Btu/unit):</label>
        <input type="number" id="fuelHoC" value="1000000" step="100" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;" id="fuelHoCLabel">1,000,000 Btu/MMBtu (by definition)</p>
    </div>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 20px 0;">
    <div>
        <label for="heatingMonths" style="display: block; margin-bottom: 5px; font-weight: 500;">Number of Heating Months per Year:</label>
        <input type="number" id="heatingMonths" value="6" step="1" min="1" max="12" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Months per year with heating demand (typically 5 to 8 in northern climates)</p>
    </div>
    <div id="demandRateSection" style="display: none;">
        <label for="hrDemandRate" style="display: block; margin-bottom: 5px; font-weight: 500;">Demand Rate ($/kW-month):</label>
        <input type="number" id="hrDemandRate" value="8.50" step="0.01" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Monthly demand charge per kW of peak demand</p>
    </div>
</div>

<h3 style="margin-top: 30px;">Results Summary</h3>

<div id="hrResults" style="margin: 20px 0; padding: 20px; background: var(--md-default-bg-color); border-radius: 6px; border: 1px solid var(--md-default-fg-color--lightest);">
    <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; margin-bottom: 20px;">
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Motor Input Power:</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="hrMotorPowerResult">254,500 Btu/hr</p>
        </div>
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Recoverable Heat (at full load):</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="hrRecoverableResult">216,325 Btu/hr</p>
        </div>
        <div>
            <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.9em;">Heating Season Hours:</p>
            <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em;" id="hrHeatingHoursResult">4,380 hrs</p>
        </div>
    </div>

    <div style="margin-top: 30px; padding: 20px; background: rgba(76, 175, 80, 0.1); border: 1px solid rgba(76, 175, 80, 0.3); border-radius: 6px;">
        <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; text-align: center;">
            <div>
                <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Annual Heat Recovered</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="hrAnnualHeatResult">0 MMBtu</p>
            </div>
            <div>
                <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Annual Fuel Displaced</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="hrFuelDisplacedResult">0 MMBtu</p>
            </div>
            <div>
                <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Annual Energy Cost Savings</p>
                <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="hrEnergyCostResult">$0</p>
            </div>
        </div>

        <div id="hrDemandResultsRow" style="display: none; margin-top: 20px; padding-top: 15px; border-top: 1px solid rgba(76, 175, 80, 0.3);">
            <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 20px; text-align: center;">
                <div>
                    <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Demand Reduction</p>
                    <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="hrKwResult">0 kW</p>
                </div>
                <div>
                    <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Demand Savings</p>
                    <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="hrKwMonthsResult">0 kW-mo</p>
                    <p style="margin: 5px 0; font-family: monospace; font-size: 1.1em; color: #4caf50;" id="hrDemandCostResult">$0</p>
                </div>
                <div>
                    <p style="margin: 5px 0; color: var(--md-default-fg-color--light); font-size: 0.85em; text-transform: uppercase; letter-spacing: 0.5px;">Total Annual Savings</p>
                    <p style="margin: 5px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: #4caf50;" id="hrTotalCostResult">$0</p>
                </div>
            </div>
        </div>
    </div>
</div>

<div style="margin-top: 20px;">
    <button onclick="hrToggleLatex()" id="hrLatexToggle" style="padding: 10px 20px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color); margin-right: 10px;">Show LaTeX Table</button>
    <button onclick="hrCopyLatex()" id="hrCopyButton" style="padding: 10px 20px; background: var(--md-primary-fg-color); color: white; border: none; border-radius: 4px; cursor: pointer; display: none;">Copy to Clipboard</button>
</div>

<div id="hrLatexContent" style="display: none; margin-top: 15px; padding: 15px; background: var(--md-code-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; overflow-x: auto;">
    <pre id="hrLatexCode" style="margin: 0; font-family: monospace; font-size: 0.75em; color: var(--md-default-fg-color--light); white-space: pre;"></pre>
</div>

<div style="margin-top: 20px;">
    <button onclick="hrToggleEquations()" id="hrEquationsToggle" style="padding: 10px 20px; background: var(--md-default-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; cursor: pointer; color: var(--md-default-fg-color); margin-right: 10px;">Show LaTeX Equations</button>
    <button onclick="hrCopyEquations()" id="hrCopyEquationsButton" style="padding: 10px 20px; background: var(--md-primary-fg-color); color: white; border: none; border-radius: 4px; cursor: pointer; display: none;">Copy to Clipboard</button>
</div>

<div id="hrEquationsContent" style="display: none; margin-top: 15px; padding: 15px; background: var(--md-code-bg-color); border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; overflow-x: auto;">
    <pre id="hrEquationsCode" style="margin: 0; font-family: monospace; font-size: 0.75em; color: var(--md-default-fg-color--light); white-space: pre;"></pre>
</div>

</div>

<script>
// Constants
const HR_BTU_PER_HP = 2545;
const HR_BTU_PER_KW = 3412;

const HR_FUEL_DEFAULTS = {
    'natural-gas': { hoc: 1000000, cost: 15.00, efficiency: 85, unit: 'MMBtu', label: '$/MMBtu for natural gas',   hocLabel: '1,000,000 Btu/MMBtu (by definition)' },
    'propane':     { hoc: 1000000, cost: 27.00, efficiency: 85, unit: 'MMBtu', label: '$/MMBtu for propane',       hocLabel: '1,000,000 Btu/MMBtu (by definition)' },
    'fuel-oil':    { hoc: 1000000, cost: 25.00, efficiency: 83, unit: 'MMBtu', label: '$/MMBtu for No. 2 fuel oil', hocLabel: '1,000,000 Btu/MMBtu (by definition)' },
    'electric':    { hoc: 3412,    cost: 0.12,  efficiency: 100, unit: 'kWh',  label: '$/kWh for electric resistance', hocLabel: '3,412 Btu/kWh' }
};

const HR_REJECTION_DEFAULTS = {
    'rotary-screw':  0.85,
    'oil-free':      0.89,
    'reciprocating': 0.60,
    'centrifugal':   0.85
};

function hrUpdateRejectionFactor() {
    const type = document.getElementById('compressorType').value;
    document.getElementById('rejectionFactor').value = HR_REJECTION_DEFAULTS[type];
    hrCalculate();
}

function hrUpdateFuelDefaults() {
    const fuelType = document.getElementById('fuelType').value;
    const defaults = HR_FUEL_DEFAULTS[fuelType];
    document.getElementById('fuelHoC').value = defaults.hoc;
    document.getElementById('fuelCost').value = defaults.cost;
    document.getElementById('heatingEfficiency').value = defaults.efficiency;
    document.getElementById('fuelCostLabel').textContent = defaults.label;
    document.getElementById('fuelHoCLabel').textContent = defaults.hocLabel;

    const isElectric = fuelType === 'electric';
    document.getElementById('demandRateSection').style.display = isElectric ? 'block' : 'none';

    hrCalculate();
}

function hrFormatNumber(num, decimals = 0) {
    return num.toLocaleString('en-US', {
        minimumFractionDigits: decimals,
        maximumFractionDigits: decimals
    });
}

let hrCalculationResults = null;

function hrCalculate() {
    const motorPower = parseFloat(document.getElementById('motorPower').value);
    const powerUnit = document.getElementById('powerUnit').value;
    const rejectionFactor = parseFloat(document.getElementById('rejectionFactor').value);
    const annualHours = parseFloat(document.getElementById('annualCompressorHours').value);
    const fuelType = document.getElementById('fuelType').value;
    const heatingEfficiency = parseFloat(document.getElementById('heatingEfficiency').value) / 100;
    const fuelCost = parseFloat(document.getElementById('fuelCost').value);
    const fuelHoC = parseFloat(document.getElementById('fuelHoC').value);
    const heatingMonths = parseFloat(document.getElementById('heatingMonths').value);

    // Convert motor power to Btu/hr
    let qInput;
    if (powerUnit === 'hp') {
        qInput = motorPower * HR_BTU_PER_HP;
    } else {
        qInput = motorPower * HR_BTU_PER_KW;
    }

    // Recoverable heat at full load (Btu/hr)
    const qRecoverable = qInput * rejectionFactor;

    // Heating season hours
    const heatingHours = annualHours * (heatingMonths / 12);

    // Total heat recovered during heating season (Btu)
    const totalHeatRecovered = qRecoverable * heatingHours;

    // Fuel displaced
    const fuelUnit = HR_FUEL_DEFAULTS[fuelType].unit;
    const fuelDisplaced = totalHeatRecovered / (fuelHoC * heatingEfficiency);

    // Energy cost savings
    const energyCostSavings = fuelDisplaced * fuelCost;

    // Electric demand savings
    const isElectric = fuelType === 'electric';
    let kwReduction = 0;
    let kwMonths = 0;
    let demandCostSavings = 0;
    let totalCostSavings = energyCostSavings;

    if (isElectric) {
        const demandRate = parseFloat(document.getElementById('hrDemandRate').value) || 0;
        kwReduction = qRecoverable / (HR_BTU_PER_KW * heatingEfficiency);
        kwMonths = kwReduction * heatingMonths;
        demandCostSavings = kwMonths * demandRate;
        totalCostSavings = energyCostSavings + demandCostSavings;
    }

    hrCalculationResults = {
        qInput: qInput,
        qRecoverable: qRecoverable,
        heatingHours: heatingHours,
        totalHeatRecovered: totalHeatRecovered,
        fuelDisplaced: fuelDisplaced,
        energyCostSavings: energyCostSavings,
        kwReduction: kwReduction,
        kwMonths: kwMonths,
        demandCostSavings: demandCostSavings,
        totalCostSavings: totalCostSavings,
        fuelUnit: fuelUnit,
        isElectric: isElectric
    };

    // Update summary displays
    document.getElementById('hrMotorPowerResult').textContent = `${hrFormatNumber(qInput)} Btu/hr`;
    document.getElementById('hrRecoverableResult').textContent = `${hrFormatNumber(qRecoverable)} Btu/hr`;
    document.getElementById('hrHeatingHoursResult').textContent = `${hrFormatNumber(heatingHours)} hrs`;
    document.getElementById('hrAnnualHeatResult').textContent = `${hrFormatNumber(totalHeatRecovered / 1e6, 1)} MMBtu`;
    document.getElementById('hrFuelDisplacedResult').textContent = `${hrFormatNumber(fuelDisplaced, 1)} ${fuelUnit}`;
    document.getElementById('hrEnergyCostResult').textContent = `$${hrFormatNumber(energyCostSavings)}`;

    // Electric demand results
    if (isElectric) {
        document.getElementById('hrDemandResultsRow').style.display = 'block';
        document.getElementById('hrKwResult').textContent = `${hrFormatNumber(kwReduction, 1)} kW`;
        document.getElementById('hrKwMonthsResult').textContent = `${hrFormatNumber(kwMonths, 1)} kW-mo`;
        document.getElementById('hrDemandCostResult').textContent = `$${hrFormatNumber(demandCostSavings)}`;
        document.getElementById('hrTotalCostResult').textContent = `$${hrFormatNumber(totalCostSavings)}`;
    } else {
        document.getElementById('hrDemandResultsRow').style.display = 'none';
    }

    // Update LaTeX
    hrGenerateLatex();
}

function hrGenerateLatex() {
    if (!hrCalculationResults) return;

    const motorPower = parseFloat(document.getElementById('motorPower').value);
    const powerUnit = document.getElementById('powerUnit').value;
    const rejectionFactor = parseFloat(document.getElementById('rejectionFactor').value);
    const annualHours = parseFloat(document.getElementById('annualCompressorHours').value);
    const heatingEfficiency = parseFloat(document.getElementById('heatingEfficiency').value);
    const heatingMonths = parseFloat(document.getElementById('heatingMonths').value);
    const fuelCost = parseFloat(document.getElementById('fuelCost').value);

    const { qInput, qRecoverable, heatingHours, totalHeatRecovered, fuelDisplaced, energyCostSavings,
            isElectric, kwReduction, kwMonths, demandCostSavings, totalCostSavings, fuelUnit } = hrCalculationResults;

    const unitLabel = powerUnit === 'hp' ? 'HP' : 'kW';

    let latex = `\\begin{table}[htbp]
\\centering
\\caption{Compressor Heat Recovery Savings Analysis}
\\label{tab:heat-recovery}
\\begin{tabular}{@{}lrl@{}}
\\toprule
Parameter & Value & Unit \\\\
\\midrule
Motor Power & ${hrFormatNumber(motorPower)} & ${unitLabel} \\\\
Heat Input & ${hrFormatNumber(qInput)} & Btu/hr \\\\
Heat Rejection Factor & ${rejectionFactor.toFixed(2)} & \\\\
Recoverable Heat & ${hrFormatNumber(qRecoverable)} & Btu/hr \\\\
Annual Operating Hours & ${hrFormatNumber(annualHours)} & hrs/yr \\\\
Heating Months & ${hrFormatNumber(heatingMonths)} & months/yr \\\\
Heating Season Hours & ${hrFormatNumber(heatingHours)} & hrs/yr \\\\
Annual Heat Recovered & ${hrFormatNumber(totalHeatRecovered / 1e6, 2)} & MMBtu/yr \\\\
Heating System Efficiency & ${heatingEfficiency}\\% & \\\\
Fuel Displaced & ${hrFormatNumber(fuelDisplaced, 1)} & ${fuelUnit}/yr \\\\
Fuel Cost & \\$${fuelCost.toFixed(2)} & /${fuelUnit} \\\\
\\midrule
Energy Cost Savings & \\$${hrFormatNumber(energyCostSavings)} & /yr \\\\`;

    if (isElectric) {
        const demandRate = parseFloat(document.getElementById('hrDemandRate').value) || 0;
        latex += `
Demand Reduction & ${hrFormatNumber(kwReduction, 1)} & kW \\\\
Demand Savings & ${hrFormatNumber(kwMonths, 1)} & kW-months/yr \\\\
Demand Cost Savings & \\$${hrFormatNumber(demandCostSavings)} & /yr \\\\
\\midrule
Total Annual Savings & \\$${hrFormatNumber(totalCostSavings)} & /yr \\\\`;
    }

    latex += `
\\bottomrule
\\end{tabular}
\\end{table}`;

    document.getElementById('hrLatexCode').textContent = latex;
}

function hrToggleLatex() {
    const content = document.getElementById('hrLatexContent');
    const button = document.getElementById('hrLatexToggle');
    const copyButton = document.getElementById('hrCopyButton');

    if (content.style.display === 'none') {
        content.style.display = 'block';
        button.textContent = 'Hide LaTeX Table';
        copyButton.style.display = 'inline-block';
    } else {
        content.style.display = 'none';
        button.textContent = 'Show LaTeX Table';
        copyButton.style.display = 'none';
    }
}

function hrCopyLatex() {
    const latexCode = document.getElementById('hrLatexCode').textContent;
    const btn = document.getElementById('hrCopyButton');

    if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(latexCode).then(() => {
            hrShowCopySuccess(btn);
        }).catch(() => {
            hrFallbackCopy(latexCode, btn);
        });
    } else {
        hrFallbackCopy(latexCode, btn);
    }
}

function hrToggleEquations() {
    const content = document.getElementById('hrEquationsContent');
    const button = document.getElementById('hrEquationsToggle');
    const copyButton = document.getElementById('hrCopyEquationsButton');

    if (content.style.display === 'none') {
        hrGenerateEquationsLatex();
        content.style.display = 'block';
        button.textContent = 'Hide LaTeX Equations';
        copyButton.style.display = 'inline-block';
    } else {
        content.style.display = 'none';
        button.textContent = 'Show LaTeX Equations';
        copyButton.style.display = 'none';
    }
}

function hrGenerateEquationsLatex() {
    if (!hrCalculationResults) {
        document.getElementById('hrEquationsCode').textContent = 'Please run calculations first.';
        return;
    }

    const motorPower = parseFloat(document.getElementById('motorPower').value);
    const powerUnit = document.getElementById('powerUnit').value;
    const rejectionFactor = parseFloat(document.getElementById('rejectionFactor').value);
    const heatingEfficiency = parseFloat(document.getElementById('heatingEfficiency').value) / 100;
    const fuelCost = parseFloat(document.getElementById('fuelCost').value);
    const fuelHoC = parseFloat(document.getElementById('fuelHoC').value);
    const fuelType = document.getElementById('fuelType').value;
    const annualHours = parseFloat(document.getElementById('annualCompressorHours').value);
    const heatingMonths = parseFloat(document.getElementById('heatingMonths').value);

    const { qInput, qRecoverable, heatingHours, totalHeatRecovered, fuelDisplaced,
            energyCostSavings, isElectric, kwReduction, kwMonths, demandCostSavings, totalCostSavings, fuelUnit } = hrCalculationResults;

    const unitLabel = powerUnit === 'hp' ? 'HP' : 'kW';
    const conversionLabel = powerUnit === 'hp' ? '2{,}545' : '3{,}412';

    let latex = `\\section*{Compressor Heat Recovery Savings Calculation}

\\subsection*{System Parameters}

\\begin{itemize}
    \\item Compressor motor power: ${motorPower} ${unitLabel}
    \\item Heat rejection factor: ${rejectionFactor}
    \\item Annual compressor operating hours: ${hrFormatNumber(annualHours)} hours
    \\item Heating months per year: ${heatingMonths}
    \\item Heating fuel type: ${fuelType.replace(/-/g, ' ')}
    \\item Heat of combustion: ${hrFormatNumber(fuelHoC)} Btu/${fuelUnit}
    \\item Heating system efficiency: ${(heatingEfficiency * 100).toFixed(0)}\\%
    \\item Fuel cost: \\$${fuelCost.toFixed(2)}/${fuelUnit}
\\end{itemize}

\\subsection*{Heat Input Calculation}

The total heat equivalent of the electrical input to the compressor is:

\\begin{equation}
Q_{\\text{input}} = P_{\\text{motor}} \\times ${conversionLabel} \\text{ Btu/hr per ${unitLabel}} = ${motorPower} \\times ${conversionLabel} = ${hrFormatNumber(qInput)} \\text{ Btu/hr}
\\label{eq:heat-input}
\\end{equation}

\\subsection*{Recoverable Heat}

The recoverable waste heat at full load is:

\\begin{equation}
Q_{\\text{recoverable}} = Q_{\\text{input}} \\times f_{\\text{rejection}} = ${hrFormatNumber(qInput)} \\times ${rejectionFactor} = ${hrFormatNumber(qRecoverable)} \\text{ Btu/hr}
\\label{eq:recoverable-heat}
\\end{equation}

\\subsection*{Heating Season}

The compressor operating hours during the heating season are:

\\begin{equation}
H_{\\text{heating}} = H_{\\text{annual}} \\times \\frac{N_{\\text{heating}}}{12} = ${hrFormatNumber(annualHours)} \\times \\frac{${heatingMonths}}{12} = ${hrFormatNumber(heatingHours)} \\text{ hours}
\\label{eq:heating-hours}
\\end{equation}

\\subsection*{Displaced Fuel}

The total heat recovered during the heating season is:

\\begin{equation}
Q_{\\text{annual}} = Q_{\\text{recoverable}} \\times H_{\\text{heating}} = ${hrFormatNumber(qRecoverable)} \\times ${hrFormatNumber(heatingHours)} = ${hrFormatNumber(totalHeatRecovered / 1e6, 2)} \\text{ MMBtu}
\\label{eq:annual-heat}
\\end{equation}

The displaced fuel quantity is:

\\begin{equation}
\\text{Fuel Displaced} = \\frac{Q_{\\text{annual}}}{H_c \\times \\eta_{\\text{heating}}} = \\frac{${hrFormatNumber(totalHeatRecovered)}}{${hrFormatNumber(fuelHoC)} \\times ${heatingEfficiency.toFixed(2)}} = ${hrFormatNumber(fuelDisplaced, 1)} \\text{ ${fuelUnit}}
\\label{eq:fuel-displaced}
\\end{equation}

\\subsection*{Annual Savings}

\\begin{equation}
\\begin{split}
\\text{Energy Cost Savings} &= \\text{Fuel Displaced} \\times \\text{Fuel Cost} \\\\
&= ${hrFormatNumber(fuelDisplaced, 1)} \\text{ ${fuelUnit}} \\times \\$${fuelCost.toFixed(2)}\\text{/${fuelUnit}} \\\\
&= \\$${hrFormatNumber(energyCostSavings)}
\\end{split}
\\label{eq:energy-cost}
\\end{equation}`;

    if (isElectric) {
        const demandRate = parseFloat(document.getElementById('hrDemandRate').value) || 0;
        latex += `

\\subsection*{Demand Savings}

The demand reduction from displaced electric resistance heating is:

\\begin{equation}
\\Delta kW = \\frac{Q_{\\text{recoverable}}}{3{,}412 \\times \\eta_{\\text{heating}}} = \\frac{${hrFormatNumber(qRecoverable)}}{3{,}412 \\times ${heatingEfficiency.toFixed(2)}} = ${hrFormatNumber(kwReduction, 1)} \\text{ kW}
\\label{eq:kw-reduction}
\\end{equation}

\\begin{equation}
\\Delta kW\\text{-months} = \\Delta kW \\times N_{\\text{heating}} = ${hrFormatNumber(kwReduction, 1)} \\times ${heatingMonths} = ${hrFormatNumber(kwMonths, 1)} \\text{ kW-months}
\\label{eq:kw-months}
\\end{equation}

\\begin{equation}
\\text{Demand Cost Savings} = \\Delta kW\\text{-months} \\times \\text{Demand Rate} = ${hrFormatNumber(kwMonths, 1)} \\times \\$${demandRate.toFixed(2)} = \\$${hrFormatNumber(demandCostSavings)}
\\label{eq:demand-cost}
\\end{equation}

\\begin{equation}
\\text{Total Annual Savings} = \\$${hrFormatNumber(energyCostSavings)} + \\$${hrFormatNumber(demandCostSavings)} = \\$${hrFormatNumber(totalCostSavings)}
\\label{eq:total-savings}
\\end{equation}`;
    }

    document.getElementById('hrEquationsCode').textContent = latex;
}

function hrCopyEquations() {
    const equationsCode = document.getElementById('hrEquationsCode').textContent;
    const btn = document.getElementById('hrCopyEquationsButton');

    if (navigator.clipboard && window.isSecureContext) {
        navigator.clipboard.writeText(equationsCode).then(() => {
            hrShowCopySuccess(btn);
        }).catch(() => {
            hrFallbackCopy(equationsCode, btn);
        });
    } else {
        hrFallbackCopy(equationsCode, btn);
    }
}

function hrFallbackCopy(text, btn) {
    const textArea = document.createElement('textarea');
    textArea.value = text;
    textArea.style.position = 'fixed';
    textArea.style.left = '-9999px';
    textArea.style.top = '-9999px';
    document.body.appendChild(textArea);
    textArea.focus();
    textArea.select();

    try {
        document.execCommand('copy');
        hrShowCopySuccess(btn);
    } catch (err) {
        btn.textContent = 'Copy failed';
        setTimeout(() => {
            btn.textContent = 'Copy to Clipboard';
        }, 2000);
    }

    document.body.removeChild(textArea);
}

function hrShowCopySuccess(btn) {
    btn.textContent = 'Copied!';
    setTimeout(() => {
        btn.textContent = 'Copy to Clipboard';
    }, 2000);
}

// Initialize calculator on page load
document.addEventListener('DOMContentLoaded', hrCalculate);

// Add event listeners to all inputs
document.querySelectorAll('#heat-recovery-calculator input, #heat-recovery-calculator select').forEach(input => {
    input.addEventListener('change', hrCalculate);
    input.addEventListener('input', hrCalculate);
});
</script>
