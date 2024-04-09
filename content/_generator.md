
+++

title = "Simulation and software process engineering in pervasive computing"
description = "Why we need simulation for developing pervasive systems, and how we do it."
outputs = ["Reveal"]
aliases = []

+++


# Simulation and software process engineering in pervasive computing

[Danilo Pianini](mailto:danilo.pianini@unibo.it) -- {{% today %}}

---

# Development phases {{< frag c="$\Rightarrow$ *in pervasive computing*" >}}

* Analysis {{< frag c="$\Rightarrow$ *No relevant changes*" >}}
* Design {{< frag c="$\Rightarrow$ *Abstraction gap: novel approaches such as aggregate computing*" >}}
* Implementation {{< frag c="$\Rightarrow$ *Languages and tools implementing these abstractions*" >}}
* Build {{< frag c="$\Rightarrow$ *Compilers or interpreters*" >}}
* Verification
    * Debug
    * Functional (testing)
    * Non-functional (performance, security, etc.)
* Continuous Integration
# {{< frag c="$\Rightarrow$ ![](https://miro.medium.com/v2/resize:fit:600/format:webp/0*E6pTrKTFvvLDOzzj.png)" >}}

---

# Verification of pervasive systems

{{% multicol %}}{{% col %}}
## Desiderata
* Reproducible execution
* Stop-the-world semantics
* Long runs
* Run on a single machine
* Control over external influences
* Verify resilience to disruption
* Measure performance over multiple runs and conditions
{{% /col %}}{{% col %}}
## Reality
* Inherently stochastic
* Distribution imposes asynchrony
* Limited time
* Hundreds/Thousands of devices involved
* Subject to unpredictability
* Induced disruption can be catastrophic
* Testing for performance and monitoring is difficult
{{% /col %}}{{% /multicol %}}

---
{{% multicol %}}{{% col %}}
![](https://i.imgflip.com/8m3fqm.jpg)
{{% /col %}}{{% col %}}
## Pros
* Enables debugging
* Enforces reproducibility
* Accelerates time
* Emulates multiple devices at once
* Stops the world for inspection
* Enables investigation of catastrophic events
* Multiple runs provide insights over stochastic phenomena

## Limitations
* Reality gap

## Caveats
* Are you simulating the same software that will end up in production?
{{% /col %}}{{% /multicol %}}

---

# Reality / performance trade off

* Reducing the reality gap requires *more accurate models*
* Simulating with greater accuracy requires *more resources and time*

<h3 style="text-align: center">
$\Leftarrow$ simpler model $\Leftarrow$ $~~~~~~~~~~~~~~~~~~~~~$ $\Rightarrow$ more realism $\Rightarrow$ 
</h3>

<canvas id="colorMapCanvas" width="1800" height="200"></canvas>

<script>
    // Get canvas element and its context
    var canvas = document.getElementById('colorMapCanvas');
    var ctx = canvas.getContext('2d');

    // Create linear gradient
    var gradient = ctx.createLinearGradient(0, 0, canvas.width, 0);
    gradient.addColorStop(0, 'red');
    gradient.addColorStop(0.5, 'orange');
    gradient.addColorStop(1, 'green');

    // Fill canvas with the gradient
    ctx.fillStyle = gradient;
    ctx.fillRect(0, 0, canvas.width, 3 * canvas.height / 5);

    function drawLineAndLabel(fraction, label) {
      // Draw vertical line
      var xPos = canvas.width * fraction;
      ctx.beginPath();
      ctx.strokeStyle = 'black';
      ctx.moveTo(xPos, 30);
      ctx.lineTo(xPos, canvas.height - 60);
      ctx.stroke();

      // Draw label
      ctx.fillStyle = 'black';
      ctx.font = '.7em Arial';
      ctx.fillText(label, xPos - 100, canvas.height - 20);
    }
    drawLineAndLabel(0.1, 'formal properties');
    drawLineAndLabel(0.3, 'debug while developing');
    drawLineAndLabel(0.5, 'robustness evaluation');
    drawLineAndLabel(0.7, 'early performance');
    drawLineAndLabel(0.9, 'detailed performance');
</script>

### $\Rightarrow$ Different simulators for different phases of development

* Formal properties are captured by *model checkers* and dedicated tools
often using a *different formalism* than the final language
* Detailed performance is measured through simulators with a *detailed model of the world* (physics, network), often allowing integration of *external frameworks*
* Not many mid-spectrum simulators supporting *debug* to *early performance evaluation*

---

![https://alchemistsimulator.github.io/images/logo-text-path.svg](https://alchemistsimulator.github.io/images/logo-text-path.svg)

<div style="text-align: center;">
<video loop="" playsinline="" autoplay="" muted="" style="max-width: 100%; display: inline-block; ">
  <source src="https://alchemistsimulator.github.io/home-animation.mp4" type="video/mp4">
  If your browser supported the video tag, there would be a nice video.
</video>
</div>

---

# [Alchemist](https://alchemistsimulator.github.io)

* Discrete event simulator
* JVM-based
* Languages are pluggable
  * Tuple spaces / tuple centers
  * Biochemistry-oriented reactions
  * Protelis
  * Scafi
  * Collektive (work in progress)
  * JaKtA (work in progress)
* Arbitrary networks
* Mobility
* Can use maps/gps data/floor plans
* Scales to tens of thousands of devices
* Used in dozens of scientific contributions
