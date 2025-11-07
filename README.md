AI Footfall Counter: Real-Time Pedestrian Analysis

This project develops a computer vision system to accurately count the directional flow of people (entries and exits) within a defined Region of Interest (ROI) in a video stream. It integrates a state-of-the-art detection and tracking model with custom counting logic to provide reliable footfall analytics.

1. Technical Approach (Model Implementation: 25%)

The solution utilizes a highly optimized three-stage pipeline: Detection, Tracking, and Counting.

Detection Model: We use YOLOv8-Nano (yolov8n.pt). Its single-stage architecture enables near real-time processing necessary for high-volume video analysis and addresses the performance criteria.

Tracking: We integrate ByteTrack (via the Ultralytics framework). This tracker maintains a persistent, unique Tracking ID for each individual, which is crucial for handling multiple people and preventing double-counting.

Filtering: The model is configured to only detect and track the person class, enhancing processing speed.

2. Counting Logic Explanation (Counting Logic: 25%)

The logic is contained within a clean, modular LineCounter Python class. This ensures the system provides an Accurate entry/exit count based on ROI crossing.

1. Virtual ROI: A vertical virtual line is defined at the center of the frame (LINE_REF_PERCENT = 50). This line serves as the boundary for counting.

2. Centroid Check: For every tracked object, the algorithm calculates the object's centroid and checks its current location against its previous location.

3. Crossing Event: A count is registered only when an object's centroid straddles the virtual line—meaning its position changes from one side of the line to the other between two consecutive frames.

4. Directional Assignment: The assignment of "Entry" or "Exit" is determined by the configured COUNT_DIRECTION variable. For the current setup ('left_to_right'):

  Entry: Movement from the Left side of the line to the Right side.

  Exit: Movement from the Right side of the line to the Left side.

3. Setup and Running Instructions

The code is contained in a single Jupyter Notebook (Footfall_Counter.ipynb) and requires Python >= 3.8.

3.1 Dependencies

Install the necessary libraries:

pip install ultralytics opencv-python numpy

3.2 Execution Steps

1. Ensure your video file (demofootfall.mp4) is in the same directory as the notebook.

2. Open and run the Footfall_Counter.ipynb notebook.

3. The output will be displayed in a separate OpenCV window, showing the video with bounding boxes and the live entry/exit counts overlaid.

4. The final total count is also printed to the console.

4. Video Source Used

File Name: demofootfall.mp4

Source Description: [Insert a brief, professional description of your video here, e.g., A self-recorded video of moderate pedestrian traffic in a hallway entrance.]

Example Output: A short processed video of the system in action is provided as demofootfall.mp4 in the repository.
