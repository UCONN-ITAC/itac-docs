---
hide:
  - toc
---

# MEASUR Setup and Weekly Power Analysis

This page provides tools for analyzing compressed air system power consumption patterns to identify operating schedules and calculate average demand profiles.

---

## Weekly Power Pattern Analyzer

This calculator analyzes compressed air power consumption by day of week and hour of day to identify operational patterns. Upload current monitoring data to visualize daily schedules and calculate average hourly demand profiles.

<div id="weekly-analyzer" style="max-width: 1200px; margin: 20px auto; padding: 20px; border: 1px solid #ddd; border-radius: 8px; background: var(--md-code-bg-color);">

<h3>Step 1: Upload CSV File</h3>

<div style="margin: 15px 0;">
    <p style="font-size: 0.9em; color: var(--md-default-fg-color--light); margin-bottom: 10px;">
        Upload a CSV file containing a date-time column and a current (amps) column. You will select which columns to use after loading.
    </p>
    <input type="file" id="csvFileInput" accept=".csv" style="padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
    <button onclick="loadCSV()" style="margin-left: 10px; padding: 8px 16px; background: #4051b5; color: white; border: none; border-radius: 4px; cursor: pointer;">Load Data</button>
</div>

<div id="fileInfo" style="margin: 10px 0; font-size: 0.9em; color: var(--md-default-fg-color--light);"></div>

<div id="columnSelection" style="margin: 15px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px; display: none;">
    <h4 style="margin-top: 0;">Step 1b: Select Columns</h4>
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
        <div>
            <label for="dateTimeColSelect" style="display: block; margin-bottom: 5px; font-weight: 500;">Date-Time Column:</label>
            <select id="dateTimeColSelect" onchange="updateDateRangePreview()" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;"></select>
        </div>
        <div>
            <label for="currentColSelect" style="display: block; margin-bottom: 5px; font-weight: 500;">Current (Amps) Column:</label>
            <select id="currentColSelect" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;"></select>
        </div>
    </div>
</div>

<h3>Step 2: Enter System Parameters</h3>

<div style="margin: 15px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px;">
    <div style="display: grid; grid-template-columns: 1fr 1fr; gap: 15px;">
        <div>
            <label for="systemVoltage" style="display: block; margin-bottom: 5px; font-weight: 500;">System Voltage (V):</label>
            <input type="number" id="systemVoltage" placeholder="480" step="1" value="480" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Common: 208V, 240V, 480V, 600V</p>
        </div>
        <div>
            <label for="powerFactor" style="display: block; margin-bottom: 5px; font-weight: 500;">Power Factor:</label>
            <input type="number" id="powerFactor" placeholder="0.85" step="0.01" min="0" max="1" value="0.85" style="width: 100%; padding: 8px; border: 1px solid #ccc; border-radius: 4px; background: white; color: black;">
            <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 5px;">Typical range: 0.80-0.95</p>
        </div>
    </div>
</div>

<h3>Step 3: Analyze Weekly Patterns</h3>

<div style="margin: 15px 0;">
    <button onclick="analyzeWeeklyPattern()" style="padding: 12px 24px; background: #4051b5; color: white; border: none; border-radius: 4px; cursor: pointer; font-size: 1.1em; font-weight: 500;">Analyze Weekly Pattern</button>
</div>

<div id="weeklyChart" style="margin: 20px 0; height: 500px; display: none;"></div>

<div id="calendarHeatmap" style="margin: 20px 0; height: 400px; display: none;"></div>

