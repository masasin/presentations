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
Flowchart!

Note:
- Operator sends commands to AR.Drone <!-- .element: class="fragment" -->
- Get pose and orientation from mocap <!-- .element: class="fragment" -->
- Reduce drone video frequency to simulate bad signal <!-- .element: class="fragment" -->
- Associate each frame with its pose <!-- .element: class="fragment" -->
- Store all frames in chronological array (actually a deque) <!-- .element: class="fragment" -->
- With each pose, select best frame and overlay <!-- .element: class="fragment" -->

-v-
## Variables
<img src="media/20170216_drones_ref.png" width=400 alt="Variables">
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
## Setup
- Target is a small box
- Fly drone to target 6 m away using either:
  - Onboard view
  - SPIRIT view
- Press a button when arrived
- Repeat experiment with same method
- Repeat process with remaining method
-v-
## Participants
- 9 participants
- All male, Kyoto University students
- Age was 24.2$\,\pm\,$2.1 years
- Practiced first
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
# Results
-v-
Video Onboard!
-v-
Video SPIRIT!
-v-
## Results
- Path length: +9.5% (CI=86.1%, $g$=0.391) <!-- .element: class="fragment highlight-red" -->
- Accuracy: +39.8% (CI=98.1%, $g$=1.053) <!-- .element: class="fragment highlight-blue" -->
- Duration: +12.9% (CI=81.5%, $g$=0.304) <!-- .element: class="fragment highlight-red" -->
- NASA-TLX score: $-$37.5% (CI=97.6%, $g$=$-$0.978) <!-- .element: class="fragment highlight-blue" -->
- Survey score: +35.7% (CI=98.8%, $g$=1.304) <!-- .element: class="fragment highlight-blue" -->

Note:
  - Position awareness: +41.4% (CI=95.8%, g=0.909)
  - Position control: +44.8% (CI=97.9%, g=1.173)
  - Rel pos awareness: +105.3% (CI=98.8%, g=1.415)
  - Rel pos control: +108.7% (CI=99.9%, g=2.511)
-v-
Graphs!
-v-
## Notes
- Practice with method decreased path length
- Practice flying decreased task duration

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
## Licensing
- SPIRIT is licenced under BSD 3-clause 
- Analysis code is licensed under MIT 
- Thesis and defense are licensed under CC-BY-SA 

-s-
## Thank you for listening
> because […] if you don’t know where you are, then you don’t know where you’re going. And if you don’t know where you’re going, you’re probably going wrong.

Terry Pratchett
