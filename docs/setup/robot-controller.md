---
icon: lucide/computer
---

# Robot Controller

The robot controller is how the code gets ran on the bot. It takes your Java, C, Python, etc and executes it and talks to the motors and sensors to make it move.

Please note that for FSC's unofficial offseason events (SCRIW and SCRAP) both the RoboRIO and Systemcore will be competition-legal.

## Systemcore

Starting from 2027's kickoff, Systemcore will be the only allowed robot controller, entirely replacing the RoboRIO for FRC teams. It is currently in alpha testing with a limited set of FRC and FTC teams.

It's not entirely known how the setup process will work for Systemcore firmware updates when its moved out of alpha, but it's assumed that it will be either updated through the web UI or still based on SD card flashing (like the RoboRIO 2.0 below).

The Systemcore will simplify many parts of the process, including networking in the shop (due to its onboard 2.4ghz radio) and built-in vision processing (provided by Limelight), however due to its limited availability it is impossible to write comprehensive documentation for. Therefore, most of this documentation has been written with the RoboRIO in mind.

## RoboRIO 1.0 and 2.0 (⚠️ Legacy)

The RoboRIO was the robot controller from 2015 to 2026.

Depending on which version of the RoboRIO your team owns, the imaging process is fundamentally different. 

=== "RoboRIO 2.0 (MicroSD)"

    The RoboRIO 2.0 runs its entire Operating System (OS) from a **MicroSD card**. 
    
    *   **The Workflow:** You do **not** use the RoboRIO Imaging Tool for the OS. Instead, you flash the SD card directly using your laptop.
    *   **Tools Needed:** [Balena Etcher](https://etcher.balena.io/) or Raspberry Pi Imager.
    *   **Process:**

        1.  Remove the MicroSD card from the RIO.
        2.  Download the latest image (usually found in `~/wpilib/YYYY/images/`).
        3.  Flash the image to the card using Balena Etcher.
        4.  Insert the card back into the RIO and boot.
    
    !!! tip "Judson's Pro-Tip: Card Quality Matters"
        Standard consumer SD cards often fail under the vibration and heat of a robot. FSC recommends using **SanDisk Industrial MicroSD cards**. They are designed for high write cycles and are much less likely to corrupt mid-match.

=== "RoboRIO 1.0 (Internal Flash)"

    The RoboRIO 1.0 has internal memory. You must "push" the image to it over a USB cable.
    
    *   **Tools Needed:** **RoboRIO Imaging Tool** (installed with NI Game Tools).
    *   **Process:**

        1.  Connect the RIO to your laptop via a **USB-B cable**.
        2.  Open the Imaging Tool.
        3.  Select your RIO, enter your team number, and click **Reformat**.
    
    !!! warning "RIO 1 Memory Issues"
        The RIO 1 has significantly less RAM than the RIO 2. To prevent crashes during a match, we recommend **disabling the Web Dashboard**. This frees up precious memory for your actual robot code.

---

## Formatting the SD Card (RIO 2.0)

When you image an SD card for a RIO 2.0, the card is partitioned into several sections. 

1.  **Boot Partition:** Small area for startup files.
2.  **System Partition:** Where the Linux OS lives.
3.  **User Data:** Where your actual robot code is deployed.

**Never** try to drag-and-drop files onto the SD card through Windows Explorer. Always use a proper imaging tool (Balena Etcher) to ensure the partitions are aligned correctly.

### Common Troubleshooting

*   **RIO 1 Not Showing Up:** Ensure you are using a data-ready USB-B cable. Some cheap cables only provide power.
*   **"Unteathered" Imaging:** You cannot image a RIO over Wi-Fi. Always use USB or Ethernet.
*   **Firewall Blocks:** If the Imaging Tool fails to "see" the RIO, temporarily disable your Windows Firewall. FRC networking protocols are often flagged as "suspicious" by default Windows settings.