<div id="daySelection" style="margin: 20px 0; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px; display: none;">
    <h3>Step 4: Select Operating Days</h3>
    <p style="font-size: 0.9em; color: var(--md-default-fg-color--light); margin-bottom: 15px;">
        Select which days represent normal operating conditions:
    </p>
    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(120px, 1fr)); gap: 10px; margin: 15px 0;">
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-0" value="0" checked style="margin-right: 8px;">
            <span>Sunday</span>
        </label>
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-1" value="1" checked style="margin-right: 8px;">
            <span>Monday</span>
        </label>
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-2" value="2" checked style="margin-right: 8px;">
            <span>Tuesday</span>
        </label>
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-3" value="3" checked style="margin-right: 8px;">
            <span>Wednesday</span>
        </label>
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-4" value="4" checked style="margin-right: 8px;">
            <span>Thursday</span>
        </label>
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-5" value="5" checked style="margin-right: 8px;">
            <span>Friday</span>
        </label>
        <label style="display: flex; align-items: center; padding: 10px; background: var(--md-code-bg-color); border-radius: 4px; cursor: pointer;">
            <input type="checkbox" id="day-6" value="6" checked style="margin-right: 8px;">
            <span>Saturday</span>
        </label>
    </div>
    <button onclick="calculateAverageProfile()" style="margin-top: 15px; padding: 10px 20px; background: #4caf50; color: white; border: none; border-radius: 4px; cursor: pointer; font-weight: 500;">Calculate Average Profile</button>
</div>

<div id="averageResults" style="margin: 20px 0; padding: 20px; background: var(--md-default-bg-color); border-radius: 6px; display: none;">
    <h3 style="margin-top: 0; color: #4caf50;">Average Hourly Power Profile</h3>
    <div id="averageResultsContent"></div>
</div>

<div id="averageChart" style="margin: 20px 0; height: 400px; display: none;"></div>

</div>

<script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>

<script>
let csvData = [];
let headers = [];
let hourlyByDayData = null;

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

    // Populate column selectors, defaulting to column 2 (datetime) and column 3 (current)
    const dateTimeSelect = document.getElementById('dateTimeColSelect');
    const currentSelect = document.getElementById('currentColSelect');
    dateTimeSelect.innerHTML = '';
    currentSelect.innerHTML = '';
    headers.forEach((header, index) => {
        const opt1 = document.createElement('option');
        opt1.value = header; opt1.text = header;
        if (index === 1) opt1.selected = true;
        dateTimeSelect.appendChild(opt1);

        const opt2 = document.createElement('option');
        opt2.value = header; opt2.text = header;
        if (index === 2) opt2.selected = true;
        currentSelect.appendChild(opt2);
    });

    document.getElementById('columnSelection').style.display = 'block';
    document.getElementById('fileInfo').innerHTML = `<strong>✓ File loaded:</strong> ${csvData.length} data points`;
    updateDateRangePreview();
}

function updateDateRangePreview() {
    const dateTimeCol = document.getElementById('dateTimeColSelect').value;
    try {
        const dates = csvData
            .map(row => parseDateString(row[dateTimeCol]))
            .filter(d => !isNaN(d.getTime()));

        if (dates.length === 0) {
            document.getElementById('fileInfo').innerHTML =
                `<strong>✓ File loaded:</strong> ${csvData.length} data points<br>` +
                `<span style="color: #e74c3c;">⚠ Could not parse dates from the selected column — check that the correct column is chosen.</span>`;
            return;
        }

        const timestamps = dates.map(d => d.getTime());
        const minDate = new Date(Math.min(...timestamps));
        const maxDate = new Date(Math.max(...timestamps));
        const durationDays = (maxDate - minDate) / (1000 * 60 * 60 * 24);

        document.getElementById('fileInfo').innerHTML =
            `<strong>✓ File loaded:</strong> ${csvData.length} data points<br>` +
            `<strong>Date Range:</strong> ${minDate.toLocaleDateString()} to ${maxDate.toLocaleDateString()} (${durationDays.toFixed(1)} days)`;
    } catch (error) {
        console.error('Error parsing dates:', error);
    }
}

