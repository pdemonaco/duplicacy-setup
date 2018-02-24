# Installation

1. Download the latest binary version from [github](https://github.com/gilbertchen/duplicacy/releases).
2. Copy the binary to system32 so it's in the path.
    
    ```powershell
    Copy-Item "%USERPROFILE%\Downloads\duplicacy_win_x64_2.0.10.exe" "C:\Windows\System32\duplicacy.exe"
    ```

# Backup Directory Configuration

Note that this is the same process for attaching another machine to the same repository. By using different snapshot IDs for each machine you can get extra storage savings without crossing the metadata streams...

1. Initialize the repository. This command has two mandatory arguments, the snapshot ID (basically the name of the backup set) and the target. I'm using b2

    ```powershell
    # duplicacy init -e <snapshot ID> b2://<bucket name>
    duplicacy init -e home-phil-loki b2://duplicacy-primary
    ```
2. You'll be prompted for your Backblaze Account ID as well as your Application Key. Finally, you'll be prompted for an encryption password to actually encrypt the data. 
    
    ![Repo Init Complete](img/repo-init-result.png)


# Scheduled Task Creation

1. Open windows task scheduler and right click on the library and choose **Import Task...**.
2. Import the XML file included for reference.
3. Change the run option to **Run whether user is logged on or not**.

    ![Run regardless](img/run-when-not-logged-in.png)
4. Update the start-in directory of the **Start a program** action under the actions tab to the location of your repository.
5. Save and enter your credentials.
6. Enable the task by right clicking on it.
7. Run it - make sure it all goes well.
