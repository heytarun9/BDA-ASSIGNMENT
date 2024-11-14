*** # BDA-ASSIGNMENT 1 ***
# Pyspark program to count number of words in a file stored in local system.

import pandas as pd

# Load the file
file_path = '/content/MentalHealthSurvey.csv'
data = pd.read_csv(file_path)  # Use pd.read_csv if it's actually a CSV file

# Count the number of entries per column
word_counts_per_column = data.count()

# Display the counts
print(word_counts_per_column)





*** # BDA-ASSIGNMENT 2 ***
# pyspark program to analyze a video stream.

import cv2
from google.colab.patches import cv2_imshow
import numpy as np
import time

# Replace with the path to your video file
video_file_path = "/content/3833491-hd_1080_1920_30fps.mp4"

# Open the video file
video_capture = cv2.VideoCapture(video_file_path)

if not video_capture.isOpened():
    print("Error opening video stream or file")
    exit()

# Get the frames per second (fps) of the video
fps = video_capture.get(cv2.CAP_PROP_FPS)

# Calculate the frame number for a 1-second interval
frame_interval = int(fps)

# Initialize a frame counter
frame_count = 0

while True:
    # Set the video position to the current frame count
    video_capture.set(cv2.CAP_PROP_POS_FRAMES, frame_count)

    # Read a frame from the video stream
    ret, frame = video_capture.read()

    # If frame is read correctly, ret is True
    if not ret:
        print("Can't receive frame (stream end?). Exiting ...")
        break

    # Display the color frame using cv2_imshow for Colab
    cv2_imshow(frame)

    # Extract the pixel values
    pixels = np.array(frame)
    print(f"Frame at {frame_count / fps:.2f} seconds (Frame {frame_count}) pixels:\n{pixels}\n")

    # Move to the next frame after 1 second time stamp
    frame_count += frame_interval

    # Introduce a delay of 1 second before showing the next frame
    time.sleep(1)

# When everything is done, release the capture
video_capture.release()   
