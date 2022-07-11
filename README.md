# devops-netology  
## Шевякин Кирилл  

# Домашнее задание к занятию "7.5. Основы golang"

С `golang` в рамках курса, мы будем работать не много, поэтому можно использовать любой IDE. 
Но рекомендуем ознакомиться с [GoLand](https://www.jetbrains.com/ru-ru/go/).  
![image](https://user-images.githubusercontent.com/93198418/178197154-4c7d4d79-b53b-4af3-9dc1-25b8b79642d1.png)  

## Задача 1. Установите golang.
1. Воспользуйтесь инструкций с официального сайта: [https://golang.org/](https://golang.org/).  
![image](https://user-images.githubusercontent.com/93198418/178198548-a53daa8e-0eac-43b9-ac30-b4ba48d28c24.png)  

3. Так же для тестирования кода можно использовать песочницу: [https://play.golang.org/](https://play.golang.org/).  
![image](https://user-images.githubusercontent.com/93198418/178198699-17e59ad1-6406-4d47-b82c-43197688d91a.png)  

## Задача 2. Знакомство с gotour.
У Golang есть обучающая интерактивная консоль [https://tour.golang.org/](https://tour.golang.org/). 
Рекомендуется изучить максимальное количество примеров. В консоли уже написан необходимый код, 
осталось только с ним ознакомиться и поэкспериментировать как написано в инструкции в левой части экрана.  
![image](https://user-images.githubusercontent.com/93198418/178199170-b111b872-f230-4b1a-8efa-2454a3fd0230.png)  

## Задача 3. Написание кода. 
Цель этого задания закрепить знания о базовом синтаксисе языка. Можно использовать редактор кода 
на своем компьютере, либо использовать песочницу: [https://play.golang.org/](https://play.golang.org/).

1) Напишите программу для перевода метров в футы (1 фут = 0.3048 метр). Можно запросить исходные данные 
у пользователя, а можно статически задать в коде.
    Для взаимодействия с пользователем можно использовать функцию `Scanf`:
    ```
    package main
    
    import "fmt"
    
    func main() {
        fmt.Print("Enter a number: ")
        var input float64
        fmt.Scanf("%f", &input)
    
        output := input * 2
    
        fmt.Println(output)    
    }
    ```  
    
### Ответ
1 вариант  
```  
package main
import "fmt"
func main() {
	fmt.Print("10 метров = ")
	input := 10.0
	output := input * 0.3048
	fmt.Println(output, "футов")
}
```  
![image](https://user-images.githubusercontent.com/93198418/178203390-1fa28332-4143-4cf8-b0d2-93ddabfc999c.png)  

2 вариант  
```
package main
import "fmt"
func main() {
	fmt.Print("Введите количество метров:")
	var input float64
	fmt.Scanf("%f", &input)
	output := input * 0.3048
	fmt.Println(input, "метров =", output, "футов")
	}
```
![image](https://user-images.githubusercontent.com/93198418/178203575-e95eaf35-f1b5-4e6c-867a-d016350ddcda.png)  
  
  
2) Напишите программу, которая найдет наименьший элемент в любом заданном списке, например:
    ```
    x := []int{48,96,86,68,57,82,63,70,37,34,83,27,19,97,9,17,}
    ```   
### Ответ  
```
package main
import "fmt"
func main() {
	x := []int{48, 2, 96, 86, 3, 68, 57, 82, 63, 70, 37, 34, 83, 27, 19, 97, 9, 17, 100}
	min := 0
	for i, value := range x {
		if i == 0 {
			min = value
		} 
		else {
   			if value < min {
				min = value
			}
		}
	}
	fmt.Println("Минимум в массиве: ", min)
}
```
![image](https://user-images.githubusercontent.com/93198418/178211091-e1e02fb3-f3f6-4ed1-9a5b-cbdea73f61af.png)  

3) Напишите программу, которая выводит числа от 1 до 100, которые делятся на 3. То есть `(3, 6, 9, …)`.

### Ответ
```
package main

import "fmt"

func main() {
	fmt.Println("Список чисел от 1 до 100, делящихся на 3:")
	for i := 1; i <= 100; i++ {
		if (i % 3) == 0 {
			fmt.Print(i, " ")
		}
	}
}
```  
![image](https://user-images.githubusercontent.com/93198418/178211950-7cfe01fe-4efd-4fc9-93f6-6dc105d18e86.png)

 
