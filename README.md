# Web Service for Intel RealSense Camera
This is a web service written in python Flask for RealSense Cameras which are compatible with Intel RealSense SDK 2.0.  
The end points are
* startStream: Stream RGB frames from camera
* getImage: Get the current RGB frame
* getDepth: Get depth of a given point in RGB image
* get3d: Get 3d coordinates in metre of a given point in RGB image

## Prerequisites
* Install latest version of python 2 with pip
* Pip install python dependencies  
`pip install Flask`  
`pip install numpy`  
`pip install opencv-python`
> Do **NOT** pip install pyrealsense2. This is the python wrapper for Intel RealSense SDK 1 (as of 27/06/2018)
* Download and install Intel RealSense SDK 2 from [here](https://github.com/IntelRealSense/librealsense)

## Launching the web service
Connect your RealSense camera and run the python script app.py 
`python3 app.py`

## Endpoint Documentation
### http://localhost:5000
To start stream of RGB frames from camera  
* **URL** `/`
* **Method** `GET`
* **Success Response:** A JPEG image of the current aligned RGB + Depth frame of camera input. The frame is rendered on a resizable clickable canvas x,y corrected to the current scale.  Note scrolling will create invalid corrected values. 
* **OnClick** URL `/get3d` called with corrected x,y coordinates 

### startStream
To start stream of RGB frames from camera  
* **URL** `/startStream`
* **Method** `GET`
* **Success Response:** The current RGB input from camera as MJPEG. The resolution will be max camera resolution.

### getImage
To get the current RGB frame
* **URL** `/getImage`
* **Method** `GET`
* **Success Response:** A JPEG image of the current RGB frame of camera input. The resolution will be max camera resolution.

### getDepth
To get the current depth of an (x,y) pixel coordinate of the RGB image. The response will be a floating-point value as a string which correspond to the depth in metres. The request coordinates must be in bound with the maximum resolution.
* **URL** `/getDepth?x=[integer]&y=[integer]`
* **Method** `GET`
* **Success Response:** 0.6550000309944153
* **Error Response:** Invalid coordinate values

### get3d
To get the current 3D real world coordinates in metres of an (x,y) pixel coordinate of the RGB image. The response will be x,y,z coordinates in JSON format. The request coordinates must be in bound with the maximum resolution.
* **URL** `/get3d?x=[integer]&y=[integer]`
* **Method** `GET`
* **Success Response:**  
`{  
    "x": 0.5442482456265268  
    "y": 0.4660094894248493  
    "z": 0.3578798298485989  
 }`  
* **Error Response:** Invalid coordinate values

## Acknowledgement
* Enhanced for D455 and added clickable canvas service to [Web Service for Intel RealSense Camera] (https://github.com/millerhooks/realsense-webservice) by Miller Hooks (https://github.com/millerhooks) which is under MIT License
* Default template to hold canvas adapted from [Flask Video Streaming](https://github.com/miguelgrinberg/flask-video-streaming) by [Miguel Grinberg](https://github.com/miguelgrinberg) which is under MIT License  
* [Examples](https://github.com/IntelRealSense/librealsense/tree/master/wrappers/python/examples) provided by [librealsense](https://github.com/IntelRealSense/librealsense) were referred and used.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
