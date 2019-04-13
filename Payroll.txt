// Tax rate for reference: 
// http://www.ficatax.org/florida-fica-tax/
// https://smartasset.com/taxes/florida-paycheck-calculator 
import java.awt.Component;
import java.util.Scanner;
import javax.swing.JOptionPane;
/**
 * Florida company A Paycheck - Version 1.8
 * @author Tony, Emma, Rasik, Ben, and Group A.
 * 
 * This program is made to calculate and display WEEKLY employee pay stubs for ABC Company
 * 
 */
public class Payroll {
    
    public static void main (String[] args) {
        
        Scanner reader = new Scanner (System.in);
 /*DECLARE VARIABLES*/       
        double regPay, PayPerHr, hoursaweek, pay, overtimehoursSat, overtimepaySat,
                overtimehoursSun, overtimepaySun, overtimepay, grossPay, deduction, 
                fedDeduction, stateDeduction, socSecDeduction, medicDeduction, 
                pensionDeduction, retirementDeduction, lifeDeduction; // <-- might be favorite coding line of all time!  
 
 /*DECLARE STATIC VARIABLES*/       
        final double federal_tax_rate = .124, state_tax_rate = 0.1222, social_security_tax_rate = .062,
                     medicare_tax_rate = .029, pension_plan_tax_rate = 0.025, retirement_plan= 0.05, 
                     life_insurance = 0.04;
        
        String companyName = "ABC Company";
        String companyAddress = "3826  Timberbrook Lane, FLEMING ISLAND FL 32003";
        String usersChoiceString2;
        Component frame = null;
        
/*USER INPUTS*/
        JOptionPane.showMessageDialog(frame, "Welcome to ABC Company's Payroll program. "
            + "This program is to be used by authorized payroll administrators only. \n" 
            + "By pressing OK you are confirming yourself as an authorized user of this program. \n" 
            + "Please note ABC Company currently runs payroll WEEKLY so all reporting and statements will be entered with that in mind. \n" 
            + "If you would like to change the payroll pay periods to be BIWEEKLY or MONTHLY "
            + "please have an authorized payroll administrator contact your payroll company:  Group A, Inc. \n");

        String periodStart;
        periodStart = JOptionPane.showInputDialog("Enter Period Starting Date (FORMAT: mm/dd/yyyy):");
        
        String periodEnd;
        periodEnd = JOptionPane.showInputDialog("Enter Period Ending Date (FORMAT: mm/dd/yyyy):");
        
        String payDate;
        payDate = JOptionPane.showInputDialog("Enter Pay Date (FORMAT: mm/dd/yyyy):");
        
        String payeeName;
        payeeName = JOptionPane.showInputDialog("Enter payee's first and last name:");
        
        String payeeAddress;
        payeeAddress = JOptionPane.showInputDialog("Enter payee's full mailing address:");

 /*CALCULATION INPUTS*/
        PayPerHr = Double.parseDouble(JOptionPane.showInputDialog("Enter payee's regular hourly pay: "));
        hoursaweek = Double.parseDouble(JOptionPane.showInputDialog("Enter payee's base hours worked this period: "));
        overtimehoursSat = Double.parseDouble(JOptionPane.showInputDialog("Enter payee's Saturday hours worked this period: "));
        overtimehoursSun = Double.parseDouble(JOptionPane.showInputDialog("Enter payee's Sunday hours worked this period: "));
        
        regPay = PayPerHr * hoursaweek;
        overtimepay = (overtimehoursSat * 1.5 + overtimehoursSun * 2.0) * PayPerHr;
        deduction = (federal_tax_rate + state_tax_rate + social_security_tax_rate + medicare_tax_rate
                    + pension_plan_tax_rate + retirement_plan + life_insurance) * (overtimepay + regPay);
        fedDeduction = (federal_tax_rate)*(overtimepay + regPay);
        stateDeduction = (state_tax_rate)*(overtimepay + regPay);
        socSecDeduction = (social_security_tax_rate)*(overtimepay + regPay);
        medicDeduction = (medicare_tax_rate)*(overtimepay + regPay);
        pensionDeduction = (pension_plan_tax_rate)*(overtimepay + regPay);
        retirementDeduction = (retirement_plan)*(overtimepay + regPay);
        lifeDeduction = (life_insurance)*(overtimepay + regPay);
        pay = overtimepay + regPay - deduction;

/*OUTPUT DECLARATIONS*/
        JOptionPane.showMessageDialog(null, "YOUR WEEKLY PAYCHECK: " + "\n" 
        + "Period Starting: " + periodStart + "\n" + "Period Ending: " + periodEnd
        + "Pay Date: " + payDate + "\n" + "Company Name: " + companyName + "\n" 
        + "Company Address: " + companyAddress + "\n" + "Payee Name: " + payeeName + "\n"
        + "Payee Address: " + payeeAddress + "\n" 
        + "____________________________________________" + "\n" 
        + "EARNINGS: " 
        + "\n" + "Normal weekly pay:  $" +regPay + "\n"  + "Overtime pay:  $" +overtimepay + "\n" 
        + "GROSS EARNINGS:  $" + (grossPay = regPay + overtimepay) + "\n" 
        + "____________________________________________" + "\n" 
        + "DEDUCTIONS:" 
        + "\n" + "Federal tax: " + "$" + fedDeduction + "\n" 
        + "State tax: " + "$" +  stateDeduction + "\n" + "Social security tax: " + "$" + socSecDeduction 
        + "\n" + "Medicaid Plan: " + "$" + medicDeduction + "\n" + "Pension Plan: " + "$" + pensionDeduction + "\n" 
        + "401k Retirement Plan: " + "$" + retirementDeduction + "\n" + "Life Insurance: " + "$" + lifeDeduction + "\n" 
        + "DEDUCTIONS TOTAL: " + "$" + deduction + "\n" 
        + "____________________________________________" + "\n" 
        + "TOTAL WEEKLY NET PAY: $ " +pay );
      
    }//End of main method
}//End of Payroll class
