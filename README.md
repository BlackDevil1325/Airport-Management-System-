public LoginFrame() {
    setTitle("Airlines Database Login");
    setSize(400, 250); // Adjusted size for login
    setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    setLocationRelativeTo(null); // Center the window
    setLayout(new BorderLayout(10, 10)); // Use BorderLayout

    // Panel for components
    JPanel panel = new JPanel(new GridBagLayout());
    panel.setBorder(BorderFactory.createEmptyBorder(20, 20, 20, 20));
    GridBagConstraints gbc = new GridBagConstraints();
    gbc.insets = new Insets(5, 5, 5, 5); // Padding
    gbc.fill = GridBagConstraints.HORIZONTAL;

    // Username Label and Field
    gbc.gridx = 0;
    gbc.gridy = 0;
    gbc.anchor = GridBagConstraints.EAST;
    panel.add(new JLabel("Username:"), gbc);

    gbc.gridx = 1;
    gbc.gridy = 0;
    gbc.anchor = GridBagConstraints.WEST;
    usernameField = new JTextField(15); // Field size
    panel.add(usernameField, gbc);

    // Password Label and Field
    gbc.gridx = 0;
    gbc.gridy = 1;
    gbc.anchor = GridBagConstraints.EAST;
    panel.add(new JLabel("Password:"), gbc);

    gbc.gridx = 1;
    gbc.gridy = 1;
    gbc.anchor = GridBagConstraints.WEST;
    passwordField = new JPasswordField(15);
    panel.add(passwordField, gbc);

    // Error Label
    gbc.gridx = 0;
    gbc.gridy = 2;
    gbc.gridwidth = 2; // Span across two columns
    gbc.anchor = GridBagConstraints.CENTER;
    errorLabel = new JLabel(" "); // Start with empty space
    errorLabel.setForeground(Color.RED);
    errorLabel.setHorizontalAlignment(SwingConstants.CENTER);
    panel.add(errorLabel, gbc);

    // Login Button
    gbc.gridx = 0;
    gbc.gridy = 3;
    gbc.gridwidth = 2; // Span across two columns
    gbc.anchor = GridBagConstraints.CENTER;
    loginButton = new JButton("Login");
    loginButton.setFont(new Font("Segoe UI", Font.BOLD, 13));
    loginButton.setPreferredSize(new Dimension(100, 30)); // Button size
    panel.add(loginButton, gbc);

    // Add panel to frame
    add(panel, BorderLayout.CENTER);

    // Login Button Action Listener
    loginButton.addActionListener(e -> performLogin());

    // Allow login on Enter key press in password field
    passwordField.addActionListener(e -> performLogin());
}

private void performLogin() {
    String username = usernameField.getText();
    String password = new String(passwordField.getPassword()); // Get password safely

    // --- Basic Authentication ---
    // !! WARNING: Hardcoded credentials - NOT SECURE for production !!
    // Replace with database lookup or a more secure method in a real application
    if ("admin".equals(username) && "password123".equals(password)) {
        // Login successful
        dispose(); // Close the login window

        // Open the main Airlines Database window
        SwingUtilities.invokeLater(() -> {
            AirlinesDatabase dbFrame = new AirlinesDatabase();
            dbFrame.setVisible(true);
        });

    } else {
        // Login failed
        errorLabel.setText("Invalid username or password.");
        passwordField.setText(""); // Clear password field
        usernameField.requestFocus(); // Focus back on username
    }
}
