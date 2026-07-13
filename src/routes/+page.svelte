<script>
  import SystemDiagram from '$lib/components/SystemDiagram.svelte';
  import PinSwap from '$lib/components/PinSwap.svelte';
</script>

<svelte:head><title>Sorter V2 - Wire harness</title></svelte:head>

<h1>Wire harness</h1>
<p class="sub">Working documentation for review.</p>
<p class="meta">24V power distribution from the PSU, plus everything connected to basically board v1.3. Wire IDs match the schedule tables. Open items in section 6.</p>

<h2>1 &nbsp; Power supply</h2>
<dl class="spec">
  <dt>Model</dt><dd>MEAN WELL LRS-350-24</dd>
  <dt>Output</dt><dd>24V, 14.6A, 350.4W, single output</dd>
  <dt>Enclosure</dt><dd>Custom 3D-printed box, fused AC input</dd>
  <dt>DC outputs</dt><dd>6 &times; female DC jack, each a 4 in wire with 2 &times; fork / screw terminals onto the PSU output</dd>
</dl>

<h2>2 &nbsp; Interconnect diagram</h2>
<SystemDiagram />

<h3>2.1 &nbsp; Stepper polarity</h3>
<div class="note flag">
  Source of truth is the basically board v1.3 pinout. Relative to how StepperOnline ships these motors, the inner two wires are flipped: shipped <code>1&middot;2&middot;3&middot;4</code> &rarr; basically board v1.3 order <code>1&middot;3&middot;2&middot;4</code>. Mark polarity on each of the 4 channel steppers.
</div>
<p class="meta">Full basically board v1.3 pinout (J23-J40), connector-to-connector mapping, and connector photos: <a href="/steppers">stepper connectors</a>.</p>
<PinSwap />

<h2>3 &nbsp; Wire schedule</h2>

<h3>3.1 &nbsp; From PSU (24V)</h3>
<table>
  <thead><tr><th>ID</th><th>Load</th><th>From</th><th>To</th><th>Cond.</th><th>Length</th><th>Gauge</th></tr></thead>
  <tbody>
    <tr><td class="id">J1-6</td><td>PSU output jacks (&times;6)</td><td>PSU output, 2&times; fork/screw terminal</td><td>Female DC jack</td><td>2</td><td>4 in</td><td>TBD</td></tr>
    <tr><td class="id">W1</td><td>basically board v1.3</td><td>PSU J1, male DC</td><td>JST female (board)</td><td>2</td><td>36 in <span class="flag">too long</span></td><td>TBD</td></tr>
    <tr><td class="id">W2</td><td>Waveshare 4-port USB hub, 24V</td><td>PSU J2, male DC</td><td>Male DC (hub)</td><td>2</td><td>12 in</td><td>TBD</td></tr>
    <tr><td class="id">W3</td><td>Orange Pi 5</td><td>PSU J3, male DC</td><td>24V-5V USB-C buck</td><td>2</td><td>6 in</td><td>TBD</td></tr>
    <tr><td class="id">W4</td><td>Fan, 24V 40mm</td><td>PSU J4, male DC</td><td>Fan</td><td>2</td><td>36 in <span class="flag">too long</span></td><td>TBD</td></tr>
    <tr><td class="id">W5</td><td>Fan, 24V 40mm</td><td>PSU J5, male DC</td><td>Fan</td><td>2</td><td>36 in <span class="flag">too long</span></td><td>TBD</td></tr>
  </tbody>
</table>
<p class="meta">J6 output is unassigned. Confirm spare or missing load.</p>

<h3>3.2 &nbsp; LEDs (from basically board v1.3)</h3>
<p class="meta">All three LED drops share one power connector on basically board v1.3: J1, a 2-pin JST VH (3.96 mm pitch). Each drop has a female/male DC jack (unplug point) and a 4 in pigtail into the module.</p>
<table>
  <thead><tr><th>ID</th><th>Drop</th><th>From (board)</th><th>To</th><th>Cond.</th><th>Length</th></tr></thead>
  <tbody>
    <tr><td class="id">L1</td><td>COB board</td><td>J1, 2-pin JST VH 3.96 mm</td><td>Female DC jack, 4 in pigtail to COB board</td><td>2</td><td>36 in + 4 in</td></tr>
    <tr><td class="id">L2</td><td>COB board</td><td>J1 (shared)</td><td>Female DC jack, 4 in pigtail to COB board</td><td>2</td><td>36 in + 4 in</td></tr>
    <tr><td class="id">L3</td><td>LED strip (6000K)</td><td>J1 (shared)</td><td>Female DC jack, 4 in pigtail to LED strip</td><td>2</td><td>36 in + 4 in</td></tr>
  </tbody>
