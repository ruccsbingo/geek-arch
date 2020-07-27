## 单例模式

![](https://github.com/ruccsbingo/geek-arch/blob/master/WX20200617-132941%402x.png)



## 组合模式
```go
package design

import (
	"fmt"
	"strings"
)

type IComponent interface {
	PrintName(depth int)
	Add(c IComponent)
}

type Container struct {
	name       string
	components []IComponent
}

func (w *Container) PrintName(depth int) {
	fmt.Println(strings.Repeat("-", depth), " ", w.name)
	for _, c := range w.components {
		c.PrintName(depth + 2)
	}
}

func (w *Container) Add(c IComponent) {
	w.components = append(w.components, c)
}

func NewComponent(n string) IComponent {
	var w Container
	w.name = n
	return &w
}

type Leaf struct {
	name string
}

func (l *Leaf) PrintName(depth int) {
	fmt.Println(strings.Repeat("-", depth), " ", l.name)
}

func (l *Leaf) Add(c IComponent) {

}

func NewLeaf(n string) IComponent {
	var l Leaf
	l.name = n
	return &l
}
```

![](https://github.com/ruccsbingo/geek-arch/blob/master/WX20200617-144154.png)
