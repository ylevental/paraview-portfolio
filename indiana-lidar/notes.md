# Indiana Statewide Lidar — Land Cover Classification

## Dataset

**Source:** [IndianaMap Framework Lidar (2011)](https://doi.org/10.5069/G9959FHZ)
**Provider:** Indiana Statewide Imagery and LiDAR Program, distributed by OpenTopography
**Format:** LAS point cloud

## Classification

The corrected visualization contains four land cover classes based on ASPRS LAS standard codes:

| Class Code | Label | Color | Description |
|---|---|---|---|
| 2 | Ground | Tan (#C4A882) | Bare earth, roads, driveways |
| 1 | Buildings/Structures | Gray (#808080) | Rooftops, walls, and other built structures |
| 5 | High Vegetation | Dark green (#2D5F2D) | Tree canopy |
| 7 | Noise | Blue (#0000FF) | Low-point sensor errors (very few points) |

## Data Quality Findings

### Flight strip classification inconsistency

The raw dataset exhibited a visible banding pattern aligned with flight line swaths. Inspection revealed inconsistent ground labeling between processing batches: some strips labeled ground as ASPRS class 0 (Never Classified), while others used class 2 (Ground). Vegetation (class 5) was consistent across all strips, confirming all strips had been classified — the inconsistency was limited to ground label convention.

**Fix:** Calculator filter - `if(Classification == 0, 2, Classification)`

### Point density banding

After correcting classification, a subtler strip pattern remains visible due to point density variation between single-coverage and overlapping flight line regions. Overlap zones contain roughly twice the point density, creating a visible difference in rendering. This is an acquisition geometry artifact, not a processing error, and would typically be addressed by point thinning in the lidar processing pipeline.

## Techniques

- Categorical color mapping with custom colors and ASPRS-standard labels
- Point attribute inspection (Hover Points On)
- Calculator filter for conditional reclassification
- Color legend editing (Edit Color Legend Properties)
- High-resolution screenshot export
