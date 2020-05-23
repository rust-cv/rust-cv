# rust-cv

Rust CV is a project to implement computer vision algorithms in Rust.

## What is computer vision

Many people are familiar with covolutional neural networks and machine learning in computer vision, but computer vision is much more than that. One of the first things that Rust CV focused on was algorithms in the domain of Multiple-View Geometry (MVG). Today, Rust now has enough MVG algorithms to perform relatively simple camera tracking and odometry tasks. Weakness still exists within image processing and machine learning domains.

## Goals

Here are some of the domains of computer vision that Rust CV intends to persue along with examples of the domain (not all algorithms below live within the Rust CV organization, and some of these may exist and are unknown):

* [ ] Image processing ([Wikipedia](https://en.wikipedia.org/wiki/Digital_image_processing))
  * [ ] Diffusion & blur
    * [x] [Gaussian blur](https://docs.rs/imageproc/0.20.0/imageproc/filter/fn.gaussian_blur_f32.html) ([Wikipedia](https://en.wikipedia.org/wiki/Gaussian_blur))
    * [ ] Fast Explicit Diffusion (FED) (implementation exists [within `akaze` crate](https://github.com/rust-cv/akaze/blob/a25ff0448d95600f10c69acb7e4f7d95045c1293/src/fed_tau.rs))
  * [ ] Contrast enhancement
    * [ ] Normalization ([Wikipedia](https://en.wikipedia.org/wiki/Normalization_(image_processing)))
    * [ ] Histogram equalization ([Wikipedia](https://en.wikipedia.org/wiki/Histogram_equalization))
  * [ ] Edge detection ([Wikipedia](https://en.wikipedia.org/wiki/Edge_detection)) & gradient extraction ([Wikipedia](https://en.wikipedia.org/wiki/Image_derivatives))
    * [ ] Scharr filters (exists [within `akaze` crate](https://github.com/rust-cv/akaze/blob/a25ff0448d95600f10c69acb7e4f7d95045c1293/src/derivatives.rs))
    * [ ] Sobel filter ([Wikipedia](https://en.wikipedia.org/wiki/Sobel_operator))
    * [ ] Canny edge detector ([Wikipedia](https://en.wikipedia.org/wiki/Canny_edge_detector))
* [ ] Multiple-View Geometry (MVG)
  * [ ] Feature extraction ([Wikipedia](https://en.wikipedia.org/wiki/Feature_detection_(computer_vision)))
    * [x] [AKAZE](https://docs.rs/akaze/0.3.1/akaze/struct.Akaze.html)
    * [x] [FAST](https://docs.rs/imageproc/0.20.0/imageproc/corners/index.html) ([Wikipedia](https://en.wikipedia.org/wiki/Features_from_accelerated_segment_test))
    * [ ] ORB ([Wikipedia](https://en.wikipedia.org/wiki/Oriented_FAST_and_rotated_BRIEF))
    * [ ] SIFT ([Wikipedia](https://en.wikipedia.org/wiki/Scale-invariant_feature_transform))
  * [ ] [Camera models and calibration](https://docs.rs/cv-core/0.10.0/cv_core/trait.CameraModel.html) (both from and to image coordinates from bearings)
    * [ ] Pinhole Camera ([Wikipedia](https://en.wikipedia.org/wiki/Pinhole_camera))
      * [x] [Skew, focals, and principle point](https://docs.rs/cv-pinhole/0.1.1/cv_pinhole/struct.CameraIntrinsics.html)
      * [ ] Kn radial distortion ([Wikipedia](https://en.wikipedia.org/wiki/Distortion_(optics)#Radial_distortion))
        * [x] [K1 radial distortion](https://docs.rs/cv-pinhole/0.1.1/cv_pinhole/struct.CameraIntrinsicsK1Distortion.html)
        * [ ] K1-K6 radial distortion
    * [ ] Fisheye Camera ([Wikipedia](https://en.wikipedia.org/wiki/Fisheye_lens))
      * [ ] Skew, focals, and principle point
      * [ ] K1-K4 fisheye distortion (same as OpenCV)
    * [ ] Equirectangular ([Wikipedia](https://en.wikipedia.org/wiki/Equirectangular_projection))
  * [ ] Matching ([Wikipedia](https://en.wikipedia.org/wiki/Point_feature_matching))
    * [x] Descriptor matching strategies
      * [x] [Brute force](https://docs.rs/space/0.10.3/space/fn.linear_knn.html) (for camera traking with binary features)
      * [x] [HNSW](https://docs.rs/hnsw/0.6.1/hnsw/struct.HNSW.html) (for loop closure)
    * [ ] Filtering strategies
      * [ ] Symmetric matching (exists [within vslam-sandbox](https://github.com/rust-cv/vslam-sandbox/blob/0a0bd760ceee2da38f0626a8a8678b9e98a657e1/src/main.rs#L59-L75))
      * [ ] Lowe's ratio test matching
  * [ ] Geometric verification (utilized abstractions in [sample-consensus](https://docs.rs/sample-consensus/0.2.0/sample_consensus/))
    * [ ] [Consensus algorithms](https://docs.rs/sample-consensus/0.2.0/sample_consensus/trait.Consensus.html)
      * [x] [ARRSAC](https://docs.rs/arrsac/0.3.0/arrsac/struct.Arrsac.html)
      * [ ] AC-RANSAC
      * [ ] RANSAC ([Wikipedia](https://en.wikipedia.org/wiki/Random_sample_consensus))
    * [ ] [Estimation algorithms](https://docs.rs/sample-consensus/0.2.0/sample_consensus/trait.Estimator.html)
      * [x] P3P ([Wikipedia](https://en.wikipedia.org/wiki/Perspective-n-Point#P3P))
        * [x] [Lambda Twist](https://docs.rs/lambda-twist/0.2.0/lambda_twist/struct.LambdaTwist.html)
      * [x] Motion estimation ([Wikipedia](https://en.wikipedia.org/wiki/Motion_estimation))
        * [x] [Eight Point](https://docs.rs/eight-point/0.4.0/eight_point/struct.EightPoint.html) ([Wikipedia](https://en.wikipedia.org/wiki/Eight-point_algorithm))
        * [ ] [Nister-Stewenius](https://github.com/rust-cv/nister-stewenius/) (basically done, but not packaged up)
    * [ ] [Models](https://docs.rs/sample-consensus/0.2.0/sample_consensus/trait.Model.html)
      * [x] [Essential matrix](https://docs.rs/cv-core/0.10.0/cv_core/struct.EssentialMatrix.html) ([Wikipedia](https://en.wikipedia.org/wiki/Essential_matrix))
        * [x] With residual for [feature matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureMatch.html)
      * [x] [Pose of world relative to camera](https://docs.rs/cv-core/0.10.0/cv_core/struct.WorldPose.html) ([Wikipedia](https://en.wikipedia.org/wiki/3D_pose_estimation))
        * [x] With residual for [feature to world matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureWorldMatch.html)
      * [x] [Relative pose of camera](https://docs.rs/cv-core/0.10.0/cv_core/struct.RelativeCameraPose.html) ([Wikipedia](https://en.wikipedia.org/wiki/3D_pose_estimation))
        * [ ] With residual for [feature matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureMatch.html)
      * [ ] Homography matrix ([Wikipedia](https://en.wikipedia.org/wiki/Homography_(computer_vision)))
        * [ ] With residual for [feature matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureMatch.html)
    * [ ] [PnP](https://github.com/rust-cv/pnp) (estimation, outlier filtering, and optimization) (incomplete)
  * [ ] Image registration ([Wikipedia](https://en.wikipedia.org/wiki/Image_registration))
  * [ ] Real-time depth-map estimation (for direct visual odometry algorithms that require it) ([Wikipedia](https://en.wikipedia.org/wiki/Depth_map))
  * [ ] Visual concept detection (used for loop closure)
    * [ ] Bag of Visual Words (BoW, see [Wikpedia article](https://en.wikipedia.org/wiki/Bag-of-words_model_in_computer_vision))
    * [ ] Second order occurence pooling (as per the paper "Higher-order Occurrence Pooling for Bags-of-Words: Visual Concept Detection")
    * [ ] Fisher vector encoding
    * [ ] Learned place recognition (also see pattern recognition domain below)
  * [ ] Reconstruction ([Wikipedia](https://en.wikipedia.org/wiki/3D_reconstruction))
    * [ ] Visibility graph ([Wikipedia](https://en.wikipedia.org/wiki/Visibility_graph))
    * [ ] Graph optimization
    * [ ] Loop closure ([Wikipedia](https://en.wikipedia.org/wiki/Simultaneous_localization_and_mapping#Loop_closure))
    * [ ] Exporting ([point cloud Wikipedia](https://en.wikipedia.org/wiki/Point_cloud))
      * [ ] To NVM file
      * [ ] To PLY file ([Wikipedia](https://en.wikipedia.org/wiki/PLY_(file_format)))
  * [ ] Post-reconstruction depth-map estimation (for reconstruction post-processing) ([Wikipedia](https://en.wikipedia.org/wiki/Depth_map))
  * [ ] Densification
    * [ ] Using more extracted features
      * [ ] Using curvature maximas (as per "VITAMIN-E: VIsual Tracking And MappINg with Extremely Dense Feature Points")
    * [ ] Using patch-match ([Wikipedia](https://en.wikipedia.org/wiki/PatchMatch)) and depth-map
    * [ ] Using depth-map only with edge detection
  * [ ] Meshing ([Wikipedia](https://en.wikipedia.org/wiki/Point_cloud#Conversion_to_3D_surfaces))
    * [ ] Delaunay triangulation
      * [ ] Filtered with NLTGV minimization (as per "VITAMIN-E: VIsual Tracking And MappINg with Extremely Dense Feature Points")
    * [ ] Poisson surface reconstruction ([Wikipedia](https://en.wikipedia.org/wiki/Poisson%27s_equation#Surface_reconstruction))
    * [ ] Surface refinement
    * [ ] Texturing ([related Wikipedia](https://en.wikipedia.org/wiki/Texture_mapping))
* [ ] Pattern recognition
  * [x] k-NN search
    * [x] [Brute force](https://docs.rs/space/0.10.3/space/fn.linear_knn.html)
    * [x] [HNSW](https://docs.rs/hnsw/0.6.1/hnsw/struct.HNSW.html)
  * [ ] Face recognition ([Wikipedia](https://en.wikipedia.org/wiki/Facial_recognition_system))
  * [ ] Object recognition ([Wikipedia](https://en.wikipedia.org/wiki/Outline_of_object_recognition))
  * [ ] Place recognition (can assist in MVG)
  * [ ] Segmentation ([Wikipedia](https://en.wikipedia.org/wiki/Image_segmentation))
    * [ ] Semantic segmentation mapping (see [this blog post](https://www.jeremyjordan.me/semantic-segmentation/))

To support computer vision tooling, the following will be implemented:

* [ ] Point clouds ([Wikipedia](https://en.wikipedia.org/wiki/Point_cloud))
  * [ ] Display tool
    * [ ] LoD refinement ([Wikipedia](https://en.wikipedia.org/wiki/Level_of_detail))
      * [ ] Potree file format ([GitHub](https://github.com/potree/potree/))
    * [ ] PLY files ([Wikipedia](https://en.wikipedia.org/wiki/PLY_(file_format)))
