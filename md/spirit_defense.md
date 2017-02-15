<!-- .slide: data-state="no-toc-progress" -->
### A UAV Teleoperation System Using Subimposed Past Image Records <!-- .element: class="no-toc-progress" -->
#### （過去画像を用いた飛行ロボットの遠隔操作手法）

#### Jean Nassar
Mechatronics Lab, Kyoto University

February 16, 2017

-s-
# Background
-v-
## Drones
- Unmanned aerial vehicles (UAVs)
- Various applications
- Usually at least one camera as payload
- Usually controlled by:
  - line-of-sight
  - Onboard camera <!-- .element: class="fragment highlight-blue" -->
-v-
## Problems
- No knowledge of vehicle boundaries
- Degradation of signal
  - long distance to drone
  - in bad communication environments
    <ul class="fragment">
      <li>thick concrete or metal</li>
      <li>nuclear power plants</li>
      <li>debris in disaster areas</li>
    </ul>
- Recipe for disaster<!-- .element: class="fragment" -->

Note: Some examples:
  - Power outages
  - people being knocked unconscious
  - people getting their eyeballs slided
  - drones flying too close to airports
-v-
## Research Objective
- Use only one fixed, onboard, monocular camera <!-- .element: class="fragment" -->
- Work well in low-bandwidth situation <!-- .element: class="fragment" -->
- Increase accuracy and situational awareness <!-- .element: class="fragment" -->
- Reduce workload and task duration <!-- .element: class="fragment" -->

-s-
# Proposed Solution
-v-
## What is SPIRIT?
<table height="100%">
<img src="media/spirit_defense/spirit_summary.png" width=400 style="background-color:white;">

- Store frames obtained from normal operation
- Superimpose drone CG model onto stored image

Note:
- A novel UAV teleoperation interface
- Designed to increase situational awareness
  - Operator can see boundaries of drone
-v-
## Position comparison
<table height="100%">
  <tr>
    <td style="vertical-align:top">
      <img src="media/spirit_defense/drones_ref.png" width=400/><br/>
      <small>$l_0$: reference distance</small><br/>
      <small>$D$: with respect to drone
    </td>
    <td style="vertical-align:top">
      <ul>
	<li class="fragment">closeness to centre: $\sqrt{\Delta x_D^2 + \Delta z_D^2}/{l_0}$</li>
	<li class="fragment">difference in yaw: $\Delta \psi_D^2$</li>
	<li class="fragment">distance: $((l_D - l_0)/l_0)^2$</li>
      </ul>
    </td>
  </tr>
</table>
-v-
## Frame comparison
<table height="100%">
  <tr>
    <td style="vertical-align:top">
      <img src="media/spirit_defense/frames_ref.png" width=400/><br/>
      <small>$l_0$: reference distance</small><br/>
      <small>$F$: with respect to frame
    </td>
    <td style="vertical-align:top">
      <ul>
	<li class="fragment">difference in yaw: $\Delta \psi_F^2$</li>
	<li class="fragment">distance: $l_F/l_0$</li>
      </ul>
    </td>
  </tr>
</table>
-v-
## Evaluation function
$E(f) =  k_1\sqrt{\Delta x_D^2 + \Delta z_D^2}/{l_0} $

  $+ k_2\Delta \psi_D^2  + k_3\left(\left(l_D - l_0\right)/l_0\right)^2$

  $+ k_4\Delta \psi_F^2 + k_5l_F/l_0$

Select $\underset{f}{\arg\min}\left(E\left(f\right)\right);\ f \in\,$frame buffer

-s-
# Making Of
-v-
## Components
- ROS Kinetic in a Docker container
- OpenGL for visualization
- Python 2.7 and associated packages
- Easy to configure 
  - change YAML config file 
  - regenerate launch files from xacro.
- PS3 controller
-v-
## Overview
<img src="media/spirit_defense/flowchart.png" width=400/>

