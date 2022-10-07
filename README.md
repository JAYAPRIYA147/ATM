# ATM
import java.util.*;
public class Main {
	static List<CustomerDetails> detail=new ArrayList<>();
	static Scanner sc=new Scanner(System.in);
	static loadCash lc=new loadCash();
	public static void main(String[] args) {
		customerdetails();
		lc.upadate_cash(20, 100, 100);
		int choice;
		do {
			System.out.println("1.Load Cash to ATM");
			System.out.println("2.Balance in ATM");
			System.out.println("3.Details of the customer");
			System.out.println("4.Operations in ATM");
			System.out.println("Enter Choices to do Operation");
			choice=sc.nextInt();
			switch(choice) {
			case 1:
			    loadcash();break;
			case 2:
				displayATMdenomenation();break;
			case 3:
				displaydetails();break;
	 		case 4:
	 			ATMoperation();break;
	 		case 5:
	 		   break;
	 		 default:
	 			 System.out.println("Enter correct choice");break;
			}
		}while(choice!=5);
	}
   static void ATMoperation() {
		ATMOperations ob=new ATMOperations(); 
	}
	static void loadcash() {
		System.out.println("**********Load Cash to ATM**********");
	    System.out.println("Enter note count->");
	    System.out.println("Enter count_2000");
	    int _2000=sc.nextInt();
	    System.out.println("Enter count_500");
	    int _500=sc.nextInt();
	    System.out.println("Enter count_100");
	    int _100=sc.nextInt();
	    lc.upadate_cash(_2000,_500,_100);
	    displayATMdenomenation();
	}
	static void customerdetails() {
		CustomerDetails a1=new CustomerDetails(101,"Suresh",2343,25234);
		CustomerDetails a2=new CustomerDetails(102,"Ganesh",5432,34123);
		CustomerDetails a3=new CustomerDetails(103,"Magesh",7854,26100);
		CustomerDetails a4=new CustomerDetails(104,"Naresh",2345,80000);
		CustomerDetails a5=new CustomerDetails(105,"Harish",1907,103400);
        detail.addAll(Arrays.asList(a1,a2,a3,a4,a5));
	}
    static void displaydetails() {
    	System.out.println("------------------------Customer Details-----------------------");
		System.out.println("************************************************************");  
		System.out.printf("%8s %20s %12s %16s", "Acc No", "Account Holder", "Pin Number", "Account Balance");  
		System.out.println();  
		System.out.println("************************************************************");   
		for(CustomerDetails Customerdetail: detail)  
		{  
		System.out.format("%7s %14s %14s %16s",Customerdetail.getAccNo(), Customerdetail.getAccName(), Customerdetail.getPin(), Customerdetail.getBalance());  
		System.out.println();  
		}  
		System.out.println("************************************************************");
		System.out.print("\n");
	}
    static void displayATMdenomenation() {
    	System.out.println("------------------ATM Balance-------------------");
		System.out.println("************************************************************");  
		System.out.printf("%8s %12s %12s ", "Denomination", "Number", "Value");  
		System.out.println();  
		System.out.println("************************************************************");  
		System.out.format("%7s %16s %12s ","2000", lc.getCount_2000(),lc.getTotal_2000());
		System.out.println();
		System.out.format("%7s %16s %12s ","500", lc.getCount_500(),lc.getTotal_500());  
		System.out.println();
		System.out.format("%7s %16s %12s ","100", lc.getCount_100(),lc.getTotal_100()); 
		System.out.println();
		System.out.println("************************************************************");  
		System.out.print("\n");
    }
}


class CustomerDetails extends Main {
	int accNo;
	String AccName;
	int Pin;
	int Bal;
	public CustomerDetails(int accNo, String AccName, int Pin, int Bal) {
		super();
		this.accNo = accNo;
		this.AccName = AccName;
		this.Pin = Pin;
		this.Bal = Bal;
	}
	public int getAccNo() {
		return accNo;
	}
	public void setAccNo(int accNo) {
		this.accNo = accNo;
	}
	public String getAccName() {
		return AccName;
	}
	public void setAccName(String AccName) {
		this.AccName = AccName;
	}
	public int getPin() {
		return Pin;
	}
	public void setPin(int Pin) {
		this.Pin = Pin;
	}
	public int getBalance() {
		return Bal;
	}
	public void setBalance(int Balance) {
		this.Bal = Bal;
	}
	public void updateBalance(int amt) {
		Bal -= amt;
		return;
	}
	void customercashupdate(CustomerDetails obj, int amt, int _2000count, int _500count, int _100count) {
		if (amt <= obj.Bal) {
			if (lc.update_withdrawl(amt, _2000count, _500count, _100count)) {
				obj.updateBalance(amt);
			} 
			else {
				System.out.println("Sorry Atm Balance Is Low");
			}
		} 
		else {
			System.out.println("Sorry Your Account Balance Is Low");
		}
		return;
	}
	public String toString() {
		return accNo + AccName + Pin + Bal;
	}
}


