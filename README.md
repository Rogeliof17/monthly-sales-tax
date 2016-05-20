# monthly-sales-tax
a program demonstrating using GUI and calculates a total sales tax


*/
import java.awt.*;
import javax.swing.*;
import java.awt.event.*;

public class SalesTax extends JFrame
{
    private JPanel panel;
    private JTextField totalSales;
    private JButton calcButton;

    private final double COUNTY_RATE = 0.02;
    private final double STATE_RATE = 0.04;

    private final int WINDOW_WIDTH = 360;
    private final int WINDOW_HEIGHT = 100;

    public SalesTax()
    {
        setTitle("Monthly Sales Tax Reporter");

        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        buildPanel();

        add(panel);

        setSize(WINDOW_WIDTH, WINDOW_HEIGHT);
        setVisible(true);
    }

    private void buildPanel()
    {
        JLabel totalSalesMsg = new JLabel("Enter Total Sales: ");

        totalSales = new JTextField(10);

        calcButton = new JButton("Calculate Sales Tax");

        calcButton.addActionListener(new CalcButtonListener());

        panel = new JPanel();

        panel.add(totalSalesMsg);
        panel.add(totalSales);
        panel.add(calcButton);


    }

    private class CalcButtonListener implements ActionListener
    {
        public void actionPerformed (ActionEvent e)
        {
              double totalSalesAmount,
                      countyTaxAmount,
                      stateTaxAmount,
                      totalTaxAmount;

            totalSalesAmount = Double.parseDouble(totalSales.getText());

            countyTaxAmount = totalSalesAmount * COUNTY_RATE;

            stateTaxAmount = totalSalesAmount * STATE_RATE;

            totalTaxAmount = countyTaxAmount + stateTaxAmount;

            JOptionPane.showMessageDialog(null, String.format(
                                                        "County Sales Tax: $%,.2f\n" +
                                                        "State Sales Tax: $%,.2f\n" +
                                                        "Total Sales Tax: $%,.2f",
                                                            countyTaxAmount, stateTaxAmount,
                                                            totalTaxAmount));
        }
    }

    public static void main(String[] args)
    {
        new SalesTax();
    }
}
