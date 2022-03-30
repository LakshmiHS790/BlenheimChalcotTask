# Koodoo Software Engineer Technical Assessment 👾

---

**Background**:

Consider the following data structure.

```
const accountBalanceHistory = [
  {
    monthNumber: 0, // current month
    account: {
      balance: { amount: 0 },
    },
  },
  {
    monthNumber: 1, // last month
    account: {
      balance: { amount: 100 },
    },
  },
  {
    monthNumber: 2, // two months ago
    account: {
      balance: { amount: 200 },
    },
  }
]
```

Account balance history is an array that denotes a monthly track record of the balance in someone's account (or simply put how much money they had left that month!)

Each top level object within the array denotes the running balance value within that particular month.

E.g. in our example above, I can see that someone
started of with a balance of 200 2 months ago, this decreased to 100 the following month, and again to 0 in the final and current month.

### Task

Write a function (JavaScript) such that given a accountBalanceHistory array as an argument, it will categorise the array based on the way that the balance value is changing month by month.

```
// ****To get the balance amount in the account from each month****

function getBalanceAmtArr(accountBalanceHistory)
{
   var balanceArrFromAccount = [];
   for(let i=0; i<accountBalanceHistory.length; i++){
   let balanceAmt = accountBalanceHistory[i].account.balance.amount;
   balanceArrFromAccount.push(balanceAmt);
}
  return balanceArrFromAccount;
}

// ****To get the difference between each balance amount from the statement****

function getDifferenceBetweenEachBalanceAmt(balanceArr){
  var diffBalanceArr = [];
  for(let j=0; j<balanceArr.length-1; j++){
  let diff = balanceArr[j+1] - balanceArr[j];
     var resultToReturn = false;
  diffBalanceArr.push(diff);
}
  return diffBalanceArr;
}


// ****To check the difference is same for all months****

function toCheckForUniformBalance(diffArr){
  var count = 1;
  var resultToReturn = false;
   for (let i = 0; i < diffArr.length; i++) {
        for (let j = 0; j < diffArr.length; j++) {
          
            // prevents the element from comparing with itself
            if (i !== j) {
                // check if elements' values are equal
                if (diffArr[i] === diffArr[j]) {
                    // duplicate element present  
                    count++;
                    resultToReturn = true;
                    // terminate inner loop
                }
            }
        }
        // terminate outer loop                                                                      
        if (resultToReturn) {
            break;
        }
    }
  if(count == diffArr.length)
    {
      return true;
    }
  else {
    return false;
  }
}


const accountTypeChecker = (accountBalanceHistory) => {
  /***
  Your goal is to write a function that determines from someone's ${accountBalanceHistory} 🧾 (see the array above for an example)
  whether this array is of type A (variable) or type B (fixed).

  Type 🅰 denotes a balance history where the balance amount decreases by varying amounts each month.

  Type 🅱 is one where the balance amount changes by the same amount each month.
  ***/

  // Write your logic here  - No pressure 😁 //


  let result;
  let balanceArr = [];
  let diffArr = [];
  /****
  ******Algorithm******
  1. Initially get the balance amount from each month
  2. Check difference between the balance amount from each month
  3. Check if the difference is same for all the months.
  4. If the differene is same then return Type 🅱 else if the difference varies then return Type 🅰
  ****/

  balanceArr = this.getBalanceAmtArr(accountBalanceHistory);
  diffArr = this.getDifferenceBetweenEachBalanceAmt(balanceArr);
  result = !this.toCheckForUniformBalance(diffArr);
  return result ? "A" : "B";
};


```

### Things to consider in my solution

- Does it solve the basic case? 
    --> Yes

- What other cases might need to be considered? - 
    --> Tested positive workflow, by giving the account details in which the balance varies consistantly by month by month. For ex, all the difference amount from months will be either 100 or 1000 or 200. In this case it returns TYPE 🅱 

    --> Given account details as if the balance varies month by month with inconsistance difference amount, for ex from 3rd month to 2nd month the difference is 1000, and from 2nd to 1st month the difference  is 500. In this case difference amount is inconsstance hence it has to return TYPE 🅰

    --> Tried the snippet for different types of account balance, below given sample queries on which the function is tested. 

- What unit tests might you write for this type of function?
    --> In this type of function, initially we have to mock the data for different types of inputs then can check whether this function satisfies all possible use cases or not.



 ### Tested same code for below sample inputs: 
```
1.
const accountBalanceHistory = [
  {
    monthNumber: 0, // current month
    account: {
      balance: { amount: 0 },
    },
  },
  {
    monthNumber: 1, // last month
    account: {
      balance: { amount: 100 },
    },
  },
  {
    monthNumber: 2, // two months ago
    account: {
      balance: { amount: 200 },
    },
  }
] ---> returns TYPE 🅱 


2. 
const accountBalanceHistory = [
  {
    monthNumber: 0, 
    account: {
      balance: { amount: 0 },
    },
  },
  {
    monthNumber: 1, 
    account: {
      balance: { amount: 200 },
    },
  },
  {
    monthNumber: 2, 
    account: {
      balance: { amount: 400 },
    },
  },
    {
    monthNumber: 2, 
    account: {
      balance: { amount: 600 },
    },
  }
] ---> returns TYPE 🅱 


3.
const accountBalanceHistory = [
  {
    monthNumber: 0, 
    account: {
      balance: { amount: 0 },
    },
  },
  {
    monthNumber: 1, 
    account: {
      balance: { amount: 1000 },
    },
  },
  {
    monthNumber: 2, 
    account: {
      balance: { amount: 200 },
    },
  },
    {
    monthNumber: 2, 
    account: {
      balance: { amount: 3000 },
    },
  }
] ---> returns TYPE 🅰
```
Thanks for providing the opportunity to work on this. 🤝
