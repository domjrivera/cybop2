---
title: Using Python to Extract System Log Artifacts from MacOS
description: Using Python to Extract System Log Artifacts from MacOS
author: Cyber Operator
date: 2024-11-18T15:49:27.407Z
tags:
  - Forensics
---
`import os
import datetime
import pandas as pd`

# `Define the log file paths`

`log_files = [
    '/var/log/system.log',
    '/var/log/security.log',
    '/var/log/install.log'
]`

# `Create an empty list to store the extracted data`

`data = []`

# `Iterate through each log file`

`for log_file in log_files:
    # Check if the log file exists
    if os.path.exists(log_file):
        # Open the log file in read mode
        with open(log_file, 'r') as f:
            # Iterate through each line in the log file
            for line in f:
                # Split the line into its components (date, time, message)
                date_str, time_str, message = line.split(' ', 2)
                # Parse the date and time strings into a datetime object
                dt = datetime.datetime.strptime(f'{date_str} {time_str}', '%b %d %H:%M:%S')
                # Append the extracted data to the list
                data.append({
                    'Date': dt,
                    'Message': message.strip()
                })`

# `Create a Pandas DataFrame from the extracted data`

`df = pd.DataFrame(data)`

# `Output the DataFrame to a CSV file`

`df.to_csv('system_logs.csv', index=False)`
