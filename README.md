# CMPE283Assignment3

## Steps to reproduces the development steps:

1. Assignment is done by me

2. Please find the steps to recreate the development steps:

● Create a free tier account in the Google Cloud Platform to make use of the services.

● Create a VM through UI or fill in the information like Name, InstanceId, Zone, machine type, and CPU Platform and click on the Equivalent command line button (present at the bottom of the page), cloud shell will open with the information filled similar to the screenshot below. Below are the details that were chosen for this assignment:

Name: instance1

Zone: us-central1-b

Machine Type: n2-standard-8

CPU Platform: Intel Cascade Lake

Boot disk : 100GB

● Add extra capabilities as per the requirement, here add enable nested virtualization before creating the instance.

<img width="1440" alt="Screenshot 2022-12-11 at 10 08 10 AM" src="https://user-images.githubusercontent.com/111544172/206932137-8a22fcf9-9a11-43c2-a766-3b35ee389ad3.png">


● Click on the SSH on the newly created instance like below:

<img width="1440" alt="Screenshot 2022-12-11 at 10 08 40 AM" src="https://user-images.githubusercontent.com/111544172/206932252-7692822d-add5-4f23-a552-7e18a4808d05.png">


● To check the configuration use the command - 'df -h'

<img width="897" alt="Screenshot 2022-12-04 at 2 17 05 AM" src="https://user-images.githubusercontent.com/111544172/205786819-c64cc9b0-1b69-4618-bb28-2456f34b316e.png">


● generate the public key by using the command 'ssh-keygen' and get the public key and add in the github account where linux code has been forked.

<img width="892" alt="Screenshot 2022-12-04 at 2 56 36 AM" src="https://user-images.githubusercontent.com/111544172/205809044-5259752b-7c5e-4b22-b5f3-43e36657a75d.png">

● Clone the linux repository here:

<img width="892" alt="Screenshot 2022-12-04 at 3 30 21 AM" src="https://user-images.githubusercontent.com/111544172/205817094-0ef2b578-c1b1-44a5-949b-e647b3902997.png">

● Copy the config file in the directory from /boot and install make

<img width="899" alt="Screenshot 2022-12-04 at 2 11 38 PM" src="https://user-images.githubusercontent.com/111544172/205819815-99e5f9f1-dfa4-4b78-a053-684b92c202d4.png">

<img width="892" alt="Screenshot 2022-12-04 at 4 20 31 AM" src="https://user-images.githubusercontent.com/111544172/205817465-356bb6f1-ff04-42ce-9eea-f8138ee27c13.png">

● Install all the necessary dependencies:

<img width="892" alt="Screenshot 2022-12-04 at 4 28 32 AM" src="https://user-images.githubusercontent.com/111544172/205819102-89fc1234-08d4-410c-88a2-a53ca783b987.png">


● Excecute the commands make menuconfig and make oldconfig:

<img width="900" alt="Screenshot 2022-12-04 at 6 37 13 PM" src="https://user-images.githubusercontent.com/111544172/205820575-1a19903f-8f1f-49fb-8909-cafa5819fe8e.png">


● To avoid getting error while running make modules make the below changes to config :

scripts/config --disable SYSTEM_TRUSTED_KEYS <br/>
scripts/config --disable SYSTEM_REVOCATION_KEYS<br/>

<img width="900" alt="Screenshot 2022-12-04 at 7 26 39 PM" src="https://user-images.githubusercontent.com/111544172/205821070-2886a9a3-4fba-413a-a865-a79a57cf6c51.png">

