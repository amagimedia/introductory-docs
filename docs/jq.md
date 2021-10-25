# JQ examples

JQ command line is a "filter" program which consumes json input stream and produces 
output in json or text format. It has a well defined syntax to express the filter
to acieve the required data transformation. Jq manual can be found [here](https://stedolan.github.io/jq/manual/).


## Usage Examples

Download an example json from https://github.com/ZackAkil/video-intelligence-api-visualiser/blob/main/assets/test_json.json.

This following examples apply different filters using `jq` cli on the above example json file.

#### Key Extraction Examples
```
jq 'keys' test_json.json
[
  "annotation_results"
]
```

```
jq '.annotation_results|.[0]' test_json.json | jq 'keys'
[
  "explicit_annotation",
  "face_detection_annotations",
  "input_uri",
  "logo_recognition_annotations",
  "object_annotations",
  "person_detection_annotations",
  "segment",
  "segment_label_annotations",
  "shot_annotations",
  "shot_label_annotations",
  "text_annotations"
]
```


#### Get Specific Objects

```
jq '.annotation_results|.[0]|.shot_annotations|.[0]' test_json.json 
{
  "start_time_offset": {},
  "end_time_offset": {
    "seconds": 6,
    "nanos": 798458000
  }
}

jq '.annotation_results|.[0]|.shot_annotations|.[0:4]' test_json.json 
[
  {
    "start_time_offset": {},
    "end_time_offset": {
      "seconds": 6,
      "nanos": 798458000
    }
  },
  {
    "start_time_offset": {
      "seconds": 6,
      "nanos": 840166000
    },
    "end_time_offset": {
      "seconds": 10,
      "nanos": 10000000
    }
  },
  {
    "start_time_offset": {
      "seconds": 10,
      "nanos": 51708000
    },
    "end_time_offset": {
      "seconds": 14,
      "nanos": 431083000
    }
  },
  {
    "start_time_offset": {
      "seconds": 14,
      "nanos": 472791000
    },
    "end_time_offset": {
      "seconds": 16,
      "nanos": 141125000
    }
  }
]
```

#### Get POST paths

Get all POST paths from github_swagger.json file checked in here.

```
jq -c '.paths | to_entries[] | select(.value.patch?) | .key' github_swagger.json
```


## Good online resources
1. [Taking a simple example through jq analysis](https://www.youtube.com/watch?v=EIhLl9ebeiA&list=PLKaiHc24qCTSOGkkEpeIMupEmnInqHbbV&index=2)
2. JQ in [depth](https://earthly.dev/blog/jq-select/)

