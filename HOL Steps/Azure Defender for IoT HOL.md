# Internet of Things - Azure Defender for IoT  HOL

# ***WORK IN PROGRESS, NOT TO SHARE***

1) Azure Digital Twins, theory, deck presented avialable at **pdf files** folder.

Before Starting this Lab make sure you complete the steps specified in **Azure Digital Twins BHOL.md** File.

## Architecture Diagram ## 

## **Content:** ##
- [Exercise #1: Enabling Defender](#Exercise-1-Enabling-Defender)
  - [Task 1: Enabling Azure Defender for IoT](#Task-1-Enabling-Azure-Defender-for-fIoT)
  


## **Exercise #1:** Enabling Defender##

### **Task 1: Enabling Azure Defender for IoT:**

[In Azure Portal](#https://ms.portal.azure.com/) open **Security Center**, on the left panel under **Cloud Security** select **Azure Defender**

  ![Security Center](./images/security-center.png 'Security Center')

Next, select **IoT Security** under **Advanced Protection** section as shown below:

   ![IoT security Access](./images/iot-security.png 'IoT security Access')

Next in the **Getting Started** section, select **Oboard Subscription**


Before selecting your subscription make sure you select the option to **+Start Trial** as shown below:

   ![Trial Selection](./images/trial-selection.png 'Trial Selection')

Then, select your subscription and keep the devices selection to 1000, that is the minimum amout of devices configuration. These devices represents all those equipments/sensors connected to your network, this configuration allows you for a 30 days trial for free. Select **Evaluate** to continue.



### **Task 2: Setting up sensors:**



 2. After creation go to the resource group you just created, in the Overview panel, you will see at the top **+ Create**, click there and type **IoT Hub** in the search box, then clikc **Create**.

 3. In the next screen you will ask to fill the **Basics** tab

 - **Subscription**: Select the Subscription you are woking on.
 - **Resource Group**: Should be the resource group created in previous step.
 - **IoT Hub Name**: adt4iothub+SUFFIX
 - **Region**: East US


  ![IoT Hub Create](./images/iot-hub-create.png 'IoT Hub Create')
 


 Next, click on **Management** tab and make sure it is selected **S1:Standard Tier** in the **Pricing and scale tier** section.

 Last, clikc **Review + create**, once validation is completed, click **Create**


### **Task 3 - Onboarding sensors** ###

For the hands-on lab we will wrok with two type of sensors, one offline and one online connectected to Azure. In the next steps we will create both of them.


1. Go back to Azure Defender for IoT to create the sensors. You can go back through **Security Center**, **Cloud Security**, **Defender** then in the right side, under **Advanced Protection**, click on **IoT Security**

2. In the **Getting Started** section, select **Sensor**, then pick the **10.3.1 (Stable) and above - Recommended** version, and click **Download**.

![Onboard sensor](./images/onboard-sensor.png 'Onboard Sensor')

Fill the contact info window and then wait for a few minutes to complete the download.

3. Next go to **Sites and Sensors** and click on **+ Onboard sensor**

![Onboard sensor](./images/sensor.png 'Onboard Sensor')


In this step we will set up the offline sensor. 

4. then assigned a name to the sensor **myofflinesensor**, select your subscription and make sure you toogle **Cloud Connected** once you disable this option the rest of the form below will dissapear. Click **Register**




5. In the next step, click on **Download activation file** the activation zip and click **Finish**

 ![Activation Offline sensor](./images/downaload-offline-activation.png 'ActivationOffline Sensor')

6. You should see your sensor onboarded, locally managed, in your list of sensors as shown below.

![Sensor Onboarded](./images/sensor-onboarded.png 'Sensor Oonboarded')

7. Now, we will create another sensor, in this case we will be the online sensor. Click on **+ Onboard sensor**, in the next screen input the following information:
  - **Sensor name**: myonlinesensor
  - **Subscription**: Select the subscription you are using for this lab.
  - **Cloud Connected**: Enabled
  - **Automatic Threat Intelligence Updates**: Enable
  
  **Site** Section
  - **Hub**: Select the IoT Hub created in previous step.
  - **Display Name**:AD4IoTHub

  
  ![Onboard Online Sensor](./images/onboard-online-sensor.png 'Onboard Online Sensor')
 
 8. Click **Register**
 9. In the next step **Download activation file** and click **Finish**
 10. At this point if you check again your **Sites and sensors** section you should see both sensors onboarded.


## **Exercise #2:** Setting up your offline sensor.##

During this exercise we will set up the Virtual Machine created before with Azure Defender. 

### **Task 1: Set up Virtual Machine**

1. Connect to the Virtual machine created, using RDP or Bastion.

2.  Open HyperV, select **New** on the left side will open multiple options, select **Virtual Machine**

 ![Onboard Online Sensor](./images/hyperv-create-vm.png 'Onboard Online Sensor')

3. In the first tab, assign a name **ad4iotsensoroffline**, then click **Next**

4. The next tab **Specify Generation**, select **Generation 1**, click **Next** again.

5. Then change the memory to **2024MB**, **Next** again.

6. **Configure Network** tab, select in **Connection**, **Default Switch**, **Next** again.

7. **Connect Virtual Hard Disk** tab, only modify the **Size** to 80GB as shown below, click **Next**.

 ![Disk Size](./images/disk-size.png 'Disk Size')

8.  In the **Connect Virtual Hard Disk** section, select **Install operating system from a bootable CD/DVD-ROM** option, then click in **Image file .(iso):** browse to the Download folder where you have the iso file downloaded from the Storage Explorer. Clikc **Next** and then **Finish**

![Disk Size](./images/select-iso.png 'Disk Size')


9. Now you have the Virtual Machine available and Off. right click on the VM, select **Settings**

10. Select **Network Adapter** and click **Add**. The select **Default Switch**, **Apply** and **Ok**

![Network Adapter](./images/network-adapter.png 'Network Adapter')

12. Select **Processor** section in hte left panel, and assign **2** to **Number of virtual processors**, select **Apply** and **Ok**.

13. Back to the VM, right click to **Start**, then right click again to **Connect**

14. When you connect to the VM after a few minutes of running the system installation, you should see the following configuration next

 ![Connect to  Sensor](./images/connect-to-sensor.png 'Connect to Sensor')
### **Task 2: Collect Information**

Before setting up Azure Defender is important you take a prtscrn of the Virtual Machine IP so both can communicate to each other, we are going to use this info to set up Defender.


1. Login to the Windows Virtual Machine where you are hosting the Ubuntu VM with Defender.
2. In the search box next to the windows logo, type **cmd** this should open a command window, type **ipconfig**, take a prtscrn, we will use this parameters to configure defender

![Network Properties](./images/network-properties.png 'Netowrk Properties')

Keep this screen open or take a prtscrn.

We will map this values in the next Task.

  
 ### **Task 3: Configure Azure Defender**

During this task we will configure Azure Defender, 

1. Press **Enter** for English.

2. Select the third option (Office 4CPUs)and press **Enter**


  ![Setting up  Sensor](./images/setting-up-sensor-version.png 'Setting up Sensor')


3. You will ask to fulfill some parameters, it is **VERY IMPORTANT** you pay attention to the previous task because you will use the network information you captured before, this is unique to each Virtual Machine. So the following is an **EXAMPLE** based on the prtscrn presented above.


- **configure hardware profile**: **Office**, then press enter. 
- **Configure network interface**, type **eth0**
- **Configure management network interface**: this is an example **172.25.224.2**, you will use the **Ipv4 Address** from the previous task **+1 or -1** NOT THE SAME. Click Enter to continue
- **Subnets mask**: **255.255.240.0** this will be the SAME as the **Subnet Mask** captured in previous task.
- **Configure DNS**: **8.8.8.8**
- **Configure default gateway IP Address**: This value will be the sam as **Default Gateway** captured in previous task, in this example will be 10.4.0.1
- **Configure input interface(s)**: **eth1**
- **Configure bridge interface**: Just press Enter
- Then type **Y** and click **Enter**.

Now the installation we run for 10-15minutes.

***Note: Once the installation is complete, you will be able to access Azure Defender Console, check if you can open a cmd window, ping the Ip Adrress  you enter in the step 'Configure management network interface'
If the request timeout, you will need to reconfigure this step again, for that review the IPs one more time and use the command below to start over:***

```powershell
sudo cyberx-xsense-network-reconfigure 
```

Below, a ***sample*** screen, your parameters will be different.

 ![Setting up  Sensor](./images/defender-config.png 'Setting up Sensor')

</br>

4. ***IMPORTANT STEP!!!*** Once the installation is complete, you will have the login information availabe in the screen **TAKE THE PRTSCRN!!** before continuing, press **Enter**. Now you will have the support account, again in the screen **TAKE THE PRTSCRN!!** press **Enter** to continue.

</br>


![Setting up  Sensor](./images/login-info.png 'Setting up Sensor')

5. Open a brower, type the Ip you use for the this step above **Configure management network interface**: this example was **172.25.224.2**, you should be able to login to Azure Defender 


![Defender Login](./images/defender-login-page.png 'Defender Login')

</br>

6. Login with the credentials provided in step **4**
7. Next, you will be ask to activate the product, click **Upload**, then **Browse Files**, in your dowloads folder select the file you downloaded from the Storage Explorer, in this example **myofflinesensor.zip**

![Defender Login](./images/activation.png 'Defender Login')

8. Click **Aprove these terms and Conditions**, then **Activate**.

9. You will be prompted to select **SSL/TLS Certificates | Onboarding 1/2** for this lab will use the second option **Use a locally generated self signed certificate(..)**. Then click **I CONFIRM**, **Next**.

![Certificate selection](./images/Certificate.png 'Certificate selection')
 
 10. For this lab in the next step we will **Disable** the system wide validation. **Finish**

 11. Let's analyze together what information we already have available before moving forward.



## **Exercise 4: Clean Up**

### **Task 1: Delete resources**
When you're done using the virtual network and VM, delete the resource group and all of the resources it contains:

Search for and select myResourceGroup.

Select Delete resource group.

Enter myResourceGroup for TYPE THE RESOURCE GROUP NAME and select Delete.