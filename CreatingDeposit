import java.util.ArrayList;
import java.util.Collections;
import java.util.Queue;


public class DepositService {
    public static ArrayList<BankDeposit> bankDeposits = new ArrayList<>();

    public static Double calculateDeposit(Integer startSum, Integer monthlyPay, Integer days, BankDeposit deposit) {
        if (startSum < deposit.getMinAmount() || (days < deposit.getMinTime()))
            return 0.;
        int capType = 0;

        if (deposit.getCapType() == CapitalizationType.MONTH)
            capType = 1;
        else if
                (deposit.getCapType() == CapitalizationType.QUARTAL)
            capType = 3;
        else if (deposit.getCapType() == CapitalizationType.YEAR)
            capType = 12;

        if (days > deposit.getMaxTime())
            days = deposit.getMaxTime();
        double sum = startSum + startSum * deposit.getEntryBonus();
        while ((days / (30 * capType)) > 0) {
            sum = sum + monthlyPay * (capType - 1);
            sum = sum + sum * deposit.getYearlyInterest() / (12 / capType);
            sum += monthlyPay;
            days -= 30*capType;
        }

        while (days/30 > 0){
            sum += monthlyPay;
            days -= 30;
        }
        return sum;
    }

    public static String determineTheBest(Integer startSum, Integer monthlyPay, Integer days) {
        ArrayList<Double> moneyFromDeposits = new ArrayList<>();
        for (BankDeposit i : bankDeposits)
            moneyFromDeposits.add(calculateDeposit(startSum, monthlyPay, days, i));

        Double max = Collections.max(moneyFromDeposits);
        int count = 0;
        for (Double i : moneyFromDeposits) {
            if (max == i)
                return bankDeposits.get(count).getDepositName();
            count++;
        }
        return "";
    }

    public static void main(String[] args){
        Queue<String> output = Adapter.readTheFile();
        int length = output.peek().length()*2;
        StringBuffer buf = new StringBuffer(length);
        for (int i = 0; i< 5; i++) {
            buf.append(output.poll());
            Adapter.addDeposit(buf);
            buf.delete(0, length - 1);
        }
