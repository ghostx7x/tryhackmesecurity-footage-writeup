## Challenge Description

**Title:** Security Footage  
**Category:** Forensics / Network  
**Difficulty:** Medium


> Someone broke into our office last night, but they destroyed the hard drives with the security footage. Can you recover the footage?

In this challenge, we are given a `.pcap` file that appears to contain HTTP traffic. Our goal is to extract and recover any image that might contain the security footage.

## Tools Used
- Wireshark
- Foremost


## Summary of Steps
1. Opened the `.pcap` file in Wireshark.
"Make sure your terminal is in the same directory as the .pcap file."

![image](https://github.com/user-attachments/assets/b0c87be3-2c37-4c2f-9bd7-ebe22efde968)

2.🧑‍💻 Checking the TCP Stream

Once we inspected the TCP stream, we noticed key indicators that helped confirm the file type. Here's how you can check it:

   **Inspect the TCP Stream:**
   - In Wireshark, right-click on any packet that is part of the conversation and select **Follow > TCP Stream** | or Ctrl+Alt+Shift+T
   - ![Screenshot 2025-05-10 112646](https://github.com/user-attachments/assets/f50d0e21-1f70-4e19-8d5c-0b8f29cfc9f5)
   - This will allow you to see the entire HTTP exchange and its content.

3. **Look for Image Indicators:**
   - In the stream, you’ll see headers like `Content-Type: image/jpeg` and `Content-Length`, which will confirm the file type as JPEG.

   ![Screenshot 2025-05-10 112843](https://github.com/user-attachments/assets/d2b9999d-c077-452f-8991-f84ee54a21b9)


4. **Check the Raw Data**
After inspecting the TCP stream, the next step is to check the raw data for further confirmation of the file type. Here's how to do it:

"After opening the TCP Stream, locate the Show data as option at the bottom of the window.
By default, it will be set to ASCII.
Change it to Raw to view the raw (binary) data instead of text."

-Inspect the Raw Data:

Once you're viewing the TCP stream in Wireshark, scroll through the raw data. You’ll see hexadecimal values that represent the content of the file.

-Look for File Signatures:

In the raw data, look for specific file signatures. For example, in this case, the file starts with 47 46, which indicates that the file is a GIF image.

![image](https://github.com/user-attachments/assets/e3eb0b32-92a6-463b-af29-a36d85ab0451)


Applying the Filter:

After confirming the file type, we proceed to apply a more specific filter to focus on the relevant packets. We used the filter:

** tcp contains "jpeg" ** 

This filter searches for packets that contain the word "jpeg", which is typically part of the HTTP headers when dealing with JPEG images. By using this filter, we narrow down the traffic to only the packets that are related to the JPEG image, making it easier to locate and extract the file.


![Screenshot 2025-05-10 120718](https://github.com/user-attachments/assets/66a0efe9-bd02-4f1f-9075-d97d829ed9b7)

This also indicates that there are multiple images within the file, as several packets contain the word "jpeg", suggesting the presence of multiple image parts or frames.

6. **Using Foremost to Extract Images:**

Instead of manually saving each image one by one from the TCP stream, we decided to use **Foremost**, a tool designed to extract files like images from raw data files. 

This tool automatically identifies and extracts various types of files based on their headers.

We ran **Foremost** on the `.pcap` file, and it efficiently extracted all the images present in the traffic. 

This tool saved us time and allowed us to quickly recover all the images embedded in the captured data without having to manually extract each one.

** Here is how to use the Tool **

1. Install Foremost:
   - If you haven't installed Foremost yet, you can install it using the following command:
    
      ```bash
     sudo apt install foremost
     ```
      
![image](https://github.com/user-attachments/assets/0a928d38-a692-4c89-9c1a-e4772b0007aa)

     

2. Run Foremost on the `.pcap` file:
   - To extract files from the `.pcap` file, use the following command:
     
     ```bash
     foremost -i security-footage-1648933966395.pcap -o results_folder
     ```

     ![image](https://github.com/user-attachments/assets/c3c5e19e-66f5-4445-9f21-dae01d3b2c99)


3. Check the output folder:
   - After running the command, I successfully extracted a `.jpg` folder which contains the images of the flags.
     
   - ![Screenshot 2025-05-10 122316](https://github.com/user-attachments/assets/6511417e-8e3a-4595-81df-17a89444b405)
     

- inside jpg folder :

-    ![Screenshot 2025-05-10 122459](https://github.com/user-attachments/assets/b516f56e-440d-463f-ac9d-d5c0999308a4)

-  **Holds to View as Animated Image:**
- Click on the first image and hold down the right arrow key➡️. this will make it appear as if it's an animated image.



🙏Thanks for reading my write ups🙏

