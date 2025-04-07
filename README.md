# create a file named with "Grafana.sh"
# paste the below content in the file 
-----------------------------------------------------------------------------------------------------------
#!/bin/bash

# Define variables
GRAFANA_VERSION="10.2.2"
GRAFANA_RPM="grafana-${GRAFANA_VERSION}-1.x86_64.rpm"
DOWNLOAD_URL="https://dl.grafana.com/oss/release/${GRAFANA_RPM}"

# Update system and install dependencies
sudo yum install -y wget

# Download Grafana
wget -q "$DOWNLOAD_URL" -O "$GRAFANA_RPM"

# Install Grafana
if [ -f "$GRAFANA_RPM" ]; then
    sudo yum install -y "./$GRAFANA_RPM"
    rm -f "$GRAFANA_RPM"
else
    echo "Download failed, exiting."
    exit 1
fi

# Enable and start Grafana service
sudo systemctl enable --now grafana-server

# Open firewall port
sudo firewall-cmd --add-port=3000/tcp --permanent && sudo firewall-cmd --reload

# Verify service status
sudo systemctl status grafana-server --no-pager
-----------------------------------------------------------------------------------------------------------------

# create the file exectable with the below  commands

  sudo chmod +x grafana.sh 

  sudo ./grafana.sh
  