Note:
- Operator sends commands to AR.Drone
- Get pose and orientation from mocap
- Reduce drone video frequency to simulate bad signal
- Associate each frame with its pose
- Store all frames in chronological array (actually a deque)
- With each pose, select best frame and overlay

-s-
# Experiment
-v-
## Procedure
<table height="100%">
  <tr>
    <td style="vertical-align:top">
      <img src="media/spirit_defense/drone_long_target.jpg" width=360/>
    </td>
    <td style="vertical-align:top">
      <ul>
	<li>Fly drone to target using either:
	  <ul>
	    <li>Onboard view</li>
	    <li>SPIRIT view</li>
	  </ul>
	</li>
        <li>Press a button when arrived</li>
        <li>Repeat experiment with same method</li>
        <li>Repeat process with remaining method</li>
      </ul>
    </td>
  </tr>
</table>
-v-
## Participants
- 9 participants
- All male, Kyoto University students
- Age was 24.2$\,\pm\,$2.1 years
- Practice session first
- Odd-numbered participants: Onboard then SPIRIT
- Even-numbered participants: SPIRIT then Onboard
-v-
## Data collection
- Recording to mpeg:
  - Bird's-eye view
  - Onboard output
  - SPIRIT outuput
- ROS data recorded to Bag files.
-v-
## Onboard video
<video data-autoplay src="media/spirit_defense/onboard.mp4"></video>
-v-
## SPIRIT video
<video data-autoplay src="media/spirit_defense/spirit.mp4"></video>

-s-
# Results
-v-
## Credibility Interval (CI) <!-- .element: class="no-toc-progress" -->
- Significance at 95%
- <span class="fragment highlight-green">Significant</span> or <span class="fragment highlight-red">non-significant</span>
-v-
## Effect size (Hedges's $g$) <!-- .element: class="no-toc-progress" -->

|$g$|effect size|
|---|---|
|0.01|very small|
|0.20|small|
|0.50|medium|
|0.80|large|
|1.20|very large|
|2.0|huge|
-v-
## Ground tracks
![](./media/spirit_defense/paths_overview.png)
-v-
## Path length
![](./media/spirit_defense/movement.png)

+9.5% (CI=86.1%, $g$=0.391) <!-- .element: class="fragment highlight-red" -->
-v-
## Accuracy
![](./media/spirit_defense/rms.png)

+39.8% (CI=98.1%, $g$=1.053) <!-- .element: class="fragment highlight-green" -->
-v-
## Duration
![](./media/spirit_defense/duration.png)

+12.9% (CI=81.5%, $g$=0.304) <!-- .element: class="fragment highlight-red" -->
-v-
## NASA-TLX
![](./media/spirit_defense/tlx_results.png)

$-$37.5% (CI=97.6%, $g$=$-$0.978) <!-- .element: class="fragment highlight-green" -->
-v-
## NASA-TLX
![](./media/spirit_defense/tlx_components.png)
-v-
## Survey
![](./media/spirit_defense/survey_results.png)

+35.7% (CI=98.8%, $g$=1.304) <!-- .element: class="fragment highlight-green" -->
-v-
## Survey
![](./media/spirit_defense/survey_components.png)

Note:
- Position awareness: +41.4% (CI=95.8%, g=0.909)
- Position control: +44.8% (CI=97.9%, g=1.173)
- Rel pos awareness: +105.3% (CI=98.8%, g=1.415)
- Rel pos control: +108.7% (CI=99.9%, g=2.511)

-s-
# Conclusions
-v-
## Future work
- Make evaluation more efficient
- Increase buffer size
- Add zooming for smoother transitions
- Investigate:
  - rotating the horizon to keep it level
  - adding depth cues
  - handling moving behind obstacles

-s-
<!-- .slide: data-state="no-toc-progress" -->
## Thank you for listening <!-- .element: class="no-toc-progress" -->
> because […] if you don’t know where you are, then you don’t know where you’re going. And if you don’t know where you’re going, you’re probably going wrong.

Terry Pratchett
