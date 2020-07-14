1. 性能压测的时候，随着并发压力的增加，系统响应时间和吞吐量如何变化,为什么？


2.用你熟悉的编程语言写一个web性能压测工具，输入参数:URL，请求总次数，并发数，输出参数：平均响应时间，95%响应时间，用这个测试工具以10并发、1000次请求压测 www.baidu.com
```go
package main

import (
	"flag"
	"fmt"
	"net/http"
	"sort"
	"time"
)

var url = flag.String("url", "", "")
var requests = flag.Int("r", 1, "")
var concurrency = flag.Int("c", 1, "")
var chans = make(chan int, *requests)

func main() {
	for i := 0; i < *concurrency; i++ {
		go run((*requests) / (*concurrency))
	}

	res := []int{}
	for j := 0; j < *concurrency; j++ {
		r := <-chans
		res = append(res, r)
	}
}

func run(tasks int) {
	for i := 0; i < tasks; i++ {
		start := time.Now()
		http.Get(*url)
		elaspsed := time.Since(start)
		chans <- int(elaspsed.Microseconds())
	}
}

func stat(res []int) {
	sum := 0
	for i := range res {
		sum += res[i]
	}
	avg := sum / len(res)
	fmt.Println("avg: ", avg)

	sort.Ints(res)
	r := int(float64(len(res)) * 0.95)
	fmt.Println("95%: ", res[r])
}
```