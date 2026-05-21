import java.util.Scanner;

class FileData {
    private String fileName;
    private String content;

    // Constructor
    FileData(String fileName, String content) {
        this.fileName = fileName;
        this.content = content;
    }

    // Method to compress file
    public String compress() {
        String compressed = "";

        for (int i = 0; i < content.length(); i++) {
            char ch = content.charAt(i);
            int count = 1;

            while (i < content.length() - 1 &&
                   content.charAt(i) == content.charAt(i + 1)) {
                count++;
                i++;
            }

            compressed += ch + "" + count;
        }

        return compressed;
    }

    // Method to decompress file
    public String decompress(String compressed) {
        String decompressed = "";

        for (int i = 0; i < compressed.length(); i += 2) {
            char ch = compressed.charAt(i);
            int count = Character.getNumericValue(compressed.charAt(i + 1));

            for (int j = 0; j < count; j++) {
                decompressed += ch;
            }
        }

        return decompressed;
    }

    // Display File Info
    public void display() {
        System.out.println("File Name : " + fileName);
        System.out.println("Original Content : " + content);
    }
}

public class FileCompressionSimulator {

    public static void main(String[] args) {

        Scanner sc = new Scanner(System.in);

        System.out.println("===== File Compression Simulator =====");

        System.out.print("Enter File Name : ");
        String fileName = sc.nextLine();

        System.out.print("Enter File Content : ");
        String content = sc.nextLine();

        FileData file = new FileData(fileName, content);

        int choice;

        do {
            System.out.println("\n===== MENU =====");
            System.out.println("1. Display File");
            System.out.println("2. Compress File");
            System.out.println("3. Decompress File");
            System.out.println("4. Exit");

            System.out.print("Enter your choice : ");
            choice = sc.nextInt();

            switch (choice) {

                case 1:
                    file.display();
                    break;

                case 2:
                    String compressed = file.compress();
                    System.out.println("Compressed Data : " + compressed);
                    break;

                case 3:
                    String compressedData = file.compress();
                    String decompressed = file.decompress(compressedData);

                    System.out.println("Compressed Data : " + compressedData);
                    System.out.println("Decompressed Data : " + decompressed);
                    break;

                case 4:
                    System.out.println("Exiting Program...");
                    break;

                default:
                    System.out.println("Invalid Choice!");
            }

        } while (choice != 4);

        sc.close();
    }
}
