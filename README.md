 Below, we show how to load and replay the hand motion data from the Spatial Description Corpus. The data is available [here](https://pub.uni-bielefeld.de/data/2913177)

### Install Mumodo to load hand motion data
To load the hand motion data, you need a python package: “**mumodo: MUltiMOdal DOcument - import, analyze, plot and manage multimodal data**”. Its documents and source code are available in the GitHub repository: https://github.com/dsg-bielefeld/mumodo.git. Please follow the instruction to install the package.

After intalling mumodo, you can use the notebook in the code folder to load the data.


### Replay hand motion data
With [InstantReality](http://www.instantreality.org/) and [Venice](https://github.com/dsg-bielefeld/Venice), you can replay the hand motion data and view the data from different viewpoints.

#### Preparations: 

1. Install InstantPlayer from [here](http://www.instantreality.org/downloads/). Choose the right version for your OS.
2. Download Venice from Github `git clone https://github.com/dsg-bielefeld/Venice.git` and add it to the system path so that you can run `java -jar VeniceHub` from any folder on your computer.

#### Replay the hand motion data:

1. Launch the Instant Player
2. Navigate to the folder where `leap.x3d` and `leap.xml` are located.
3. open a terminal window, run following command to replay the data: `java -jar VeniceHub.jar -i Disk -o IIO -f file.xio.gz`. Then you can see one or two hands in the window of the Instant Player.

 *For more information of how to use Venice, please refer to the manual in the github repository or write to ting.han[AT]uni-bielefeld.de*
 
 
### Hand motion features
 
The hand motion data in the Spatial Description Corpus was logged with the Leap SDK v2.3.1. 

- For each dataframe, it provides:
  -  `FrameID`:   integer, a unique ID assigned to this data frame.
  -  `HandNum` : integer, the number of tracked hands

- For each hand

   - `hand type`: string, left hand or right hand
   - `hand ID`: integer, a unique ID assigned to this Hand object. The value remains the same across consecutive frames while the tracked hand remains visible. 
  - `hand confid`: float, ranging from 0 to 1. It indicates how well the internal hand model fits the observed data.
  - `hand direction`: 3-d vector. The direction from the palm position toward the fingers.
  - `hand sphere center`: 3-d vector. The center of a sphere fit to the curvature of this hand.
  - `sphere radius`: float, the radius of a sphere fit to the curvature of this hand.
  - `palm width`: float, the average width of the hand (not including fingers or thumb).
  - `palm position`: 3-d vector, the center position of the palm in millimeters from the Leap Motion Controller origin.
  - `palm velocity`: 3-d vector, the rate of change of the palm position in millimeters/second.
  - `GrabStrength`: float, the strength of a grab hand pose as a value in the range [0..1]. 0 when the hand is closed.
  - `PinchStrength`: float, t he strength of a pinch pose between the thumb and the closest finger tip as a value in the range [0..1].

- Each detected hand is associated with several fingers. Each finger is represented with following features:
  - `FingerType`: integer, the integer code representing the finger name.
      -  0 = TYPE_THUMB
      -  1 = TYPE_INDEX
      - 2 = TYPE_MIDDLE
      - 3 = TYPE_RING
      - 4 = TYPE_PINKY
 - `FingerLength`: float, the apparent length of a finger.
 - `FingerWidth`: float, the average width of a finger.

- Each finger is composed of following bone objects: *tip, meta bone, prox bone, inter bone, dist bone*. Each bone is represented with following features:
  - `Direction`:  3-d vector, the current pointing direction vector.
  - `PrevJoint`: 3-d vector, the position of the end of the bone closest to the wrist.
  - `NextJoint`: 3-d vector, the position of the end of the bone closest to the finger tip.
  - `Length`: float, the length of the bone in millimeters.

 - `Angles between bones` float. For example, MetaProxAngle is computed according to the vectors of metacarpal bone and proximal bone.
 - `Angles between fingers`:  float. For example, thumbIndexAngle is computed according to vectors of thumb and index finger.