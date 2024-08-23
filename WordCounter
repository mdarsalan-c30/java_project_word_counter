import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.util.Scanner;
import java.util.StringTokenizer;

public class WordCounter extends JFrame {

    private JTextArea inputTextArea;
    private JTextArea resultTextArea;
    private JButton browseButton;
    private JButton countButton;
    private JFileChooser fileChooser;

    public WordCounter() {
        // Frame settings
        setTitle("Word Counter");
        setSize(500, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new BorderLayout(10, 10));

        // Create UI components
        JLabel instructionLabel = new JLabel("Type text or select a file:");
        instructionLabel.setFont(new Font("Arial", Font.BOLD, 16));
        instructionLabel.setHorizontalAlignment(JLabel.CENTER);

        inputTextArea = new JTextArea(5, 30);
        inputTextArea.setLineWrap(true);
        inputTextArea.setWrapStyleWord(true);
        inputTextArea.setBorder(BorderFactory.createLineBorder(Color.GRAY, 1));

        resultTextArea = new JTextArea(10, 30);
        resultTextArea.setEditable(false);
        resultTextArea.setLineWrap(true);
        resultTextArea.setWrapStyleWord(true);
        resultTextArea.setBorder(BorderFactory.createLineBorder(Color.GRAY, 1));

        browseButton = new JButton("Browse File");
        countButton = new JButton("Count Words");

        // File chooser
        fileChooser = new JFileChooser();

        // Panel for input area and buttons
        JPanel inputPanel = new JPanel(new BorderLayout(5, 5));
        inputPanel.add(new JScrollPane(inputTextArea), BorderLayout.CENTER);

        JPanel buttonPanel = new JPanel(new FlowLayout(FlowLayout.CENTER, 10, 10));
        buttonPanel.add(browseButton);
        buttonPanel.add(countButton);

        inputPanel.add(buttonPanel, BorderLayout.SOUTH);

        // Add action listeners
        browseButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                int result = fileChooser.showOpenDialog(WordCounter.this);
                if (result == JFileChooser.APPROVE_OPTION) {
                    File selectedFile = fileChooser.getSelectedFile();
                    processFile(selectedFile);
                }
            }
        });

        countButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                String inputText = inputTextArea.getText();
                if (!inputText.isEmpty()) {
                    processText(inputText);
                } else {
                    JOptionPane.showMessageDialog(WordCounter.this, "Please enter text or select a file.", "Warning", JOptionPane.WARNING_MESSAGE);
                }
            }
        });

        // Main layout
        add(instructionLabel, BorderLayout.NORTH);
        add(inputPanel, BorderLayout.CENTER);
        add(new JScrollPane(resultTextArea), BorderLayout.SOUTH);

        // Set frame visible
        setVisible(true);
    }

    private void processFile(File file) {
        StringBuilder fileContent = new StringBuilder();
        try (Scanner scanner = new Scanner(file)) {
            while (scanner.hasNextLine()) {
                fileContent.append(scanner.nextLine()).append("\n");
            }
            inputTextArea.setText(fileContent.toString());
            processText(fileContent.toString());
        } catch (Exception e) {
            e.printStackTrace();
            JOptionPane.showMessageDialog(this, "Error reading the file.", "Error", JOptionPane.ERROR_MESSAGE);
        }
    }

    private void processText(String text) {
        int vowels = 0, consonants = 0, lines = 0, words = 0, digits = 0, specialChars = 0;

        Scanner scanner = new Scanner(text);
        while (scanner.hasNextLine()) {
            String line = scanner.nextLine();
            lines++;

            for (char ch : line.toCharArray()) {
                if (Character.isLetter(ch)) {
                    if ("AEIOUaeiou".indexOf(ch) != -1) {
                        vowels++;
                    } else {
                        consonants++;
                    }
                } else if (Character.isDigit(ch)) {
                    digits++;
                } else if (!Character.isWhitespace(ch)) {
                    specialChars++;
                }
            }

            words += new StringTokenizer(line).countTokens();
        }

        // Display the results in the result text area
        resultTextArea.setText("Lines: " + lines + "\n");
        resultTextArea.append("Words: " + words + "\n");
        resultTextArea.append("Vowels: " + vowels + "\n");
        resultTextArea.append("Consonants: " + consonants + "\n");
        resultTextArea.append("Digits: " + digits + "\n");
        resultTextArea.append("Special Characters: " + specialChars + "\n");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new WordCounter();
            }
        });
    }
}
