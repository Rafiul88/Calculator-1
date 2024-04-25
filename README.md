# Calculator-1
Caimport javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class Calculator extends JFrame {
    private JTextField textField;
    private CalculatorModel model;
    public Calculator() {
        model = new CalculatorModel();

        setTitle("Calculator");
        setSize(300, 400);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(null);

        textField = new JTextField();
        textField.setBounds(20, 20, 260, 40);
        add(textField);
        String[] buttonLabels = {
            "7", "8", "9", "/",
            "4", "5", "6", "*",
            "1", "2", "3", "-",
            "0", "C", "=", "+"
        };
        for (int i = 0; i < 16; i++) {
            JButton button = new JButton(buttonLabels[i]);
            button.setBounds((i % 4) * 60 + 20, (i / 4) * 60 + 80, 50, 50);
            button.addActionListener(new ButtonClickListener());
            add(button);
        }
    }
    private class ButtonClickListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent evt) {
            String command = evt.getActionCommand();
            handleButtonClick(command);
        }
    }

    private void handleButtonClick(String command) {
        try {
            if (command.matches("[0-9]")) {
                textField.setText(textField.getText() + command);
            } else if (command.equals("C")) {                textField.setText("");
                model.clear();
            } else if (command.equals("=")) {
                
                double result = model.evaluate(textField.getText());
                textField.setText(Double.toString(result));
            } else {
                
                model.setOperator(command);
                model.setOperand(Double.parseDouble(textField.getText()));
                textField.setText("");
            }
        } catch (Exception e) {
            textField.setText("Error");
        }
    }
    private static class CalculatorModel {
        private double result;
        private String operator;
        private double operand;

        public CalculatorModel() {
            result = 0;
            operator = "";
        }

        public void clear() {
            result = 0;
            operator = "";
        }

        public void setOperator(String operator) {
            this.operator = operator;
        }

        public void setOperand(double operand) {
            this.operand = operand;
        }

        public double evaluate(String expression) {
            double num = Double.parseDouble(expression);
            switch (operator) {
                case "+":
                    result += num;
                    break;
                case "-":
                    result -= num;
                    break;
                case "*":
                    result *= num;
                    break;
                case "/":
                    if (num == 0) {
                        throw new ArithmeticException("Cannot divide by zero");
                    }
                    result /= num;
                    break;
            }
            return result;
        }
    }    public static void main(String[] args) {    

    Calculator calculator = new Calculator();
        calculator.setVisible(true);
    }
}lculator by Rafiul islam-230240088
