#include <iostream>

using namespace std;

double amountOfCosts();
double taxCalculation();

int guide(){
    int choice;
    cout << "Выберите, что вам нужно рассчитать." << endl << endl;
    cout << "Если хотите узнать, какую сумму налога вам придется заплатить - введдите 1." << endl;
    cout << "Если хотите узнать, какая будет чистая прибыль - введите 2." << endl;
    cout << "Если хотите узнать на какую сумму нужно продать товара, чтобы зафиксировать доход в N проц. - введите 3." << endl;
    cin >> choice;
    return choice;
}

double taxCalculation(int rental_of_premises, double taxes, double purchase_of_products, int employee_salaries,
double communalPayments, int depreciation, double income_from_lunches, double income_from_desserts){
    double amountOfTaxes;
    double costs = rental_of_premises + purchase_of_products + employee_salaries + communalPayments +
    depreciation;
    double income = income_from_desserts + income_from_lunches;
    if (income > costs){
        amountOfTaxes = (((income_from_desserts + income_from_lunches) - costs) * taxes) / 100;
        return amountOfTaxes;
    } else {
        return 0;
    }
    
    //return amountOfTaxes;
};

double calculationOfNetProfit(int rental_of_premises, double taxes, double purchase_of_products, int employee_salaries,
double communalPayments, int depreciation, double income_from_lunches, double income_from_desserts){
    
    double amountOfTaxes = taxCalculation(rental_of_premises, taxes, purchase_of_products, employee_salaries, communalPayments, 
          depreciation, income_from_lunches, income_from_desserts);

    double costs = rental_of_premises + purchase_of_products + employee_salaries + communalPayments +
    depreciation + amountOfTaxes;
    
    return (income_from_desserts + income_from_lunches) - costs;
}

double fixationOfIncome(int rental_of_premises, double taxes, double purchase_of_products, int employee_salaries,
double communalPayments, int depreciation, double income_from_lunches, double income_from_desserts){
    int percent;
    double amountOfTaxes;
    cout << "Какой доход вы хотите получить в процентах? - ";
    cin >> percent;
    cout << "Сумма уплаченных налогов - ";
    cin >> amountOfTaxes;
          
    double costs = rental_of_premises + purchase_of_products + employee_salaries + communalPayments +
    depreciation + amountOfTaxes;
    cout << costs << endl;
    
    return (costs + ((costs * percent) / 100));
}



void selection_function(int rental_of_premises, double taxes, double purchase_of_products, int employee_salaries,
double communalPayments, int depreciation, double income_from_lunches, double income_from_desserts){
    
    int choice = guide();
    switch(choice){
        case 1:{
          double amountOfTaxes = taxCalculation(rental_of_premises, taxes, purchase_of_products, employee_salaries, communalPayments, 
          depreciation, income_from_lunches, income_from_desserts);
          if (amountOfTaxes != 0){
          cout << "Сумма налогов составит " << amountOfTaxes << " руб. " << endl;
          } else cout << "У комании нет прибыли. " << endl;
          break;}
        case 2:{
          double net_profit = calculationOfNetProfit(rental_of_premises, taxes, purchase_of_products, employee_salaries, communalPayments, 
          depreciation, income_from_lunches, income_from_desserts);
          if (net_profit >= 0){
              cout << "Чистая прибыль составит " << net_profit << " руб." << endl;
          } else 
              cout << "Вы ушли в минус, издержки превышают прибыль." << endl;
          break;}
        case 3:
           double income = fixationOfIncome(rental_of_premises, taxes, purchase_of_products, employee_salaries, communalPayments, 
           depreciation, income_from_lunches, income_from_desserts);
           cout << "Чтобы получить желаемый вами процент доходности , вам нужно продать товар на сумму " << income << " руб. "<< endl;
          break;
    }
}

int main()
{
    int rental_of_premises, employee_salaries, depreciation;
    double taxes, purchase_of_products, communalPayments, income_from_desserts, income_from_lunches;
    
    cout << "Калькулятор рассчета ежемесячного дохода и затрат." << endl << endl;
    cout << "Стоимость аренды помещения - ";
    cin >> rental_of_premises;
    cout << "Процент налога - ";
    cin >> taxes;
    cout << "Цена закупки продуктов - ";
    cin >> purchase_of_products;
    cout << "Зарплата сотрудников - ";
    cin >> employee_salaries;
    cout << "Коммунальные платежи - ";
    cin >> communalPayments;
    cout << "Амортизационные отчисления - ";
    cin >> depreciation;
    cout << "Доход с продажи десертов - ";
    cin >> income_from_desserts;
    cout << "Доход с продажи ланчей - ";
    cin >> income_from_lunches;
    
    if (taxes <= 20){
    
    selection_function(rental_of_premises, taxes, purchase_of_products, employee_salaries, communalPayments, 
    depreciation, income_from_lunches, income_from_desserts);
    } else {
        cout << "Налог не должен превышать 20 процентов." << endl;
    }
    return 0;
}




 
