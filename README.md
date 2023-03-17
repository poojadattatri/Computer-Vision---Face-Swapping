# Face-Swapping-in-Videos

The goal of this project is to automatically detect and swap faces between two videos. Our approach follows the following basic steps - We first break down our videos into frames and detect the facial landmarks, we then perform frame-wise stabilization using 68- point detector. We then swap faces between the frames of the two videos using Delaunay triangulation. We then perform blending to blend the swapped face with the rest of the video and finally we stitch the frames to get the resultant video.

## Implementation Details- 
The project mainly consists of the following steps-

- Face and Facial Landmarks Detection: In this step, we detect faces within a given frame of the video and further proceed to identify the facial landmarks within the detected face. Facial landmark points are precisely extracted from the face images to allow for efficient swapping of faces while maintaining realism. 
- Stabilization: In this function, histogram equalization is initially performed to adjust the global contrast by updating the pixel intensity distribution of the image’s histogram. Doing so enables areas of low contrast to obtain higher contrast in the output image. The inter-eye distance is then estimated to account for facial contortions. 
- Feature Extraction: Using the landmarks previously obtained, a convex hull is created that will further serve as indices for both the frames in consideration for swapping. A Delaunay Triangulation is then generated for the convex hull. The resultant mesh that is formed is then utilised during the warping and transformation processes that are executed during the final step of face swapping. 
- Face Swapping: For each of the triangles obtained on Delaunay Triangula-tion, the vertices are to be warped between the source and target images. A bounding rectangle is created for the triangle in the source. A mask is also defined to reflect the bounding rectangle for the triangle in the target image. Finally, the affine transformation is applied to the source image based on the affine transform calculated from the target. The triangular region from this transformed image may then be utilised for the final swapped result. Once this is done, the mask of the hull is utilised to obtain the center of the face which is required for the final refinement procedure of seamless cloning. 
- Video to Video Replacement: The procedure described thus far explains the steps to be executed for face swapping between two given frames. However, to successfully execute this task across an entire video, the pipeline is sequentially executed for all frames from the given source and target videos. To account for varying lengths between the source and target videos, the last frame from the shorter video will be utilised to populate the frames until the last frame from the longer video is reached. Finally, the individual frames are stitched back to generate the resultant videos after swapping.

## The following packages need to be installed-

- matplotlib
- cv2
- numpy
- dlib
- skvideo.io
- scipy.spatial.Delaunay

## Usage-

- Download all packages mentioned.
- Just specify the paths for source and target video and then run all the cells in the notebook FaceSwapping.ipynb. 
- For the extra credit, specify the path for the video and run all the cells in FaceSwappinginSameVideo.ipynb.
