# Jean Nassar
### 21 June 2016
[gh: @masasin](https://www.github.com/masasin)



# Who am I?
- Jean Nassar <!-- .element: class="fragment" -->
- Engineer In Training <!-- .element: class="fragment" -->
- Interested in languages, anatomy, aerospace, robotics <!-- .element: class="fragment" -->
- Kyoto University, MS Mechanical Engineering <!-- .element: class="fragment" -->
  - Mechatronics laboratory
- University of Waterloo, BASc Mechatronics Engineering  <!-- .element: class="fragment" -->


## I'm international!
- Grew up on 3 continents
- Have 3 nationalities
- Speak 8 languages
  - English, French, Lebanese (Native)
  - Japanese (C2); Arabic (C1)
  - Spanish (B2)
  - German, Krio (A2); Russian, Chinese (A1)

Note:
CEFR (Common European Framework of Reference for Languages)



# Programming
- Experience leading, directing a small programming team
- Always striving to maintain quality in all languages


## Main Languages
- Python is my daily driver
  - Rospy
  - Scipy stack
  - Jupyter for exploration
  - Templating (like my resume generator)
- C++ for low-level programming (Arduino, mbed etc)
- LaTeX for report generation


## Also have experience with
- C for data structures, RTOS, FPGA, microcontrollers
- Octave/Matlab for many courses (e.g., numerical methods)
- bash for Linux scripting
- gnuplot for plot generation
- One-offs (3-4 months each) include:
  - VHDL, PLC, LabVIEW (courses) 
  - VBA, C#, Perl, LISP (work terms)

Note:
- Passing experience with:
  - html, js, Haskell, Ruby, nim, etc



# Waterloo
- University of Waterloo
  - BASc, Honours Mechatronics Engineering
  - Graduated in 2013
- Best university in Canada for robotics

Note:
- Project-based, including many group projects
- Cooperative education system
- Everything you discover is yours


## Fields of study
- Mechanical engineering
- Electrical engineering
- Systems engineering
- Computer science
- Software engineering


## Co-op
- 6 full-time work terms, 4 months each
- I had 4 companies, 2 labs in 3 countries
- Exposed to:
  - Programming
  - 3D CAD
  - Construction
  - Electronics


## Relevant courses
- Robotics courses
- Controls courses
- Project-based design courses
- Numerical methods
- Mechatronic systems integration
- Electromechanical machine design
- Microprocessor systems and interfacing
- Computer structures and realtime systems



# Kyoto
- Kyoto University
  - MS, Mechanical Engineering 
  - Mechatronics laboratory
  - Target graduation date is September


## Summary
- Came for Masters instead of taking job offer
- Research student until start of academic year
- Masters student since April 2014
- Research topic approved in October 2014
- Research topic switched completely in mid-2015
  - Graduation delayed due to that <!-- .element: class="fragment" -->


## As a research student
- First exposure to research environment
- Masters entrance exam prep (I passed!)
- Got familiar with the lab
- Scipy stack
- Basics of ROS

Note:
- Research env:
  - How to find papers
  - How papers are written
  - Requirements for something to be called research
- Scipy stack: incl Jupyter, numpy, matplotlib etc. KSP project


## As a Masters student
- First six months were classes
- Participated in Robocup Japan Open (rescue robotics)
  - Team SHINOBI's Yozakura
- Worked on original research topic
  - Framework for controlling external devices using EMG
  - Heavy development, but no good publishing ideas
  - After many meetings, switched to current topic
- Currently working on third person view for drones
  - Codename: SPIRIT

Note:
- Original research
  - Used off-the-shelf EMG sensor
  - Goal was multiple types of input devices



# Yozakura
<img src="https://imgur.com/WJAvywg.jpg" width="60%" alt="Yozakura Unarmed">


## Overview
- Lab has a Robocup team
- 8 members worked on teleoperation robot
- Yozakura is the team's teleoperation robot
- Everyone wore multiple hats
- Was software lead for robot-side development


## Responsibilities
- High level overview
- Selection of language, platform, sensors, protocols
- Teaching students about source control, Python, etc
- Initial implementation of most details
  - Error correction, interrupts, modularity, robustness
  - Server, client, controller input
  - Device drivers
  - Motor controller
  - Dynamixel library (unused)


## Structure
- Base station receives controller input to send to robot
- RPi on robot receives, determines motor instructions
- RPi commands motors and servos via mbed
- mbed collects information from attached sensors
- RPi collects information from sensors and mbed
- RPi processes and sends back to base for display


## Communication
- TCP: Transmission of commands, Ricoh Theta
- UDP: Transmission of measurements
- I2C: Current sensors, IMU, 4x4 thermal sensor
- PWM: Motors
- Serial: mbed, Dynamixels
- Analog: CO2 sensor, Potentiometers


## Additional notes
- I wrote the initial server while ROS was being learnt
- Server was replaced by ROS locally
  - Still communicated with robot via TCP and UDP
  - Many parts of initial server were reused
- Not involved with robot-side devices communicating directly to server (LRF, WiFi cameras, CONTEC)

Note: Initially there was no GUI



# SPIRIT
- Superimposed Past Image Records In Teleoperation
- Third person operation for drones
- Uses ROS

Note: Improved situational awareness, fewer crashes esp in constrained envs.


## Motivation
- Lack of spatial awareness when flying drones
- Usually only 2D view is available
- No knowledge about vehicle boundaries
  - Hard to maneuver in confined spaces
- Bonus: Works with bad communication

Note: Say in the end I will give an example.


### In First Person View
<img src="media/20160621_drone_fpv.png" width="60%" alt="Drone FPV">


### In Third Person (External) View
<img src="media/20160621_drone_chase.png" width="60%" alt="Drone Chase">


### Actual screenshot
<img src="media/20160621_spirit.png" width="60%" alt="SPIRIT">

Note: Some problems
- Flying forward hides horizon due to pitch
- Appearing in a previously imaged spot


## System overview
### Flowchart
<img src="media/20160621_spirit_flowchart.png" width="60%" alt="SPIRIT flowchart">

- Pose obtained from motion capture system


## System overview
### Rosgraph
<img src="media/20160621_spirit_rosgraph.png" width="100%" alt="SPIRIT rosgraph">

Note: Mention what tracking verifier does


## Current status
- Code is done
- Trying to figure out good, general-purpose eval functions
- Then there are user experiments and thesis finalization

Note: Continue down if any time left


## Configuration
- xacro templates for launch files
- Configured using a yaml file
```javascript
  pose:
    mock_pose: false
    real:
      use_mocap: true
      use_odometry: false
```
- Each eval_method has different params
```javascript
  past_image:
    general:
      eval_method: spirit
      image_queue_length: 60
    constant_distance:
      distance: 1.5
    constant_time_delay:
      delay: 200
```


## Automatic regeneration
- Regererate all launch files (and one xacro file!)
```bash
  $ ./regenerate_launch_files.py
  Regenerating: 100%|██████| 6/6 [00:01<00:00, 4.65 files/s]
```
- Can easily change parameters and methods on the fly
- Using function generators, metaprogramming


## Visualization
- Can't use rviz due to limitations
- Had to write own visualization engine
- Using OpenGL on top of pygame
- Very responsive
- Using wrappers to stay sane


### Before
```python
    # Enable 2D orthographic projection
    gl.glMatrixMode(gl.GL_PROJECTION)
    gl.glPushMatrix()
    gl.glLoadIdentity()
    glu.gluOrtho2D(-width / 2, width / 2, -height / 2, height / 2)
    gl.glMatrixMode(gl.GL_MODELVIEW)
    gl.glPushMatrix()
    gl.glLoadIdentity()
    do_something()
    gl.glMatrixMode(gl.GL_PROJECTION)
    gl.glMatrixMode(gl.GL_MODELVIEW)
```


### After
```python
    with gl_ortho(width, height):
        do_something()
```

Note: Abridged and undocumented for the sake of brevity


### The fix
```python
    @contextmanager
    def new_matrix(mode_start, mode_end):
	gl.glMatrixMode(mode_start)
	gl.glPushMatrix()
	yield
	gl.glPopMatrix()
	gl.glMatrixMode(mode_end)

    @contextmanager
    def gl_ortho(w, h):
	with new_matrix(gl.GL_PROJECTION, gl.GL_MODELVIEW):
	    gl.glLoadIdentity()
	    glu.gluOrtho2D(-w / 2, w / 2, -h / 2, h / 2)
	    with new_matrix(gl.GL_MODELVIEW, gl.GL_PROJECTION):
		gl.glLoadIdentity()
		yield
``` 


## External packages
- `ardrone_autonomy`
- `tum_ardrone`
- `joystick_drivers`
- `mocap_optitrack`
- `usb_cam`



# Thanks!
## Any questions?
