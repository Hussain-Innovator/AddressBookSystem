// **Java Swing application**
// **AddressBookSystem**
// Here is The Source Code for the logn page of AddressBookSystem , Where we have to enter Username and Password that is builded in The Source Code
// The Password and Username field can change from the code if you Want 
// Use Eclipse Ide for The project
// Username = "Admin"
// Password = 'admin'
package myPackage;

import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class LoginWindow extends JFrame implements ActionListener {
    /**
	 * 
	 */
	private static final long serialVersionUID = 1L;
	private JTextField usernameField;
    private JPasswordField passwordField;
    private JButton loginButton;
    
    private static final String USERNAME = "Admin";
    private static final String PASSWORD = "admin";

    public LoginWindow() {
        setTitle("Login");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        
        setLayout(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.gridwidth = GridBagConstraints.REMAINDER;
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.insets = new Insets(5, 5, 5, 5);

        add(new JLabel("Username:"), gbc);
        usernameField = new JTextField(20);
        usernameField.setPreferredSize(new Dimension(200,30));
        add(usernameField, gbc);

        add(new JLabel("Password:"), gbc);
        passwordField = new JPasswordField(20);
        passwordField.setPreferredSize(new Dimension(200, 30));
        add(passwordField, gbc);

        loginButton = new JButton("Login");
        loginButton.addActionListener(this);
        add(loginButton, gbc);

        pack();
        setMinimumSize(new Dimension(400, 300));
        setLocationRelativeTo(null);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String enteredUsername = usernameField.getText();
        String enteredPassword = new String(passwordField.getPassword());

        if (USERNAME.equals(enteredUsername) && PASSWORD.equals(enteredPassword)) {
        	AddressBookSystem addressBookSystem = new AddressBookSystem();
            addressBookSystem.setVisible(true);
            // Further code to proceed after successful login
        } else {
            JOptionPane.showMessageDialog(this, "Invalid username or password.");
        }
    }

	    public static void main(String[] args) {
	        SwingUtilities.invokeLater(() -> {
	            LoginWindow loginWindow = new LoginWindow();
	            loginWindow.setVisible(true);
	        });
	    }
	}

 // Here is the complete Source Code of AddressBookSystem:
 package myPackage;

import javax.swing.*;
import java.awt.*;
import java.io.*;
import java.util.Hashtable;

public class AddressBookSystem extends JFrame {
    private static final long serialVersionUID = 1L;
    private Hashtable<Integer, String[]> addressBook;
    @SuppressWarnings("unused")
	private int nextUserId; 
    private JTextField fullNameField, contactNoField, emailField, addressField, streetField, cityField, stateField;
    private JComboBox<String> titleComboBox, languageComboBox, genderComboBox;
    private JTextField userIdField;
    private GridBagConstraints gbc;

    public AddressBookSystem() {
        addressBook = new Hashtable<>();
        nextUserId = 1;
        loadEntries();
        createGUI();
    }
    
    private JLabel createLabel1(String text) {
        JLabel label = new JLabel(text, SwingConstants.CENTER);
        label.setFont(new Font("Sitka Small", Font.BOLD, 28));
        
        // Set the text color
        label.setForeground(new Color(51, 51, 204));

        label.setAlignmentX(Component.CENTER_ALIGNMENT);
        label.setMaximumSize(new Dimension(600, 30));
        return label;
    }


    private void createGUI() {
        setTitle("Address Book System");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel mainPanel = new JPanel();
        mainPanel.setLayout(new BoxLayout(mainPanel, BoxLayout.Y_AXIS));
        mainPanel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JPanel formPanel = new JPanel(new GridBagLayout());
        gbc = new GridBagConstraints();
        gbc.fill = GridBagConstraints.HORIZONTAL;
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.gridx = 0;	
        gbc.gridy = 0;
        mainPanel.add(createLabel1("Address Book System"));
        // Add fields to the form
        addFormField(formPanel, "User ID:", userIdField = new JTextField(20), gbc);
        addFormField(formPanel, "Title:", titleComboBox = new JComboBox<>(new String[]{"Mr", "Ms", "Other"}), gbc);
        addFormField(formPanel, "Full Name:", fullNameField = new JTextField(20), gbc);
        addFormField(formPanel, "Contact No:", contactNoField = new JTextField(20), gbc);
        addFormField(formPanel, "Email:", emailField = new JTextField(20), gbc);
        addFormField(formPanel, "Address:", addressField = new JTextField(20), gbc);
        addFormField(formPanel, "Street:", streetField = new JTextField(20), gbc);
        addFormField(formPanel, "City:", cityField = new JTextField(20), gbc);
        addFormField(formPanel, "State:", stateField = new JTextField(20), gbc);
        addFormField(formPanel, "Language:", languageComboBox = new JComboBox<>(new String[]
        	{"Urdu", "English", "Shina", "Punjabi", "Sindhi", "Pashto", "Balochi", "Saraiki", "Hindko", "Brahui", "Kashmiri"}), gbc);
        addFormField(formPanel, "Gender:", genderComboBox = new JComboBox<>(new String[]{"Male", "Female", "Other"}), gbc);

        mainPanel.add(formPanel);

        // Buttons
        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10)); // Added gaps between buttons
        buttonPanel.setBackground(Color.decode("#a3daff"));
        buttonPanel.add(createButton("Add"));
        buttonPanel.add(createButton("Update"));
        buttonPanel.add(createButton("Save"));
        buttonPanel.add(createButton("Delete"));
        buttonPanel.add(createButton("Show"));

        mainPanel.add(buttonPanel);

        add(mainPanel);
        pack();
        setLocationRelativeTo(null); // Center on screen
        setVisible(true);
    }
    
    private void addFormField(JPanel panel, String label, Component comp, GridBagConstraints gbc) {
        panel.add(new JLabel(label), gbc);
        gbc.gridx++;
        panel.add(comp, gbc);
        gbc.gridx = 0;
        gbc.gridy++;
    }

    @SuppressWarnings("unused")
	private JLabel createLabel(String text) {
        JLabel label = new JLabel(text, SwingConstants.CENTER);
        label.setFont(new Font("Arial", Font.BOLD, 24));
        label.setForeground(Color.WHITE); // Set the text color to white if the background is dark
        label.setAlignmentX(Component.CENTER_ALIGNMENT); // This will align the label text to the center
        label.setMaximumSize(new Dimension(600, 30));
        return label;
    }

    @SuppressWarnings("unused")
	private JPanel createFormField(String labelText, String[] options, boolean isComboBox) {
        JPanel formPanel = new JPanel();
        formPanel.setLayout(new FlowLayout(FlowLayout.LEFT));
        formPanel.setMaximumSize(new Dimension(600, 30));

        JLabel label = new JLabel(labelText);
        formPanel.add(label);

        if (isComboBox) {
            JComboBox<String> comboBox = new JComboBox<>(options);
            formPanel.add(comboBox);
            if ("Title:".equals(labelText)) {
                titleComboBox = comboBox;
            } else if ("Language:".equals(labelText)) {
                languageComboBox = comboBox;
            } else if ("Gender:".equals(labelText)) {
                genderComboBox = comboBox;
            }
        } else {
            JTextField textField = new JTextField(20);
            formPanel.add(textField);
            switch (labelText) {
            	case "User ID:": 
            		userIdField = textField;
                break;
                case "Full Name:":
                    fullNameField = textField;
                    break;
                case "Contact No:":
                    contactNoField = textField;
                    break;
                case "Email:":
                    emailField = textField;
                    break;
                case "Address:":
                    addressField = textField;
                    break;
                case "Street:":
                    streetField = textField;
                    break;
                case "City:":
                    cityField = textField;
                    break;
                case "State:":
                    stateField = textField;
                    break;
            }
        }

        return formPanel;
    }
    private void addEntry() {
        String userIdStr = userIdField.getText();
        String fullName = fullNameField.getText();
        if (!fullName.isEmpty() && !userIdStr.isEmpty()) {
            try {
                int userId = Integer.parseInt(userIdStr);
                if (addressBook.containsKey(userId)) {
                    JOptionPane.showMessageDialog(this, "User ID already in use.");
                    return;
                }
                String[] details = {
                    (String)titleComboBox.getSelectedItem(),
                    fullName, // Include the full name as the second detail
                    contactNoField.getText(),
                    emailField.getText(),
                    addressField.getText(),
                    streetField.getText(),
                    cityField.getText(),
                    stateField.getText(),
                    (String)languageComboBox.getSelectedItem(),
                    (String)genderComboBox.getSelectedItem()
                };
                addressBook.put(userId, details);
                JOptionPane.showMessageDialog(this, "Added: " + fullName + " with User ID: " + userId);
            } catch (NumberFormatException e) {
                JOptionPane.showMessageDialog(this, "Invalid User ID.");
            }
        } else {
            JOptionPane.showMessageDialog(this, "User ID and Full Name fields cannot be empty.");
        }
    }

    
    private void showEntryById() {
        String userIdStr = JOptionPane.showInputDialog(this, "Enter User ID to Show:");
        try {
            int userId = Integer.parseInt(userIdStr);
            String[] details = addressBook.get(userId);
            if (details != null) {
                StringBuilder detailsBuilder = new StringBuilder();

                // Ensure you are accessing indices within the bounds of the 'details' array
                detailsBuilder.append("Title: ").append(details.length > 0 ? details[0] : "");
                detailsBuilder.append("\nName: ").append(details.length > 1 ? details[1] : "");
                detailsBuilder.append("\nPhone: ").append(details.length > 2 ? details[2] : "");
                detailsBuilder.append("\nEmail: ").append(details.length > 3 ? details[3] : "");
                detailsBuilder.append("\nAddress: ").append(details.length > 4 ? details[4] : "");
                detailsBuilder.append("\nStreet: ").append(details.length > 5 ? details[5] : "");
                detailsBuilder.append("\nCity: ").append(details.length > 6 ? details[6] : "");
                detailsBuilder.append("\nState: ").append(details.length > 7 ? details[7] : "");
                detailsBuilder.append("\nLanguage: ").append(details.length > 8 ? details[8] : "");
                detailsBuilder.append("\nGender: ").append(details.length > 9 ? details[9] : "");

                JOptionPane.showMessageDialog(this, "Details for User ID " + userId + ":\n" + detailsBuilder.toString());
            } else {
                JOptionPane.showMessageDialog(this, "No entry found for User ID: " + userId);
            }
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Invalid User ID.");
        }
    }

    private static final String FILE_PATH = "C:\\Users\\Dell\\Desktop\\New folder\\AddressBookSystem.txt";

    private void saveEntries() {
        try (BufferedWriter writer = new BufferedWriter(new FileWriter(FILE_PATH))) {
            for (Integer key : addressBook.keySet()) {
                String[] details = addressBook.get(key);
                String line = key + ": " + String.join(", ", details);
                writer.write(line);
                writer.newLine();
            }
            JOptionPane.showMessageDialog(this, "Address Book saved successfully.");
        } catch (IOException e) {
            JOptionPane.showMessageDialog(this, "Failed to save Address Book.");
            e.printStackTrace();
        }
    }

    private void loadEntries() {
        addressBook = new Hashtable<>();
        try (BufferedReader reader = new BufferedReader(new FileReader(FILE_PATH))) {
            String line;
            int highestId = 0; // Variable to track the highest user ID

            while ((line = reader.readLine()) != null) {
                String[] parts = line.split(": ");
                try {
                    Integer key = Integer.parseInt(parts[0]); // Convert the user ID to Integer
                    String[] details = parts[1].split(", ");
                    addressBook.put(key, details);

                    // Update the highest user ID
                    if (key > highestId) {
                        highestId = key;
                    }
                } catch (NumberFormatException e) {
                    System.out.println("Skipping invalid line: " + line);
                }
            }

            nextUserId = highestId + 1; // Set nextUserId to one more than the highest ID found
        } catch (FileNotFoundException e) {
            JOptionPane.showMessageDialog(this, "No data file found. Starting with an empty address book.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }



    private JButton createButton(String text) {
        JButton button = new JButton(text);
        button.setFont(new Font("Times New Roman", Font.PLAIN, 20));
        button.setBackground(new Color(0,100,0)); // Dark green background
        button.setForeground(Color.WHITE); // White text
        button.setFocusPainted(false); // Remove focus border
        button.setBorderPainted(false); // Remove border for flat style
        button.addActionListener(e ->  {
            switch (text) {
                case "Add":
                    addEntry();
                    break;
                case "Show":
                    showEntryById();
                    break;
                case "Save":
                    saveEntries();
                    break;
                case "Update":
                    updateEntry();
                    break;
                case "Delete":
                    deleteEntry();
                    break;
            }
        });
        return button;
    }
    
    private void deleteEntry() {
        String userIdStr = JOptionPane.showInputDialog(this, "Enter User ID to Delete:");
        try {
            int userId = Integer.parseInt(userIdStr);
            if (addressBook.containsKey(userId)) {
                addressBook.remove(userId);
                JOptionPane.showMessageDialog(this, "Deleted entry with User ID: " + userId);
            } else {
                JOptionPane.showMessageDialog(this, "No entry found for User ID: " + userId);
            }
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Invalid User ID.");
        }
    }

    private void updateEntry() {
        String userIdStr = JOptionPane.showInputDialog(this, "Enter User ID to Update:");
        try {
            int userId = Integer.parseInt(userIdStr);
            if (addressBook.containsKey(userId)) {
                String fullName = fullNameField.getText();
                if (!fullName.isEmpty()) {
                    String[] details = {
                        (String)titleComboBox.getSelectedItem(),
                        contactNoField.getText(),
                        emailField.getText(),
                        addressField.getText(),
                        streetField.getText(),
                        cityField.getText(),
                        stateField.getText(),
                        (String)languageComboBox.getSelectedItem(),
                        (String)genderComboBox.getSelectedItem()
                    };
                    addressBook.put(userId, details);
                    JOptionPane.showMessageDialog(this, "Updated entry with User ID: " + userId);
                } else {
                    JOptionPane.showMessageDialog(this, "Full Name field cannot be empty.");
                }
            } else {
                JOptionPane.showMessageDialog(this, "No entry found for User ID: " + userId);
            }
        } catch (NumberFormatException e) {
            JOptionPane.showMessageDialog(this, "Invalid User ID.");
        }
    }


    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            AddressBookSystem addressBookSystem = new AddressBookSystem();
            addressBookSystem.setVisible(true);
        });
    }
}
