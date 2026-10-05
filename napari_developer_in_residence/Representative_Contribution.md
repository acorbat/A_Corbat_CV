# Representative Contribution

**GulLiver: a Python workflow for whole-slide liver immunostaining images**  
Repository: https://github.com/acorbat/gulliver

I developed GulLiver to make analysis of large liver whole-slide images more systematic and reproducible. The workflow segments and classifies Sox9-positive structures and vascular regions, then quantifies properties such as region area and distances between vessel classes. Its outputs are stored as OME-Zarr so large image data and labels can be handled and inspected without treating an entire slide as a small, in-memory image; the repository documents visualization of those results in napari.

The contribution combined domain-specific image analysis with a usable Python package and command-line workflow. I organized processing into segmentation and quantification steps, made image and label outputs available for inspection, and documented installation and use so collaborators could run the pipeline on their own data. This project reflects how I approach scientific software: translate a concrete user question into a repeatable workflow, preserve the connection between measurements and image data, and make intermediate results inspectable. It is a representative personal software project, not an upstream napari pull request.