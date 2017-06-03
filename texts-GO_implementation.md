# `/texts`-Service in Go

## Go & JSON reply

To express the [requirements for the JSON format](https://github.com/cite-architecture/cite-services-spec/blob/master/json-formatting.md) in Go the following structs have to be created:

1. A TextResponse struct:
  ```go
  type TextResponse struct {
    RequestUrn string`json:"requestUrn,omitempty"`
    Status string`json:"status"`
    Message string `json:"message,omitempty"`
    URN []string `json:",omitempty"`
    Nodes []Node `json:",omitempty"`
   }
```
2. A Node struct:
  ```go
  type Node struct {
	URN string `json:"URN"`
	Text string `json:"text,omitempty"`
	Previous string `json:"previous"`
	Next string `json:"next"`
	Index int `json:"index"`
}
  ```

### Test

#### Code
```go
func main() {
	ValidEmpty := &TextResponse{
		Status: "Success",
	}
	ValidEmptyJSON, _ := json.Marshal(ValidEmpty)
	fmt.Println(string(ValidEmptyJSON))

	Exception := &TextResponse{
		Status: "Exception",
		Message: "Invalid URN valid 'xyz'",
	}
	ExceptionJSON, _ := json.Marshal(Exception)
	fmt.Println(string(ExceptionJSON))

	ListURN := &TextResponse{
		Status: "Success",
		URN: []string{"URN1", "URN2"},
	}
	ListURNJSON, _ := json.Marshal(ListURN)
	fmt.Println(string(ListURNJSON))

	CitNodes := &TextResponse{
		RequestUrn: "URN1:1.1",
		Status: "Success",
		Nodes: []Node{Node{URN: "URN1:1.1", Text: "String Value", Previous: "", Next: "URN1:1.2", Index: 1}},
	}
	CitNodesJSON, _ := json.Marshal(CitNodes)
	fmt.Println(string(CitNodesJSON))
}
```

#### Output
```json
{"status":"Success"}
{"status":"Exception","message":"Invalid URN valid 'xyz'"}
{"status":"Success","URN":["URN1","URN2"]}
{"requestUrn":"URN1:1.1","status":"Success","Nodes":[{"URN":"URN1:1.1","text":"String Value","previous":"","next":"URN1:1.2","index":1}]}
```