function parseDateString(dateStr) {
    if (!dateStr || dateStr.trim() === '') return new Date(NaN);
    dateStr = dateStr.trim();

    // M/D/YYYY H:MM[:SS] — common US data logger format (e.g. 1/15/2026 14:04)
    let m = dateStr.match(/^(\d{1,2})\/(\d{1,2})\/(\d{4})\s+(\d{1,2}):(\d{2})(?::(\d{2}))?/);
    if (m) return new Date(+m[3], +m[1]-1, +m[2], +m[4], +m[5], +(m[6]||0));

    // YYYY-MM-DD[THH:MM[:SS]] — ISO 8601 / Excel export
    m = dateStr.match(/^(\d{4})[-\/](\d{1,2})[-\/](\d{1,2})(?:[T\s](\d{1,2}):(\d{2})(?::(\d{2}))?)?/);
    if (m) return new Date(+m[1], +m[2]-1, +m[3], +(m[4]||0), +(m[5]||0), +(m[6]||0));

    // D-Mon-YYYY HH:MM[:SS] — e.g. 15-Jan-2026 14:04
    const months = {jan:0,feb:1,mar:2,apr:3,may:4,jun:5,jul:6,aug:7,sep:8,oct:9,nov:10,dec:11};
    m = dateStr.match(/^(\d{1,2})-([A-Za-z]{3})-(\d{4})(?:\s+(\d{1,2}):(\d{2})(?::(\d{2}))?)?/);
    if (m && months[m[2].toLowerCase()] !== undefined)
        return new Date(+m[3], months[m[2].toLowerCase()], +m[1], +(m[4]||0), +(m[5]||0), +(m[6]||0));

    // Fallback: native browser Date parsing (handles RFC 2822, full ISO 8601, etc.)
    return new Date(dateStr);
}

function analyzeWeeklyPattern() {
    if (csvData.length === 0) {
        alert('Please load a CSV file first');
        return;
    }

    const voltage = parseFloat(document.getElementById('systemVoltage').value);
    const powerFactor = parseFloat(document.getElementById('powerFactor').value);

    if (isNaN(voltage) || voltage <= 0) {
        alert('Please enter a valid system voltage');
        return;
    }

    if (isNaN(powerFactor) || powerFactor <= 0 || powerFactor > 1) {
        alert('Please enter a valid power factor (0-1)');
        return;
    }

    const dateTimeCol = document.getElementById('dateTimeColSelect').value;
    const currentCol = document.getElementById('currentColSelect').value;

    if (!dateTimeCol || !currentCol) {
        alert('Please load a CSV file and select columns first');
        return;
    }

    // Initialize data structure: [day of week][hour] = array of power values
    hourlyByDayData = {};
    for (let day = 0; day < 7; day++) {
        hourlyByDayData[day] = {};
        for (let hour = 0; hour < 24; hour++) {
            hourlyByDayData[day][hour] = [];
        }
    }

    // Group data by day of week and hour
    csvData.forEach(row => {
        const date = parseDateString(row[dateTimeCol]);
        const current = parseFloat(row[currentCol]);

        if (!isNaN(current)) {
            const power = Math.sqrt(3) * voltage * current * powerFactor / 1000; // kW
            const dayOfWeek = date.getDay(); // 0 = Sunday, 6 = Saturday
            const hour = date.getHours();

            hourlyByDayData[dayOfWeek][hour].push(power);
        }
    });

    // Calculate averages for each day/hour combination
    const traces = [];
    const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const colors = ['#e74c3c', '#3498db', '#2ecc71', '#f39c12', '#9b59b6', '#1abc9c', '#34495e'];

    for (let day = 0; day < 7; day++) {
        const hours = [];
        const avgPowers = [];

        for (let hour = 0; hour < 24; hour++) {
            const values = hourlyByDayData[day][hour];
            if (values.length > 0) {
                const avg = values.reduce((a, b) => a + b, 0) / values.length;
                hours.push(hour);
                avgPowers.push(avg);
            } else {
                hours.push(hour);
                avgPowers.push(0);
            }
        }

        traces.push({
            x: hours,
            y: avgPowers,
            type: 'scatter',
            mode: 'lines+markers',
            name: dayNames[day],
            line: { color: colors[day], width: 2 },
            marker: { size: 4 }
        });
    }

    const layout = {
        title: 'Average Power by Day of Week and Hour',
        xaxis: {
            title: 'Hour of Day',
            dtick: 2,
            range: [0, 23]
        },
        yaxis: {
            title: 'Average Power (kW)',
            rangemode: 'tozero'
        },
        hovermode: 'x unified',
        legend: {
            orientation: 'h',
            y: -0.2
        },
        paper_bgcolor: 'rgba(0,0,0,0)',
        plot_bgcolor: 'rgba(0,0,0,0)',
        font: {color: getComputedStyle(document.body).getPropertyValue('--md-default-fg-color')},
        margin: {t: 50, b: 100, l: 60, r: 20}
    };

    const config = {responsive: true, displayModeBar: true};

    document.getElementById('weeklyChart').style.display = 'block';
    Plotly.newPlot('weeklyChart', traces, layout, config);

    // Create calendar heatmap
    createCalendarHeatmap(voltage, powerFactor, dateTimeCol, currentCol);

    // Show day selection section
    document.getElementById('daySelection').style.display = 'block';
}

