# Book-Store-Bill-Generation-System-
Developed a Java Swing application for bookstore billing with discount calculation, automated bill generation, and user-friendly GUI.
import javax.swing.*; 
import java.awt.*; 
import java.awt.event.ActionEvent; 
import java.awt.event.ActionListener; 
public class BookStoreApp { 
    public static void main(String[] args) { 
        new HomeScreen(); 
    } 
} 
class HomeScreen { 
    JFrame frame; 
    HomeScreen() { 
        frame = new JFrame("Home Screen"); 
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
        frame.setSize(600, 400); 
        frame.setLayout(new BorderLayout()); 
        JPanel backgroundPanel = new JPanel() { 
            private Image backgroundImage; 
            { 
                backgroundImage = new ImageIcon("background.jpg").getImage(); 
            } 
         protected void paintComponent(Graphics g) { 
                super.paintComponent(g); 
                Graphics2D g2d = (Graphics2D) g.create(); 
                g2d.setComposite(AlphaComposite.getInstance(AlphaComposite.SRC_OVER, 
0.8f)); 
                g2d.drawImage(backgroundImage, 0, 0, getWidth(), getHeight(), this); 
                g2d.dispose(); 
            } 
        }; 
        backgroundPanel.setLayout(new FlowLayout()); 
      JButton startButton = new JButton("St Agnes Book Center Mangaluru"); 
        startButton.setFont(new Font("Times New Roman", Font.ITALIC, 16)); 
        startButton.setBackground(new Color(139, 69, 19));  
        startButton.setForeground(Color.WHITE);  
        startButton.setFocusPainted(false);  
        startButton.addActionListener(e -> { 
            frame.dispose(); 
            new BookEntryForm(); 
        }); 
       backgroundPanel.add(startButton); 
        frame.setContentPane(backgroundPanel); 
        frame.setVisible(true); 
    } 
} 
class BookEntryForm { 
    JFrame frame; 
    JTextField bookIdField, bookNameField, amountField, discountField; 
   BookEntryForm() { 
        frame = new JFrame("Book Entry Form"); 
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
        frame.setSize(600, 400); 
        frame.setLayout(new GridLayout(6, 2, 10, 10)); 
        frame.getContentPane().setBackground(new Color(240, 240, 240)); 
       JLabel bookIdLabel = new JLabel("Book ID:"); 
        bookIdField = new JTextField(); 
        JLabel bookNameLabel = new JLabel("Book Name:"); 
        bookNameField = new JTextField(); 
       JLabel amountLabel = new JLabel("Amount:"); 
        amountField = new JTextField(); 
        JLabel discountLabel = new JLabel("Discount (%):"); 
        discountField = new JTextField(); 
        JButton convertButton = new JButton("CONVERT"); 
        JButton clearButton = new JButton("CLEAR"); 
        JButton generateBillButton = new JButton("GENERATE BILL"); 
        JButton exiButton = new JButton("EXIT"); 
        convertButton.setBackground(new Color(0, 128, 0));  
        convertButton.setForeground(Color.WHITE);  
        convertButton.setFocusPainted(false); 
        convertButton.setFont(new Font("Arial", Font.BOLD, 14)); 
       clearButton.setBackground(new Color(255, 69, 0));  
        clearButton.setForeground(Color.WHITE);  
        clearButton.setFocusPainted(false); 
        clearButton.setFont(new Font("Arial", Font.BOLD, 14)); 
        generateBillButton.setBackground(new Color(70, 130, 180));  
        generateBillButton.setForeground(Color.WHITE);  
        generateBillButton.setFocusPainted(false); 
        generateBillButton.setFont(new Font("Arial", Font.BOLD, 14)); 
        exiButton.setBackground(new Color(255, 99, 71));  
        exiButton.setForeground(Color.WHITE); 
        exiButton.setFocusPainted(false); 
        exiButton.setFont(new Font("Arial", Font.BOLD, 14)); 
       convertButton.addActionListener(e -> convertAmount()); 
        clearButton.addActionListener(e -> clearFields()); 
        generateBillButton.addActionListener(e -> generateBill()); 
        exiButton.addActionListener(e -> exitfield()); 
       frame.add(bookIdLabel); frame.add(bookIdField); 
        frame.add(bookNameLabel); frame.add(bookNameField); 
        frame.add(amountLabel); frame.add(amountField); 
        frame.add(discountLabel); frame.add(discountField); 
        frame.add(convertButton); frame.add(clearButton); 
        frame.add(generateBillButton); 
        frame.add(exiButton); 
       frame.setVisible(true); 
    } 
private void convertAmount() { 
        try { 
            double amount = Double.parseDouble(amountField.getText()); 
            double discount = Double.parseDouble(discountField.getText()); 
            double discountedPrice = amount - (amount * discount / 100); 
            JOptionPane.showMessageDialog(frame, "Discounted Price: " + discountedPrice); 
        } catch (NumberFormatException e) { 
            JOptionPane.showMessageDialog(frame, "Enter valid numeric values.", "Error", 
JOptionPane.ERROR_MESSAGE); 
        } 
    } 
private void clearFields() { 
        bookIdField.setText(""); 
        bookNameField.setText(""); 
        amountField.setText(""); 
        discountField.setText(""); 
    } 
private void exitfield() { 
        System.exit(0); 
    } 
 private void generateBill() { 
        try { 
            String bookId = bookIdField.getText(); 
            String bookName = bookNameField.getText(); 
            double amount = Double.parseDouble(amountField.getText()); 
            double discount = Double.parseDouble(discountField.getText()); 
            double discountedPrice = amount - (amount * discount / 100); 
String billDetails = "==== BOOK BILL ====" + 
                    "\nBook ID: " + bookId + 
                    "\nBook Name: " + bookName + 
                    "\nOriginal Price: $" + amount + 
                    "\nDiscount: " + discount + "%" + 
                    "\nFinal Price: $" + discountedPrice; 
new BillDisplayFrame(billDetails); 
            frame.dispose(); 
        } catch (NumberFormatException e) { 
            JOptionPane.showMessageDialog(frame, "Enter valid numeric values.", "Error", 
JOptionPane.ERROR_MESSAGE); 
        } 
    } 
} 
class BillDisplayFrame { 
    JFrame frame; 
BillDisplayFrame(String billDetails) { 
        frame = new JFrame("Bill Details"); 
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
        frame.setSize(400, 300); 
        frame.setLayout(new BorderLayout()); 
       frame.getContentPane().setBackground(new Color(240, 240, 240)); 
        JTextArea billArea = new JTextArea(billDetails); 
        billArea.setEditable(false); 
        billArea.setFont(new Font("Arial", Font.PLAIN, 14)); 
        billArea.setBorder(BorderFactory.createLineBorder(Color.BLACK, 1));  
        JScrollPane scrollPane = new JScrollPane(billArea); 
        frame.add(scrollPane, BorderLayout.CENTER); 
        JButton closeButton = new JButton("CLOSE"); 
        closeButton.addActionListener(e -> frame.dispose()); 
        JPanel buttonPanel = new JPanel(); 
        buttonPanel.add(closeButton); 
        frame.add(buttonPanel, BorderLayout.SOUTH); 
        frame.setVisible(true); 
    } 
} 

