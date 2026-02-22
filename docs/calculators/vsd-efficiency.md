---
hide:
  - toc
---

# VSD Isentropic Efficiency Estimator

For VSD compressors, the CAGI datasheet doesn't always report isentropic efficiency. When it does, it reports it at a single test point, which may not represent the typical operating point. Use this calculator to back-calculate isentropic efficiency from measured specific power data.

First, analyze the CT data in order to figure out the average operating power. To do this, average all non-near-zero values. Then, take that power and figure out the corresponding airflow. You will likely need to interpolate.

<div id="vsd-efficiency-calc" style="max-width: 800px; margin: 20px auto; padding: 20px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 8px; background: var(--md-code-bg-color);">

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 15px 0;">
    <div>
        <label for="vsdCfm" style="display: block; margin-bottom: 5px; font-weight: 500;">Measured Flow Rate (CFM):</label>
        <input type="number" id="vsdCfm" value="" step="1" placeholder="e.g. 350" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 4px;">Average non-near-zero flow from CT data</p>
    </div>
    <div>
        <label for="vsdKw" style="display: block; margin-bottom: 5px; font-weight: 500;">Measured Power (kW):</label>
        <input type="number" id="vsdKw" value="" step="0.1" placeholder="e.g. 75.2" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 4px;">Average power at the measured flow point</p>
    </div>
</div>

<div style="display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 15px 0;">
    <div>
        <label for="vsdPressure" style="display: block; margin-bottom: 5px; font-weight: 500;">Discharge Pressure (PSI):</label>
        <input type="number" id="vsdPressure" value="" step="1" placeholder="e.g. 125" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
    </div>
    <div>
        <label for="vsdInletTemp" style="display: block; margin-bottom: 5px; font-weight: 500;">Inlet Temperature (°C):</label>
        <input type="number" id="vsdInletTemp" value="20" step="0.1" placeholder="e.g. 20" style="width: 100%; padding: 8px; border: 1px solid var(--md-default-fg-color--lightest); border-radius: 4px; background: var(--md-default-bg-color); color: var(--md-default-fg-color);">
        <p style="font-size: 0.85em; color: var(--md-default-fg-color--light); margin-top: 4px;">Temperature at test conditions (CAGI standard: 20°C)</p>
    </div>
</div>

<div id="vsdResult" style="margin-top: 15px; padding: 15px; background: var(--md-default-bg-color); border-radius: 6px; border: 1px solid var(--md-default-fg-color--lightest);">
    <p style="color: var(--md-default-fg-color--light);">Enter values above to calculate isentropic efficiency.</p>
</div>

</div>

<script>
(function() {
    const GAMMA_VSD = 1.40287268;
    const R_AIR_VSD = 0.28703905;
    const P_ATM_VSD = 101.325;
    const CFM_TO_KGS_VSD = 0.000472 * 1.225;

    function calcVsdEff() {
        const cfm = parseFloat(document.getElementById('vsdCfm').value);
        const kw = parseFloat(document.getElementById('vsdKw').value);
        const psi = parseFloat(document.getElementById('vsdPressure').value);
        const inletC = parseFloat(document.getElementById('vsdInletTemp').value);
        const resultDiv = document.getElementById('vsdResult');

        if (isNaN(cfm) || isNaN(kw) || isNaN(psi) || isNaN(inletC) || cfm <= 0 || kw <= 0) {
            resultDiv.innerHTML = '<p style="color: var(--md-default-fg-color--light);">Enter values above to calculate isentropic efficiency.</p>';
            return;
        }

        const massFlow = cfm * CFM_TO_KGS_VSD;
        const T1 = inletC + 273.15;
        const P2 = psi * 6.894757 + P_ATM_VSD; // gauge to absolute
        const exponent = (GAMMA_VSD - 1) / GAMMA_VSD;
        const idealPower = (GAMMA_VSD * R_AIR_VSD * T1 / (GAMMA_VSD - 1)) *
                           (Math.pow(P2 / P_ATM_VSD, exponent) - 1) * massFlow;
        const efficiency = (idealPower / kw) * 100;
        const specificPower = kw / (cfm / 100);

        let color = '#4caf50';
        let note = '';
        if (efficiency > 100) {
            color = '#f44336';
            note = '<p style="margin: 8px 0 0 0; font-size: 0.85em; color: #f44336;">Efficiency > 100% indicates an inconsistency in the inputs. Check that the pressure is gauge (not absolute) and the power measurement corresponds to the flow rate.</p>';
        } else if (efficiency < 50) {
            color = '#ff9800';
            note = '<p style="margin: 8px 0 0 0; font-size: 0.85em; color: #ff9800;">Efficiency below 50% is unusually low. Verify the inputs are correct.</p>';
        }

        resultDiv.innerHTML = `
            <div style="display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 15px; text-align: center;">
                <div>
                    <p style="margin: 4px 0; color: var(--md-default-fg-color--light); font-size: 0.85em;">Isentropic Efficiency</p>
                    <p style="margin: 4px 0; font-family: monospace; font-size: 1.4em; font-weight: 600; color: ${color};">${efficiency.toFixed(2)}%</p>
                </div>
                <div>
                    <p style="margin: 4px 0; color: var(--md-default-fg-color--light); font-size: 0.85em;">Ideal Power</p>
                    <p style="margin: 4px 0; font-family: monospace; font-size: 1.4em;">${idealPower.toFixed(2)} kW</p>
                </div>
                <div>
                    <p style="margin: 4px 0; color: var(--md-default-fg-color--light); font-size: 0.85em;">Specific Power</p>
                    <p style="margin: 4px 0; font-family: monospace; font-size: 1.4em;">${specificPower.toFixed(2)} kW/100cfm</p>
                </div>
            </div>
            ${note}
            <p style="margin: 10px 0 0 0; font-size: 0.85em; color: var(--md-default-fg-color--light);">Use the efficiency value above as the "Isentropic Eff." input in the cold air intake calculator.</p>`;
    }

    document.addEventListener('DOMContentLoaded', function() {
        ['vsdCfm', 'vsdKw', 'vsdPressure', 'vsdInletTemp'].forEach(function(id) {
            var el = document.getElementById(id);
            if (el) {
                el.addEventListener('change', calcVsdEff);
                el.addEventListener('input', calcVsdEff);
            }
        });
    });
})();
</script>
