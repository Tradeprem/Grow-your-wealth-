import java.io.IOException;
import java.io.OutputStreamWriter;
import java.net.HttpURLConnection;
import java.net.URL;
import java.net.URLEncoder;
import java.util.Scanner;

public class FormSubmitter {
    public static void main(String[] args) throws IOException {
        System.out.println("Get Started!");

        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.print("Enter your email: ");
        String email = scanner.nextLine();

        System.out.print("Enter your phone number: ");
        String phone = scanner.nextLine();

        System.out.print("Enter your password: ");
        String password = scanner.nextLine();

        // Replace 'https://your-website-url/submit-form' with the actual URL of your form submission endpoint
        String urlString = "https://your-website-url/submit-form";

        // Construct the POST data
        String postData = "name=" + URLEncoder.encode(name, "UTF-8") +
                "&email=" + URLEncoder.encode(email, "UTF-8") +
                "&phone=" + URLEncoder.encode(phone, "UTF-8") +
                "&password=" + URLEncoder.encode(password, "UTF-8");

        // Create the HTTP connection
        URL url = new URL(urlString);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setDoOutput(true);
        conn.setRequestMethod("POST");
        conn.setRequestProperty("Content-Type", "application/x-www-form-urlencoded");
        conn.setRequestProperty("Content-Length", Integer.toString(postData.length()));

        // Send the POST data
        OutputStreamWriter writer = new OutputStreamWriter(conn.getOutputStream());
        writer.write(postData);
        writer.flush();

        // Read the response
        int responseCode = conn.getResponseCode();
        System.out.println("Response Code: " + responseCode);

        // Handle the response as needed
        if (responseCode == 200) {
            System.out.println("Form submitted successfully!");
            // You can add code to open the website here, if desired
            // For example, using a web browser automation library like Selenium
        } else {
            System.out.println("Form submission failed.");
        }

        writer.close();
        conn.disconnect();
    }
}
