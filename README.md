# demo
 own demo

 <!-- own codes -->
package main

import (
	"fmt"
	"os"
)

// 全局声明
var (
	allStudent map[int64]*student
)

/*
函数型学生管理系统
功能：查看/新增/删除学生
*/
type student struct {
	name string
	id   int64
}

// 构造函数
func newStu(id int64, name string) student {
	return student{
		id:   id,
		name: name,
	}
}
func showAllstudent() {
	// 打印所有学生
	for k, v := range allStudent {
		fmt.Printf("学号:%d\t姓名:%s\n", k, v.name)
	}
}
func addStudent() {
	// 添加学生信息
	// 1.创建新学生
	var (
		id   int64
		name string
	)
	// 1.1d获取用户输入
	fmt.Println("请输入要添加的学生学号:")
	fmt.Scanln(&id)
	fmt.Println("请输入要添加的学生姓名:")
	fmt.Scanln(&name)
	// 1.2调用构造函数
	newstu := newStu(id, name)
	// 2.追加进allStudent中
	allStudent[id] = &newstu
	fmt.Println(*allStudent[id])
}
func delStudent() {

}

func main() {
	allStudent = make(map[int64]*student, 50) //初始化，为student信息分配内存
	for {
		// 1.打印菜单
		fmt.Println("欢迎进入学生管理系统")
		fmt.Println(`
	1.查看所有学生
	2.新增学生
	3.删除学生
	4.推出
	`)
		fmt.Print("请选择你要实现的功能:")
		// 2.等待用户选择
		var option int
		fmt.Scanln(&option)
		fmt.Printf("你选择了%d这一项功能\n", option)
		// 3.执行对应函数
		if option == 1 {
			showAllstudent()
		} else if option == 2 {
			addStudent()
		} else if option == 3 {
			delStudent()
		} else if option == 4 {
			os.Exit(1) //退出
		} else {
			fmt.Println("请重新做出你的选择")
		}
	}
}
