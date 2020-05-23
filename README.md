# rust-cv

Rust CV is a project to implement computer vision algorithms in Rust.

Many people are familiar with covolutional neural networks and machine learning in computer vision, but computer vision is much more than that. One of the first things that Rust CV focused on was algorithms in the domain of Multiple-View Geometry (MVG). Today, Rust now has enough MVG algorithms to perform relatively simple camera tracking and odometry tasks. Weakness still exists within image processing and machine learning domains.

Here are some of the domains of computer vision that Rust CV intends to persue along with examples of the domain (not all algorithms below live within the Rust CV organization, and some of these may exist and are unknown):

* [o] Image processing
  * [o] Diffusion & blur
    * [x] [Gaussian blur](https://docs.rs/imageproc/0.20.0/imageproc/filter/fn.gaussian_blur_f32.html)
    * [ ] Fast Explicit Diffusion (FED) (implementation exists [within `akaze` crate](https://github.com/rust-cv/akaze/blob/a25ff0448d95600f10c69acb7e4f7d95045c1293/src/fed_tau.rs))
  * [ ] Contrast enhancement
    * [ ] Histogram equalization
  * [ ] Edge detection & gradient extraction
    * [ ] Scharr filters (exists [within `akaze` crate](https://github.com/rust-cv/akaze/blob/a25ff0448d95600f10c69acb7e4f7d95045c1293/src/derivatives.rs))
    * [ ] Sobel filter
    * [ ] Canny edge detector
* [o] Multiple-View Geometry (MVG)
  * [o] Feature extraction
    * [x] [AKAZE](https://docs.rs/akaze/0.3.1/akaze/struct.Akaze.html)
    * [x] [FAST](https://docs.rs/imageproc/0.20.0/imageproc/corners/index.html)
    * [ ] ORB
    * [ ] SIFT
  * [o] [Camera models and calibration](https://docs.rs/cv-core/0.10.0/cv_core/trait.CameraModel.html) (both from and to image coordinates from bearings)
    * [o] Pinhole Camera
      * [x] [Skew, focals, and principle point](https://docs.rs/cv-pinhole/0.1.1/cv_pinhole/struct.CameraIntrinsics.html)
      * [x] [K1 radial distortion](https://docs.rs/cv-pinhole/0.1.1/cv_pinhole/struct.CameraIntrinsicsK1Distortion.html)
      * [ ] K1-K6 radial distortion
    * [ ] Fisheye Camera
      * [ ] Skew, focals, and principle point
      * [ ] K1-K4 fisheye distortion
    * [ ] Equirectangular (see [Wikipedia article](https://en.wikipedia.org/wiki/Equirectangular_projection))
  * [o] Matching
    * [x] Descriptor matching strategies
      * [x] [Brute force](https://docs.rs/space/0.10.3/space/fn.linear_knn.html) (for camera traking with binary features)
      * [x] [HNSW](https://docs.rs/hnsw/0.6.1/hnsw/struct.HNSW.html) (for ANN in large datasets/loop closure/SfM)
    * [ ] Filtering strategies
      * [ ] Symmetric matching (exists [within vslam-sandbox](https://github.com/rust-cv/vslam-sandbox/blob/0a0bd760ceee2da38f0626a8a8678b9e98a657e1/src/main.rs#L59-L75))
      * [ ] Lowe's ratio test matching
  * [o] Geometric verification (abstractions in [sample-consensus](https://docs.rs/sample-consensus/0.2.0/sample_consensus/))
    * [o] [Consensus algorithms](https://docs.rs/sample-consensus/0.2.0/sample_consensus/trait.Consensus.html)
      * [x] [ARRSAC](https://docs.rs/arrsac/0.3.0/arrsac/struct.Arrsac.html)
      * [ ] AC-RANSAC
      * [ ] RANSAC
    * [o] [Estimation algorithms](https://docs.rs/sample-consensus/0.2.0/sample_consensus/trait.Estimator.html)
      * [x] P3P (see [Wikipedia article](https://en.wikipedia.org/wiki/Perspective-n-Point#P3P))
        * [x] [Lambda Twist](https://docs.rs/lambda-twist/0.2.0/lambda_twist/struct.LambdaTwist.html)
    * [o] [Models](https://docs.rs/sample-consensus/0.2.0/sample_consensus/trait.Model.html)
      * [x] [Essential matrix](https://docs.rs/cv-core/0.10.0/cv_core/struct.EssentialMatrix.html)
        * [x] With residual for [feature matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureMatch.html)
      * [x] [Pose of world relative to camera](https://docs.rs/cv-core/0.10.0/cv_core/struct.WorldPose.html)
        * [x] With residual for [feature to world matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureWorldMatch.html)
      * [ ] [Relative pose of camera](https://docs.rs/cv-core/0.10.0/cv_core/struct.RelativeCameraPose.html)
        * [ ] With residual for [feature matches](https://docs.rs/cv-core/0.10.0/cv_core/struct.FeatureMatch.html)
    * [ ] [PnP](https://github.com/rust-cv/pnp) (estimation, outlier filtering, and optimization) (incomplete)
