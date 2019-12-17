# labelstudio-image-segmenation
Image segmentation model for Label Studio

### Predict API

POST */predict*

##### Request:
```json
{
  "tasks": [{
    "data": {"image_url": "http://s3.amazonaws.com/heartex-private/cats_n_dogs/training_set/dogs/dog.1753.jpg"},
    "id": 1234
  }],
  "project": "123.1234567890",
  "schema": {
    "output_names": ["segmentation"],
    "input_names": ["image"],
    "input_values": ["image_url"],
    "input_types": ["Image"]
  },
  "model_version": "987654321",
  "params": {"some_useful_param": 1}
}
```

##### Response:
```json
{
  "results": [{
    "result": [{
      "from_name": "segmentation",
      "to_name": "image",
      "type": "polygonlabels",
      "value": {
        "polygonlabels": ["Dog"],
        "points": [[10,20], [30,40], [50,60]],
        "score": 0.8
      }
    }],
    "score": 0.95,
    "neighbors": [1234, 3456, 5678],
    "encodings": [0.1, 0.2, 0.3, 0.4],
    "cluster": 123
  }]
}
```

### Train API

POST /update

##### Request
```json
{
    "id": 1234,
    "project": "123.1234567890",
    "schema": {
      "output_names": ["segmentation"],
      "input_names": ["image"],
      "input_values": ["image_url"],
      "input_types": ["Image"]
    },
    "data": {"image_url": "http://s3.amazonaws.com/heartex-private/cats_n_dogs/training_set/dogs/dog.1753.jpg"},
    "meta": {"image_url": "optional alternative resource replacing image_url in data field"},
    "result": [{
      "from_name": "segmentation",
      "to_name": "image",
      "type": "polygonlabels",
      "value": {
        "polygonlabels": ["Dog"],
        "points": [[10,20], [30,40], [50,60]]
      }
    }],
    "retrain": true,
    "params": {
        "some train param": 1
    }
}
```

##### Response
```json
{
  "job": "training job ID"
}
```

