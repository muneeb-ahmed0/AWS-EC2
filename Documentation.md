# **Deploy a basic HTML/CSS Website on AWS EC2 Using Apache**

### **Step 1: Launch an Ubuntu EC2 Instance**

1. **Log in to the AWS Console** and navigate to the EC2 Dashboard.
    
2. **Launch an Instance:**
    
    - **AMI:** Select **Ubuntu Server 24.04 LTS**.
    - **Instance Type:** `t2.micro` (Free Tier Eligible).
    - **Key Pair:** Create or use an existing key pair.
    - **Security Group:**
        - Allow **HTTP (Port 80)** from 0.0.0.0/0.
        - Allow **SSH (Port 22)** from your IP. 
3. **Launch the Instance.**

![[1 launch.png]]
![[2-AMI.png]]

![[3-Instance type.png]]

![[4-Network.png]]

![[5-Ports.png]]

![[6-storage.png]]



---

### **Step 2: Connect to the EC2 Instance**

1. **Use SSH to connect:**
    
    ```bash
    ssh -i "your-key-file.pem" ubuntu@<INSTANCE_PUBLIC_IP>
    ```

![[7-Connect.png]]

![[8-ssh.png]]



1. **Update the System:**
    
    ```bash
    sudo apt update
    sudo apt upgrade -y
    ```
    

	![[9-update 1.png]]
	![[10-upgrade 1.png]]
	

---

### **Step 3: Install Apache Web Server**

1. **Install Apache:**
    
    ```bash
    sudo apt install apache2 -y
    ```
	
	![[11-install apache.png]]
	
	 
2. **Start and Enable Apache:**
	
    ```bash
    sudo systemctl start apache2
    sudo systemctl enable apache2
    ```
	 ![[12-start&enable.png]]
	 
	
3. **Verify Apache:**
    
    - Open a browser and visit:
        
        ```
        http://<INSTANCE_PUBLIC_IP>
        ```
        
    - You should see the Apache default page.
    ![[13-apache.png]]
    

---

### **Step 4: Create the HTML/CSS Web Page**

1. **Write the HTML File:**
    
    - Create a new file:
        
        ```bash
        sudo vi /var/www/html/index.html
        ```
		 ![[14-vi 2.png]]
		
	- Add the following content:
        
        ```html
       <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test Webpage</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <h1>Welcome to My Test Website!</h1>
        <p>This is a simple webpage to test your Apache server.</p>
        <p>Enjoy testing!</p>
    </div>
</body>
</html>

        ```
		 
		 ![[15-vi.png]]
	
2. **Save the File:**
    
    - Press `:`, then `X` to save and exit.
    

---

### **Step 5: Test the Web Page**

1. Open your browser and visit:
    
    ```
    http://<INSTANCE_PUBLIC_IP>
    ```
    
2. You should see the webpage with the following:
    
    - A header with the title "Welcome to My Test Website!."
    - A main section with the message:
	     This is a simple webpage to test your Apache server.
	     Enjoy testing!
         ![[16-website.png]]

---

### **Step 6: Secure and Clean Up**

1. **Restrict SSH Access:**
    - Update the security group to allow SSH only from your IP.
2. **Clean Up Files (Optional):**
    - Remove unnecessary default files in `/var/www/html`:
        
        ```bash
        sudo rm /var/www/html/index.html.bak
        ```
        


