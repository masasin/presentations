### A UAV Teleoperation System Using Subimposed Past Image Records
#### (過去画像を用いた飛行ロボットの遠隔操作手法)
### Jean Nassar
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
  - first-person view (FPV) <!-- .element: class="fragment highlight-red" -->
-v-
## Problems (FPV)
- No knowledge of vehicle boundaries
- Degradation of signal
  - long distance to drone
  - in bad environments
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
- A novel UAV teleoperation interface
- Designed to increase situational awareness
  - Operator can see boundaries of drone
- Store frames obtained from normal operation
- Superimpose drone CG model onto stored image
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
<img src="media/spirit_defense/flowchart.png" width=400 alt="Flowchart">

Note:
- Operator sends commands to AR.Drone
- Get pose and orientation from mocap
- Reduce drone video frequency to simulate bad signal
- Associate each frame with its pose
- Store all frames in chronological array (actually a deque)
- With each pose, select best frame and overlay
-v-
## Variables
<img src="media/spirit_defense/drones_ref.png" width=400 alt="Variables">
-v-
## Evaluation function
- closeness to centre: $\sqrt{\Delta x^2 + \Delta z^2}/{l_0}$ <!-- .element: class="fragment" -->
- difference in yaw: $\Delta \psi^2$ <!-- .element: class="fragment" -->
- difference in distance: $((l - l_0)/l_0)^2$ <!-- .element: class="fragment" -->
- frame similarity: <!-- .element: class="fragment" -->
  - yaw: $\Delta \psi^2$
  - distance: $l/l_0$

-s-
# Experiment
-v-
## Procedure
<table height="100%">
  <tr>
    <td valign="middle">
      <img src="media/spirit_defense/drone_long_target.jpg" width=400/>
    </td>
    <td>
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

-s-
# Videos
-v-
## Onboard
<video data-autoplay src="media/spirit_defense/onboard.mp4"></video>
-v-
## SPIRIT
<video data-autoplay src="media/spirit_defense/spirit.mp4"></video>
-s-
# Results
-v-
## Credibility Interval (CI)
- Significance at 95%
- <span class="fragment highlight-blue">Significant</span> or <span class="fragment highlight-red">non-significant</span>
-v-
## Effect size (Hedges's $g$)

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
![](/media/spirit_defense/paths_overview.png)
-v-
## Path length
![](/media/spirit_defense/movement.png)

+9.5% (CI=86.1%, $g$=0.391) <!-- .element: class="fragment highlight-red" -->
-v-
## Accuracy
![](/media/spirit_defense/rms.png)

+39.8% (CI=98.1%, $g$=1.053) <!-- .element: class="fragment highlight-blue" -->
-v-
## Duration
![](/media/spirit_defense/duration.png)

+12.9% (CI=81.5%, $g$=0.304) <!-- .element: class="fragment highlight-red" -->
-v-
## NASA-TLX
![](/media/spirit_defense/tlx_results.png)

$-$37.5% (CI=97.6%, $g$=$-$0.978) <!-- .element: class="fragment highlight-blue" -->
-v-
## NASA-TLX
![](/media/spirit_defense/tlx_components.png)
-v-
## Survey
![](/media/spirit_defense/survey_results.png)

+35.7% (CI=98.8%, $g$=1.304) <!-- .element: class="fragment highlight-blue" -->
-v-
## Survey
![](/media/spirit_defense/survey_components.png)

Note:
- Position awareness: +41.4% (CI=95.8%, g=0.909)
- Position control: +44.8% (CI=97.9%, g=1.173)
- Rel pos awareness: +105.3% (CI=98.8%, g=1.415)
- Rel pos control: +108.7% (CI=99.9%, g=2.511)

-s-
# Conclusions
-v-
## Conclusions
- Significant increase in accuracy <!-- .element: class="fragment" -->
- Significant decrease in workload <!-- .element: class="fragment" -->
- Significant increases in position awareness and control, absolutely and relative to target <!-- .element: class="fragment" -->
- Significant increase in user satisfaction <!-- .element: class="fragment" -->
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
## Thank you for listening
> because […] if you don’t know where you are, then you don’t know where you’re going. And if you don’t know where you’re going, you’re probably going wrong.

Terry Pratchett
