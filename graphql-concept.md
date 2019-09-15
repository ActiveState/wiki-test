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
    "id": "AAA-83838-03030-83838"
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


We can retreive the artifacts from the ingredient


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
      "timestamp": 1234
      "activestate/A": {
        "status": BUILT
        "revision": 0
        "version": 0
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
 src : "http://activestate.com/some-tar-file"
 builder: activestate/builders/concat.sh@123
 args: ["hello.txt"]
){
  id
  revision
}
``` 


```
{
  name: B

  requires:
    
    
}
```
