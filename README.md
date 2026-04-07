# MC3D-samples
A dataset of 200 motorcycle complexes computed on seamless parametrizations via the 3D motorcycle complex ([MC3D](https://github.com/HendrikBrueckler/MC3D)).

The dataset has been prepared by calling MC3D on three different input datasets containing seamless parametrizations of tetrahedral meshes in ```.hexex``` file format, listed below.
After motorcycle complex construction, all tetrahedral meshes have been heavily remeshed and decimated while preserving features as well as parametrization injectivity to reduce file size and speed up file handling.

### First Dataset: Seamless Parametrizations of models from [*Singularity-Constrained Octahedral Fields*](https://dl.acm.org/doi/10.1145/3197517.3201344)
The input seamless parametrizations were kindly provided to us by the paper's authors.
This part of the dataset contains no feature markers.

### Second Dataset: Seamless Parametrizations of [*HexMe*](https://github.com/cgg-bern/hex-me-if-you-can) models
The input seamless parametrizations were computed using the [AlgoHex](https://github.com/cgg-bern/AlgoHex) library.
These inputs are the only ones containing explicit feature markers, propagated to the output files.
Non-injective seamless parametrizations were filtered out before computing the motorcycle complexes on the rest.

### Third Dataset: Seamless Parametrizations, guided by meta-meshes via models collected under [*HexaLab*](https://github.com/cnr-isti-vclab/HexaLab)
The input seamless parametrizations were computed using a modified version of the AlgoHex library, where blank tetrahedral meshes of the models were input together with the hexahedral meshes from HexaLab, serving as meta-meshes to guide the initial frame-field (cf. [CubeCover](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-8659.2011.02014.x)).
Non-injective seamless parametrizations were filtered out before computing the motorcycle complexes on the rest.
This part of the dataset contains no feature markers.

## Output file format
The output file format is specified as follows:
```
<N(number of vertices)>
<v1_coord_x v1_coord_y v1_coord_z>
...
<vN_coord_x vN_coord_y vN_coord_z>
<M(number of tets)>
<tet1_vidx1 tet1_vidx2 tet1_vidx3 tet1_vidx4 tet1_v1_paramU tet1_v1_paramV tet1_v1_paramW tet1_v2_paramU tet1_v2_paramV tet1_v2_paramW tet1_v3_paramU tet1_v3_paramV tet1_v3_paramW tet1_v4_paramU tet1_v4_paramV tet1_v4_paramW>
...
<tetM_vidx1 tetM_vidx2 tetM_vidx3 tetM_vidx4 tetM_v1_paramU tetM_v1_paramV tetM_v1_paramW tetM_v2_paramU tetM_v2_paramV tetM_v2_paramW tetM_v3_paramU tetM_v3_paramV tetM_v3_paramW tetM_v4_paramU tetM_v4_paramV tetM_v4_paramW>
<W(number of MC wall facets)>
<facet1_vidx1 facet1_vidx2 facet1_vidx3 facet1_dist>
...
<facetW_vidx1 facetW_vidx2 facetW_vidx3 facetW_dist> 
<FV(number of feature vertices) FE(number of feature edges) FF(number of feature facets)>
<feature_v1_idx>
...
<feature_vFV_idx>
<feature_edge1_vidx1 feature_edge1_vidx2>
...
<feature_edgeFE_vidx1 feature_edgeFE_vidx2>
<feature_facet1_vidx1 feature_facet1_vidx2 feature_facet1_vidx3>
...
<feature_facetFE_vidx1 feature_facetFF_vidx2 feature_facetFF_vidx3>
```
These values are in the following formats:
"number", "idx": int
"coord", "dist": float
"param": rational number (string-encoded via GMP library; <+-numerator/denominator>, both encoded as integers with arbitrarily many digits)
