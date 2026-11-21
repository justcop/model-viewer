# 3D Model Viewer — GitHub Pages

A general-purpose, entirely client-side 3D mesh viewer. Intended to be published as a **public GitHub Pages website** from the repository `justcop/model-viewer`.

## Viewer

Once GitHub Pages is enabled, use `https://justcop.github.io/model-viewer/`.

- **Files:** drag/drop or choose `.stl`, `.obj`, `.off`, ASCII `.ply`, or mesh `.json`.
- **URLs:** paste a CORS-enabled direct link; ordinary GitHub `/blob/` paths are converted to `raw.githubusercontent.com`. The hosting server must permit browser `fetch()`.
- **Model data:** paste ASCII STL/OBJ/OFF/PLY or mesh JSON into the editor.
- **Shareable model URL:** `https://justcop.github.io/model-viewer/?url=https%3A%2F%2Fraw.githubusercontent.com%2Fjustcop%2Fmodel-viewer%2Fmain%2Fexamples%2Finfowindow-aa-bezel.stl`.
- Rotate/zoom, toggle axes, fit, compare multiple meshes, or export a PNG snapshot.
- **Try sample** button loads the real InfoWindow bezel STL from the same site.

No model is uploaded to a server when loading a local file. Remote URL fetching occurs from the browser (so the file host will see the browser's request). GitHub Pages and models committed to this public repository are public.

**OpenSCAD `.scad` source is not a mesh.** The website cannot compile it directly. Use `make_viewer.py` with OpenSCAD installed on your computer, or export it to STL first. Other solid CAD formats (STEP/3MF/Fusion) are currently not supported; convert to STL/OBJ beforehand.

## Deploy

1. **Repository setup is complete:** files are committed to the public [`justcop/model-viewer`](https://github.com/justcop/model-viewer) repository on `main`.
2. To publish the website, open **[Settings → Pages](https://github.com/justcop/model-viewer/settings/pages)**. Under **Build and deployment**, choose **Deploy from a branch**, select branch `main` and folder `/(root)`, and press **Save**. This is a one-time setting.
3. Once GitHub Pages confirms deployment, open **https://justcop.github.io/model-viewer/**. Later updates to `main` publish automatically; there is no custom Actions workflow to maintain.

This is a pure static site; no build, paid hosting or GitHub Actions workflow is required. The browser requires network access for the Plotly CDN unless you use an offline generated HTML.

## Convert a model into a portable viewer HTML

```bash
python make_viewer.py your-model.stl --offline -o model-preview.html
python make_viewer.py your-model.scad --offline -o model-preview.html
cat your-model.scad | python make_viewer.py - --type scad --offline -o model-preview.html
```

`--offline` embeds Plotly and requires `python -m pip install plotly`. `.scad` compilation requires OpenSCAD installed. The helper also accepts compatible file URLs, but the browser supports loading URLs directly.

The sample STL represents an *unverified experimental* InfoWindow AA holder bezel; confirm dimensions before manufacturing.