function createCalendarHeatmap(voltage, powerFactor, dateTimeCol, currentCol) {
    // Calculate daily power statistics by day of week
    const dayOfWeekData = {};
    for (let day = 0; day < 7; day++) {
        dayOfWeekData[day] = [];
    }

    // Group daily averages by day of week
    const dailyAverages = {};

    csvData.forEach(row => {
        const date = parseDateString(row[dateTimeCol]);
        const current = parseFloat(row[currentCol]);

        if (!isNaN(current)) {
            const power = Math.sqrt(3) * voltage * current * powerFactor / 1000; // kW
            const dateKey = date.toISOString().split('T')[0]; // YYYY-MM-DD

            if (!dailyAverages[dateKey]) {
                dailyAverages[dateKey] = {
                    powers: [],
                    dayOfWeek: date.getDay()
                };
            }
            dailyAverages[dateKey].powers.push(power);
        }
    });

    // Calculate average power for each date and group by day of week
    Object.keys(dailyAverages).forEach(dateKey => {
        const data = dailyAverages[dateKey];
        const avgPower = data.powers.reduce((a, b) => a + b, 0) / data.powers.length;
        dayOfWeekData[data.dayOfWeek].push(avgPower);
    });

    // Calculate min, mean, max for each day of week
    const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const minPowers = [];
    const meanPowers = [];
    const maxPowers = [];

    for (let day = 0; day < 7; day++) {
        const powers = dayOfWeekData[day];
        if (powers.length > 0) {
            minPowers.push(Math.min(...powers));
            meanPowers.push(powers.reduce((a, b) => a + b, 0) / powers.length);
            maxPowers.push(Math.max(...powers));
        } else {
            minPowers.push(0);
            meanPowers.push(0);
            maxPowers.push(0);
        }
    }

    // Create traces
    const traces = [
        {
            x: dayNames,
            y: maxPowers,
            type: 'scatter',
            mode: 'lines+markers',
            name: 'Max',
            line: { color: '#e74c3c', width: 2 },
            marker: { size: 6 }
        },
        {
            x: dayNames,
            y: meanPowers,
            type: 'scatter',
            mode: 'lines+markers',
            name: 'Mean',
            line: { color: '#3498db', width: 3 },
            marker: { size: 8 }
        },
        {
            x: dayNames,
            y: minPowers,
            type: 'scatter',
            mode: 'lines+markers',
            name: 'Min',
            line: { color: '#2ecc71', width: 2 },
            marker: { size: 6 }
        }
    ];

    const layout = {
        title: 'Daily Average Power Statistics by Day of Week',
        xaxis: {
            title: 'Day of Week'
        },
        yaxis: {
            title: 'Average Power (kW)',
            rangemode: 'tozero'
        },
        hovermode: 'x unified',
        paper_bgcolor: 'rgba(0,0,0,0)',
        plot_bgcolor: 'rgba(0,0,0,0)',
        font: {color: getComputedStyle(document.body).getPropertyValue('--md-default-fg-color')},
        margin: {t: 50, b: 50, l: 60, r: 20},
        legend: {
            orientation: 'h',
            y: -0.15
        }
    };

    const config = {responsive: true, displayModeBar: true};

    document.getElementById('calendarHeatmap').style.display = 'block';
    Plotly.newPlot('calendarHeatmap', traces, layout, config);
}

