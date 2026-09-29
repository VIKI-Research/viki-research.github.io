# Airport annotation transfer

`LOW_TELJES_80k_2x4K.glb` is an unchanged copy of the supplied export.
The original `Airport_Sample` assets remain available as a reference.

The replacement contains the same site with a different reconstruction origin
and bounds. All two POIs and three strokes (50 points) were transferred together;
IDs, labels, symbols, styles, timestamps, and viewer settings were preserved.
POI normals were rotated with the geometry alignment.

## Registration

Height-map feature matching found 208 consistent correspondences, followed by
trimmed rigid closest-point registration of the two meshes. The median sampled
vertex-to-vertex residual was 1.13 model units (95th percentile 3.86), so this is
an approximate alignment between differently reduced scans, not survey control.
No independent scale change was fitted.

For a source position in the old viewer's normalized scene:

1. Undo the old viewer normalization (longest bounding-box dimension / 5),
   then add the old world bounding-box center.
2. Subtract `[725486.5, 5218562, 319.6917419433594]`.
3. Apply the following row-major rotation, then add
   `[-43.06685382345163, 61.41991731036404, -18.359311627627836]`.
4. Subtract the new GLB bounding-box center and divide by its longest
   bounding-box dimension / 5.

```text
 0.9999999339430709  -0.0002675607338644   0.0002460185224830
 0.0002675100587775   0.9999999430031143   0.0002059906200129
-0.0002460736234621  -0.0002059247939751   0.9999999485213767
```

The new GLB bounds are:

```text
min: [-387.3818664550781, -17.663354873657227, -325.636962890625]
max: [ 386.469482421875,   17.29461669921875,   325.64678955078125]
```

## Coordinate companion

The export processing metadata records its Blender world center as
`[725486.5, -319.6917419433594, 5218562]`. Comparing the final GLB with the
source OBJ confirms that adding `[725486.5, 5218562, 319.6917419433594]`
recovers the source OBJ coordinate basis. The replacement `.rsInfo` retains
the source CRS and uses the inverse of this translation as `transformToModel`.
The annotation registration above is separate from this export-origin mapping.
