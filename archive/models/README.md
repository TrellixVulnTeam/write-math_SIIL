Put all JSON models in here. All models should be named like this:

`YYYY-MM-DD-HH-MM.json`

Additional information about the model should be organzied in a YAML file
called `YYYY-MM-DD-HH-MM.yml`. Those YAML files should have names like this:

All paths should be relative to the `write-math` root path.

```yaml
data-source: archive/datasets/2014-08-04-18-24-handwriting_datasets-raw.pickle
preprocessed: archive/datasets/2014-08-05-13-59-handwriting_datasets-preprocessed.pickle
data:
    training: archive/pfiles/2014-08-05-17-29-traindata.pfile
    validating: archive/pfiles/2014-08-05-17-29-validdata.pfile
    testing: archive/pfiles/2014-08-05-17-29-testdata.pfile
training: nntoolkit train --epochs 300 --learning-rate 1 --momentum 0.1 {{training}} {{validation}} < {{src_model}} > {{target_model}}
preprocessing:
    - scale_and_shift:
    - connect_lines:
        - minimum_distance: 0.01
    - douglas_peucker:
        - EPSILON: 0.01
    - space_evenly:
        - kind: cubic
        - number: 100
    - scale_and_shift:
features:
    - Stroke_Count:
    - Constant_Point_Coordinates:
        - lines: -1
        - points_per_line: 81
        - fill_empty_with: 0
model:
    type: mlp
    topology: '244:488:370'
    folder: 'archive/models/'
    basename: '2014-08-05-21-00'
```