function calculateAverageProfile() {
    if (!hourlyByDayData) {
        alert('Please analyze weekly pattern first');
        return;
    }

    // Get selected days
    const selectedDays = [];
    for (let day = 0; day < 7; day++) {
        const checkbox = document.getElementById(`day-${day}`);
        if (checkbox && checkbox.checked) {
            selectedDays.push(day);
        }
    }

    if (selectedDays.length === 0) {
        alert('Please select at least one operating day');
        return;
    }

    // Calculate average across selected days for each hour
    const hourlyAverages = [];
    for (let hour = 0; hour < 24; hour++) {
        let allValues = [];
        selectedDays.forEach(day => {
            allValues = allValues.concat(hourlyByDayData[day][hour]);
        });

        const avg = allValues.length > 0
            ? allValues.reduce((a, b) => a + b, 0) / allValues.length
            : 0;

        hourlyAverages.push({
            hour: hour,
            avgPower: avg,
            sampleCount: allValues.length
        });
    }

    // Display results table
    const dayNames = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const selectedDayNames = selectedDays.map(d => dayNames[d]).join(', ');

    let tableHTML = `
        <p style="margin-bottom: 15px;"><strong>Selected Days:</strong> ${selectedDayNames}</p>
        <table style="width: 100%; border-collapse: collapse; margin: 10px 0;">
            <tr style="background: var(--md-code-bg-color); border-bottom: 2px solid var(--md-default-fg-color--lightest);">
                <th style="padding: 8px; text-align: left;">Hour</th>
                <th style="padding: 8px; text-align: right;">Average Power (kW)</th>
                <th style="padding: 8px; text-align: right;">Sample Count</th>
            </tr>
    `;

    hourlyAverages.forEach(data => {
        tableHTML += `
            <tr style="border-bottom: 1px solid var(--md-default-fg-color--lightest);">
                <td style="padding: 8px;">${data.hour}:00 - ${data.hour}:59</td>
                <td style="padding: 8px; text-align: right;">${data.avgPower.toFixed(2)}</td>
                <td style="padding: 8px; text-align: right;">${data.sampleCount}</td>
            </tr>
        `;
    });

    const totalAvg = hourlyAverages.reduce((sum, d) => sum + d.avgPower, 0) / 24;
    tableHTML += `
        <tr style="border-top: 2px solid var(--md-default-fg-color--lightest); font-weight: bold;">
            <td style="padding: 8px;">24-Hour Average</td>
            <td style="padding: 8px; text-align: right;">${totalAvg.toFixed(2)}</td>
            <td style="padding: 8px; text-align: right;">--</td>
        </tr>
    `;

    tableHTML += '</table>';

    document.getElementById('averageResultsContent').innerHTML = tableHTML;
    document.getElementById('averageResults').style.display = 'block';

    // Plot average profile
    const trace = {
        x: hourlyAverages.map(d => d.hour),
        y: hourlyAverages.map(d => d.avgPower),
        type: 'scatter',
        mode: 'lines+markers',
        fill: 'tozeroy',
        line: { color: '#4051b5', width: 3 },
        marker: { size: 6, color: '#4051b5' },
        name: 'Average Power'
    };

    const layout = {
        title: `Average Hourly Profile (${selectedDayNames})`,
        xaxis: {
            title: 'Hour of Day',
            dtick: 2,
            range: [0, 23]
        },
        yaxis: {
            title: 'Average Power (kW)',
            rangemode: 'tozero'
        },
        paper_bgcolor: 'rgba(0,0,0,0)',
        plot_bgcolor: 'rgba(0,0,0,0)',
        font: {color: getComputedStyle(document.body).getPropertyValue('--md-default-fg-color')},
        margin: {t: 50, b: 50, l: 60, r: 20},
        showlegend: false
    };

    const config = {responsive: true, displayModeBar: true};

    document.getElementById('averageChart').style.display = 'block';
    Plotly.newPlot('averageChart', [trace], layout, config);
}
</script>