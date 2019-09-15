# First principals

There is an Ingredient *A* whose source is the content "Hell World!"

It uses the concat builder and sends the hello.txt argument

## Request
 ```graphql
mutation AddIngredient (
 name : "activestate/A"
 src : "data:,Hello%2C%20World!"
 builder: activestate/builders/concat.sh@123
 args: ["hello.txt"]
){
  id
  revision
}
``` 


## Response

```json
{
  "data" : {
    "id": "AAA-83838-03030-83838",
    "revision": 0
  }
}
```


Note the concat builder takes a url and saves it's results to the name that was set as the first argument.


It's implementated in the ActiveState/builders.git repo

```
activestate/builders/
/
   builders/
        concat.sh
```

It's contents are simply (note being hand wavy on how you get a data url to contents is bash...)

```bash
echo data_url_to_file($SRC) > $out/$1
```


We can retreive the artifacts for the ingredient if it were built at time 1234


## Request


```graphql

query {
  artifacts(time=1234, platform=macos){
    activestate/A
  }
}
```

The `artifacts()` query will return a list of artifact records that include it's status, version and revisions.
Each artifact will have a list of URLs that are the outputed results after the build process.


```json
{
  "data" : {
    "artifacts" : {
      "timestamp": 1234,
      "activestate/A": {
        "status": BUILT,
        "revision": 0,
        "version": 0,
        "urls": ["http://activestate.com/storage/AAA-83838-03030-83838-activestate-A/hello.txt"]
      }
    }
  }
}
```


There is an ingredient B who depends on A

## Request
 ```graphql
mutation AddIngredient (
 name : "activestate/B"
 src : "http://activestate.com/some-other-file"
 builder: activestate/builders/zip.py@123
 requires : {
    "activestate/A/hello.txt": "Latest"
 }
){
  timestamp
  id
  revision
}
``` 

## Response

```json
{
  "data" : {
    timestamp: 1235
    "id": "BBB-83838-03030-83838",
    "revision": 0
  }
}
```


Above we created an ingredient **B** who depends on A and uses `some-other-builder.py` to build it whose contents look like this

```python
from zimpfile import ZipFile
import os
import json

SRC = os.environ['SRC']
OUT = os.environ['OUT']
REQUIREMENTS = json.loads(os.environ['REQUIREMENTS'])

OUT_PATH = os.path.join(OUT, os.path.basename(SRC), '.zip)

with ZipFile(OUT_PATH, 'w') as myzip:
    myzip.write(SRC)
    myzip.write(REQUIRMENTS['activestate/A/hello.txt'])
```

Note this time we used a builder script written in python which creates a new zipfile named after our SRC (in this case some-other-file.zip). In the zip is placed the SRC which is `http://activestate.com/some-other-file` *AND* hello.txt which was available
from activestate/A.

Note requirements are passed as a JSON structure, the contents and other metadata is available in the REQUIREMENTS json structure. The zip builder uses this information to locate the contents of hello.txt and include it in the `some-other-file.zip`


## Request


```graphql

query {
  artifacts(time=1234, platform=macos){
    activestate/B
  }
}
```

## Response


```json
{
  "errors" : {
    timestamp: 1235
    "id": "BBB-83838-03030-83838",
    "revision": 0
  }
}
```
