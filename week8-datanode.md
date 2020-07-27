1. 有两个单向链表（链表长度分别为m，n），这两个单向链表有可能在某个元素合并，如下图所示的这样，也可能不合并。
现在给定两个链表的头指针，在不修改链表的情况下，如何快速地判断这两个链表是否合并？
如果合并，找到合并的元素，也就是图中的 x 元素。请用（伪）代码描述算法，并给出时间复杂度和空间复杂度。
算法描述：
1. 计算两个链表的长度len1, len2;
2. 找出较长的链表longer
3. 计算两个链表的长度差lag
4. 先遍历较长的链表lag步
5. 同时表里两个链表longer-lag步，判断是否重复

```go
package list

import (
	"fmt"
	"math"
)

type node struct {
	value int
	next  *node
}

func ShareNode(l1 *node, l2 *node) {
	l1Len := 0
	l2Len := 0
	l1Tmp := l1
	l2Tmp := l2
	for {
		if l1Tmp == nil {
			break
		}
		l1Len++
		l1Tmp = l1Tmp.next
	}

	for {
		if l2Tmp == nil {
			break
		}
		l2Len++
		l2Tmp = l2Tmp.next
	}

	l := l1
	longer := l2
	shorterLen := l1Len
	if l1Len > l2Len {
		longer = l1
		l = l2
		shorterLen = l2Len
	}

	lag = math.Abs(l1Len - l2Len)

	for i := 0; i < lag; i++ {
		longer = longer.next
	}

	for i := 0; i < shorterLen; i++ {
		if l == longer {
			fmt.Println(l)
			break
		}
		l = l.next
		longer = longer.next
	}
}

```


2. 请画出DataNode服务器节点宕机的时候，HDFS的处理过程时序图。

@startuml
participant Client  
participant NameNode1
participant NameNode2
participant DataNode1
participant DataNode2
participant DataNode3

NameNode1 <- DataNode1 : 心跳包成功
NameNode1 <- DataNode2 : 心跳包成功
NameNode1 <- DataNode1 : 心跳包失败

NameNode1 -> NameNode1 : 修改元数据

NameNode1 -> DataNode1 : 发送数据复制命令
NameNode1 -> DataNode2 : 发送数据复制命令
NameNode1 -> NameNode1 : 修改元数据

Client -> NameNode1 : 获取datanode信息
Client -> DataNode1 : 读写datanode数据


@enduml


![](http://www.plantuml.com/plantuml/png/SoWkIImgAStDuIe0qfd9cGM9UIKApZcPgK1A0KNGBp4trIy_9TKGgwWHYgXBOaaYM2s6A6wrnbnSS2iKR7GHPYXOAJpTt_nY--QdFQtFEYOyxPgFNQ4Hfa8YJ7owPEEBBKkHxTQr0_iAflB9_dNFfknysjhyREg6PxthK5MYcja_yML38qJPqoMzJpksFPsuzydk9TXr6E7HGO9h8765hkn5t_Qd_TDIW5Rb0KMUx5_uh74zL2cwgr-it_sqRIPCASnOBeVKl1HWkW00)
