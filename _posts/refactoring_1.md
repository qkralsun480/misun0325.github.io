---
title: "리팩토링"
date: 2022-02-305
categories: ['일반']
tags: ['refactoring', 'github', 'github.io']
---
# 리팩토링, 첫번째 예제

- 리팩토링 첫번째 단계
    - 리팩토링 할 부분의 코드에 대한 견고한 테스트 셋을 만드는것이다.

```java
public String statement() {
    double totalAmount =0;
    int frequentRenterPoints =0;
    Enumeration rentals = retals.element();
    
    while (rentals.hasmoreElement()) {
        double thisAmount =0;
        Rental each = (Rental) rentals.nextElements();

        // 각 영화에 대한 요금 결정
        switch(each.getMovie().getPriceCode()){
            case Movie.REGULAR:
                thisAmount += 2;
                if (each.getDaysRented()>2)
                    thisSmount += (each.getDaysRented()-2) * 1.5;
                break;
            case Movie.RELEASE:
                thisSmount += each.getDaysRented() * 3;
                break;
            case Movie.CHILDRENS:
                thisAmount += 1.5;
                if (each.getDaysRented()>3)
                    thisSmount += (each.getDaysRented()-3) * 1.5;
                break;
        }
    }
}
```

- 메소드내의 지역변수와 파라미터를 주위한다.
- each값이 수정되지 않지만, thisAmount 값이 수정된다.
- 값이 수정되지 않는 변수는 파라미터로 넘길수 있다. 


```java
public String statement() {
    double totalAmount =0;
    int frequentRenterPoints =0;
    Enumeration rentals = retals.element();

    while (rentals.hasmoreElement()) {
        double thisAmount =0;
        Rental each = (Rental) rentals.nextElements();

        // swtich 문을 메소드로 빼기
        thisAmount = amountFor(each);
    }
}

private double amountFor(Rental each){
    double thisAmount =0;

    // 각 영화에 대한 요금 결정
    switch(each.getMovie().getPriceCode()){
        case Movie.REGULAR:
            thisAmount += 2;
            if (each.getDaysRented()>2)
                thisSmount += (each.getDaysRented()-2) * 1.5;
            break;
        case Movie.RELEASE:
            thisSmount += each.getDaysRented() * 3;
            break;
        case Movie.CHILDRENS:
            thisAmount += 1.5;
            if (each.getDaysRented()>3)
                thisSmount += (each.getDaysRented()-3) * 1.5;
            break;
    }
    return thisAmount;
} 
```