● Run the command '  make -j <your-vm-cpu-total-core-number> modules' to build the modules -> make -j 8 modules in our case
  
  <img width="900" alt="Screenshot 2022-12-04 at 8 07 32 PM" src="https://user-images.githubusercontent.com/111544172/205821550-829d714b-b232-4c0e-94ca-df318f6113b1.png">

  <img width="900" alt="Screenshot 2022-12-04 at 8 08 22 PM" src="https://user-images.githubusercontent.com/111544172/205821589-9bd8fe96-6228-423e-9488-533100f1c4e0.png">

  to avoid the error change the config file with the below change:
  
  <img width="900" alt="Screenshot 2022-12-04 at 8 19 32 PM" src="https://user-images.githubusercontent.com/111544172/205821835-e95b3334-ba11-4ea9-b17a-e1040177f7f5.png">

  ● Now run 'make -j 8'
  
  <img width="900" alt="Screenshot 2022-12-04 at 8 21 43 PM" src="https://user-images.githubusercontent.com/111544172/205821932-f963f278-1151-41b7-812f-4249cfe7441a.png">

  ● Run the coomand 'make -j 8' and then 'sudo make -j <your-vm-cpu-total-core-number> INSTALL_MOD_STRIP=1 modules_install' and then run 'make install'
  
  <img width="900" alt="Screenshot 2022-12-04 at 8 32 08 PM" src="https://user-images.githubusercontent.com/111544172/205822535-5dcce9c2-3843-407c-a5fe-146ae54595c9.png">

  <img width="900" alt="Screenshot 2022-12-04 at 8 33 55 PM" src="https://user-images.githubusercontent.com/111544172/205822654-ac7cc3a2-8094-4dea-8dac-2ef3cdafb406.png">

  And our linux kernal is built now.
  
  ● Reboot the VM  and connect back and give the command 
  
  <img width="900" alt="Screenshot 2022-12-04 at 8 38 53 PM" src="https://user-images.githubusercontent.com/111544172/205822909-dfebed1c-0ff7-40f1-987d-82fa3757092d.png">

  ● Now that linux kernal is built to make the necessary changes for assignment redirect to the directory as follows:
  
  <img width="889" alt="Screenshot 2022-12-04 at 10 28 29 PM" src="https://user-images.githubusercontent.com/111544172/205823150-11cc5ef5-541c-469a-8b3a-5bbb0bbbb6f4.png">

  ● Once after making necessary changes to the code in cpuid.c and vmx.c, install the modules agaim
  
  <img width="963" alt="Screenshot 2022-12-05 at 12 43 17 AM" src="https://user-images.githubusercontent.com/111544172/205824403-ebe928c5-80c4-4365-9392-dd4f3ae767ab.png">

  ● Run the following commands after building the modules:
  
    sudo rmmod kvm_intel
    sudo rmmod kvm
    sudo modprode kvm
    sudo modprobe kvm_intel
  
  
  ●  To test , we have to create an inner VM that can be done as follows:
  
  Download the cloud image and give the command -  wget https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img 
  
  and install all the necessary packages
    ●  sudo apt update && sudo apt install qemu-kvm -y
    ●  sudo apt-get install cloud-image-utils
  
  ●  Create the user data and pass it as input to create the ubuntu instance
    cat >user-data <<EOF
    #cloud-config
    password: NewGCP - ( Enter any password to set )
    chpasswd: { expire: False }
    ssh_pwauth: True
    EOF
  
    ●  And execute the img as follows:
    
  <img width="1440" alt="Screenshot 2022-12-05 at 5 54 28 PM" src="https://user-images.githubusercontent.com/111544172/205835119-9cbe0671-dc13-4d30-afe2-4b5d25d50da3.png">

    ●  Ubuntu login would be prompted and enter the password that was set before:
  
  <img width="1440" alt="Screenshot 2022-12-05 at 5 59 26 PM" src="https://user-images.githubusercontent.com/111544172/205835378-fc2ca1bc-ea86-4c77-9b0d-6a1784998eec.png">

    ●  Now install the cpuid package :
        
      sudo apt-get update
      sudo apt-get install cpuid


    ● Open a new ternminal from the instance and keep the ubuntu terminal handy to test the cpuid leaf nodes
  
      In terminal where is ubuntu is installed create the following test script with filename="testing_cpuid.sh")
  
      #!/bin/bash

      for i in {0..76}
      do
          echo "EXIT $i"
          cpuid -l $1 -s $i
      done
    
     ● To test the functionality for %eax=0x4ffffffe run the command --> bash testing_cpuid.sh -0x4ffffffe in the terminal where ubuntu is installed.
     
<img width="1440" alt="Screenshot 2022-12-11 at 12 26 46 PM" src="https://user-images.githubusercontent.com/111544172/206938782-d37b5d75-32bf-421b-aca4-48e0a059528f.png">

 <img width="1440" alt="Screenshot 2022-12-11 at 12 26 53 PM" src="https://user-images.githubusercontent.com/111544172/206938799-a3ef2e27-2f5d-42c6-adfe-d0e009acda02.png">

 <img width="1440" alt="Screenshot 2022-12-11 at 12 27 07 PM" src="https://user-images.githubusercontent.com/111544172/206938842-e16cdaab-75cc-4bfb-ad39-fc27711a0e5d.png">
     
<img width="1440" alt="Screenshot 2022-12-11 at 12 27 14 PM" src="https://user-images.githubusercontent.com/111544172/206938856-fd892154-604a-4c14-ba49-c8330a446716.png">

<img width="1440" alt="Screenshot 2022-12-11 at 12 27 20 PM" src="https://user-images.githubusercontent.com/111544172/206938865-74e1314e-e2fa-464c-a9db-2f5ae26907ad.png">

     ● In new terminal - run the command --> sudo dmesg
     
<img width="1440" alt="Screenshot 2022-12-11 at 12 28 11 PM" src="https://user-images.githubusercontent.com/111544172/206939318-f204dc65-39ac-44f8-b4af-f557a7f4b1ef.png">

<img width="1440" alt="Screenshot 2022-12-11 at 12 28 19 PM" src="https://user-images.githubusercontent.com/111544172/206939327-d82ed485-6e74-45b6-9919-df35d2bc855c.png">

<img width="1440" alt="Screenshot 2022-12-11 at 12 28 24 PM" src="https://user-images.githubusercontent.com/111544172/206939332-1937a2d8-d5e3-4c1b-b18c-f051f4ae9657.png">

 ● To test the functionality for %eax=0x4fffffff run the command --> bash testing_cpuid.sh -0x4fffffff in the terminal where ubuntu is installed.
 
 <img width="1440" alt="Screenshot 2022-12-11 at 12 29 07 PM" src="https://user-images.githubusercontent.com/111544172/206939427-46ffb3df-867c-427a-a42f-c5b4d8d352a8.png">

<img width="1440" alt="Screenshot 2022-12-11 at 12 29 15 PM" src="https://user-images.githubusercontent.com/111544172/206939434-0c51ef5a-32ce-4f39-b40e-c886a8c8fe8a.png">

<img width="1440" alt="Screenshot 2022-12-11 at 12 29 25 PM" src="https://user-images.githubusercontent.com/111544172/206939441-e14d31d3-2e2c-49f6-83b4-9606c79fb0b7.png">

<img width="1440" alt="Screenshot 2022-12-11 at 12 29 38 PM" src="https://user-images.githubusercontent.com/111544172/206939449-4aa600a1-f3ca-4585-bc09-844c0be035a2.png">



     
     
     
     
