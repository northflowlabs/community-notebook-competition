---
contact_name: "Northflow Technologies AS"
email_address: "hello@northflow.no"
notebook_authors: [
    "Northflow Technologies AS"
]
notebook_title: "Validating Sentinel-3 SLSTR Land Surface Temperature with climval"
docker_image_used: "Python"
makes_use_of_eopf_zarr_sample_service_data: false
incorporates_one_or_more_eopf_plugins: false
data_sources_used: ["Sentinel-3"]
had_challenges_working_with_sample_service_data: true
all_declarations_affirmed: true
---

# Submission

## Abstract (100 words)

This notebook demonstrates a validation pipeline for Sentinel-3 SLSTR Level-2 Land
Surface Temperature (LST) products in EOPF Zarr format, using climval, an open-source
Python library by Northflow Technologies AS. Products are discovered via the EOPF STAC
catalog with no credentials. The Zarr products could not be opened in our environment,
so the LST values, the ERA5 reference and the six metrics (RMSE, MAE, Mean Bias, NRMSE,
Pearson r, Taylor Skill Score) are seeded synthetic stand-ins: the notebook shows the
workflow, not a measured result. Reports are exported as HTML, JSON and Markdown, and a
custom Kling-Gupta Efficiency metric is added in ten lines.

## AI Disclosure: Describe how you used AI in authoring this notebook (100 words)

This notebook was developed with assistance from Claude (Anthropic). AI was used to
help structure the validation pipeline, draft code cells, and iterate on debugging
during live testing on the EOPF JupyterHub. The authors reviewed and ran all code. The
climval library used in this notebook was independently
developed and published to PyPI by Northflow Technologies AS. Scientific interpretation,
metric selection, and reference choices were made by the authors. AI assistance is
disclosed in accordance with the competition rules.

## References: Provide the URLs of all code sources that you used in authoring this notebook

- climval library: https://github.com/northflowlabs/climval
- climval on PyPI: https://pypi.org/project/climval
- pystac-client: https://github.com/stac-utils/pystac-client
- xarray: https://github.com/pydata/xarray
- EOPF STAC catalog: https://stac.core.eopf.eodc.eu

## Feedback (If you answered `true` to `had_challenges_working_with_sample_service_data` please provide feedback here!)

The EOPF STAC catalog was straightforward to query via pystac-client with no
authentication required. The main challenge was opening Zarr products directly:
`xarray.open_datatree()` and `zarr.open_group()` both raised `GroupNotFoundError`
on the EOPF JupyterHub environment, likely due to a zarr-python version mismatch
with the EOPF Zarr v3 product structure. The product URL also contained a relative
path segment (`/30/../`) that may affect fsspec resolution. We worked around this
by using STAC metadata and seeded synthetic values. Better documentation
on the required zarr-python version and a minimal working example for direct Zarr
access would significantly improve the developer experience.

## Declarations
By submitting this notebook:
- I/we agree to abide by the competition rules.
- I/we confirm this submission is my/our own original work.
- I/we grant the European Space Agency and thriveGEO GmbH a non-exclusive license to use, reproduce, modify, and display my/our work for promotional and educational purposes, including featuring it in the EOPF 101 online book.
- I/we confirm that the code submitted may be published under the Apache 2 license.

## Notes (optional)

climval (v0.1.0) is an open-source Python library developed by Northflow Technologies AS
specifically for composable climate model validation. It is publicly available at
https://pypi.org/project/climval and https://github.com/northflowlabs/climval.