import java.util.Scanner;
class ATMOperations extends Main {
	CustomerDetails obj1;
	Scanner sc = new Scanner(System.in);
	public ATMOperations() {
		System.out.println("1.Balance Checking");
		System.out.println("2.Money withdrawl");
		System.out.println("3.Money Transfer");
		System.out.println("4.Check ATM balance");
		System.out.println("5.Amount Deposit");
		int choice = sc.nextInt();
		switch (choice) {
		case 1:
			checkbalance();break;
		case 2:
			withdrawmoney();break;
		case 3:
			transfermoney();break;
		case 4:
			ATMbalance();break;
		case 5:
			DepositAmount();break;
		}
	}
	void checkbalance() {
		System.out.println("Enter Secret Pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				System.out.println(customerdeatail.getBalance());
			}
		}
	}
	void withdrawmoney() {
		System.out.println("Enter Secret Pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				obj1 = customerdeatail;
				int amt;
				int flag = 1;
				do {
					System.out.println("Enter Amount Multiples by 100 and less than 10000:");
					amt = sc.nextInt();
					if (amt >= 100 && amt <= 10000 && amt % 100 == 0) {
						flag = 0;
					}
				} while (flag != 0);
				int _2000count = 0, _500count = 0, _100count = 0;
				int amt_copy = amt;
				while (amt >= 100) {
					if (amt >= 2000) {
						_2000count++;
						amt -= 2000;
					} else if (amt >= 500 && amt < 2000) {
						_500count++;
						amt -= 500;
					} else if (amt >= 100 && amt < 500) {
						_100count++;
						amt -= 100;
					}
				}
				customerdeatail.customercashupdate(obj1, amt_copy, _2000count, _500count, _100count);
			}
		}
	}
	void transfermoney() {
		System.out.println("Enter pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				CustomerDetails obj1 = customerdeatail;
				moneyupdate(obj1);
			}
		}
	}
	void moneyupdate(CustomerDetails obj) {
		System.out.println("Enter Account Holder Name:");
		String s = sc.next();
		System.out.println("Enter account number to transfer:");
		int accno = sc.nextInt();
		for (CustomerDetails customerdeatail1 : detail) {
			if (customerdeatail1.getAccNo() == accno) {
				int amt;
				do {
					System.out.println("Enter Amount less than 10000:");
					amt = sc.nextInt();
				} while (amt > 10000);

				if (obj.Bal >= amt) {
					obj.Bal -= amt;
					customerdeatail1.Bal += amt;
					System.out.println("Amount transfered successfully!");
				}
			}
		}
	}
	void ATMbalance() {
		displayATMdenomenation();
	}
	void DepositAmount() {
		System.out.println("Enter pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				System.out.println("Enter Amount to Deposit:");
				int amount = sc.nextInt();
				customerdeatail.Bal += amount;
			}
		}
	}
}



import java.util.Scanner;
class ATMOperations extends Main {
	CustomerDetails obj1;
	Scanner sc = new Scanner(System.in);
	public ATMOperations() {
		System.out.println("1.Balance Checking");
		System.out.println("2.Money withdrawl");
		System.out.println("3.Money Transfer");
		System.out.println("4.Check ATM balance");
		System.out.println("5.Amount Deposit");
		int choice = sc.nextInt();
		switch (choice) {
		case 1:
			checkbalance();break;
		case 2:
			withdrawmoney();break;
		case 3:
			transfermoney();break;
		case 4:
			ATMbalance();break;
		case 5:
			DepositAmount();break;
		}
	}
	void checkbalance() {
		System.out.println("Enter Secret Pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				System.out.println(customerdeatail.getBalance());
			}
		}
	}
	void withdrawmoney() {
		System.out.println("Enter Secret Pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				obj1 = customerdeatail;
				int amt;
				int flag = 1;
				do {
					System.out.println("Enter Amount Multiples by 100 and less than 10000:");
					amt = sc.nextInt();
					if (amt >= 100 && amt <= 10000 && amt % 100 == 0) {
						flag = 0;
					}
				} while (flag != 0);
				int _2000count = 0, _500count = 0, _100count = 0;
				int amt_copy = amt;
				while (amt >= 100) {
					if (amt >= 2000) {
						_2000count++;
						amt -= 2000;
					} else if (amt >= 500 && amt < 2000) {
						_500count++;
						amt -= 500;
					} else if (amt >= 100 && amt < 500) {
						_100count++;
						amt -= 100;
					}
				}
				customerdeatail.customercashupdate(obj1, amt_copy, _2000count, _500count, _100count);
			}
		}
	}
	void transfermoney() {
		System.out.println("Enter pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				CustomerDetails obj1 = customerdeatail;
				moneyupdate(obj1);
			}
		}
	}
	void moneyupdate(CustomerDetails obj) {
		System.out.println("Enter Account Holder Name:");
		String s = sc.next();
		System.out.println("Enter account number to transfer:");
		int accno = sc.nextInt();
		for (CustomerDetails customerdeatail1 : detail) {
			if (customerdeatail1.getAccNo() == accno) {
				int amt;
				do {
					System.out.println("Enter Amount less than 10000:");
					amt = sc.nextInt();
				} while (amt > 10000);

				if (obj.Bal >= amt) {
					obj.Bal -= amt;
					customerdeatail1.Bal += amt;
					System.out.println("Amount transfered successfully!");
				}
			}
		}
	}
	void ATMbalance() {
		displayATMdenomenation();
	}
	void DepositAmount() {
		System.out.println("Enter pin");
		int pin = sc.nextInt();
		for (CustomerDetails customerdeatail : detail) {
			if (customerdeatail.getPin() == pin) {
				System.out.println("Enter Amount to Deposit:");
				int amount = sc.nextInt();
				customerdeatail.Bal += amount;
			}
		}
	}
}
