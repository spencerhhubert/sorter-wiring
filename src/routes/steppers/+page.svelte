<script>
  import StepperPinout from '$lib/components/StepperPinout.svelte';
  import PinSwap from '$lib/components/PinSwap.svelte';
</script>

<svelte:head><title>Sorter V2 - Stepper connectors</title></svelte:head>

<h1>Stepper connectors &amp; polarity</h1>
<p class="sub">basically board v1.3 &middot; stepper outputs</p>
<p class="meta">basically board v1.3 pinout (all five stepper outputs identical), the connector-to-motor mapping, and the connector reference.</p>

<h2>1 &nbsp; basically board v1.3 connector pinout</h2>
<p>Every stepper output connector on <b>basically board v1.3</b> has the same pinout, pin&nbsp;1 &rarr; pin&nbsp;4:</p>
<table style="max-width:360px">
  <thead><tr><th>Pin</th><th>Net</th><th>Coil</th></tr></thead>
  <tbody>
    <tr><td>1</td><td>A2</td><td>coil A</td></tr>
    <tr><td>2</td><td>A1</td><td>coil A</td></tr>
    <tr><td>3</td><td>B1</td><td>coil B</td></tr>
    <tr><td>4</td><td>B2</td><td>coil B</td></tr>
  </tbody>
</table>

<StepperPinout />

<ul>
  <li>Holds for all five <b>JST-PH 4-pin</b> connectors: <code>J23, J27, J31, J35, J39</code>.</li>
  <li>The parallel <b>2.54&nbsp;mm headers</b> next to each are wired identically: <code>J24, J28, J32, J36, J40</code>.</li>
  <li>Pin&nbsp;1 is the roundrect (square-ish) pad on the footprint.</li>
  <li>Straight pass-through of the BigTreeTech TMC2209 module output order: module pins&nbsp;3-6 = A2, A1, B1, B2 &rarr; connector pins&nbsp;1-4.</li>
</ul>

<div class="note">
  <b>Coil rule.</b> Pins 1-2 are one coil (A), pins 3-4 the other (B). Swapping the two wires <i>within</i> a coil only reverses motor direction. Splitting a coil across the 2/3 boundary is what actually breaks operation, so keep each pair together.
</div>

<h2>2 &nbsp; basically board v1.3 &rarr; motor connections</h2>
<p>The 4 channel motors are StepperOnline NEMA 17, shipped with a <b>JST-XH 2.54&nbsp;mm</b> 4-pin lead (the 3D-printer "XH2.54" cable, black/green/red/blue). The chute motor ships as bare flying leads.</p>
<table>
  <thead><tr><th>Stepper</th><th>basically board v1.3 connector</th><th>Motor connector</th><th>Wire length</th><th>Gauge</th><th>Notes</th></tr></thead>
  <tbody>
    <tr>
      <td>Channels 1-4 (&times;4)</td>
      <td><div class="conncell"><img src="/jst-ph.jpg" alt="JST-PH connector" /><span class="n">JST-PH 2.0&nbsp;mm, 4-pin<br />(J23 / J27 / J31 / J35)</span></div></td>
      <td><div class="conncell"><img src="/jst-xh.jpg" alt="JST-XH stepper cable" /><span class="n">JST-XH 2.54&nbsp;mm, 4-pin<br />(StepperOnline "XH2.54")</span></div></td>
      <td>40 in</td>
      <td>unknown</td>
      <td>Inner two wires flipped (positions 2&harr;3) so coils line up</td>
    </tr>
    <tr>
      <td>Chute (5th)</td>
      <td><div class="conncell"><img src="/jst-ph.jpg" alt="JST-PH connector" /><span class="n">JST-PH 2.0&nbsp;mm, 4-pin<br />(J39)</span></div></td>
      <td><span class="n">Bare flying leads &rarr; crimp into a 4-position housing</span></td>
      <td>unknown</td>
      <td>unknown</td>
      <td>Motor has no connector; crimp leads to the coil order above</td>
    </tr>
  </tbody>
</table>
<p class="meta">Refdes-to-channel assignment (which of J23/J27/J31/J35/J39 is which channel, and which is the chute) to confirm.</p>

<div class="note flag">
  <b>Polarity, restated.</b> The basically board v1.3 order is fixed (section 1). For channels 1-4 the cable swaps the inner two conductors relative to how StepperOnline ships them, so the motor coils match the basically board v1.3 grouping. Confirm against the actual motor before crimping the chute.
</div>
<PinSwap />

<h2>3 &nbsp; Connector reference</h2>
<div class="cref"><img class="big" src="/jst-ph.jpg" alt="JST-PH" /><div><div class="t">JST-PH 2.0&nbsp;mm, 4-pin</div><div class="d">basically board v1.3 stepper outputs: J23, J27, J31, J35, J39.</div></div></div>
<div class="cref"><img class="big" src="/pin-header.jpg" alt="2.54mm pin header" /><div><div class="t">2.54&nbsp;mm (0.1") pin header, 4-pin</div><div class="d">Parallel headers next to each JST-PH: J24, J28, J32, J36, J40. Same pinout.</div></div></div>
<div class="cref"><img class="big" src="/jst-xh.jpg" alt="JST-XH" /><div><div class="t">JST-XH 2.54&nbsp;mm, 4-pin ("XH2.54")</div><div class="d">StepperOnline motor lead (channels 1-4). Standard color code black/green = one coil, red/blue = the other.</div></div></div>

<h2>4 &nbsp; Sources &amp; image credits</h2>
<ul class="tight">
  <li>StepperOnline NEMA 17 motors (XH2.54 lead): <a href="https://www.omc-stepperonline.com/nema-17-stepper-motor">omc-stepperonline.com</a></li>
  <li>JST PH series: <a href="https://www.jst.com/products/crimp-style-connectors-wire-to-board-type/ph-connector/">jst.com</a></li>
  <li>Image credits: JST-PH cable, Adafruit; XH2.54 stepper cable, hta3d.com; 2.54&nbsp;mm header, Wikimedia Commons.</li>
</ul>
