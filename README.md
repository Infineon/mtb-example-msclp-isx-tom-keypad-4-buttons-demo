# PSOC&trade; 4: MSCLP inductive sensing touch-over-metal keypad-4 demo

This code example demonstrates the implementation of inductive sensing based touch-over-metal (ToM) keypad buttons using SmartSense. This low-power application showcases recommended power states and transitions and the SmartSense based tuning flow for inductive sensing based buttons. This example uses the multi-sense low-power (MSCLP: fifth-generation low-power) inductive sensing technology to demonstrate different considerations to implement a low-power design.


[View this README on GitHub.](https://github.com/Infineon/mtb-example-msclp-isx-tom-keypad-4-buttons-demo)

[Provide feedback on this code example.](https://cypress.co1.qualtrics.com/jfe/form/SV_1NTns53sK2yiljn?Q_EED=eyJVbmlxdWUgRG9jIElkIjoiQ0UyNDAxNDYiLCJTcGVjIE51bWJlciI6IjAwMi00MDE0NiIsIkRvYyBUaXRsZSI6IlBTT0MmdHJhZGU7IDQ6IE1TQ0xQIEluZHVjdGl2ZSBTZW5zaW5nIFRvdWNoIG92ZXIgTWV0YWwgS2V5cGFkLTQgRGVtbyIsInJpZCI6ImphaW5zaWRoYXJ0aCIsIkRvYyB2ZXJzaW9uIjoiMi4wLjAiLCJEb2MgTGFuZ3VhZ2UiOiJFbmdsaXNoIiwiRG9jIERpdmlzaW9uIjoiTUNEIiwiRG9jIEJVIjoiSUNXIiwiRG9jIEZhbWlseSI6IlBTT0MifQ==)


## Requirements

- [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) v3.4 or later

   > **Note:** This code example version requires ModusToolbox&trade; v3.4 and is not backward compatible with v3.4 or older versions.

- Board support package (BSP) minimum required version: 3.2.0
- Programming language: C
- Associated parts: [PSOC&trade; 4000T](https://www.infineon.com/cms/en/product/microcontroller/32-bit-psoc-arm-cortex-microcontroller/psoc-4-32-bit-arm-cortex-m0-mcu/psoc-4000-entry-level/psoc-4000t)


## Supported toolchains (make variable 'TOOLCHAIN')

- GNU Arm&reg; Embedded Compiler v11.3.1 (`GCC_ARM`) – Default value of `TOOLCHAIN`
- Arm&reg; Compiler v6.22 (`ARM`)
- IAR C/C++ Compiler v9.50.2 (`IAR`)


## Supported kits (make variable 'TARGET')

- [PSOC&trade; 4000T CAPSENSE&trade; Multi-Sense Prototyping Kit](https://www.infineon.com/CY8CPROTO-040T-MS) (`CY8CPROTO-040T-MS`) - Default `TARGET`


## Hardware setup

This example uses the board's default configuration. See the [kit user guide](https://www.infineon.com/dgdl/Infineon-CY8CPROTO-040T-MS_UG-UserManual-v02_00-EN.pdf?fileId=8ac78c8c93dda25b019466a75dd07a01) to ensure that the board is configured correctly to use VDD at 3.3 V.


## Software setup

See the [ModusToolbox&trade; tools package installation guide](https://www.infineon.com/ModusToolboxInstallguide) for information about installing and configuring the tools package.

This example requires [ModusToolbox&trade; CAPSENSE&trade; and Multi-Sense Pack](https://softwaretools.infineon.com/tools/com.ifx.tb.tool.modustoolboxpackmultisense) to be installed.


## Using the code example


### Create the project

The ModusToolbox&trade; tools package provides the Project Creator  both as a GUI tool and a command line tool.

<details><summary><b>Use Project Creator GUI</b></summary>

1. Open the Project Creator GUI tool.

   There are several ways to do this, including launching it from the dashboard or from inside the Eclipse IDE. For more details, see the [Project Creator user guide](https://www.infineon.com/ModusToolboxProjectCreator) (locally available at *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/docs/project-creator.pdf*).

2. On the **Choose Board Support Package (BSP)** page, select a kit supported by this code example. See [Supported kits](#supported-kits-make-variable-target).

   > **Note:** To use this code example for a kit not listed here, you may need to update the source files. If the kit does not have the required resources, the application may not work.

3. On the **Select Application** page:

   a. Select the **Applications(s) Root Path** and the **Target IDE**.

   > **Note:** Depending on how you open the Project Creator tool, these fields may be pre-selected for you.

   b. Select this code example from the list by enabling its check box.

   > **Note:** You can narrow the list of displayed examples by typing in the filter box.

   c. (Optional) Change the suggested **New Application Name** and **New BSP Name**.

   d. Click **Create** to complete the application creation process.

</details>


<details><summary><b>Use Project Creator CLI</b></summary>

The 'project-creator-cli' tool can be used to create applications from a CLI terminal or from within batch files or shell scripts. This tool is available in the *{ModusToolbox&trade; install directory}/tools_{version}/project-creator/* directory.

Use a CLI terminal to invoke the 'project-creator-cli' tool. On Windows, use the command-line 'modus-shell' program provided in the ModusToolbox&trade; installation instead of a standard Windows command-line application. This shell provides access to all ModusToolbox&trade; tools. You can access it by typing "modus-shell" in the search box in the Windows menu. In Linux and macOS, you can use any terminal application.

The following example clones the "[mtb-example-msclp-isx-tom-keypad-4-buttons-demo](https://github.com/Infineon/mtb-example-msclp-isx-tom-keypad-4-buttons-demo)" application with the desired name "CY8CPROTO_040T_MS_demo" configured for the *CY8CPROTO-040T* BSP into the specified working directory, *C:/mtb_projects*:

   ```
   project-creator-cli --board-id CY8CPROTO-040T-MS --app-id mtb-example-msclp-isx-tom-keypad-4-buttons-demo --user-app-name CY8CPROTO_040T_MS_demo --target-dir "C:/mtb_projects"
   ```

The 'project-creator-cli' tool has the following arguments:

Argument | Description | Required/optional
---------|-------------|-----------
`--board-id` | Defined in the <id> field of the [BSP](https://github.com/Infineon?q=bsp-manifest&type=&language=&sort=) manifest | Required
`--app-id`   | Defined in the <id> field of the [CE](https://github.com/Infineon?q=ce-manifest&type=&language=&sort=) manifest | Required
`--target-dir`| Specify the directory in which the application is to be created if you prefer not to use the default current working directory | Optional
`--user-app-name`| Specify the name of the application if you prefer to have a name other than the example's default name | Optional

> **Note:** The project-creator-cli tool uses the `git clone` and `make getlibs` commands to fetch the repository and import the required libraries. For details, see the "Project creator tools" section of the [ModusToolbox&trade; tools package user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at {ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf).

</details>


### Open the project

After the project has been created, you can open it in your preferred development environment.


<details><summary><b>Eclipse IDE</b></summary>

If you opened the Project Creator tool from the included Eclipse IDE, the project will open in Eclipse automatically.

For more details, see the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_ide_user_guide.pdf*).

</details>


<details><summary><b>Visual Studio (VS) Code</b></summary>

Launch VS Code manually, and then open the generated *{project-name}.code-workspace* file located in the project directory.

For more details, see the [Visual Studio Code for ModusToolbox&trade; user guide](https://www.infineon.com/MTBVSCodeUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_vscode_user_guide.pdf*).

</details>


<details><summary><b>Keil µVision</b></summary>

Double-click the generated *{project-name}.cprj* file to launch the Keil µVision IDE.

For more details, see the [Keil µVision for ModusToolbox&trade; user guide](https://www.infineon.com/MTBuVisionUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_uvision_user_guide.pdf*).

</details>


<details><summary><b>IAR Embedded Workbench</b></summary>

Open IAR Embedded Workbench manually, and create a new project. Then select the generated *{project-name}.ipcf* file located in the project directory.

For more details, see the [IAR Embedded Workbench for ModusToolbox&trade; user guide](https://www.infineon.com/MTBIARUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mt_iar_user_guide.pdf*).

</details>


<details><summary><b>Command line</b></summary>

If you prefer to use the CLI, open the appropriate terminal, and navigate to the project directory. On Windows, use the command-line 'modus-shell' program; on Linux and macOS, you can use any terminal application. From there, you can run various `make` commands.

For more details, see the [ModusToolbox&trade; tools package user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox&trade; install directory}/docs_{version}/mtb_user_guide.pdf*).

</details>


## Operation

1. Connect the USB cable between the [CY8CPROTO-040T-MS kit](https://www.infineon.com/CY8CPROTO-040T-MS) and the PC with the keypad-4 extension board, as shown in **Figure 1**.

   **Figure 1. Connecting the CY8CPROTO-040T-MS kit with the USB cable**

   <img src="images/ms-proto-kit-kp4.png" width=""/>

2. Program the board using one of the following:

   <details><summary><b>Using Eclipse IDE</b></summary>

      1. Select the application project in the Project Explorer.

      2. In the **Quick Panel**, scroll down, and click **\<Application Name> Program (KitProg3_MiniProg4)**.
   </details>


   <details><summary><b>In other IDEs</b></summary>

   Follow the instructions in your preferred IDE.
   </details>


   <details><summary><b>Using CLI</b></summary>

     From the terminal, execute the `make program` command to build and program the application using the default toolchain to the default target. The default toolchain is specified in the application's Makefile but you can override this value manually:
      ```
      make program TOOLCHAIN=<toolchain>
      ```

      Example:
      ```
      make program TOOLCHAIN=GCC_ARM
      ```
   </details>

3. After programming, the application starts automatically.

4. Press any of the sensors with your finger; LEDs turn ON, indicating the activation of different ISX sensors as shown in **Figure 2**.

   **Figure 2. Press the CY8CPROTO-040T-MS kit with the PC**

   <img src="images/press-kp4.png" width=""/>

   **Table 1. LED states for different sensors**

   Sensor | LED indication
   :---------------------| :-----
   ISX button 1  | LED D1 turns ON
   ISX button 2  | LED D2 turns ON
   ISX button 3  | LED D3 turns ON (see note below)
   ISX button 4  | LED D4 turns ON
   
   <br>

   All LEDs will be OFF when none of the sensor buttons are pressed.
   
   > **Note:** When pressing ISX button 3, the LED D3 on the expansion board and LED3 on the control board will both turn ON because they share the same GPIO pin (P3.0).


### Monitor data using CAPSENSE&trade; Tuner

1. Open the CAPSENSE&trade; Tuner from the **Tools** section in the IDE Quick Panel.

   You can also run the CAPSENSE&trade; Tuner application standalone from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-tuner*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is located in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config* folder.

   See the [ModusToolbox&trade; user guide](https://www.infineon.com/ModusToolboxUserGuide) (locally available at *{ModusToolbox install directory}/docs_{version}/mtb_user_guide.pdf*) for options to open the CAPSENSE&trade; Tuner application using the CLI.

2. Ensure that the status LED is ON and not blinking; this indicates that the onboard KitProg3 is in CMSIS-DAP Bulk mode. See the [Firmware-loader](https://github.com/Infineon/Firmware-loader) to learn how to update the firmware and switch modes in KitProg3.

3. In the tuner application, click on the **Tuner Communication Setup** icon or select **Tools** > **Tuner Communication Setup** as shown in **Figure 3**.

   **Figure 3. Tuner communication setup**

   <img src="images/tuner-comm-setup.png" width="300" /> 

   Select I2C under KitProg3 and configure it as follows:

   - **I2C address:** 8
   - **Sub-address:** 2-Bytes
   - **Speed (kHz):** 400

   These are the same values set in the EZI2C resource as shown in **Figure 4**.

   **Figure 4. Tuner Communication Setup parameters**

   <img src="images/tuner-comm-settings.png" width="450"/>

4. Click **Connect** or select **Communication** > **Connect** to establish a connection.

   **Figure 5. Establish connection**

   <img src="images/tuner-connect.png" width="300" />

5. Click **Start** or select **Communication** > **Start** to begin data streaming from the device.

   **Figure 6. Start Tuner communication**

   <img src="images/tuner-start.png" width="300" />

   The **Widget/Sensor Parameters** tab is updated with the parameters configured in the **CAPSENSE&trade; Configurator** window. The tuner displays the data from the sensor in the **Widget View** and **Graph View** tabs.

6. Set the **Read mode** to **Synchronized mode**. Navigate to the **Widget view** tab and notice that the pressed widget is highlighted in **blue** as shown in **Figure 7**.

   **Figure 7. Widget view of the CAPSENSE&trade; Tuner**

   <img src="images/tuner-widget-view.png" width=""/>

7. Go to the **Graph View** tab to view the raw count, baseline, difference count, and status of each sensor.
To view the sensor data for the different ISX buttons, select Button0_Rx0_Lx0 under Button0 and so on, respectively (see **Figure 8**).

   **Figure 8. Graph view of the CAPSENSE&trade; Tuner for the ISX button**

   <img src="images/tuner-graph-view-intro.png" width=""/>

8. Observe that the low-power widget sensor (**LowPower0_Rx0_Lx0**) raw count is plotted after the device completes the full frame scan (or detects a press) in **WoT** mode and moves to **Active/ALR** mode.

   **Figure 9. Graph view of the CAPSENSE&trade; Tuner for the low-power widget**

   <img src="images/graph-view-wot.png" width=""/>

9. See the **Widget/Sensor parameters** section in the CAPSENSE&trade; Tuner window as shown in **Figure 7**.

10. Switch to the **SNR Measurement** tab for measuring the signal-to-noise ratio (SNR) and verify that the SNR is greater than 10:1, and the signal count is above 50; select the **Button0** widget and **Button0_Rx0_Lx0** sensor, and then click **Acquire noise** as shown in **Figure 10**.

    **Figure 10. CAPSENSE&trade; Tuner - SNR measurement: Acquire noise**

    <img src="images/tuner-acquire-noise.png" width=""/>
    
    <br>

    > **Note:** Because the scan refresh rate is lower in **ALR** and **WoT** mode, it takes more time to acquire noise. Press any of the ISX buttons on the keypad-4 expansion board before clicking **Acquire noise** to transition the device to Active mode to receive the signal faster.
    
    <br>
11. Once the noise is acquired, press the finger/force touch meter at the required position on the button and click **Acquire signal**. Ensure that the finger/force touch meter remains on the button as long as the signal acquisition is in progress. Observe that the SNR is greater than 10:1 and the signal count is above '50'.

    The calculated SNR on this button is displayed as shown in **Figure 11**. Based on the end system design, test the signal with a finger press force that matches the size and pressure of a normal use case. Also, test using lighter presses that will be rejected by the system to ensure that they do not reach the finger threshold.
   
    **Figure 11. CAPSENSE&trade; Tuner - SNR measurement: Acquire signal**

    <img src="images/tuner-acquire-signal.png" width=""/>

    **Table 2. SNR values for the regular widgets for the keypad-4 board**

    Sensor | SNR for 3N force
    :---------------------| :-----
    Button0  | 18
    Button1  | 33
    Button2  | 17
    Button3  | 17

   <br>

12. To measure the SNR of the low-power sensor (**LowPower0_Rx0_Lx0**), set the **Finger threshold** to max (65535) in **Widget/Sensor Parameters** as shown in **Figure 12** for all widgets. This is required to stop detecting a touch in low-power mode and ALR mode and to avoid state transitions to Active mode from both low-power mode and ALR mode. To perform this, set the tuning mode for the regular widgets to **SMARTSENSE - HW parameter** via the CAPSENSE&trade; Configurator temporarily (as shown in **Figure 17**) and program the device.

    Use the **Apply to Device** option to set the modified parameters to the device instantaneously. But make the final configuration using the CAPSENSE&trade; Configurator.

    **Figure 12. CAPSENSE&trade; update finger threshold**

    <img src="images/tuner-threshold-update.png" width="750"/>

    **Figure 13. Apply changes to device**

    <img src="images/tuner-apply-settings-device.png" />

    <br>

13. Repeat steps **10** and **11** to observe the SNR and signal count as shown in **Figure 14**.

    **Figure 14. CAPSENSE&trade; Tuner - SNR measurement: low-power widget**

    <img src="images/tuner-lowpower-snr.png" width=""/>


    **Table 3. SNR values for the low power widgets for the keypad-4 board**

    Sensor | SNR for 3N force
    :---------------------| :-----
    LowPower0  | 26
    LowPower1  | 29
    LowPower2  | 13
    LowPower3  | 16
   
   <br>
 


## Operation at other voltages

[CY8CPROTO-040T-MS kit](https://www.infineon.com/CY8CPROTO-040T-MS) supports operating voltages of 1.8 V, 3.3 V, and 5 V. See the [kit user guide](https://www.infineon.com/dgdl/Infineon-CY8CPROTO-040T-MS_UG-UserManual-v02_00-EN.pdf?fileId=8ac78c8c93dda25b019466a75dd07a01) to set the preferred operating voltage and see section [Setup the VDDA supply voltage and debug mode in Device Configurator](#set-up-the-vdda-supply-voltage-and-debug-mode-in-device-configurator).

The functionalities of this application is optimally tuned for 3.3 V. Observe that the basic functionalities work across other voltages.

For better performance, it is recommended to tune the application to use the preferred voltages. 


## Tuning procedure

<details><summary><b>Create custom BSP for your board</b></summary>

1. Follow the steps mentioned in [ModusToolbox&trade; BSP Assistant user guide](https://www.infineon.com/ModusToolboxBSPAssistant) to create a custom BSP for your board having any device. In this code example, it is created for the **CY8C4046LQI-T452** device.

2. Open the *design.modus* file from *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config* folder obtained in the previous step and enable CAPSENSE&trade; to get the *design.cycapsense* file. CAPSENSE&trade; configuration can then be started from scratch as explained in the following sections.
</details>

<br>

> **Note:** See the "Tuning the inductive-sensing solution" section in the [AN239751 – Flyback inductive sensing (ISX) design guide](https://www.infineon.com/AN239751) and the "Selecting CAPSENSE&trade; hardware parameters" section in [AN85951 – PSOC&trade; 4 and PSOC&trade; 6 CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) to learn about the considerations for selecting each parameter value. In addition, see the "Low-power Widget parameters" section in [AN234231 – Achieving lowest-power capacitive sensing with PSOC&trade; 4000T](https://www.infineon.com/AN234231) for more details about the considerations for parameter values specific to low-power widgets.


**Figure 15. Low-power widget tuning flow**

<img src="images/tuning-flowchart.png" width="" />


Do the following to tune the button widget

- [Stage 1: Set the initial configuration](#stage-1-set-the-initial-configuration)

- [Stage 2: Fine-tune for the required SNR, power, and refresh rate](#stage-2-fine-tune-for-required-snr-power-and-refresh-rate)

- [Stage 3: Tune the threshold parameters](#stage-3-tune-threshold-parameters)


### Stage 1: Set the initial configuration

1. Connect the board to the PC using the provided USB cable through the KitProg3 USB connector.

2. Launch the **Device Configurator** tool.

   Launch the Device Configurator in Eclipse IDE for ModusToolbox&trade; from the Tools section in the IDE Quick Panel or Standalone mode from the *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/device-configurator/device-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.modus* file of the respective application, which is located in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config* folder.

3. Enable the CAPSENSE&trade; channel in **Device Configurator** as shown in the **Figure 16** and save the changes.

   **Figure 16. Enable CAPSENSE&trade; in Device Configurator**

   <img src="images/device-configurator.png" />

  <br>

4. Launch the **CAPSENSE&trade; Configurator** tool.

   To launch the Configurator tool in Eclipse IDE for ModusToolbox&trade; from the CAPSENSE&trade; peripheral setting in the Device Configurator or directly from the Tools section in the IDE Quick Panel.

   The tool is launched in a Standalone mode from *{ModusToolbox&trade; install directory}/ModusToolbox/tools_{version}/capsense-configurator/capsense-configurator*. In this case, after opening the application, select **File** > **Open** and open the *design.cycapsense* file of the respective application, which is located in the *{Application root directory}/bsps/TARGET_APP_\<BSP-NAME>/config* folder.

   See the [ModusToolbox&trade; CAPSENSE&trade; Configurator user guide](https://www.infineon.com/ModusToolboxCapSenseConfig) for step-by-step instructions to configure and launch CAPSENSE&trade; in ModusToolbox&trade;.

5. In the **Basic** tab, configure the Button widgets and low-power widgets as ISX RM. Set the Tuning Mode as **SmartSense - HW parameters** for the low power widgets and **SMARTSENSE - Full** for the regular widgets as shown in **Figure 17**. 

   In the **SmartSense - HW parameters** mode, set the thresholds manually.

   In the **SMARTSENSE - Full** mode, set the thresholds using the middleware. However, this mode is not available for low-power widgets.

   Keep the touch sensitivity at its default value of 0.16 uH. The touch sensitivity is the minimum delta in inductance that the system is tuned for by SmartSense.

   **Figure 17. CAPSENSE&trade; Configurator - basic tab**

   <img src="images/basic-isx-settings.png"/>
   <br>

6. Add/select the following in the **General** tab under the **Advanced** tab:
   
   - Select **CAPSENSE&trade; IMO Clock frequency** as **46 MHz**. 
   - Set the **Modulator clock divider** to **1** to obtain the maximum available modulator clock frequency.
   - Set the **Number of init sub-conversions** based on the hint shown when you hover over the edit box. Retain the default value.
   - Use **Wake-On-Touch settings** to set the refresh rate and frame timeout while in the lowest power mode (Wake-on-Touch mode). Set **Wake-on-Touch scan interval (µs)** based on the required low-power state scan refresh rate. For example, to get a 16 Hz refresh rate, set the value to **62500**. 
   - Set the **Number of frames in Wake-on-Touch** as the maximum number of frames to be scanned in Wake-on-Touch (WoT) mode if there is no touch detected. This determines the maximum time that the device will be kept in the lowest-power mode if there is no user activity. Calculate the maximum time by multiplying this parameter with the **Wake-on-Touch scan interval (µs)** value.

   For example, to get 10 seconds as the maximum time in WoT mode, set the **Number of frames in Wake-on-Touch** to **160** for the  scan interval set as 62500 µs.

   > **Note:** For tuning low-power widgets, the **Number of frames in Wake-on-Touch** must be less than the **Maximum number of raw counts in SRAM** based on the number of sensors in WoT mode as shown in **Table 4**.

   **Table 4. Maximum number of raw counts in SRAM**

   Number of low-power widgets  | Maximum number of raw counts in SRAM
   ---------------------| -----
   1  | 245
   2  | 117
   3  | 74
   4  | 53
   5  | 40
   6  | 31
   7  | 25
   8  | 21

   <br>
      
   **Figure 18. CAPSENSE&trade; Configurator – general settings**

   <img src="images/advanced-general-settings.png" />
   
   -  Retain the default settings for all regular and low-power widget filters. To enable or update the filters later depending on the SNR requirements in [Stage 2: Fine-tune for required SNR, power, and refresh rate](#stage-2-fine-tune-for-required-snr-power-and-refresh-rate). The filters reduce the peak-to-peak noise, and using software filters results in a higher scan time.
         
      > **Note:** Each tab has a **Restore Defaults** button to restore the parameters of that tab to their default values.

7. Go to the **ISX settings** tab and make the following changes:

   - **Raw count calibration level (%)** helps to achieve the required CDAC calibration levels (35% of maximum count by default) for all sensors in the widget, while maintaining the same sensitivity across the sensor elements.
    
      **Figure 19. CAPSENSE&trade; Configurator - advanced CSD settings**

      <img src="images/advanced-isx-settings.png" />
      <br>

8. Go to the **Advanced** > **Widget Details** tab. Select **LowPower0** from the left pane and set the following:

   - **Touch Sensitivity**: Retain the default value (this will be set in [Stage 2: Fine-tune for required SNR, power, and refresh rate](#stage-2-fine-tune-for-required-snr-power-and-refresh-rate))

   - **Clock source**: Direct

   - **Finger threshold**: 65535

     Finger threshold is set to maximum to avoid waking up the device from the WoT mode due to touch detection; this is required to find the signal and SNR. 

   - **Noise threshold**: 10

   - **Negative noise threshold**: 10

   - **Low baseline reset**: 10

   - **ON debounce**: 3

     These threshold values reduce the influence of the baseline on the sensor signal that helps to get the true difference count. These parameters are set in [Stage 3: Tune threshold parameters](#stage-3-tune-threshold-parameters).

      Next, select the other widgets from the left pane and repeat the same configuration for that sensor as well.

      **Figure 20. CAPSENSE&trade; Configurator – Widget Details tab**

     <img src="images/advanced-widget-settings.png" />
     
     <br>

9. Go to the **Scan Configuration** tab to select the pins and the scan slots. Perform the following:

   - Configure pins for the electrodes using the drop-down menu.

   - Configure the scan slots using the **Auto-assign slots** option. The other option is to allot each sensor a scan slot-based on the entered slot number.

   - Check the notice list for warnings or errors.

      **Figure 21. Scan configuration tab**

      <img src="images/scan-configuration.png"/>

      <br>

10. Click **Save** to apply the settings.


### Stage 2: Fine-tune for required SNR, power, and refresh rate

Tune the sensor to have a minimum SNR of 10:1 and a minimum signal of 50 to ensure reliable operation. Increase the sensitivity by decreasing the touch sensitivity value (it is the minimum delta inductance that the system should detect) in the configurator and decrease noise by enabling filters. The touch sensitivity in this code example is set at 0.1 uH.

1. Measure the SNR as mentioned in the [Operation](#operation) section for all widgets.

3. If the SNR is less than 10:1, decrease the touch sensitivity value.

3. Load the parameters to the device and measure the SNR again.
   
      Repeat steps **1** to **3** until the following conditions are met:
      - Measured SNR from the previous stage is greater than 10:1
      - Signal count is greater than 50

4. If the system is noisy (> 40% of signal), enable the filters.

   This example has the CIC2 filter enabled, which increases the resolution for the same scan time. See the [AN234231 - Achieving lowest-power capacitive sensing with PSOC&trade; 4000T](https://www.infineon.com/AN234231) for detailed information on the CIC2 filter. Whenever a CIC2 filter is enabled, it is recommended to enable the IIR filter for optimal noise reduction. Therefore, this example has the IIR filter enabled as well.
   
   - Open **CAPSENSE&trade; Configurator** from ModusToolbox&trade; Quick Panel and select the appropriate filter as shown in **Figure 22**.

     **Figure 22. Filter settings in CAPSENSE&trade; Configurator**

     <img src="images/advanced-filter-settings.png" />
      
   - Enable the filter based on the type of noise in your system. See [AN239751 - Flyback inductive sensing (ISX) design guide](https://www.infineon.com/AN239751) and [AN85951 – PSOC&trade; 4 and PSOC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) for more details.
   
   - Click **Save** and program the device to update the filter settings.
   
     > **Note:** Decreasing the touch sensitivity and enabling filters will increase the scan time which in turn decreases the responsiveness of the sensor. The Increase in scan time also increases the power consumption. To optimize the tuning in order to achieve a balance between SNR, power, and refresh rate, manual tuning can be done. To manually tune the sensors, see the "Tuning the inductive-sensing solution" section in the [AN239751 – Flyback inductive sensing (ISX) design guide](https://www.infineon.com/AN85951) and the [PSOC&trade; 4: MSCLP inductive sensing touch-over-metal keypad-2](https://github.com/Infineon/mtb-example-psoc4-msclp-isx-tom-keypad-2-buttons) code example.


### Stage 3: Tune threshold parameters

In the **SMARTSENSE - HW parameter** tuning mode, the various thresholds, relative to the signal, need to be set for each low-power widget. For the regular widgets, the threshold parameters are automatically set by the **SMARTSENSE - Full** tuning mode.

Perform the following in CAPSENSE&trade; Tuner to set up the thresholds for a low-power widget:

1. Switch to the **Graph View** tab and select **LowPower0**.

2. For the **LowPower0** low-power widget, configure the finger threshold to **65535** and wait for the application to enter Low-power mode. As the finger threshold is set to maximum, pressing the low-power button will not switch the application to Active mode. To do this, set the tuning mode for the regular widgets to **SMARTSENSE - HW parameter** via the CAPSENSE&trade; Configurator temporarily and program the device.

3. Press the sensor and monitor the touch signal in the **Sensor signal** graph, as shown in **Figure 23**. 

   **Figure 23. Sensor signal when the sensor is touched**

   <img src="images/tuner-diff-signal.png" />

   <br>

4. Note the signal measured and set the thresholds according to the following recommendations:

   - **Finger threshold**: 80% of the signal

   - **Noise threshold**: 40% of the signal

   - **Negative noise threshold**: 40% of the signal

   - **Debounce** 3

5. Set the threshold parameters in the **Widget/Sensor parameters** section of the CAPSENSE&trade; Tuner.

   **Figure 24. Widget threshold parameters**

   <img src="images/tuner-threshold-settings.png" />

   <br>

   **Table 5. Sensor tuning parameters obtained for CY8CPROTO-040T-MS kit for LowPower0**

   Parameter|	 LowPower0
   :--------|:------
   Signal	| 100
   Finger threshold 	| 40
   Noise threshold |40
   Negative noise threshold	|40
   Low baseline reset	| 30
   ON debounce	| 3

  <br>

6. Apply the settings to the device by clicking **Apply to Device**.

   **Figure 25. Apply settings to device**

   <img src="images/tuner-apply-settings-device.png" />

   <br>

   After applying the configuration, test the performance by touching the button. If your sensor is tuned correctly, you will observe the touch status go from 0 to 1 in the **Status** panel of the **Graph View** tab as shown in **Figure 26**. The status of the button is also indicated by LED2 in the kit; LED2 turns ON when the finger touches the button and turns OFF when the finger is removed.

   **Figure 26. Sensor status in CAPSENSE&trade; Tuner**

   <img src="images/tuner-status.png" />

   <br>

7. Click **Apply to Project** as shown in **Figure 27**. The change is updated in the *design.cycapsense* file. Close **CAPSENSE&trade; Tuner** and launch **CAPSENSE&trade; Configurator**. All the changes in the CAPSENSE&trade; Tuner reflects in the **CAPSENSE&trade; Configurator**.

   **Figure 27. Apply settings to Project**

   <img src="images/tuner-apply-settings-project.png" />

   <br>
   

### Process time measurement

To set the optimum refresh rate of each power mode, measure the process time of your application.

Follow these steps to measure the process time of the blocks of application code while excluding the scan time.

1. Enable `ENABLE_RUN_TIME_MEASUREMENT` macro in *main.c* as follows:
      
    ```
    #define ENABLE_RUN_TIME_MEASUREMENT (1u)
    ```     
   This macro enables the system tick configuration and runtime measurement functionalities. 

2.	Place the `start_runtime_measurement()` function call before your application code and the `stop_runtime_measurement()` function call after it. The `stop_runtime_measurement()` function will return the execution time in microseconds (µs). 
 
      ```   
         #if ENABLE_RUN_TIME_MEASUREMENT
            uint32_t run_time = 0;
            start_runtime_measurement();
         #endif

         /* User Application Code Start */
         .
         .
         .
         /* User Application Code Stop */

         #if ENABLE_RUN_TIME_MEASUREMENT
            run_time = stop_runtime_measurement();
         #endif
      ```

3.	Run the application in the Debug mode with breakpoints placed at the `active_processing_time` and `alr_processing_time` variables as follows:
      ```
         #if ENABLE_RUN_TIME_MEASUREMENT
            active_processing_time=stop_runtime_measurement();
         #endif
         and 
         #if ENABLE_RUN_TIME_MEASUREMENT
            alr_processing_time=stop_runtime_measurement();
         #endif
      ``` 
4. Read the variables by adding them into the **Expressions view** tab.
5. Update related macros with above measured processing times in *main.c* as follows:
      ```
      #define ACTIVE_MODE_PROCESS_TIME     (xx)

      #define ALR_MODE_PROCESS_TIME        (xx)
      ```


### Scan time measurement

The scan time is also required for calculating the refresh rate of the application power modes. The total scan time of all the widgets in this code example is 16 µs.

It can be calculated as follows:

   - The scan time includes the MSCLP initialization time, Cmod, and the total sub-conversions of the sensor. 

   - To control the Cmod initialization sequence, set the **Enable Coarse initialization bypass** configurator option as listed in the following table:

     **Table 6. Enable coarse initialization bypass**

     Enable coarse initialization bypass | Behavior
     :-------------|:---------
     TRUE | Cmod initialization happens only once before scanning the sensors of the widget
     FALSE | Cmod initialization happens before scanning each sensor of the widget

Use the following equations to measure the widgets scan time based on coarse initialization bypass options selected: 

**Equation 1. Scan time calculation of a widget with coarse initialization bypass enabled**

<img src="images/scan_time_equation_bypass_enabled.png" width=500/>

**Equation 2. Scan time calculation of a widget with coarse initialization bypass disabled**

<img src="images/scan_time_equation_bypass_disabled.png" width=500/>


Where,

$n$ = Total number of sensors in the widget

$N_{init}$ = Number of init sub-conversions

$N_{sub}$ - Number of sub-conversions

$SnsClkDiv$ = The Lx clock divider for the widget

$F_{mod}$ = Modulator clock frequency

$k$ = Measured Initialization time (MSCLP+Cmod).

This value of $k$ measured for this application is ~10 µs. It remains constant for all widgets. 

Measure the value of **$k$** using an oscilloscope as shown in **Figure 28**.

**Figure 28. $k$ value measurement**

<img src="images/scantime_wave.png" />

Update the following macros in *main.c* using the scan time calculated. The value remains the same for both macros for this application.

```
#define ACTIVE_MODE_FRAME_SCAN_TIME     (xx)

#define ALR_MODE_FRAME_SCAN_TIME        (xx)
```


> **Note:** If the application has more than one widget, add the scan times of individual widgets calculated.


## Debugging

You can debug the example to step through the code.


<details><summary><b>In Eclipse IDE</b></summary>

Use the **\<Application Name> Debug (KitProg3_MiniProg4)** configuration in the **Quick Panel**. For details, see the "Program and debug" section in the [Eclipse IDE for ModusToolbox&trade; user guide](https://www.infineon.com/MTBEclipseIDEUserGuide).

</details>


<details><summary><b>In other IDEs</b></summary>

Follow the instructions in your preferred IDE.

</details>


## Design and implementation

The design has a ratiometric implementation of the following sensors:
- Four Wake-on-Touch widget (4 elements), also called "Low-power Widget"
- Four inductive sensing based button widgets (4 elements)

Following are the four LEDs used in this project: 
- LEDs D0 to D3 show the buttons' touch status. They are turned ON when the corresponding button is pressed and turned OFF when the finger is lifted. 

There are three power states defined for this project:

- Active mode

- Active-low refresh rate (**ALR**) mode

- Wake-on-Touch (**WoT**) mode

After reset, the device is in Active mode, and scans the regular CAPSENSE&trade; widgets with a high refresh rate (**128 Hz**). If user activity is detected in any other mode, the device is transferred to Active mode to provide the best user interface experience. This mode has the highest power consumption; therefore, the design should reduce the time spent in Active mode.

If there is no user activity for a certain period of time (`ACTIVE_MODE_TIMEOUT_SEC` = 10 s), the application transitions to ALR mode. Here, the refresh rate is reduced to **32 Hz** and therefore, this mode acts as an intermediate state before moving to the lowest-power mode (WoT mode). This mode can also be used for periodically updating the baselines of sensors while there is no user activity for a long time.

Further non-activity for a certain time span (`ALR_MODE_TIMEOUT_SEC` = 5 s) transitions the application to the lowest-power mode, called the **Wake-on-Touch** mode, which scans the low-power widget at a low refresh rate (**16 Hz**) and processes the results without CPU intervention.

> **Note:** An internal low-power timer (MSCLP timer) is available in CAPSENSE&trade; MSCLP hardware to set the refresh rate for each power mode as follows:

- For Active and ALR modes: Use the `Cy_CapSense_ConfigureMsclpTimer()` function.
- For WoT mode: Use the Wake-on-Touch scan interval in CAPSENSE&trade; Configurator.

Different power modes and transition conditions for a typical use case are shown in **Figure 29**.

   **Figure 29. State machine showing different power states of the device**

   <img src="images/capsense_lp_firmware_state_machine.png" width="350"/>


The project uses the [CAPSENSE&trade; middleware](https://github.com/Infineon/capsense) (see ModusToolbox&trade; user guide for more details on selecting a middleware). See [AN85951 – PSOC&trade; 4 and PSOC&trade; 6 MCU CAPSENSE&trade; design guide](https://www.infineon.com/AN85951) and [AN239751 - Flyback inductive sensing (ISX) design guide](https://www.infineon.com/AN239751) for more details on CAPSENSE&trade; features and usage.

The [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) provides a GUI-based tuner application for debugging and tuning the CAPSENSE&trade; system. The CAPSENSE&trade; Tuner application works with EZI2C and UART communication interfaces. This project has a Serial Communication Block (SCB) block configured in EZI2C mode to establish communication with the onboard KitProg, which in turn enables reading the CAPSENSE&trade; raw data using the CAPSENSE&trade; Tuner. See [EZI2C peripheral settings](#resources-and-settings).

The CAPSENSE&trade; data structure that contains the CAPSENSE&trade; raw data is exposed to the CAPSENSE&trade; Tuner by setting up the I2C communication data buffer with the CAPSENSE&trade; data structure. This enables the tuner to access the CAPSENSE&trade; raw data for tuning and debugging CAPSENSE&trade;.


### Set up the VDDA supply voltage and Debug mode in Device Configurator

1. Open **Device Configurator** from the Quick Panel.

2. Go to the **System** tab, select the **Power** resource, and set the VDDA value under **Operating conditions** as shown in **Figure 30**.

   **Figure 30. Setting the VDDA supply in System tab of Device Configurator**

   <img src="images/vdda-setting.png" width=""/>
<br>

3. By default, the Debug mode is disabled for this application to reduce power consumption. Enable the Debug mode to enable SWD pins as shown in **Figure 31**.

   **Figure 31. Enable the Debug mode in the System tab of Device Configurator**

   <img src="images/debug.png" width=""/>

<br>


## Resources and settings

**Figure 32. EZI2C settings**

<img src="images/ezi2c_setting.png" width=""/>
<br>

**Table 7. Application resources**

 Resource  |  Alias/object     |    Purpose
 :-------- | :-------------    | :------------
 SCB (I2C) (PDL) | CYBSP_EZI2C          | EZI2C slave driver to communicate with CAPSENSE&trade; Tuner
 CAPSENSE&trade; | CYBSP_MSC | CAPSENSE&trade; driver to interact with the MSC hardware and interface the CAPSENSE&trade; sensors

<br>

## Firmware flow

**Figure 33. Firmware flowchart**

<img src="images/firmware-flowchart.png" width=""/>


## Related resources

Resources  | Links
-----------|----------------------------------
Application notes  | [AN79953](https://www.infineon.com/AN79953) – Getting started with PSOC&trade; 4 MCU <br>  [AN234231](https://www.infineon.com/AN234231) – Achieving lowest-power capacitive sensing with PSOC&trade; 4000T <br> [AN85951](https://www.infineon.com/AN85951) – PSOC&trade; 4 and PSOC&trade; 6 MCU CAPSENSE&trade; design guide <br>  [AN239751](https://www.infineon.com/AN239751) – Flyback inductive sensing (ISX) design guide
Code examples  | [Using ModusToolbox&trade;](https://github.com/Infineon/Code-Examples-for-ModusToolbox-Software) on GitHub
Device documentation |  [PSOC&trade; 4 datasheets](https://www.infineon.com/cms/en/search.html?intc=searchkwr-return#!view=downloads&term=PSOC%204&doc_group=Data%20Sheet) <br>[PSOC&trade; 4 technical reference manuals](https://www.infineon.com/cms/en/search.html#!term=PSOC%204%20technical%20reference%20manual&view=all)
Development kits | Select your kits from the [Evaluation board finder](https://www.infineon.com/cms/en/design-support/finder-selection-tools/product-finder/evaluation-board)
Libraries on GitHub  | [mtb-pdl-cat2](https://github.com/Infineon/mtb-pdl-cat2) –  PSOC&trade; 4 Peripheral Driver Library (PDL) <br>  [mtb-hal-cat2](https://github.com/Infineon/mtb-hal-cat2)  – Hardware Abstraction Layer (HAL) library
Middleware on GitHub  | [capsense](https://github.com/Infineon/capsense) – CAPSENSE&trade; library and documents
Tools  | [ModusToolbox&trade;](https://www.infineon.com/modustoolbox) – ModusToolbox&trade; software is a collection of easy-to-use libraries and tools enabling rapid development with Infineon MCUs for applications ranging from wireless and cloud-connected systems, edge AI/ML, embedded sense and control, to wired USB connectivity using PSOC&trade; Industrial/IoT MCUs, AIROC&trade; Wi-Fi and Bluetooth&reg; connectivity devices, XMC&trade; Industrial MCUs, and EZ-USB&trade;/EZ-PD&trade; wired connectivity controllers. ModusToolbox&trade; incorporates a comprehensive set of BSPs, HAL, libraries, configuration tools, and provides support for industry-standard IDEs to fast-track your embedded application development.

<br>


## Other resources

Infineon provides a wealth of data at [www.infineon.com](https://www.infineon.com) to help you select the right device, and quickly and effectively integrate it into your design.


## Document history


Document title: *CE240146* – *PSOC&trade; 4: MSCLP inductive sensing touch-over-metal keypad-4 demo*

 Version | Description of change
 ------- | ---------------------
 1.0.0   | New code example
 2.0.0   | Major update to support ModusToolbox&trade; v3.3. This version is not backward compatible with previous versions of ModusToolbox&trade;
 2.1.0   | Major update to support ModusToolbox&trade; v3.4. This version is not backward compatible with previous versions of ModusToolbox&trade;. Added SmartSense support.
<br>


All referenced product or service names and trademarks are the property of their respective owners.

The Bluetooth&reg; word mark and logos are registered trademarks owned by Bluetooth SIG, Inc., and any use of such marks by Infineon is under license.

PSOC&trade;, formerly known as PSoC&trade;, is a trademark of Infineon Technologies. Any references to PSoC&trade; in this document or others shall be deemed to refer to PSOC&trade;.


---------------------------------------------------------

© Cypress Semiconductor Corporation, 2023-2025. This document is the property of Cypress Semiconductor Corporation, an Infineon Technologies company, and its affiliates ("Cypress").  This document, including any software or firmware included or referenced in this document ("Software"), is owned by Cypress under the intellectual property laws and treaties of the United States and other countries worldwide.  Cypress reserves all rights under such laws and treaties and does not, except as specifically stated in this paragraph, grant any license under its patents, copyrights, trademarks, or other intellectual property rights.  If the Software is not accompanied by a license agreement and you do not otherwise have a written agreement with Cypress governing the use of the Software, then Cypress hereby grants you a personal, non-exclusive, nontransferable license (without the right to sublicense) (1) under its copyright rights in the Software (a) for Software provided in source code form, to modify and reproduce the Software solely for use with Cypress hardware products, only internally within your organization, and (b) to distribute the Software in binary code form externally to end users (either directly or indirectly through resellers and distributors), solely for use on Cypress hardware product units, and (2) under those claims of Cypress's patents that are infringed by the Software (as provided by Cypress, unmodified) to make, use, distribute, and import the Software solely for use with Cypress hardware products.  Any other use, reproduction, modification, translation, or compilation of the Software is prohibited.
<br>
TO THE EXTENT PERMITTED BY APPLICABLE LAW, CYPRESS MAKES NO WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, WITH REGARD TO THIS DOCUMENT OR ANY SOFTWARE OR ACCOMPANYING HARDWARE, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  No computing device can be absolutely secure.  Therefore, despite security measures implemented in Cypress hardware or software products, Cypress shall have no liability arising out of any security breach, such as unauthorized access to or use of a Cypress product. CYPRESS DOES NOT REPRESENT, WARRANT, OR GUARANTEE THAT CYPRESS PRODUCTS, OR SYSTEMS CREATED USING CYPRESS PRODUCTS, WILL BE FREE FROM CORRUPTION, ATTACK, VIRUSES, INTERFERENCE, HACKING, DATA LOSS OR THEFT, OR OTHER SECURITY INTRUSION (collectively, "Security Breach").  Cypress disclaims any liability relating to any Security Breach, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any Security Breach.  In addition, the products described in these materials may contain design defects or errors known as errata which may cause the product to deviate from published specifications. To the extent permitted by applicable law, Cypress reserves the right to make changes to this document without further notice. Cypress does not assume any liability arising out of the application or use of any product or circuit described in this document. Any information provided in this document, including any sample design information or programming code, is provided only for reference purposes.  It is the responsibility of the user of this document to properly design, program, and test the functionality and safety of any application made of this information and any resulting product.  "High-Risk Device" means any device or system whose failure could cause personal injury, death, or property damage.  Examples of High-Risk Devices are weapons, nuclear installations, surgical implants, and other medical devices.  "Critical Component" means any component of a High-Risk Device whose failure to perform can be reasonably expected to cause, directly or indirectly, the failure of the High-Risk Device, or to affect its safety or effectiveness.  Cypress is not liable, in whole or in part, and you shall and hereby do release Cypress from any claim, damage, or other liability arising from any use of a Cypress product as a Critical Component in a High-Risk Device. You shall indemnify and hold Cypress, including its affiliates, and its directors, officers, employees, agents, distributors, and assigns harmless from and against all claims, costs, damages, and expenses, arising out of any claim, including claims for product liability, personal injury or death, or property damage arising from any use of a Cypress product as a Critical Component in a High-Risk Device. Cypress products are not intended or authorized for use as a Critical Component in any High-Risk Device except to the limited extent that (i) Cypress's published data sheet for the product explicitly states Cypress has qualified the product for use in a specific High-Risk Device, or (ii) Cypress has given you advance written authorization to use the product as a Critical Component in the specific High-Risk Device and you have signed a separate indemnification agreement.
<br>
Cypress, the Cypress logo, and combinations thereof, ModusToolbox, PSoC, CAPSENSE, EZ-USB, F-RAM, and TRAVEO are trademarks or registered trademarks of Cypress or a subsidiary of Cypress in the United States or in other countries. For a more complete list of Cypress trademarks, visit www.infineon.com. Other names and brands may be claimed as property of their respective owners.
