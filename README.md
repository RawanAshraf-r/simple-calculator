import javax.swing.;
import java.awt.;
import java.awt.event.*;

public class SimpleCalculator extends JFrame implements ActionListener {

JTextField textField;
double num1, num2, result;
char operator;

public SimpleCalculator() {
    setTitle("Simple Calculator");
    setSize(400, 500);
    setDefaultCloseOperation(EXIT_ON_CLOSE);
    setLocationRelativeTo(null); // Center the window

    textField = new JTextField();
    textField.setEditable(false);
    textField.setFont(new Font("Arial", Font.BOLD, 24));
    add(textField, BorderLayout.NORTH);

    JPanel panel = new JPanel();
    panel.setLayout(new GridLayout(4, 4, 10, 10));

    String[] buttons = {
        "7", "8", "9", "/",
        "4", "5", "6", "*",
        "1", "2", "3", "-",
        "0", "C", "=", "+"
    };

    for (String text : buttons) {
        JButton button = new JButton(text);
        button.setFont(new Font("Arial", Font.BOLD, 20));
        button.addActionListener(this);
        panel.add(button);
    }

    add(panel);

    setVisible(true);
}

public void actionPerformed(ActionEvent e) {
    String input = e.getActionCommand();

    if ((input.charAt(0) >= '0' && input.charAt(0) <= '9')) {
        textField.setText(textField.getText() + input);
    } else if (input.charAt(0) == 'C') {
        textField.setText("");
    } else if (input.charAt(0) == '=') {
        num2 = Double.parseDouble(textField.getText());
        switch (operator) {
            case '+': result = num1 + num2; break;
            case '-': result = num1 - num2; break;
            case '*': result = num1 * num2; break;
            case '/': 
                if (num2 != 0) {
                    result = num1 / num2;
                } else {
                    JOptionPane.showMessageDialog(this, "Cannot divide by zero");
                    textField.setText("");
                    return;
                }
                break;
        }
        textField.setText(String.valueOf(result));
    } else {
        try {
            num1 = Double.parseDouble(textField.getText());
            operator = input.charAt(0);
            textField.setText("");
        } catch (Exception ex) {
            JOptionPane.showMessageDialog(this, "Invalid input");
            textField.setText("");
        }
    }
}

public static void main(String[] args) {
    new SimpleCalculator();
}
}
