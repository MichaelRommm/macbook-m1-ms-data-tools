# Guide for Using Microsoft Data Tools on MacBook M1

## Introduction
As MacBook M1 users, we often encounter challenges when trying to work with Microsoft tools in the data field. During my Data Analyst course, I faced numerous issues working with SQL Server, Power BI, and Excel. In this article, I will share the solutions I found and how to overcome these challenges.

**P.S.** I am aware that there are various solutions to these issues, but I will focus on the easiest, most accessible, and stable methods (which may involve paid tools).

If you have any suggestions to improve and streamline these processes, I would love to hear them. I am open to collaborations and recommendations as I am a beginner data analyst.

## Installing Parallels Desktop
To start, we need to install Parallels Desktop on your MacBook M1. This software allows you to run Windows on a virtual machine.

1. Download and install [Parallels Desktop](https://www.parallels.com/products/desktop/).
2. Follow the installation instructions and set up a new virtual machine (VM) with Windows.

After installation, you should have a Windows environment running on your Mac.

## Installing Docker and Running MS SQL Server
Docker allows us to run containers, which are lightweight virtual machines that can run applications.

1. Install Docker on your MacBook M1:
    - Download Docker from the [official website](https://www.docker.com/products/docker-desktop).
    - Follow the installation instructions.

2. Download and run MS SQL Server in a Docker container:
    - Pull the MS SQL Server image from Docker Hub:
        ```sh
        docker pull mcr.microsoft.com/mssql/server
        ```
    - Run the container with the desired settings:
        ```sh
        docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=YourPassword123' -p 1433:1433 --name sqlserver -d mcr.microsoft.com/mssql/server
        ```
    - Replace `YourPassword123` with a strong password of your choice.

3. Connecting to MS SQL Server from your Windows VM:
    - Use SQL Server Management Studio (SSMS) or another SQL client. [Install MS SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
    - Connect using the IP address of your Mac and the port 1433.
    - Login with the username `sa` and the password you set (e.g., `YourPassword123`).

4. Running Docker commands from the Mac terminal:
    - To start the container if it’s stopped:
        ```sh
        docker start sqlserver
        ```
    - To stop the container:
        ```sh
        docker stop sqlserver
        ```
    - To view the running containers:
        ```sh
        docker ps
        ```

## Running Microsoft Power BI and Excel
To work with Power BI and Excel, we need to install them on the Windows VM.

1. Download and install [Microsoft Power BI](https://powerbi.microsoft.com/desktop/).
2. Download and install [Microsoft Excel](https://www.microsoft.com/en-us/microsoft-365/excel).

After installation, you should be able to use these tools seamlessly within your Windows environment.

## Working with Python and Visual Studio Code
To work with Python and connect to MS SQL Server, we need to set up Visual Studio Code (VS Code) in the VM.

1. Download and install [Visual Studio Code](https://code.visualstudio.com/).
2. Install the Python extension for VS Code.

3. Connect to MS SQL Server using pandas:
    ```python
    import pandas as pd
    import pyodbc

    conn = pyodbc.connect(
        'DRIVER={ODBC Driver 17 for SQL Server};'
        'SERVER=your_server_name;'
        'DATABASE=your_database_name;'
        'UID=sa;'
        'PWD=YourPassword123'
    )
    query = "SELECT * FROM your_table"
    df = pd.read_sql(query, conn)
    print(df.head())
    ```

4. Resolve any connection issues by ensuring the correct driver and network settings.

## Summary and Tips
In this guide, we covered how to set up a MacBook M1 to work with Microsoft tools in the data field. We installed Parallels Desktop, Docker, and various Microsoft applications, and demonstrated how to connect Python to MS SQL Server.

### Tips:
- Always keep your software updated to avoid compatibility issues.
- Use the official documentation for troubleshooting and advanced configurations.
- Join online communities and forums for additional support and advice.

By following these steps, you can effectively work with Microsoft tools on a MacBook M1. Good luck!
