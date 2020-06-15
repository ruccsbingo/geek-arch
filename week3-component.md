## 单例模式
```go
type singleton struct {

}

var s = &singleton{}

func GetSingleton() *singleton {
	return s
}
```


## 组合模式
```go
import (
	"fmt"
)

type Printable interface {
	PrintName()
}

type Component struct {
	name       string
	components []Component
}

func (c Component) PrintName() {
	fmt.Println(c.name)
	for i := range c.components {
		c.components[i].PrintName()
		// fmt.Println(c.components[i].name)
	}
}

func (c *Component) Add(p Printable) {
	t := p.(Component)
	c.components = append(c.components, t)
}

func (c *Component) GetAll() []Component {
	return c.components
}

type WinForm struct {
	Component
}

func NewWinForm(n string) *WinForm {
	var w WinForm 
	w.name = n
	return &w
}

type Picture struct {
	Component
}

func NewPicture(n string) *Picture {
	var p Picture
	p.name = n
	return &p
}

type Button struct {
	Component
}

func NewButton(n string) *Button {
	var b Button
	b.name = n
	return &b
}

type Frame struct {
	Component
}

func NewFrame(n string) *Frame {
	var f Frame
	f.name = n
	return &f
}

type Lable struct {
	Component
}

func NewLable(n string) *Lable {
	var l Lable
	l.name = n
	return &l
}

type TextBox struct {
	Component
}

func NewTextBox(n string) *TextBox {
	var t TextBox
	t.name = n
	return &t
}

type PasswordBox struct {
	Component
}

func NewPasswordBox(n string) *PasswordBox {
	var p PasswordBox
	p.name = n
	return &p
}

type CheckBox struct {
	Component
}

func NewCheckBox(n string) *CheckBox {
	var c CheckBox
	c.name = n
	return &c
}

type LinkLable struct {
	Component
}

func NewLinkLable(n string) *LinkLable {
	var l LinkLable
	l.name = n
	return &l
}
```

**使用**
```go
func TestPrint(t *testing.T) {
	var wf WinForm
	b1 := NewButton("-")
	b2 := NewButton("+")
	b3 := NewButton("*")
	wf.Add(b1)
	wf.Add(b2)
	wf.Add(b3)

	p1 := NewPicture("logo")
	wf.Add(p1)

	f := NewWinForm("f1")
	wf.Add(f)

	l1 := NewLable("用户名")
	t1 := NewTextBox("")
	f.Add(l1)
	f.Add(t1)

	l2 := NewLable("密码")
	t2 := NewTextBox("")
	f.Add(l2)
	f.Add(t2)

	c1 := NewCheckBox("")
	l3 := NewLable("记住用户名")
	f.Add(c1)
	f.Add(l3)

	ll := NewLinkLable("忘记密码")
	f.Add(ll)

	b4 := NewButton("登录")
	b5 := NewButton("注册")
	wf.Add(b4)
	wf.Add(b5)

	wf.PrintName()
}
```


