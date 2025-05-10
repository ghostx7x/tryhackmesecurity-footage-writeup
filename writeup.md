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

![image](https://github.com/user-attachments/assets/b0c87be3-2c37-4c2f-9bd7-ebe22efde968)

2🧑‍💻 Checking the TCP Stream

Once we inspected the TCP stream, we noticed key indicators that helped confirm the file type. Here's how you can check it:

   **Inspect the TCP Stream:**
   - In Wireshark, right-click on any packet that is part of the conversation and select **Follow > TCP Stream** | or Ctrl+Alt+Shift+T
   - ![Screenshot 2025-05-10 112646](https://github.com/user-attachments/assets/f50d0e21-1f70-4e19-8d5c-0b8f29cfc9f5)
   - This will allow you to see the entire HTTP exchange and its content.

3. **Look for Image Indicators:**
   - In the stream, you’ll see headers like `Content-Type: image/jpeg` and `Content-Length`, which will confirm the file type as JPEG.

   ![Screenshot 2025-05-10 112843](https://github.com/user-attachments/assets/d2b9999d-c077-452f-8991-f84ee54a21b9)





