# CT Head — Volume Rendering

## Dataset

**Source:** [vtkvolume-data/CT-Head](https://github.com/aashish24/vtkvolume-data/tree/master/CT-Head)
**Format:** VTK structured points (ImageData)
**Description:** CT scan of a human head, commonly used in VTK/ParaView volume rendering examples.

## Visualization

Volume rendering of the CT head dataset using ray-cast rendering with a custom opacity transfer function. The visualization reveals the skull, eye sockets, nasal cavity, jaw, and teeth through semi-transparent soft tissue.

### Transfer function design

The default linear opacity ramp renders air and low-density background as a visible haze. The opacity curve was modified to create a threshold cutoff: scalar values in the lower ~25–30% of the range are mapped to zero opacity, removing background entirely. The remaining range ramps from low opacity (soft tissue, rendered as translucent blue) to full opacity (dense bone, rendered as orange/cream).

The "Cool to Warm (Extended)" color preset maps low-density soft tissue to blue tones and high-density bone to warm orange, producing a natural visual hierarchy where bone reads as solid structure and soft tissue appears as a translucent envelope.

### Slice-spacing artifact

Concentric ring patterns are visible on the top of the skull in the oblique view. This is a staircase artifact caused by the relatively coarse spacing between axial CT slices. Surfaces that run nearly parallel to the slice plane (like the top of the cranium) exhibit this stepping effect. This is an inherent limitation of the dataset's axial resolution, not a rendering error.

## Techniques

- Volume rendering (ray-cast) representation
- Opacity transfer function editing to remove background haze
- Custom color map selection for tissue differentiation
- Background color adjustment (solid black) for medical imaging presentation
- Multi-angle high-resolution screenshot export (frontal and oblique views)
