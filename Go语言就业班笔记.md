# Go语言就业班笔记

## TDD(测试驱动开发)

- #### 什么是测试驱动开发

  测试驱动开发是一种由测试案例驱动编写代码的开发方法。他从编写一个不包含任何正式代码的测试案例开始，然后编写正式代码使得测试案例通过。最后在有测试案例保障的情况下进行重构，完成有质量保证的代码。

- #### 实战案例

  #### 实现一个体脂排行榜

  **需求：**

  1. 排行榜上根据最佳体脂进行排序，体脂最低的排在最上面
  2. 输入一个姓名可以得到他/她所在排行榜的排名
  3. 如果一个参与者录入多次，只按照他的最佳体脂进行排名
  4. 相同体脂的人排名相同
  5. 只录入姓名，不录入体脂的排在最下面 
  
  **测试代码**
  
  ```go
  // main_test.go
  package main
  
  import "testing"
  
  func TestCase1(t *testing.T) {
  	inputRecord("Hud", 0.38)
  	inputRecord("Hud", 0.32)
  	inputRecord("Monica", 0.35)
  	{
  		rankOfHud, fatRateofHud := getRank("Hud")
  		if rankOfHud != 1 {
  			t.Fatalf("Expected rank of Hud is one，bur %d", rankOfHud)
  			return
  		}
  		if fatRateofHud != 0.32 {
  			t.Fatalf("expected faterate = 0.32,but resault is %v", fatRateofHud)
  		}
  	}
  	{
  		rankofMonica, fatRateofMOnica := getRank("Monica")
  		if rankofMonica != 2 {
  			t.Fatalf("Expected rank of Monica is one，bur %v", rankofMonica)
  			return
  		}
  		if fatRateofMOnica != 0.35 {
  			t.Fatalf("expected faterate = 0.32,but resault is %v", fatRateofMOnica)
  		}
  	}
  
  }
  
  func TestCase2(t *testing.T) {
  	inputRecord("Hud", 0.38)
  	inputRecord("Qbi", 0.38)
  	inputRecord("Monica", 0.35)
  	{
  		rankOfHud, fatRateofHud := getRank("Hud")
  		if rankOfHud != 2 {
  			t.Fatalf("Expected rank of Hud is one，bur %d", rankOfHud)
  			return
  		}
  		if fatRateofHud != 0.38 {
  			t.Fatalf("expected faterate = 0.32,but resault is %v", fatRateofHud)
  		}
  	}
  	{
  		rankOfQbi, fatRateofQbi := getRank("Qbi")
  		if rankOfQbi != 2 {
  			t.Fatalf("Expected rank of Qbi is one，bur %d", rankOfQbi)
  			return
  		}
  		if fatRateofQbi != 0.38 {
  			t.Fatalf("expected faterate = 0.38,but resault is %v", fatRateofQbi)
  		}
  	}
  	{
  		rankOfMonica, fatRateofMonica := getRank("Monica")
  		if rankOfMonica != 1 {
  			t.Fatalf("Expected rank of Monica is one，bur %d", rankOfMonica)
  			return
  		}
  		if fatRateofMonica != 0.35 {
  			t.Fatalf("expected faterate = 0.32,but resault is %v", fatRateofMonica)
  		}
  	}
  }
  
  func TestCase3(t *testing.T) {
  	inputRecord("Hud", 0.38)
  	inputRecord("Qbi", 0.28)
  	inputRecord("Monica")
  	{
  		rankOfHud, fatRateofHud := getRank("Hud")
  		if rankOfHud != 2 {
  			t.Fatalf("Expected rank of Hud is one，bur %d", rankOfHud)
  			return
  		}
  		if fatRateofHud != 0.38 {
  			t.Fatalf("expected faterate = 0.32,but resault is %v", fatRateofHud)
  		}
  	}
  	{
  		rankOfQbi, fatRateofQbi := getRank("Qbi")
  		if rankOfQbi != 1 {
  			t.Fatalf("Expected rank of Qbi is one，bur %d", rankOfQbi)
  			return
  		}
  		if fatRateofQbi != 0.28 {
  			t.Fatalf("expected faterate = 0.38,but resault is %v", fatRateofQbi)
  		}
  	}
  	{
  		rankOfMonica, _ := getRank("Monica")
  		if rankOfMonica != 3 {
  			t.Fatalf("Expected rank of Monica is three，bur %d", rankOfMonica)
  			return
  		}
  
  	}
  }
  
  
  ```
  
  函数实现
  
  ```go
  // main.go
  
  package main
  
  import (
  	"math"
  	"sort"
  )
  
  var (
  	// 体脂率的存储结构
  	personFatRate = map[string]float64{}
  )
  
  func inputRecord(name string, fatrate ...float64) {
  	// 不定长参数传进来是数组或者切片
  	miniFatRate := math.MaxFloat64
  	for _, item := range fatrate {
  		if miniFatRate > item {
  			miniFatRate = item
  		}
  	}
  	personFatRate[name] = miniFatRate
  }
  
  func getRank(name string) (rank int, fatRate float64) {
  	fatRate2Person := map[float64][]string{}
  	rankArr := make([]float64, 0, len(personFatRate))
  	for nameItem, frItem := range personFatRate {
  		fatRate2Person[frItem] = append(fatRate2Person[frItem], nameItem)
  		rankArr = append(rankArr, frItem)
  	}
  	sort.Float64s(rankArr)
  	for i, frItem := range rankArr {
  		_names := fatRate2Person[frItem]
  		for _, _name := range _names {
  			if _name == name {
  				rank = i + 1
  				fatRate = frItem
  				return
  			}
  		}
  
  	}
  	return 0, 0
  }
  
  ```
  
  