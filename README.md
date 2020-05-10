# Camera-Motion-and-Structure

# Planar Homography:
• We first store the given camera intrinsic matrix and distortion coefficients of the both left and right cameras in matrix and list respectively and store them in a text file using ‘np.savetxt()’ command. Then we load that file into respective np arrays using ’np.loadtxt()’.
• Now we load the image and convert into a grey scale image and store it in a variable. We use the camera matrices to undistort the image using the function ‘cv2.initUndistortRectifyMap()’ and then redraw the undistorted image using the function ‘cv2.remap()’.
• Now to find the object points we use the undistorted image and apply the ‘cv2.findChessboardCorners()’ function.
• Now the image points are the corner of the chessboard i.e. (0,0,0) which are taken as the world co-ordinates. But after homography in order to match this image with an external map we need to remap the image points. This can be done by translating the (0,0,0) point to (300, 800, 0) point and the rest according to this point.
• Now using these object points and image points we find the Homography matrix using the function ‘cv2.findHomography()’. After getting the homography matrix use this to warp the entire image, this can be done using the function ‘cv2.warpPerspective()’.

# Camera Pose Estimation from a single view:
• We import the camera intrinsic matrix and the distortion coefficients from the saved files using the ‘np.loadtxt()’ function.
• Now we load the images and store them in an np array.
• We now create dictionary using ‘aruco.Dictionary_get()’ function and we also create parameters using ‘aruco.DetectorParameters_create()’ function.
• We use this dictionary and parameters along with to detect the corners of the markers and their ids using the ‘cv2.aruco.detectMarkers()’ function.
• We now reshape these corners into a matrix, and then use the obtained corners, camera intrinsic matrix and distortion coefficients to obtain the R vector, and t(translation) matrix using the function ‘cv2.solvePnP()’ function.
• Use the R vector to obtain R matrix using the function ‘cv2.Rodrigues’. The final R(Rotation) matrix is the transpose of the matrix obtained from this function.

# Camera Pose Estimation and Reconstruction from two views:
• We first load the camera intrinsic matrix and the distortion coefficients using the ‘np.loadtxt()’ function.
• We now load a pair of images one from the left camera and the corresponding image from the right camera and undistort them using the ‘cv2.initUndistortRectifyMap()’ fuction and redraw the undistorted image using the ‘cv2.remap()’ function.
• Now we obtain feature points and their correspondences in the pair of images, for this we first create a SIFT detector using the ‘cv2.ORB_create()’ function. We now use this detector to obtain all the feature points.
• We now use the function ‘cv2.BF_matcher()’ to obtain all the point correspondences in the pair of images. We then draw these matches using the function ‘cv2.drawMatches()’.
• Using these matched feature points, we now get the essential matrix E using the function ‘cv2.findEssentialMat()’.
• Once we have the E matrix, and camera parameters we can estimate the camera pose using the function ‘cv2.recoverPose()’.


