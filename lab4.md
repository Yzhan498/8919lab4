Lab Tasks:
Task 1: Prepare Your Ubuntu Server
sudo apt-get update && sudo apt-get upgrade
![img](<img/Screenshot 2024-03-23 at 2.29.40 PM.png>)
Task 2: Install Grafana
•
Add Grafana's official APT repository and install Grafana:
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install grafana
![img](<img/Screenshot 2024-03-23 at 2.33.57 PM.png>)
•
Start and enable the Grafana server:
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
![img](<img/Screenshot 2024-03-23 at 2.39.10 PM.png>)
Task 3: Install the Azure Monitor Agent
•
Install necessary dependencies:
sudo apt-get install curl apt-transport-https gpg
•![img](<img/Screenshot 2024-03-23 at 2.36.03 PM.png>)
Import the Microsoft repository key:
curl -sL https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null
![img](<img/Screenshot 2024-03-23 at 2.41.16 PM.png>)
•Add the Azure Monitor agent repository:
AZ_REPO=$(lsb_release -cs)
echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | sudo tee /etc/apt/sources.list.d/azure-cli.list
![img](<img/Screenshot 2024-03-23 at 2.43.32 PM.png>)
• Install the Azure CLI:
sudo apt-get update
sudo apt-get install azure-cli
![img](<img/Screenshot 2024-03-23 at 2.15.35 PM.png>)
Task 4: Collect Performance Metrics
• Use the Azure CLI to configure the Azure Monitor agent to collect performance metrics:
az login
# Follow the instructions to complete the login process.
# Set up the agent to collect the desired metrics.
![img](<img/Screenshot 2024-03-23 at 4.33.52 PM.png>)
•
Validate that metrics are being collected using the Azure portal.
![img](<img/Screenshot 2024-03-23 at 4.41.03 PM.png>)
![img](<img/Screenshot 2024-03-23 at 4.45.02 PM.png>)
![img](<img/Screenshot 2024-03-23 at 5.00.18 PM.png>)
![img](<img/Screenshot 2024-03-23 at 5.03.55 PM.png>)
Task 5: Connect Grafana to Azure Monitor
•
Open Grafana in your web browser (usually http://<your-server-ip>:3000) and log in with the default credentials (admin/admin).
![img](<img/Screenshot 2024-03-23 at 4.37.50 PM.png>)
•
Navigate to Configuration > Data Sources and click on “Add data source.”
•![img](<img/Screenshot 2024-03-23 at 5.09.42 PM.png>)
Select “Azure Monitor” from the list.
•
Enter the details for your Azure subscription, tenant ID, client ID, and client secret.
•
Save and test the connection to ensure it is configured correctly.
Task 6: Create a Dashboard in Grafana
•
Click on the “+” icon on the left sidebar and select “Dashboard.”
•
Click on “Add new panel.”
•
From the data source dropdown, select “Azure Monitor.”
•
Choose the relevant metrics that you would like to visualize, such as CPU usage, memory usage, network I/O, etc.
•
Customize the panel with thresholds, colors, and labels.