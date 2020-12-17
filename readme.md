# CoppeliaSim for Universal Robots

# Description
A Matlab/Python implementation of controlling UR5 in CoppeliaSim, for detailed instructions refer to the [Official User Manual
](https://www.coppeliarobotics.com/helpFiles/index.html)


## Instructions
1. Download [CoppeliaSim](https://coppeliarobotics.com/downloads) Edu version from the official website.

2. After extracting the downloaded CoppeliaSim package, you can run the application:
   ```bash
   ./coppeliaSim.sh
   ```

    You should find the Python [remote APIs](https://www.coppeliarobotics.com/helpFiles/en/remoteApiClientSide.htm) from the extracted apllication folder:
    **~/CoppeliaSim/programming/remoteApiBindings/** or simply use the files on this repository.

    You should see the following files in the **/matlab** directory:
    - remApi.m
    - remoteApiProto.m

    You should see the following files in the **/python** directory:
    * sim.py
    * simConst.py

    You also need to include the appropriate remote API library file within the same foler. You can find the file from the extracted application folder:
    **~/CoppeliaSim/programming/remoteApiBindings/lib/lib** or simply use the one on this repository:
    - Windows: "remoteApi.dll"
    - Mac: "remoteApi.dylib"
    - Linux: "remoteApi.so"

3. Once the CoppeliaSim application is up running, create a New Scene. Then you can load a UR5.ttm model into the scene by dragging the model from the Model browser.
    On the left-side of the window, you should see the UR5 is listed under the Scene hiearchy, and there is a script icon ![script](img/icon_script.png) following it.
    Double-click the script icon and you will see the Lua script that is associated with the model which by default looks like this:
    ```Lua
    -- This is a threaded script, and is just an example!

    function sysCall_threadmain()
        jointHandles={-1,-1,-1,-1,-1,-1}
        for i=1,6,1 do
            jointHandles[i]=sim.getObjectHandle('UR5_joint'..i)
        end

        -- Set-up some of the RML vectors:
        vel=180
        accel=40
        jerk=80
        currentVel={0,0,0,0,0,0,0}
        currentAccel={0,0,0,0,0,0,0}
        maxVel={vel*math.pi/180,vel*math.pi/180,vel*math.pi/180,vel*math.pi/180,vel*math.pi/180,vel*math.pi/180}
        maxAccel={accel*math.pi/180,accel*math.pi/180,accel*math.pi/180,accel*math.pi/180,accel*math.pi/180,accel*math.pi/180}
        maxJerk={jerk*math.pi/180,jerk*math.pi/180,jerk*math.pi/180,jerk*math.pi/180,jerk*math.pi/180,jerk*math.pi/180}
        targetVel={0,0,0,0,0,0}

        targetPos1={90*math.pi/180,90*math.pi/180,-90*math.pi/180,90*math.pi/180,90*math.pi/180,90*math.pi/180}
        sim.rmlMoveToJointPositions(jointHandles,-1,currentVel,currentAccel,maxVel,maxAccel,maxJerk,targetPos1,targetVel)

        targetPos2={-90*math.pi/180,45*math.pi/180,90*math.pi/180,135*math.pi/180,90*math.pi/180,90*math.pi/180}
        sim.rmlMoveToJointPositions(jointHandles,-1,currentVel,currentAccel,maxVel,maxAccel,maxJerk,targetPos2,targetVel)

        targetPos3={0,0,0,0,0,0}
        sim.rmlMoveToJointPositions(jointHandles,-1,currentVel,currentAccel,maxVel,maxAccel,maxJerk,targetPos3,targetVel)
    end
    ```
    You can start programming the robot using this script. As you can see, there are 3 target joint poses listed on the bottom. When you start the simulation, the robot will move its joints to reach these 3 targets. Of course, we are more interested in controlling the robot using Matlab or Python.

4. Depends on which language you prefer, you may start programming from the demo example code provided on this repository.

# Author
- [Mehran Armand](https://ep.jhu.edu/faculty/mehran-armand/)