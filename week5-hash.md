## Hash类
```go
package hash

import (
	"hash/crc32"
	"math"
	"sort"
)

const mod = 8192 * 8
const INT_MAX = int(^uint32(0) >> 1)
const UINT32_MAX uint32 = ^uint32(0)

type Hash struct {
	Nodes     map[uint32]node
	SortNodes SortedNodes
}

func Init(nodeIps []string) *Hash {
	h := Hash{}
	h.Nodes = map[uint32]node{}
	h.SortNodes = []uint32{}
	for _, ip := range nodeIps {
		index := toInt(ip)
		m := map[string]interface{}{}
		n := node{
			Ip:     ip,
			Values: m,
		}
		h.Nodes[index] = n
		h.SortNodes = append(h.SortNodes, index)

		//虚拟结点
		ii := UINT32_MAX - index
		h.Nodes[ii] = n
		h.SortNodes = append(h.SortNodes, ii)
	}
	sort.Sort(h.SortNodes)
	return &h
}

type SortedNodes []uint32

func (s SortedNodes) Len() int {
	return len(s)
}
func (s SortedNodes) Less(i, j int) bool {
	return s[i] < s[j]
}
func (s SortedNodes) Swap(i, j int) {
	s[i], s[j] = s[j], s[i]
}

func (h Hash) NextInt(v uint32) uint32 {
	if v <= h.SortNodes[0] {
		return h.SortNodes[0]
	}
	if v > h.SortNodes[len(h.SortNodes)-1] {
		return h.SortNodes[0]
	}
	for i := range h.SortNodes {
		if v > h.SortNodes[i] && v <= h.SortNodes[i+1] {
			return h.SortNodes[i+1]
		}
	}
	return 0
}

type node struct {
	Ip     string
	Values map[string]interface{}
}

func toInt(key string) uint32 {
	// adler := adler32.New()
	// adler.Write([]byte(key))
	// res := adler.Sum32()
	// return int(res) % mod

	crc32InUint32 := crc32.ChecksumIEEE([]byte(key))
	return crc32InUint32
}

func (h Hash) Get(key string) interface{} {
	i := h.NextInt(toInt(key))
	n := h.Nodes[i]
	return n.Values[key]
}

func (h *Hash) Set(key string, value interface{}) {
	// fmt.Println(toInt(key))
	i := h.NextInt(toInt(key))
	// fmt.Println("Next: ", i)
	n := h.Nodes[i]
	n.Values[key] = value
}

func caculate(nums []int, avg int) float64 {
	sum := 0.0
	for _, i := range nums {
		sum += math.Pow(float64(i-avg), 2)
	}
	return sum / float64(len(nums))
}

```

## 测试100万KV方差
```go
func TestDistribute(t *testing.T) {
	TestInit(t)
	for i := 0; i < 1000000; i++ {
		H.Set(strconv.Itoa(i), i)
	}
	nums := []int{}
	m := map[string]bool{}
	for _, n := range H.Nodes {
		if _, ok := m[n.Ip]; ok {
			continue
		} else {
			fmt.Println(n.Ip, "", len(n.Values))
			nums = append(nums, len(n.Values))
			m[n.Ip] = true
		}
	}
	fmt.Println(caculate(nums, 100000))
}
```

## 方差
127.0.0.10  26701
127.0.0.1  21248
127.0.0.2  30283
127.0.0.3  61167
127.0.0.5  53569
127.0.0.8  36635
127.0.0.4  337226
127.0.0.7  63095
127.0.0.9  308175
127.0.0.6  61901
**12654056239**

