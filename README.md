package main

import "fmt"

type Employee struct {
    ID       int
    Name     string
    Position string
}

type EmployeeDatabase struct {
    employees []Employee
    maxCount  int
}

func (db *EmployeeDatabase) AddEmployee(emp Employee) {
    if len(db.employees) >= db.maxCount {
        fmt.Println("Превышено максимальное количество сотрудников (512).")
        return
    }
    db.employees = append(db.employees, emp)
    fmt.Println("Сотрудник добавлен.")
}

func (db *EmployeeDatabase) RemoveEmployee(id int) {
    for i, emp := range db.employees {
        if emp.ID == id {
            db.employees = append(db.employees[:i], db.employees[i+1:]...)
            fmt.Println("Сотрудник удалён.")
            return
        }
    }
    fmt.Println("Сотрудник не найден.")
}

func (db *EmployeeDatabase) PrintAll() {
    for _, emp := range db.employees {
        fmt.Printf("ID: %d, Имя: %s, Должность: %s\n", emp.ID, emp.Name, emp.Position)
    }
}

func main() {
    db := EmployeeDatabase{
        maxCount: 512,
    }

    // Добавляем сотрудников
    db.AddEmployee(Employee{ID: 1, Name: "Иван Иванов", Position: "Менеджер"})
    db.AddEmployee(Employee{ID: 2, Name: "Анна Петрова", Position: "Аналитик"})

    // Выводим всех сотрудников
    db.PrintAll()

    // Удаляем сотрудника
    db.RemoveEmployee(1)

    // Выводим оставшихся сотрудников
    db.PrintAll()
}
