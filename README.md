#nagios status.dat to maps converter

###struct for the output data
```
type statusData struct {
	Infostatuslist		map[string]string
	Programstatuslist	map[string]string
	Hoststatuslist		map[string]map[string]string
	Servicestatuslist	map[string]map[string]map[string]string
	Hostcommentslist	map[string]map[string]string
	Servicecommentslist	map[string]map[string]string
}
```
###example code
```
package main

import (
	"fmt"
	"encoding/json"
	"github.com/cxfcxf/nagtomaps"
)

func main() {
	
	sdata := nagtomaps.ParseStatus("status.dat1")
	// status.dat is the file from nagios
	fmt.Println(sdata.Infostatuslist)
	//print maps

	j, _ := json.Marshal(sdata.Hoststatuslist)
	fmt.Println(string(j))
	//print json

	fmt.Println(sdata.Servicestatuslist["edge21-fra"])
	// print map of all service description
	fmt.Println(sdata.Servicestatuslist["edge21-fra"]["HTTP"]["notifications_enabled"])
	// print status like 1 or 0
	
}
```
### the output map will fit the struct in the nagtomaps
