
# Format of JSON replies

>This entire document is just a proposal for discussion.


In formatting  JSON replies, what the specification calls "lists" will be JSON arrays.  URNs will be string values.  Citable nodes will be json "objects" (what I've called "maps") with five member objects.

The reply itself is presumably a JSON object.  We need some good way to send back both exceptions and valid results.  {==Maybe the object always has a "status" member, that can have one of two values (mabye "exception" or "success" ?)  Exceptions could then have a single "==}{>>I feel uneasy about this. I'd prefer if the reponse has the same struture. We could include a status field for all of them that either returns "succes" or "exception: Invalid URN valid 'xyz". TK.<<}



I'm guessing we're looking at something like this:

1. A valid but empty result

    {
      "status": "success"
      {}
    }
    
    {>>TK: I suggest
    ```json
    {"status":"success"}    
    ```
    <<<}

2. An exception


    {
      "status": "exception"
      "message": "Invalid URN valid 'xyz'"
    }
    
    {>>TK: Should be
    ```json
    {"status":"Exception","message":"Invalid URN valid 'xyz'"}
    ```
    <<<}

3. A list of URN values

    {
      "status": "success"
      {
        `URN1`,
        `URN2`
      }
    }
    {>>TK: I suggest
    ```json
    {"status":"Success","URN":["URN1","URN2"]}
    ```
    <<<}

4. A list of citable nodes


    {
      "status": "success"
      {
        { "URN" : `URN1`,
          "text" : `STRING VALUE`,
          "previous" : `URNPREV or ""`,
          "following" : `URNNEXT or ""`,
          "sequence" : `JSON int or intface VALUE`,
      }
    }
    {>>TK: I suggest
    ```json
    {
        "requestUrn":"URN1:1.1",
        "status":"Success",
        "Nodes":[
                    {
                        "URN":"URN1:1.1",
                        "text":"String Value",
                        "previous":"",
                        "next":"URN1:1.2",
                        "index":1
                    }
                ]
    }
    ```
    <<<}

Should previous/following values be a JSON empty string or a `null` value when there is no prevous or following URN?

{>> CWB: I would like one more piece of information at the top: "requestUrn". If I ask for *Iliad* 1, or *Iliad* 1.1-1.611, the array of Citable Nodes will be the same, but I would like to have in the reply the request-URN.  <<}
{>>TK: +1 <<}}