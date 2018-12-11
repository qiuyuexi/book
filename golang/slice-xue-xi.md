# slice 学习

```text
``` go
package main

import "fmt"

func add(sli []int) {
	fmt.Printf("%p\n", &sli)
	sli[1] = 100
	sli = append(sli, 111)
}

func add1(sli []int) {
	sli = append(sli, 111)
	printAddr(sli)
	sli = append(sli, 111)
	printAddr(sli)
	sli[1] = 200
	printAddr(sli)
}

func add2(sli []int) {
	sli = append(sli, 111)
	sli[1] = 200
}

func printAddr(sli []int)  {
	fmt.Println("----start")
	for i := 0; i < len(sli); i++ {
		fmt.Printf("%p\n", &sli[i])
	}
	fmt.Println("----end")
}

func main() {

	fmt.Println("----1")
	sli := make([]int, 2, 3)
	fmt.Printf("%p\n", &sli)
	add(sli)
	fmt.Println(sli)
	sli2 := sli[0:3]
	fmt.Println(sli2)

	fmt.Println("----2")

	sli = make([]int, 2, 3)
	printAddr(sli)
	add1(sli)
	fmt.Println(sli)
	sli3 := sli[0:3]
	fmt.Println(sli3)

	fmt.Println("----3")
	sli = make([]int, 2, 3)
	printAddr(sli)
	add2(sli)
	fmt.Println(sli)
	sli4 := sli[0:3]
	fmt.Println(sli4)
}


输出结果
----1
0xc00008c020
0xc00008c040
[0 100]
[0 100 111]

----2
[0 0]
[0 0 111]

----3
[0 200]
[0 200 111]


```

```

  第一种情况: 根据这个，发现slice 实际是值传递，因此在append时，虽然111已被添加，由于函数外的sli len无变化，导致sli无法输出已添加的值。 sli\[1\]能被改变，是因为slice的底层是指向一个数组的指针，因此虽然是值传递，但是仍然可以改变slice的值

 第二种情况: 函数外的sli\[1\]无变化，是因为执行多次append后，slice扩容，内存地址变化。

  