</table>
<div class="note">LED strip for the classification channel is <b>6000K</b>. Length: 2&times; revolutions around the classification channel inner tube.</div>

<h3>3.3 &nbsp; Sensors &amp; steppers (from basically board v1.3)</h3>
<table>
  <thead><tr><th>ID</th><th>Segment</th><th>From</th><th>To</th><th>Cond.</th><th>Length</th></tr></thead>
  <tbody>
    <tr><td class="id">LIM</td><td>Limit switch</td><td>basically board v1.3, 2-pos dupont</td><td>Limit switch</td><td>2</td><td>unknown</td></tr>
    <tr><td class="id">S1-4</td><td>Stepper, channels 1-4 (&times;4)</td><td>basically board v1.3, JST-PH 4-pin</td><td>Stepper (polarity: inner two flipped vs StepperOnline)</td><td>4</td><td>40 in</td></tr>
    <tr><td class="id">CH</td><td>Chute stepper</td><td>basically board v1.3, JST-PH 4-pin</td><td>Chute stepper - flying leads, need prep</td><td>4</td><td>40 in</td></tr>
  </tbody>
</table>

<h3>3.4 &nbsp; Servo adapter (ribbon)</h3>
<table>
  <thead><tr><th>ID</th><th>Segment</th><th>From</th><th>To</th><th>Cond.</th><th>Length</th></tr></thead>
  <tbody>
    <tr><td class="id">RIB</td><td>Ribbon cable</td><td>basically board v1.3, 16-pin IDC (FC)</td><td>First servo adapter board, 16-pin IDC (FC)</td><td>16</td><td>1 m</td></tr>
  </tbody>
</table>
<figure style="max-width:280px">
  <img src="/ribbon.jpg" alt="16-pin IDC ribbon cable" style="width:100%;border:1px solid var(--line);border-radius:4px" />
  <figcaption>uxcell 16-pin IDC flat ribbon, FC/FC, 2.54 mm pitch, 1 m, gray.</figcaption>
</figure>

<h2>4 &nbsp; Parts</h2>
<ul class="tight">
  <li>MEAN WELL LRS-350-24, 350.4W 24V 14.6A single output &nbsp;&middot;&nbsp; <a href="https://www.amazon.com/dp/B013ETVO12">link</a></li>
  <li>DC 12V/24V to 5V USB-C buck converter, 5A 25W, powers Orange Pi 5 &nbsp;&middot;&nbsp; <a href="https://www.amazon.com/dp/B0FV3P6KLS">link</a></li>
  <li>WINSINN 40mm 24V fan (4010), ships XH2.54-2PIN, re-terminated to male DC jack &nbsp;&middot;&nbsp; <a href="https://www.amazon.com/dp/B0757RPCN9">link</a></li>
  <li>uxcell 16-pin IDC flat ribbon cable, FC/FC, 2.54 mm, 1 m, gray &nbsp;&middot;&nbsp; <a href="https://www.amazon.com/dp/B07S2W4N9T">link</a></li>
  <li>Waveshare 4-port USB hub, 24V model</li>
  <li>Orange Pi 5</li>
</ul>

<h2>5 &nbsp; Connector / terminal types</h2>
<ul class="tight">
  <li>DC barrel jack, female: PSU outputs, LED junction</li>
  <li>DC barrel jack, male: loads, LED pigtails</li>
  <li>Fork / screw terminal: PSU output jacks</li>
  <li>JST, female: basically board v1.3 power in (series unknown)</li>
  <li>JST VH, 2-position (3.96 mm): LED power (J1)</li>
  <li>JST-PH, 4-position (2.0 mm): steppers (J23, J27, J31, J35, J39)</li>
  <li>2.54 mm (0.1") crimp housing, 2-position ("dupont"): limit switch</li>
  <li>16-pin IDC (FC), 2.54 mm: ribbon to first servo adapter board</li>
</ul>

<h2>6 &nbsp; Open items</h2>
<ol>
  <li><b>Lengths.</b> W1, W4, W5 are 36 in and longer than necessary. Pick final lengths and cut.</li>
  <li><b>JST type</b> on basically board v1.3 power input is unknown. Identify the series.</li>
  <li><b>Missing LED wire(s).</b> Re-count the LED drops against the actual LEDs.</li>
  <li><b>J6 (6th PSU output).</b> 5 loads on 6 jacks. Confirm the spare or the missing load.</li>
  <li><b>Gauge per segment.</b> Current draw per load is needed to spec gauge.</li>
  <li><b>SKU reduction.</b> Once gauges are known, standardize on as few gauges and connector types as possible.</li>
</ol>
