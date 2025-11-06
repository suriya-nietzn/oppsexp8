import java.io.BufferedReader; import java.io.BufferedWriter; import java.io.FileReader; import java.io.FileWriter; import java.io.IOException; import java.io.FileNotFoundException; 
 
public class ProcessTransactions { 
private static final String INPUT_FILE = "transactions.txt"; private static final String OUTPUT_FILE = "summary.txt"; 
 
    public static void main(String[] args) {         if (createTransactionFile()) {             processTransactions(); 
        } else { 
            System.err.println("Aborting due to error creating transaction file."); 
        } 
    } 
 
    private static boolean createTransactionFile() { 
        System.out.println("Step 1: Creating '" + INPUT_FILE + "'...");         try (BufferedWriter writer = new BufferedWriter(new FileWriter(INPUT_FILE))) {             writer.write("TXN1001|DEPOSIT|5000|SUCCESS"); 
            writer.newLine();             writer.write("TXN1002|DEPOSIT|6000|FAILED"); 
            writer.newLine(); 
            writer.write("TXN1003|WITHDRAW|2000|SUCCESS"); 
            writer.newLine();            writer.write("TXN1004|DEPOSIT|3500|SUCCESS"); 
           writer.newLine(); 
           writer.write("TXN1005|WITHDRAW|1000|FAILED"); 
    writer.newLine();     writer.write("TXN1006|DEPOSIT|7200|SUCCESS");     writer.newLine();             writer.write("TXN1007|WITHDRAW|500|SUCCESS"); 
            writer.newLine();             writer.write("TXN1008|DEPOSIT|2100|SUCCESS"); 
            writer.newLine();             writer.write("TXN1009|DEPOSIT|800|FAILED"); 
            writer.newLine(); 
            writer.write("TXN1010|WITHDRAW|1500|SUCCESS"); 
 
            System.out.println("'" + INPUT_FILE + "' created successfully."); 
            return true; 
 
        } catch (IOException e) { 
            System.err.println("ERROR creating " + INPUT_FILE + ": " + e.getMessage()); 
            return false; 
        } 
    } 
 
    private static void processTransactions() {        int successfulCount = 0;        int failedCount = 0; 
try (BufferedReader reader = new BufferedReader(new FileReader(INPUT_FILE))) { 
    String line; 
    System.out.println("\nStep 2: Reading and processing '" + INPUT_FILE + "'..."); 
 
            while ((line = reader.readLine()) != null) {                 if (line.endsWith("SUCCESS")) {                     successfulCount++; 
                } else if (line.endsWith("FAILED")) {                     failedCount++; 
                } 
            } 
            System.out.println("Processing complete."); 
 
        } catch (FileNotFoundException e) { 
            System.err.println("ERROR: File not found: " + INPUT_FILE); 
            return; 
        } catch (IOException e) { 
            System.err.println("ERROR: Could not read file: " + e.getMessage()); 
            return; 
        } 
 
       try (BufferedWriter writer = new BufferedWriter(new FileWriter(OUTPUT_FILE))) {            writer.write("--- Transaction Summary Report ---");            writer.newLine(); 
    writer.write("Total Successful Transactions: " + successfulCount);     writer.newLine();     writer.write("Total Failed Transactions: " + failedCount); 
 
            System.out.println("\nStep 3: Summary report successfully written to '" + OUTPUT_FILE + 
"'."); 
 
        } catch (IOException e) { 
            System.err.println("ERROR: Could not write summary file: " + e.getMessage()); 
        } 
    } 
} 
