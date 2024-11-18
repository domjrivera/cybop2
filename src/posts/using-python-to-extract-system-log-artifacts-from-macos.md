---
title: Using Python to Extract System Log Artifacts from MacOS
description: Using Python to Extract System Log Artifacts from MacOS
author: Cyber Operator
date: 2024-11-18T15:49:27.407Z
tags:
  - Forensics
---
# Using Python to Extract System Log Artifacts from MacOS

`import os
import datetime
import pandas as pd`

import os
import datetime
import pandas as pd
import re

# Define the log file paths

log_files = \[
    '/var/log/system.log',
    '/var/log/security.log',
    '/var/log/install.log'
]

# Create an empty list to store the extracted data

data = \[]

# Get the current year

current_year = datetime.date.today().year

# Iterate through each log file

for log_file in log_files:
    # Check if the log file exists
    if os.path.exists(log_file):
        # Open the log file in read mode
        with open(log_file, 'r') as f:
            # Iterate through each line in the log file
            for line in f:
                # Use regular expression to extract the timestamp
                match = re.search(r'\w{3}\s{1,2}\d{1,2}\s\d{2}:\d{2}:\d{2}', line)
                if match:
                    timestamp = match.group()
                    # Add the current year to the timestamp
                    dt = datetime.datetime.strptime(f'{timestamp} {current_year}', '%b %d %H:%M:%S %Y')
                    message = line\[match.end():].strip()
                    # Append the extracted data to the list
                    data.append({
                        'Date': dt,
                        'Message': message
                    })

# Create a Pandas DataFrame from the extracted data

df = pd.DataFrame(data)

# Output the DataFrame to a CSV file

df.to_csv('system_logs.csv', index=False)