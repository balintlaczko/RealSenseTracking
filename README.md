# RealSenseTracking
My tracking algorithm to sample and track an arbitrary number of points from a silhouette in Max using an Intel RealSense camera.

![depth_patch](https://user-images.githubusercontent.com/45127463/162577570-ff170659-f80b-428d-a3f4-bae08be16b0b.png)

## Dependencies
- [jit.realsense](https://github.com/robtherich/jit.realsense)
- xray package (download from Package Manager)
- cv.jit (download form Package Manager)

## The Algorithm

![depth_tracking](https://user-images.githubusercontent.com/45127463/162577308-54a53224-65d4-4179-917c-55fb73ffb512.png)

The algorithm mainly relies on optical flow, and namely the `cv.jit.track` object. It creates a silhouette from the depth map, radially downsamples it to N points and feeds that to `cv.jit.track`. For the active points it outputs the coordinates (in both spat5 and gl formats) and automatically reassigns lost points.

### The good part

- it's shape-agnostic, it will track any object in view
- the lion's share of the calculation happens in jitter matrices, and it is reasonably efficient
- battle-tested on stage :) (stable, no crashes)

### What can be improved

- does not really address noise
- requires a good amount of parameter tuning in each room / situation (kind of comes from the previous issue)
- the radial downsampling heavily favors convex shapes, and has issues with concave ones (the more concave, the less equally spaced the points will be on the silhouette)
- the automatic reassign branch for the lost points does not enforce equal spacing, and points gradually get clumped together over time (if not manually refreshed) 

## How to contribute
- Open issues on the tracker
- Create pull requests
- Become a collaborator

This project was part of my MA research on gestural sound spatialization at the Norwegian Academy of Music (2019-2021).
